---
title: "Citation signals: how to write a passage an engine will quote"
description: "Each rule that makes documentation quotable by a generative engine, paired with the retrieval behaviour that justifies it and a source you can open."
tldr: "An engine retrieves passages, not pages, so every section must survive being read alone: name the subject in full, answer in the first sentence, and give one extractable fact. Measured to help, on one 10K-query benchmark: quotations, statistics and cited sources. Measured to hurt: keyword stuffing, and rewriting a body for quotability alone."
---

# Citation signals

This page is the writing half of [GEO](./README.md). [Turning GEO on](./README.md) adds a TL;DR block, a date and an author to your pages; nothing in a toggle decides whether a *sentence* is liftable. That is decided by how the section around it is written, and the rules below are the ones with a mechanism behind them.

Every rule is stated the same way: the rule, why the retrieval and generation stack behaves that way, and a source you can open. Where the evidence is thin, the rule says so.

## The rules at a glance

| Rule | Why the stack behaves that way | Source |
|---|---|---|
| Make each section stand alone | Retrieval scores individual passages, not whole pages | [Google ranking systems](https://developers.google.com/search/docs/appearance/ranking-systems-guide) |
| Name the subject in full inside every section | A chunk is embedded without its neighbours; adding back the missing context measurably improves retrieval | [Anthropic, contextual retrieval](https://www.anthropic.com/news/contextual-retrieval) |
| Answer in the first sentence after the heading | Docsbook's own TL;DR extractor and `speakable` markup lift the opening; no public benchmark isolates this on its own | Mechanism, below |
| Add a direct quotation | Quotation Addition is the benchmark's best method: "the best methods improve upon baseline by 41%" on Position-Adjusted Word Count, over 10K queries | [GEO, KDD 2024](https://arxiv.org/abs/2311.09735) |
| Add a statistic | Statistics Addition is one of three methods reported at "a relative improvement of 30-40%" on the same metric | [GEO, KDD 2024](https://arxiv.org/abs/2311.09735) |
| Cite your own sources | Cite Sources is in that same 30-40% group | [GEO, KDD 2024](https://arxiv.org/abs/2311.09735) |
| Write plainly | Fluency Optimization and Easy-to-Understand are reported together as "a significant visibility boost of 15-30%" | [GEO, KDD 2024](https://arxiv.org/abs/2311.09735) |
| Put a byline and a date on the page | Google's self-assessment questions ask whether pages "carry a byline, where one might be expected" | [Creating helpful content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content) |
| Do not keyword-stuff | Keyword Stuffing is filed under "Non-Performing" methods and scores below the untouched baseline; on a live engine it "performs 10% worse than the baseline" | [GEO, KDD 2024](https://arxiv.org/abs/2311.09735) |
| Do not strip prose to make a page "quotable" | Body-only optimisation cut top-20 retrieval presence ~9% and final citation ~6% across 171,003 documents (Kim et al., 2026, summarised in the survey) | [Survey, arXiv 2607.14035](https://arxiv.org/abs/2607.14035) |
| Do not block the agents that cite | An opted-out site "will not be shown in ChatGPT search answers, though can still appear as navigational links" | [OpenAI bots](https://developers.openai.com/api/docs/bots) |

## Why passages, not pages

Google describes its passage ranking system as one that identifies "individual sections or 'passages' of a web page to better understand how relevant a page is to a search" ([ranking systems guide](https://developers.google.com/search/docs/appearance/ranking-systems-guide)). Retrieval-augmented assistants do the same thing more aggressively: the document is split into chunks, each chunk is embedded and scored on its own, and only the winners reach the model.

Anthropic states the failure mode plainly. A chunk reading "The company's revenue grew by 3% over the previous quarter" "doesn't specify which company it's referring to or the relevant time period", so it cannot be retrieved for a question that names the company. Re-attaching that context before embedding "reduced the top-20-chunk retrieval failure rate by 35%", and combined with contextual BM25, "by 49%" ([Anthropic, contextual retrieval](https://www.anthropic.com/news/contextual-retrieval)).

That is a vendor working around prose that does not name its own subject. Prose that *does* name its subject needs no such repair. Which gives the two rules that matter more than all the rest:

- **Name the subject in full inside every section.** "To rotate it, call the endpoint" is unretrievable — nothing in it says which product, or that the thing being rotated is an API key.
- **Answer in the first sentence after the heading**, then elaborate. "Before we get into rotation, it is worth understanding…" is the answer arriving too late to be the passage that gets picked.

**The quote test.** Paste a section into an empty file. If it no longer says what it is about, rewrite it. That is exactly the operation a retriever performs on your page.

## What Docsbook does with these rules mechanically

Three parts of Docsbook read the shapes above directly, so following the rules changes real output rather than only your odds:

- **Your first paragraph becomes your machine summary.** If a page has no `tldr:` in frontmatter, the [GEO](./README.md) TL;DR block is built from the document's first real paragraph — headings, blockquotes, lists, code fences and image-only lines are skipped — capped at 280 characters. A lede shorter than 40 characters produces no block at all.
- **A question heading becomes structured data.** With [AEO](../aeo/README.md) on, any `###` heading ending in a question mark is emitted as a `Question` in `FAQPage` JSON-LD, with the paragraphs beneath it as the answer, up to 20 questions per page and 1,000 characters per answer. Phrasing a heading as the reader's question is therefore not a style preference — it is the input to a detector.
- **`audit_geo` checks the mechanical preconditions**, including whether at least 200 words of body prose are present in the raw HTML with no JavaScript executed, and whether the page states any date at all.

## Rules with a measured effect size

The GEO paper (KDD 2024) built GEO-bench, which "consists of 10K queries", and tested nine content transformations against a generative-engine setup using "only the top 5 sources fetched from the Google search engine for every query". Its visibility metric, Position-Adjusted Word Count, weights how much of the generated answer is attributed to your source by where the citation appears.

These are the figures the paper itself prints. It reports bands and a headline, not a per-method percentage table, so neither do we:

| What the paper reports | Its own words |
|---|---|
| The best method, on Position-Adjusted Word Count | "The best methods improve upon baseline by 41% and 28% on Position-Adjusted Word Count and Subjective Impression respectively" (the best is Quotation Addition) |
| Cite Sources, Quotation Addition, Statistics Addition | "achieved a relative improvement of 30-40% on the Position-Adjusted Word Count metric and 15-30% on the Subjective Impression metric" |
| Fluency Optimization and Easy-to-Understand | "stylistic changes such as improving fluency and readability of the source text … also resulted in a significant visibility boost of 15-30%" |
| Keyword Stuffing and Unique Words | Grouped in the results table under "Non-Performing Generative Engine Optimization methods". Keyword Stuffing scores below the untouched baseline |
| The same nine methods on a live engine (Perplexity.ai) | "Quotation Addition performs best in Position-Adjusted Word Count with a 22% improvement over the baseline", and Keyword Stuffing "performs 10% worse than the baseline" |
| Overall | "GEO can boost visibility by up to 40% in generative engine responses" |

Read those bands as "which sentences a model reuses once your page is already in front of it", not as a traffic forecast — see the limits below. The paper also reports that effects vary by domain: its top-performing tags for Statistics Addition are Law & Government, Debate and Opinion, and for Quotation Addition People & Society, Explanation and History.

Practically: **give every page something extractable** — a limit, a timeout, a version, a one-sentence definition, or a number with its source named. Concrete facts are what a model lifts verbatim. And **never invent one**: a wrong figure repeated by an assistant is worse than no answer, and it will outlive your correction.

## Rules about what not to do

**Do not keyword-stuff.** It is the only transformation in the benchmark that scored *below* leaving the page alone.

**Do not strip your prose down to make it "quotable".** The 2026 critical survey of 45 GEO studies reports a controlled result (Kim et al., 2026; 171,003 documents, 2,700 queries) in which optimising only the body of a page "reduces average top-20 presence by approximately 9%, top-10 presence after reranking by 16%, and final citation by 6%" ([arXiv 2607.14035](https://arxiv.org/abs/2607.14035)). The survey's explanation is the one to remember: a rewrite can raise the chance of being cited *given* retrieval while lowering the chance of being retrieved at all, and the total effect goes negative. Prose carries the synonym variety that matches varied questions. Add the definition and the number **alongside** it, never instead of it.

**Do not block the agents that do the citing.** Vendors run different crawlers for different purposes, and blocking one does not block the others:

| Agent | Vendor's own description | Purpose |
|---|---|---|
| `OAI-SearchBot` | "used to surface websites in search results in ChatGPT's search features" — opted-out sites "will not be shown in ChatGPT search answers" | Search |
| `GPTBot` | "crawl content that may be used in training our generative AI foundation models" | Training |
| `Claude-SearchBot` | "navigates the web to improve search result quality for users" | Search |
| `ClaudeBot` | "collecting web content that could potentially contribute to their training" | Training |
| `PerplexityBot` | "surface and link websites in search results on Perplexity. It is not used to crawl content for AI foundation models" | Search |

Sources: [OpenAI](https://developers.openai.com/api/docs/bots), [Anthropic](https://support.claude.com/en/articles/8896518-does-anthropic-crawl-data-from-the-web-and-how-can-site-owners-block-the-crawler), [Perplexity](https://docs.perplexity.ai/guides/bots). Blocking training while allowing search is a coherent business decision. Blocking the search agent while expecting citations is the incoherent one, and it is almost always accidental — [`audit_geo`](./README.md) reports it as critical.

**Do not expect a special file or schema to substitute for the writing.** Google states there are "no additional requirements to appear in AI Overviews or AI Mode, nor other special optimizations necessary", and "You don't need to create new machine readable files, AI text files, or markup" ([Google AI features](https://developers.google.com/search/docs/appearance/ai-features)). See [llms.txt](./llms-txt.md) for the same question asked of that file specifically.

## Limits and open questions

- **The measured gains are conditional on already being retrieved.** The 2026 survey concludes the foundational results are "valid within its experimental setting but conditional on a source already being present in a fixed context", and that "no reviewed technique shows a stable, longitudinal, cross-platform causal effect on organic discoverability or downstream behavior". Everything above improves your odds once you are in the context window. Getting into it is [SEO](../seo/README.md) work.
- **Under question: does freshness raise citation rate?** Google documents "query deserves freshness" systems for *Search ranking*, and a page with no date gives a model nothing to attribute currency to. No primary source measures a citation-rate lift from a visible date. Treat freshness as hygiene until someone publishes a measurement.
- **One run proves nothing.** Audits summarised in the survey: Schulte et al. (2026) "observe daily source-level Jaccard scores of approximately 0.34–0.42" across four engines and 45 days, and propose "seven to eight repetitions per prompt as a starting point"; Kirsten et al. (2026) report "page overlap across two months is 18% for AI Overviews, compared with 45% for organic Google". Repeat any before-and-after check several times before believing it.
- **The numbers above are from one benchmark and one era.** GEO-bench was evaluated in 2024 on a fixed engine configuration. The direction of the findings has held up in review; the magnitudes should not be quoted as your expected result.
- **Docsbook measures none of this for you.** What your analytics can show is the trace: crawler hits from assistant user agents and referral traffic from assistant domains. A citation you did not observe is not a metric.

## Related

- [GEO](./README.md) — what Docsbook injects into the page, and how to check it.
- [llms.txt](./llms-txt.md) — the site-level machine index and its evidence.
- [AEO](../aeo/README.md) — question headings, `FAQPage` and `HowTo` markup.
- [SEO](../seo/README.md) — indexing and crawlability, the stage before citation.
- [Analytics](../analytics/README.md) — where assistant crawler hits and referrals show up.
