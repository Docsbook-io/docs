---
title: "Writing for retrieval: how an assistant picks a passage"
description: "How to write documentation an answer engine can retrieve and quote: self-contained chunks, answer-first sections, and the polish that backfires."
tldr: "An answer engine does not read your page. It retrieves passages from many pages, reranks them, and writes an answer over the survivors — so the chunk is the unit of competition, not the page. Getting retrieved is a similarity problem and getting cited is an extractability problem, and they pull in opposite directions: in the measured case, rewriting bodies purely for quotability cut top-20 retrieval presence by about 9%."
---

# Writing for retrieval

An assistant answering a question about your product does not open your page and read it. It decomposes the question into sub-queries, retrieves candidate **passages** from many pages, reranks them, fits the survivors into a context window, and generates an answer citing some of them. Your page competes as a bag of independent chunks, several times over, against passages from other sites.

Two consequences drive everything on this page:

1. **The chunk is the unit, not the page.** A section that only makes sense after the three above it loses at retrieval, because it is scored alone.
2. **There are two stages and they pull in opposite directions.** Getting *retrieved* is a similarity problem: does this passage look like the answer to that sub-query? Getting *cited once retrieved* is an extractability problem: can the model lift a clean claim out of it? Optimising only for the second is the most common and most expensive mistake — see [the polish that backfires](#how-do-i-avoid-wrecking-retrieval-while-polishing-for-citation).

This work applies to publicly reachable content only. A private or internal documentation set has no retrieval problem, because nothing is retrieving it.

## What does the evidence actually support?

Be honest about tiers, and be equally explicit when you report a finding to somebody who will spend a week on it.

| Tier | Meaning | Examples |
|---|---|---|
| **Strong** | Robust across studies and engines | Topical relevance and position dominate everything else; passage-level competition; self-contained chunks |
| **Moderate** | Real but conditional — helps once retrieved, varies by query type | Adding statistics, quotations, cited sources; answer-first structure |
| **Weak or contested** | Cheap to do, unproven at scale | A machine-readable index file at the site root; exhaustive FAQ markup on non-FAQ pages |
| **Negative** | Measurably backfires | Keyword stuffing; body rewrites tuned purely for quotability |

The controlled study behind the moderate tier ran 10,000 queries and tested nine content transformations ([GEO, KDD 2024](https://arxiv.org/abs/2311.09735)). Adding quotations, adding statistics and citing sources are its three strongest methods, reported together at "a relative improvement of 30-40% on the Position-Adjusted Word Count metric", with the best of them — quotation addition — at 41%. The same benchmark files **keyword stuffing under non-performing methods, scoring below the untouched baseline**.

A 2026 survey of 45 studies ([arXiv 2607.14035](https://arxiv.org/abs/2607.14035)) qualifies all of it. Those gains are conditional on the source already being present in the context; only 3 of 54 method–domain combinations replicated as significantly positive on an independent benchmark; and, critically, body-only optimisation **reduced top-20 retrieval presence by about 9%**.

Treat every moderate-tier tactic as a garnish on a passage that already earns its retrieval, never as a substitute. **Never promise a citation-rate lift.** The survey's own conclusion is that no reviewed technique shows a stable, cross-platform causal effect on organic discoverability. "Content optimisation raises how often engines surface you" is repeated constantly and is not settled: there is one benchmark study behind it, its headline is an "up to" figure, and it says itself that the effect varies across domains. State the mechanism and its tier; do not forecast a number.

## Where do the real questions come from?

From logs, not from imagination. The retrieval query is a *question*, usually in the reader's words, not your feature's name — and optimising against invented questions is what makes documentation "AI-optimised" and still uncited.

Sources, best first:

1. **The site's own assistant logs and failed searches** — the literal strings people typed. Two readings matter: the questions the assistant could not answer ([`get_ai_unanswered`](../../mcp/analytics/get-ai-unanswered.md)) and the searches that returned nothing ([`get_failed_searches`](../../mcp/analytics/get-failed-searches.md)). This beats any keyword tool because the phrasing is real. [`get_ai_questions`](../../mcp/analytics/get-ai-questions.md) and [`get_popular_searches`](../../mcp/analytics/get-popular-searches.md) give you the same vocabulary for questions that *did* get answered.
2. **Support tickets and community threads** — the same value, more noise.
3. **Sub-query decomposition** — for each real question, write the 3–8 sub-questions an engine would fan out into. "How do I deploy X to production?" fans into build configuration, environment variables, custom domain, rollback. Each needs a passage that answers it *alone*.

The third source is not a guess about engine behaviour. Google describes the mechanism itself: AI Mode "uses our query fan-out technique, breaking down your question into subtopics and issuing a multitude of queries simultaneously on your behalf" ([Google, AI in Search](https://blog.google/products/search/google-search-ai-mode-update/)). The page that gets used is the one covering the whole fan, not the one matching the typed words.

Write the list down before touching content. Every chunk you write should map to at least one question on it. Mapping to none is fine — it just is not a retrieval target, so do not spend optimisation effort there.

## How do I make every section a standalone chunk?

Write each section so that it names its own subject and answers one question completely. This is the highest-leverage step on the page, and the one that is unambiguously supported.

A retrievable chunk:

- **Names its subject in full.** Chunks are scored without their parent heading in many pipelines, so "it" and "this" pointing outside the chunk destroy relevance.
- **Answers one question.** One idea per block, 2–4 lines.
- **Repeats the entity, not the keyword.** Restating the product or feature name naturally in each section is entity grounding and it helps. Cramming query strings is stuffing, and stuffing scored *below* baseline. The difference is whether a human reads it as normal prose.
- **Survives the quote test.** Copy the section into a blank file. Without the rest of the page, does it still state what it is about and give a correct, complete answer?

Apply the quote test literally. It catches more real problems than any checklist, because it is the same operation a retriever performs on your page.

### The heading is the query, not the topic

Headings are chunk boundaries in most splitters and carry disproportionate weight in matching.

- Prefer the reader's question form where the section answers a question: `## How do I rotate an API key?` beats `## Key rotation`.
- Keep them literal and unclever: `## Troubleshooting 403 errors` beats `## When things go wrong`.
- **Do not turn every heading into a question.** Reference tables, concept explanations and API listings are not questions. Forcing question form on them is the same cargo cult as forcing FAQ markup onto prose.

## How much of the answer belongs in the first 60 words?

All of it. After a question-shaped heading, the first paragraph is the complete answer, standalone, with no preamble. Then elaborate.

**Bad**

```markdown
## How do I rotate an API key?

Before we get into rotation, it's worth understanding how the authentication
model works. Keys are scoped per workspace, and…
```

**Good**

```markdown
## How do I rotate an API key?

Rotate an API key in **Workspace settings → API keys → Rotate**. The old key
keeps working for 24 hours, so running deployments do not break. Rotation does
not change the workspace ID or any webhook URLs.

Rotation is scoped to a single workspace…
```

The good version answers the sub-query completely inside one chunk, names the entity, and states the non-obvious consequence — which is the part an assistant will quote.

This applies to page openers too: say what the page is and what the reader will be able to do, in the first two sentences. Never open with history or a welcome.

## What makes a passage extractable once it is retrieved?

Evidence a model can lift without rewriting. Once a passage is in context, these raise the odds it is quoted rather than paraphrased away. They are moderate tier — real, conditional, and worth doing wherever they are honest.

- **Concrete numbers** — limits, timeouts, sizes, rates, versions, prices. "The upload limit is 50 MB per file on the free plan and 2 GB on the paid one" is far more quotable than "generous upload limits".
- **Definitional sentences** — one sentence that literally defines the term. Models lift these verbatim.
- **Comparison tables** — structured, self-labelling rows survive chunking well and answer "X vs Y" sub-queries directly. Every row must be readable without the surrounding prose.
- **Sourced claims** — link the authoritative source when stating a standard, a specification, or third-party behaviour.

Hard constraint: **never invent a statistic, a limit, a price or a quotation to satisfy this step.** Fabricated evidence is the documented failure mode of this whole field. If a number is not known, omit it and say so — a wrong limit inside an assistant's answer is worse than no answer.

## How do I avoid wrecking retrieval while polishing for citation?

Add evidence alongside the existing prose; never rewrite the body to be maximally quotable. This is the most expensive mistake in the field and the one almost no guide mentions.

Tightening, condensing and stripping "redundant" background removes exactly the terminology diversity that makes a passage match varied sub-queries. In the measured case that cost about **9% of top-20 presence** and about **16% of post-rerank top-10 presence**, to buy a citation gain on the smaller set that still got through ([arXiv 2607.14035](https://arxiv.org/abs/2607.14035)).

- **Add, do not replace.** Introduce the definition, the number, the table *alongside* existing prose. Do not delete the paragraph that happens to contain the synonym someone will search with.
- **Keep natural synonym variety.** Readers ask about "API key", "token", "credentials", "secret". A passage mentioning the realistic variants matches more sub-queries. That is not stuffing — it is how a human would write it anyway.
- **Never trade breadth for polish on a page that already gets assistant traffic.** Check the page's traffic and its crawler user agents first, and treat a well-retrieved page as load-bearing.

## What has to be true of the surface before any of this matters?

The page has to be fetchable and readable as plain HTML. Content wins retrieval; the surface decides whether a crawler ever sees it. Verify each of these, do not assume them.

- **Server-rendered HTML.** If content only appears after client-side JavaScript, most assistant crawlers will not see it. Fetch the page plainly and grep for a sentence from the body — this catches more silent failures than anything else here. [How indexing works](../../seo/indexing.md) covers the stage before retrieval.
- **Crawler access.** Fetch `robots.txt` and read it verbatim; never recall the agent list from memory, because vendors change it on their own release cycles. Blocking assistant crawlers is a legitimate business decision, but it has to be a *decision* — a blanket block nobody remembers making is a common cause of "we're never cited". Which agent does what is [below](#which-crawler-is-which).
- **Structured data where it is genuine.** Answer markup on real question-and-answer content and real procedures. Where the platform has switches for it, enabling them is high-leverage — but pair the switch with the content it needs, and do not bulk-add FAQ markup to prose that is not a FAQ. Google narrowed the FAQ rich result to authoritative government and health sites in August 2023 and removed it from Search in May 2026 ([Google, FAQPage structured data](https://developers.google.com/search/docs/appearance/structured-data/faqpage)), so blanket FAQ markup is now maintenance without an upside. Docsbook's own switches are described in [AEO](../../aeo/README.md).
- **A machine-readable index file at the site root** — weak tier. Adoption is concentrated in developer-tool documentation; some assistant vendors say they read it, and Google says outright that "you don't need to create new machine readable files, AI text files, or markup" to appear in AI Overviews or AI Mode ([Google, AI features and your website](https://developers.google.com/search/docs/appearance/ai-features)). It costs an hour. Ship it, and attribute no outcome to it — see [llms.txt](../../geo/llms-txt.md), which Docsbook generates for you either way.
- **Freshness.** Visible update dates and real revision. Freshness weighting varies sharply by model and shifts between versions; treat it as hygiene, not a lever.

### Which crawler is which?

Every major vendor runs **separate agents** for training, for its search index and for a fetch a reader triggered, so blocking one does not block the others. Put every rule in your file into one of those three columns before concluding anything:

| Vendor | Training | Search index | Triggered by a person |
|---|---|---|---|
| [OpenAI](https://developers.openai.com/api/docs/bots) | `GPTBot` | `OAI-SearchBot` | `ChatGPT-User` |
| [Anthropic](https://support.claude.com/en/articles/8896518-does-anthropic-crawl-data-from-the-web-and-how-can-site-owners-block-the-crawler) | `ClaudeBot` | `Claude-SearchBot` | `Claude-User` |
| [Perplexity](https://docs.perplexity.ai/guides/bots) | — | `PerplexityBot` | `Perplexity-User` |
| [Google](https://developers.google.com/search/docs/crawling-indexing/google-common-crawlers) | `Google-Extended` | `Googlebot` | — |

OpenAI states the independence outright: a site can "allow OAI-SearchBot in order to appear in search results while disallowing GPTBot" ([OpenAI, crawlers and user agents](https://developers.openai.com/api/docs/bots)). Google states that Google-Extended "does not impact a site's inclusion in Google Search nor is it used as a ranking signal in Google Search" ([Google crawlers overview](https://developers.google.com/search/docs/crawling-indexing/google-common-crawlers)). Perplexity states that `Perplexity-User` "generally ignores robots.txt rules", because a person requested the fetch ([Perplexity crawlers](https://docs.perplexity.ai/guides/bots)) — so a wall you believe is there may not be. A site that blocks a search-index agent while expecting citations is the usual accident.

## How do I measure this honestly?

By repetition, per engine, on outcomes you can see in your own logs. Reporting a citation win from a single prompt is noise, not evidence.

- **Repetition is mandatory.** The same prompt on the same engine returns substantially different sources run to run — measured daily source-level overlap of 0.34–0.42 within 24 hours ([arXiv 2607.14035](https://arxiv.org/abs/2607.14035)). Use **7–8 repetitions per prompt minimum**.
- **Engines do not agree.** Citation overlap between two versions of the *same* model family was measured at 7%. Never generalise from one engine to "AI".
- **Search rank is not a proxy.** Roughly half of assistant-cited domains do not rank in the main search engine at all. AI Overviews is the exception, where about 76% of citations also sit in the top 10.
- **Grade what was said, not whether you were named.** An answer that names you and repeats a price you changed last quarter is worse than an absence, and it is fixable today: the sentence it is quoting is usually still on your own site.
- **What to actually track:** crawler hits from assistant user agents in your server logs, referral traffic from assistant domains, and — where the tooling exists — the site's own unanswered-question rate falling.

If somebody asks "did this work?", the honest answer is usually "assistant referrals and crawler fetches moved, or did not move" — not a citation-rate number. [Did it work?](../auditing/did-it-work.md) covers writing the baseline down before the change, which is the only thing that makes the question answerable later.

## Issue vocabulary

Use these names when reporting a retrieval finding, and always carry the evidence tier with the finding.

| Issue | What it means |
|---|---|
| `chunk_not_self_contained` | The section depends on text above it to make sense |
| `answer_not_first` | The answer arrives after preamble instead of in the first 60 words |
| `heading_not_query_shaped` | The heading names a topic where the section answers a question |
| `multi_question_section` | One section answers three questions and competes weakly for all three |
| `no_extractable_evidence` | Nothing in the passage is liftable — no number, definition or sourced claim |
| `keyword_stuffed` | Query strings crammed in; scores below an untouched baseline |
| `client_rendered_only` | The body prose is absent from the raw HTML |
| `crawler_blocked` | `robots.txt` disallows an agent whose citations the owner expects |
| `stale_undated` | The page states no date, and its content has not been revised |

A report presenting a weak-tier suggestion with the same confidence as a strong-tier one is how this field became a cargo cult.

## Related

- [Citation signals](../../geo/citation-signals.md) — the same rules paired with the verbatim source line behind each one.
- [GEO in Docsbook](../../geo/README.md) — the page-level signals Docsbook injects for you, and the honest size of the effect.
- [Writing rules](./writing-rules.md) — the minimum version of this, inside the rules for writing any page.
- [Presentation](./presentation.md) — rendered blocks that keep the underlying markdown plain, which is what a crawler reads.
- [From a finding to a change](./from-finding-to-change.md) — what to do when an audit reports that an assistant cannot answer from a page that covers the topic.
