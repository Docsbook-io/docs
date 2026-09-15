---
title: "The documentation handbook: how to write, structure, audit and maintain docs"
description: "Docsbook's working knowledge of documentation as a craft — how to shape a page, plan a doc set, read the numbers, run an audit, and keep it all current. Every strong claim carries the source under it."
tldr: "This is the craft half of Docsbook's documentation: not how to configure the product, but how to do the work well. Six sections — writing, planning, auditing, the fourteen audit lenses, keeping it current, and the evidence registry that says who backs each claim and how strongly."
---

# The documentation handbook

Everything else on this site answers *how do I make Docsbook do X*. This section answers the harder question underneath it: **what is worth doing, and what makes it good.**

It is the knowledge a documentation team accumulates over years — how a page has to be shaped before an answer engine can quote it, which number actually settles a question and which one only looks like it does, why a page that ranks can still be the wrong shape for the query, what to do in the week after a core update, and when an alert is worth installing versus when it becomes noise nobody reads by Thursday.

Two things make it usable rather than merely long:

- **Every strong claim names its source.** Where Google publishes something, we quote Google and link the page. Where a number comes from one practitioner's account, it is marked as one practitioner's account and you are told not to put it in a proposal. The whole registry is in [Evidence](./evidence/README.md).
- **You can ask it instead of reading it.** This corpus is what Docsbook's own assistant answers from. Ask it a question in the **Ask AI** box on any page of this site, or call `ask_docsbook` from an agent, and the answer comes back cited from the pages below.

## The six sections

<!-- widget:cards cols=2 -->

- [Writing](./writing/README.md) — what the page itself says: rules that catch errors while you write, writing for retrieval, presentation, and docs that ask for the sale. {file-text}
- [Planning](./planning/README.md) — deciding the page set before writing a page: which route you are on, what your reader is actually trying to do, and how to publish it. {compass}
- [Auditing](./auditing/README.md) — reading the evidence: which metric settles what, the behavioural and content detectors, and how to tell whether the change you shipped worked. {chart-line}
- [The fourteen lenses](./lenses/README.md) — the named readings an audit can take, from jobs-to-be-done to AI citation to market expansion, and the router that picks the two or three yours needs. {search}
- [Keeping it current](./automation/README.md) — drift, monitors, events and CI checks: making the work keep happening without a person remembering to do it. {history}
- [Evidence](./evidence/README.md) — the sources and the graded claims. What is established, what is contested, what is merely repeated. {scale}

<!-- /widget -->

## Where to start, by what you are doing

| You are… | Start here |
|---|---|
| Writing documentation that does not exist yet | [Which route are you on](./planning/route-the-input.md), then [Deciding the page set](./planning/page-set.md) |
| Improving pages that already exist | [Writing rules](./writing/writing-rules.md), then [Writing for retrieval](./writing/retrieval.md) |
| Trying to find out why traffic fell | [Metrics without being confidently wrong](./auditing/metrics.md), then [Choosing a lens](./auditing/choosing-a-lens.md) |
| Trying to get quoted by ChatGPT, Perplexity or AI Overviews | [The GEO and AI-search lens](./lenses/geo-ai-search.md), then [Writing for retrieval](./writing/retrieval.md) |
| Tired of the docs going stale | [Drift](./automation/drift.md) and [Monitors and alerts](./automation/monitoring.md) |
| Deciding whether a tactic is worth a sprint | [Claims](./evidence/claims.md) — find it, read its standing |

## What this handbook is not

It is not Docsbook's product documentation. When a page here says a reading is worth taking, it links out to the product page that takes it — [analytics](../analytics/README.md), [SEO](../seo/README.md), [GEO](../geo/README.md), [translations](../translation/README.md), [the MCP server](../agent-ready/mcp.md) — rather than restating how the feature is configured.

It is also not neutral about its own limits. Several of the most-repeated claims in this field are, on inspection, one webinar deep. Those are marked `hypothesis` and carry a test you can run on your own site instead, because the number that survives a customer asking "says who?" is the one you measured yourself.
