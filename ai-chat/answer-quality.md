---
title: "How Docsbook keeps AI answers grounded in your pages"
description: "The retrieval and grounding pipeline behind Docsbook AI chat: chunking, embeddings, hybrid retrieval, citation rules, the refusal path, and what we do and do not measure."
tldr: "Every answer is written from pages the server fetched for that question, and a citation survives only if it names a page that was really read. We publish no accuracy percentage — we publish the mechanism, the judge that scores real conversations, and the failure modes that remain."
---

# How answers are kept grounded

An assistant on documentation is only worth having if it does not make things up. A wrong answer with a confident tone costs more than no assistant at all: the reader acts on it, and your support queue gets the consequence a day later.

So the question that matters is not "does it use AI" — it is **what is the model allowed to answer from, and what happens when the right passage is not in front of it**. This page is the answer, at the level of detail you would get from reading the implementation.

## What you get

Every answer the reader sees is written from page text that Docsbook fetched for that specific question, in that request. The reader watches it happen: the widget prints `Found N results` and one `Reading <page>` line per page opened, each a link to the page itself. Under the answer sits a list of citations, and a citation survives only if the model quoted that page's path inline in its own answer or the server really fetched that page for this question. A path the model invented, and never quoted, cannot become a citation.

When retrieval finds nothing relevant, the model is instructed to say the documentation does not cover it rather than to compose something plausible. That refusal is recorded, not swallowed — it becomes a row in your Unanswered questions report and a `chat.no_answer` webhook, which is the signal telling you which page to write next.

## How is an answer produced?

Seven stages, in this order. Every stage below is a real branch in the request, not a diagram.

### 1. Your docs are split into units, then embedded

Automatic indexing runs at **heading granularity**: one unit per section of a page. The text sent to the embedding model is the section's heading breadcrumb followed by the section body — `Billing > Refunds` in front of the refund text — because a section called "Limits" means something different under "Webhooks" than under "AI chat", and the vector has to carry that difference. Each unit is capped at **6,000 characters**. Page-level and line-level granularity also exist in the indexer; the automatic path uses headings.

A unit's identity is its page path plus its heading anchor. Anchors repeat inside a page — a changelog can carry forty `### Fixed` headings — so a repeated anchor gets an ordinal suffix. Without that, every one of those sections is the same unit, and the write collides.

### 2. Units become vectors, and unchanged units cost nothing

Embeddings are `openai/text-embedding-3-small`, **1,536 dimensions**, requested through OpenRouter in batches of **96 units per call**. The storage column is a `vector(1536)`, and a model returning a different width is rejected outright rather than written and silently mismatched later.

Every unit carries a content hash of `sha256(model + NUL + text)`. On a re-index, a unit whose hash is already stored is skipped, so editing one page costs one page's worth of embedding, not the corpus. The estimate you are shown before a run has an **exact** unit count (the splitter is deterministic and has already run) and an **approximate** token count of `characters ÷ 4` — treat that figure as ±30%, which is why it is presented as an estimate rather than as the price.

### 3. Re-indexing follows your commits

Each commit to your docs queues a re-index. A queued run is picked up by a background runner every two minutes, not by a callback attached to the response that already shipped — a callback is exactly what used to die mid-flight and leave a stamped-but-empty index behind. Consecutive commits inside **five minutes** collapse into one run, since a publish flow commits content, then navigation, then branding.

Whether semantic retrieval is used is decided by **the presence of vectors**, never by a "last indexed" timestamp. A timestamp is a claim; a row is proof, and the difference is the whole gap between "semantic search is on" and "semantic search is working".

### 4. Retrieval runs both retrievers, every time

| Retriever | When it runs | What it contributes |
|---|---|---|
| Pages the reader `@`-mentioned | Whenever present | Forced to the front of the list |
| Vector search | Whenever the workspace has vectors and the owner's toggle is on | Up to **3** distinct pages |
| Postgres full-text search | **Always**, alongside vector search | At least **2** slots, more when vector found fewer |
| Doc-graph lexical search | Only when both of the above returned nothing | Up to **4** pages |
| Agentic search loop | Only when everything above returned nothing | Up to **2** pages |

Vector search pulls the 6 nearest rows by cosine distance, converts them to a similarity of `1 − distance`, drops anything below a similarity floor of **0.25**, deduplicates by page *before* trimming to 3 (six hits are often six sections of one page), and keeps its priority position in the final list.

Full-text search is not a fallback here. It runs on every question and its pages are merged in, capped so vector + lexical together never exceed **5 pages**. The reason is measured on our own index: for the question *"What URL pattern does Docsbook use to serve my documentation site?"*, the correct page's best-matching chunk ranked **48th out of 1,341 chunks** by cosine similarity — 18 other pages scored higher — while lexical search returned it as the top hit, because the page literally contains the query's terms. No `top-k` value fixes that; the ranking itself was wrong for that query. A non-empty but wrong vector result is the failure this merge exists to correct, and an "only run lexical when vector is empty" rule cannot detect it.

The last two rows of the table are for corpora with no index at all. The agentic loop hands the model a `search_docs` tool and lets it re-query with different phrasings for up to **4 round trips** at temperature 0 before it has to commit to at most two page paths — the way you would grep a codebase after your first guess missed.

### 5. The pages are fetched and clipped from the tail

Each selected page is fetched from your repository at its default branch and placed in the prompt with its path and title in a header line. A page over **12,000 characters** is not truncated from the front: the first 9,000 characters and the **last 3,000** are kept, with the omission marked in between. Refund policies, "Related", and troubleshooting sections live at the *end* of a page, so head-truncation drops exactly the part a question is most likely about. The page the reader is currently on is included separately, clipped to 8,000 characters.

### 6. The model is constrained before it writes

The reader chat's default model is `openai/gpt-4o-mini` — a 128,000-token context window and a 16,384-token output cap, per OpenAI's model reference. You can pick a different model per project; see [AI chat](./chat.md#which-model-runs-the-chat).

The system message is short and yours to replace. The grounding rules live in the instruction block that arrives with the content, and they are specific because each one is a failure that happened:

- **Ground only in the provided content.** Never fall back on pretrained knowledge to define a term or fill a gap the docs do not cover.
- **Do not claim absence when the fact is present.** Re-read the provided pages before saying something is missing — including when the fact sits on a page that also covers a paid or optional feature.
- **Keep free and paid behaviour distinct.** Do not blend a detail from the paid page into the description of the default one.
- **The pages were found by search, not vetted by a human.** Check each page against the *specific* thing asked, not against word overlap. A page about locale subdirectories contains the words "URL pattern" without answering a question about the default URL.
- **Watch for the narrower question.** If a page answers a qualified version of the question (a language, a plan, an add-on) and the question carried no such qualifier, that page is answering something else.
- **Setup questions need an exact sentence.** For "how do I set up X", find the sentence naming a concrete menu path, button or step for X. If there is none, say the docs do not describe a built-in X integration — a mention of X elsewhere, or a generic mechanism that could theoretically be wired to X, is not a setup flow.
- **Preconditions are mandatory, and stated twice.** Scan the whole page for a required plan, role, prior step, version or quota — docs put these in a short bolded line at the top that is easy to skip on the way to the numbered steps. A final check immediately before generation re-reads the top of every page, because a precondition stated only in a page intro competes with nothing local by the time the model has read down to the relevant subsection.

The answer is requested as strict JSON — a markdown body and a `refs` array — and streamed at temperature 0.3.

### 7. Citations are attached by the server, not trusted from the model

This is the step that decides whether a citation means anything.

| The model supplies | The server does |
|---|---|
| `pagePath` | Keeps the ref **only if** that path was cited inline in the answer's own `[ref:…]` marker **or** is a page the server actually fetched. A path the model neither read nor quoted is dropped before the reader sees it. |
| `pageTitle` | Used as the link label |
| `headingText`, copied verbatim from the page | Recomputes the anchor itself, with the same slugifier the renderer uses |
| *(nothing)* | The anchor id is never asked for and never accepted from the model |

The anchor rule is not fussiness. A hand-written slug rule ("lowercase, spaces to dashes, strip special characters") disagrees with the renderer on plain ASCII punctuation — `Edge cases & errors` becomes `edge-cases--errors` on the page and `edge-cases-errors` in a hand-rolled rule — and collapses a non-Latin heading to nothing but dashes. One owner computes that string; everyone else asks it.

## What happens when nothing relevant is found

Nothing is fabricated to fill the gap. When every retriever comes back empty, no pages are attached, no `Found N results` line appears, and the instruction the model is left with is to say plainly that the provided content does not answer the question.

The refusal is then treated as data:

- The answer text is scanned for a no-answer pattern; a match dispatches a **`chat.no_answer`** webhook alongside the ordinary `chat.question_asked` event.
- The question lands in **Unanswered questions**, which is the filtered view of every logged chat question whose answer failed that check.
- Readers can thumb an answer down in the widget; those land as a per-page dislike count in your analytics.

A gap in your documentation is worth more as a report line than as a fabricated paragraph — that is the trade this whole page is built around.

## Why this is the right way (evidence)

| Rule in Docsbook | Why it works | Source |
|---|---|---|
| Answer from retrieved pages, not from model memory | Retrieval-augmented models "generate more specific, diverse and factual language than a state-of-the-art parametric-only seq2seq baseline" | Lewis et al., 2020 — [Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://arxiv.org/abs/2005.11401) (NeurIPS) |
| A citation is only valid if it names a page really read | Measured across four generative search engines, "only 51.5% of generated sentences are fully supported by citations" and "only 74.5% of citations support their associated sentence" — a citation the system does not verify is not evidence | Liu, Zhang & Liang, 2023 — [Evaluating Verifiability in Generative Search Engines](https://arxiv.org/abs/2304.09848) |
| Run lexical search on every question, not as a fallback | Over 18 retrieval datasets, "BM25 is a robust baseline" in zero-shot settings while dense retrievers "often underperform… highlighting the considerable room for improvement in their generalization capabilities" — your corpus is out-of-domain for any embedding model | Thakur et al., 2021 — [BEIR](https://arxiv.org/abs/2104.08663) |
| 1,536-dimension vectors, 6,000-character units | `text-embedding-3-small` outputs 1,536 dimensions and accepts 8,192 input tokens; a unit capped at 6,000 characters stays inside that limit with room for the breadcrumb | OpenAI — [Embeddings guide](https://developers.openai.com/api/docs/guides/embeddings) |
| Cap the prompt at five pages, clip long pages from the tail | Model performance "is often highest when relevant information occurs at the beginning or end of the input context, and significantly degrades when models must access relevant information in the middle of long contexts" — more pages is not more accuracy | Liu et al., 2023 — [Lost in the Middle](https://arxiv.org/abs/2307.03172) |
| Instruct refusal explicitly, and record it | Ordinary instruction tuning "force[s] the model to complete a sentence no matter whether the model knows the knowledge or not"; refusal has to be asked for | Zhang et al., 2023 — [R-Tuning: Instructing LLMs to Say "I Don't Know"](https://arxiv.org/abs/2311.09677) (NAACL 2024) |
| Grounding reduces hallucination, it does not remove it | Annotating ~18,000 RAG responses found that even with retrieval, "LLMs may still present unsupported or contradictory claims to the retrieved contents" | Niu et al., 2024 — [RAGTruth](https://arxiv.org/abs/2401.00396) |

## What we measure — and what we do not publish

**We publish no accuracy percentage for Docsbook AI chat.** We have not run a labelled benchmark over customer corpora, and a number produced on our own documentation would tell you nothing about yours. Quoting one would break the rule the rest of these docs are written to.

What exists instead:

| Measurement | What it does | Where it appears |
|---|---|---|
| Answer evaluation judge | An LLM reads a finished conversation transcript (capped at 8,000 characters) at temperature 0 and returns a strict `{answered, reasoning}` verdict | The **Answered** column on the Chat tab |
| Stored once, never re-judged | A transcript does not change, so its verdict does not either — each is written once and read back afterwards | — |
| Bounded per request | At most **6** new conversations are judged per page load, so a workspace with a thousand unrated threads does not pay for a thousand calls the first time somebody opens the tab | — |
| No-answer detection | A pattern match over the answer text, dispatching `chat.no_answer` and feeding Unanswered questions | Webhooks, Unanswered questions |
| Per-answer thumbs | The reader's own verdict on that answer, counted per page | Analytics |
| Retrieval label | Every answer's stream carries which retriever produced its pages — `semantic`, `fulltext`, `semantic+fulltext`, `doc_graph`, `agentic` or `mentions` | The response stream; verifiable with one HTTP call |

That last row is deliberate. "Semantic search is on" is unfalsifiable from the outside, which is exactly how a stamped-but-empty index once passed as working for months. Naming the retriever on every answer makes the claim checkable by anyone, including you.

Docsbook also runs two internal suites — a 40-case golden set that scores which tool the model reaches for first at temperature 0, and a live scenario suite with deterministic checks plus a narrow LLM judge. **Both cover the admin assistant in your dashboard, not the reader-facing chat**, and we say so rather than letting their green ticks be read as a quality claim for this page's subject.

## Limits

- **No published accuracy figure.** See above. Treat any vendor's single accuracy number — ours included, if we ever quote one — as unusable until its corpus, question set and grader are published.
- **Retrieval can be confidently wrong.** The 48th-of-1,341 case above is ours, on our own corpus. Merging lexical retrieval corrects a large class of it; it does not close it. Retrieval is also least reliable exactly where it matters most: measured work finds retrieval helps most on less-popular facts, where the model has nothing memorised to fall back on ([Mallen et al., 2023](https://arxiv.org/abs/2212.10511)).
- **The similarity floor of 0.25 is a fixed constant**, not tuned per corpus. A corpus with unusual vocabulary may need a different floor, and there is no per-project control for it today.
- **The citation filter is an OR, not an AND.** A ref survives if the path was fetched **or** if the model quoted it inline. Requiring both emptied `refs` on almost every answer, because models fill the array and skip the marker. The consequence is that a path the model both invented and quoted inline would pass the filter; only the fetched half is grounded by construction. Under question until the inline half is checked against the corpus too.
- **Grounding is not a proof of faithfulness.** The server can guarantee that a cited page was read; it cannot guarantee that every sentence of the answer follows from it. That residual is what RAGTruth measures, and it is real.
- **The no-answer detector is an English pattern match.** A refusal written in another language will not be recognised, so `chat.no_answer` and the Unanswered questions report under-count on non-English sites. Under question until we publish a measured replacement.
- **Very long pages lose their middle.** A page over 12,000 characters reaches the model as head + tail with the middle marked as omitted. A fact that lives only in the middle of a very long page can be missed. Splitting that page is the fix, and it improves the page for humans too.
- **Model behaviour is version-dependent.** The default reader model, its context window and its refusal behaviour are the provider's to change. The mechanism on this page is ours; the model's compliance with it is not.
- **Semantic retrieval needs vectors.** Until an index run has completed, retrieval falls to full-text and the doc graph. That is a working chat, not a broken one — but it is not the one described in stage 4.

## Related

- [AI chat](./chat.md) — the contract: what the assistant can and cannot do.
- [Search](./search.md) — the lexical index this pipeline shares.
- [Sources](./sources.md) — what the assistant is allowed to read beyond your pages.
- [Chat hooks](./chat-hooks.md) — block a question, or hand the model a fact only your systems know.
- [How Docsbook proves what it claims](../evidence.md) — the rule this page is written to.
