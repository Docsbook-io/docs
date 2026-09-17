---
title: "Sources: the references behind the documentation handbook"
description: "Every reference this handbook cites — vendor documentation, one peer-reviewed study, the llms.txt specification, Diátaxis, five practitioner field reports and four of our own measurements — with what each one actually says and when we last read it."
tldr: "Twenty-two references, each with the line we quote from it verbatim and the date we last opened it. Vendor documentation and the KDD 2024 GEO study can settle a claim on their own; practitioner field reports never can, and are recorded here so a hypothesis has a traceable origin instead of being something somebody once said."
---

# Sources

Grouped by what they are about rather than by how strong they are — the question people arrive with is "what backs the GEO advice", not "show me the vendor docs". How much each kind can settle is in [Evidence](./README.md).

## What answer engines actually require

### Google — AI Features and Your Website

[developers.google.com/search/docs/appearance/ai-features](https://developers.google.com/search/docs/appearance/ai-features) · Google Search Central · vendor documentation · read 14 September 2026

> There are no additional requirements to appear in AI Overviews or AI Mode, nor other special optimizations necessary. To be eligible to be shown as a supporting link in AI Overviews or AI Mode, a page must be indexed and eligible to be shown in Google Search with a snippet. You don't need to create new machine readable files, AI text files, or markup to appear in these features.

This is the single most useful page in the registry, because it contradicts most of what is sold as GEO. It stands under [no special markup is needed](./claims.md#there-is-no-markup-that-makes-a-page-eligible-for-ai-overviews).

### Google — AI in Search: going beyond information to intelligence

[blog.google/products/search/google-search-ai-mode-update](https://blog.google/products/search/google-search-ai-mode-update/) · Google (The Keyword) · vendor documentation · published 20 May 2025 · read 14 September 2026

> AI Mode uses our query fan-out technique, breaking down your question into subtopics and issuing a multitude of queries simultaneously on your behalf.

### GEO: Generative Engine Optimization

[arxiv.org/abs/2311.09735](https://arxiv.org/abs/2311.09735) · Aggarwal, Murahari, Rajpurohit, Kalyan, Narasimhan, Deshpande — KDD 2024 · research · published 28 June 2024 · read 14 September 2026

> GEO can boost visibility by up to 40% in generative engine responses; the efficacy of these strategies varies across domains.

The only peer-reviewed study in this registry, and the origin of the 40% figure that circulates without its two qualifiers. It is a benchmark, not your site, and none of it was measured on documentation specifically.

### The /llms.txt file, v2

[llmstxt.org](https://llmstxt.org/) · Jeremy Howard · standard · published 10 August 2026 · read 14 September 2026

> Adding a /llms.txt markdown file to websites to provide LLM-friendly content. The file may sit at the root or at a subpath such as /docs/llms.txt, covering all URLs under its location; where several apply, the most specific one is used.

A specification says what a format **is**. It says nothing about whether anyone honours it — which is why `llms.txt` has [a claim of its own](./claims.md#llmstxt-is-a-proposal-not-an-engine-requirement) rather than inheriting authority from the spec.

## Who is actually fetching the page

All four vendors document **separate agents** for training, for their search index, and for a fetch a person triggered. That split is the whole subject.

### OpenAI — crawlers and user agents

[developers.openai.com/api/docs/bots](https://developers.openai.com/api/docs/bots) · OpenAI · vendor documentation · read 14 September 2026

> OAI-SearchBot surfaces websites in ChatGPT's search features; GPTBot crawls content that may be used in training; ChatGPT-User visits a page when a user asks a question; OAI-AdsBot validates ad pages. Each setting is independent of the others — a webmaster can allow OAI-SearchBot in order to appear in search results while disallowing GPTBot.

### Anthropic — does Anthropic crawl data from the web?

[support.claude.com](https://support.claude.com/en/articles/8896518-does-anthropic-crawl-data-from-the-web-and-how-can-site-owners-block-the-crawler) · Anthropic · vendor documentation · read 14 September 2026

> ClaudeBot collects web content that could contribute to training; Claude-User accesses websites when individuals ask Claude questions; Claude-SearchBot navigates the web to improve search result quality.

### Perplexity — crawlers

[docs.perplexity.ai/guides/bots](https://docs.perplexity.ai/guides/bots) · Perplexity · vendor documentation · read 14 September 2026

> PerplexityBot surfaces and links websites in search results on Perplexity. Perplexity-User supports user actions and generally ignores robots.txt rules, since a user requested the fetch.

### Google — crawlers (user agents) overview

[developers.google.com/search/docs/crawling-indexing/google-common-crawlers](https://developers.google.com/search/docs/crawling-indexing/google-common-crawlers) · Google Search Central · vendor documentation · read 14 September 2026

> Google-Extended does not impact a site's inclusion in Google Search nor is it used as a ranking signal in Google Search. Crawling preferences addressed to the Googlebot user agent affect Google Search, including Discover and all Google Search features.

## What Google rewards, and what it stopped rewarding

### Creating helpful, reliable, people-first content

[developers.google.com/search/docs/fundamentals/creating-helpful-content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content) · Google Search Central · vendor documentation · read 14 September 2026

> Experience, expertise, authoritativeness, and trustworthiness, or what we call E-E-A-T. Is it self-evident to your visitors who authored your content? Do pages carry a byline, where one might be expected? If the "why" is that you're primarily making content to attract search engine visits, that's not aligned with what our systems seek to reward.

### FAQ (FAQPage) structured data

[developers.google.com/search/docs/appearance/structured-data/faqpage](https://developers.google.com/search/docs/appearance/structured-data/faqpage) · Google Search Central · vendor documentation · read 14 September 2026

> From August 2023 the feature is only shown for well-known, authoritative government and health websites; the FAQ rich result was removed from Google Search in May 2026.

Worth carrying precisely because FAQ markup is still recommended constantly.

### Google Search's core updates and your website

[developers.google.com/search/updates/core-updates](https://developers.google.com/search/updates/core-updates) · Google Search Central · vendor documentation · read 14 September 2026

> We recommend waiting at least a full week after a core update completes before analyzing your site in Search Console. Avoid doing "quick fix" changes. There's no need to take drastic action — in fact, we recommend avoiding making changes to content that's already performing well. It could take several months for our systems to learn and confirm that the site as a whole is now producing helpful, reliable, people-first content.

### Interaction to Next Paint (INP)

[web.dev/articles/inp](https://web.dev/articles/inp) · Google (web.dev) · vendor documentation · read 14 September 2026

> An INP below or at 200 milliseconds means good responsiveness; above 500 milliseconds is poor. Assessed at the 75th percentile of page loads recorded in the field.

## How a page is shaped

### Diátaxis — a systematic framework for technical documentation

[diataxis.fr](https://diataxis.fr/) · Daniele Procida · framework · read 14 September 2026

> Four distinct needs, and four corresponding forms of documentation: tutorials (learning), how-to guides (a task), reference (information), explanation (understanding).

A framework is not evidence that something works. It is evidence that it has a definition — which is what stops four people on one team meaning four different things by "reference page".

## The field, as practitioners report it

Five recorded practitioner talks, September 2026. They are the origin of several of the sharpest working hypotheses in this handbook, and **none of them can settle a claim on its own.** They are private working notes rather than published write-ups, so they are recorded here by title, speaker and date rather than by link — an unverifiable citation is provenance, not proof, and that is exactly why the claims resting on them are graded `hypothesis` or `contested`.

Where two of them disagree, the disagreement is recorded as a [contested claim](./claims.md#what-actually-drives-whether-you-are-cited) rather than resolved by picking the more recent speaker.

### How AI search actually works — a GEO/AEO teardown

Practitioner talk · recorded 14 September 2026 · the most contrarian source in the registry

The funnel, as this source describes it: a prompt is fanned out into sub-queries, a web search returns on the order of sixty URLs, candidates are selected, and a much smaller set is cited. GEO therefore manages **probabilities, not positions** — answers differ by user, region, model and day — and the work happens on the search layer rather than on the model's weights, which move only on a slow reputation timescale.

Its central and most disputed figure:

> SERP position accounts for roughly 80% of the citation outcome, and past position 10 there is a cliff. Schemas, E-E-A-T, expertise signals and tables are secondary; textual relevance matters more.

Attributed to the speaker's own research and an independent study by Georgy Shilov, neither published. Three further claims from it, each carried into this handbook:

- Roughly **70% of cited URLs come from fan-out sub-topics, not from the main query**. Worked example, "how to brew coffee": what got cited was water chemistry, extraction and taster protocols — not the brewing guides.
- ChatGPT draws roughly 50% from Google and Bing and roughly 30% from direct site search; for commercial queries it is Google. Supported by an experiment worth more than the percentages: **a section closed to everything except Google was indexed in ChatGPT exactly as it was in Google.**
- An assistant names a brand as the solution when **the cited URLs describe it as the solution**. Consensus across sources beats volume of mentions, and links are not the mechanism — the model will find the brand's own site.

### SEO fundamentals in 2026, in six blocks

Igor Burdukov · recorded 14 September 2026

Demand and the semantic core (one query, one intent, one page) · structure derived from demand · technical health · content of substance, with models used as a skeleton rather than a keyword generator · trust and commercial signals · the link profile, where a spike is more often a competitor's spam than a win.

Its most useful contribution is the negative one — **when search is the wrong instrument at all**: no demand, heavy seasonality, impulse purchases, or no resource for a twelve-month horizon.

### How search changed in 2026, and how to rebuild for AI answers

Oleg Shestakov, Rush Agency · recorded 14 September 2026

Reported from agency practice: sites cited in Google's AI answers see about 35% more click-throughs (attributed to Stackmatics); after the March 2026 update 24% of top-10 pages fell out of the top 100, mostly compilations and AI text with no named expert; thematic clusters gave +46% traffic over six months and 3.2× more mentions in AI answers; a page slower than three seconds loses 23% of its traffic. A page's format has to match the format currently ranking for the query, and the first two paragraphs have to answer with facts and figures or nothing is quoted.

Its worked example is the clearest illustration of the format rule in the registry: GetAccept out-ranked DocuSign for "Electronic Signature Software" with a comparative review rather than a product page.

### What the May 2026 core update changed, and what to do during a rollout

Oleg Shestakov · recorded 14 September 2026

Informational pages, affiliate round-ups, bulk AI content and simple calculators are the ones being replaced by the answer itself; brands, real expertise and pages that close a commercial intent hold. During a rollout: do not rewrite the site, do not bulk-delete pages, do not buy links. Diagnose by separating impressions, positions and click-through rate before and after the date, then move informational pages toward action and rewrite the first two paragraphs of the key pages so they are a fragment an engine can lift.

### GEO overview — three mechanisms and an audit checklist

Practitioner talk · recorded 14 September 2026

GEO does not replace search optimisation, it sits on top of it. Queries have become conversational sentences with conditions, and what gets cited is the page with the direct answer in the first paragraph. The model takes a specific paragraph, table or list, never the whole page.

**Three mechanisms produce an answer:** real-time retrieval over the top of the index, the AI layer inside the search engine, and the model's own memory of having seen the brand mentioned. The third is why the target is not the top three but *being among the model's sources* — reviews, industry media, forums, encyclopaedias, and mentions that carry no link at all.

Its audit checklist is the method this handbook recommends for measuring citation: take ten real queries from Search Console, ask them in plain conversational language in several assistants, and record who was named instead of you, which sources were cited, and what those articles say about competitors.

Every number in this section is reported, not verified. The mechanisms behind them are well supported and safe to explain; the figures are not safe to put in a proposal. Each claim that rests on one of them says so and gives you a test to run instead.

## What we measured ourselves

Four measurements, each taken on a stated date against a stated subject. They are strong about that subject and silent about anybody else's, which is the only reason they may be quoted at all. They are recorded here without links because they live in Docsbook's own private repository and test suite.

| Measurement | Date | What it found |
|---|---|---|
| A documentation vendor serving `llms.txt` at a subpath | 13 August 2026 | Measured live: `mintlify.com` serves `llms.txt` at `/docs/llms.txt` and has none at the root. A check that looked only at the root would have reported "you have no llms.txt" to a site that has one. |
| Generated heading anchors disagreeing with the rendered page | 5 September 2026 | Across 21,827 headings in one repository, 6.3% of generated anchors did not match the id on the rendered page and 263 collapsed to nothing but hyphens. On a clean English corpus of 2,968 headings the rate was 1.7% — concentrated on the most-used page, where every step of a quickstart missed because of an em dash. Nothing failed; the links simply led nowhere. |
| Answer engines repeating a site's own stale sentence | 3 September 2026 | Across Perplexity, GPT and Gemini with web search, a brand's site was found in 9 of 9 answers, and the answers repeated "the API is coming soon" in 5 of 9 and "no pricing published" in 3 of 3 — while the API was live with 96 operations and a price sat on the landing page. Google's AI Mode answered a pricing question about a different company's product entirely. |
| A large tool catalogue is not a set a calling model chooses from | 12 September 2026 | Of the call ledger since 29 August 2026: 1 of 136 action tools and 2 of 41 agents had ever been called, and every call from outside the founding team landed on one of five names. The failure is silent on both sides — the model answers from the five it can see, and nothing in the logs distinguishes a near miss from a correct answer. |

## Using this registry

A source is worth adding when somebody needed a citation and could not find one. That is a signal. A registry does not grow by being filled in advance — a hundred references nobody cites makes the handbook look researched and makes the fifteen that matter unreadable.

## Next steps

<!-- widget:cards plain cols=2 -->

- [Claims](./claims.md) — the graded claims each of these references stands under. {scale}
- [Evidence](./README.md) — how a source's kind decides what it can settle. {info}
- [GEO and AI search](../lenses/geo-ai-search.md) — the audit that leans most heavily on the AI-search sources above. {sparkles}

<!-- /widget -->
