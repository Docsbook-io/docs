---
title: "Sources: the references behind the documentation handbook"
description: "Every reference this handbook cites — vendor documentation, one peer-reviewed study, the llms.txt specification, Diátaxis, three practitioner field reports and four of our own measurements — with what each one actually says and when we last read it."
tldr: "Twenty references, each with the line we quote from it verbatim and the date we last opened it. Vendor documentation and the KDD 2024 GEO study can settle a claim on their own; practitioner field reports never can, and are recorded here so a hypothesis has a traceable origin instead of being something somebody once said."
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

Three practitioner accounts, recorded September 2026. They are the origin of several of the sharpest working hypotheses in this handbook, and **none of them can settle a claim on its own.** They are private working notes rather than published write-ups, so they are recorded here by title, author and date rather than by link — an unverifiable citation is provenance, not proof, and that is exactly why the claims resting on them are graded `hypothesis`.

| Report | Recorded | What it contributes |
|---|---|---|
| Generative Engine Optimization overview — query fan-out, the three answer mechanisms, and a brand-presence audit checklist | 14 September 2026 | A query is split into a fan of sub-queries and the page has to close the whole fan at once; engines lift a paragraph, a table or a list rather than a page. Three mechanisms produce an answer: real-time retrieval over the index, the AI layer in the search engine, and the model's own memory of being mentioned. Audit method: take ten real queries from Search Console, ask them conversationally in several assistants, and record who was named instead of you and which sources were cited. |
| How search changed in 2026 and how to rebuild SEO for AI answers — Oleg Shestakov, Rush Agency | 14 September 2026 | From agency practice: sites cited in Google's AI answers see about 35% more click-throughs; after the March 2026 update 24% of top-10 pages fell out of the top 100, mostly compilations and AI text with no named expert; thematic clusters gave +46% traffic over six months and 3.2× more mentions in AI answers; a page slower than 3 seconds loses 23% of its traffic. A page's format has to match the format currently ranking for the query, and the first two paragraphs have to answer with facts and figures or nothing is quoted. |
| What the May 2026 core update and AI Mode changed, and what to do during a rollout — Oleg Shestakov | 14 September 2026 | Informational pages, affiliate round-ups, bulk AI content and simple calculators are the ones being replaced by the answer itself; brands, real expertise and pages that close a commercial intent hold. During a rollout: do not rewrite the site, do not bulk-delete pages, do not buy links. Diagnose by separating impressions, positions and CTR before and after the date. |

Every number in that table is reported, not verified. The mechanisms behind them are well supported and safe to explain; the figures are not safe to put in a proposal. Each claim that rests on one of these says so and gives you a test to run instead.

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
