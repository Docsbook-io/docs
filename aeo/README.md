---
title: "AEO: what an answer engine needs from a docs page"
description: "What Docsbook emits so an answer engine can lift a passage from your docs, what the markup can and cannot buy in Google today, and what you still have to write yourself."
tldr: "Docsbook emits FAQPage, HowTo and speakable JSON-LD from your Markdown when AEO is on, plus Organization, TechArticle and BreadcrumbList on every page regardless. Google retired the FAQ and HowTo rich results, so the markup is a machine-parsing layer now — the answer box is won by the shape of the prose, which is what our content rules cover."
---

# AEO — Answer Engine Optimization

An answer engine — a Google featured snippet, a voice assistant, an in-product AI helper — does not read your page. It picks one **passage** out of it, shows that passage instead of the page, and moves on. AEO is the work of making sure a passage on your page is the one that can be picked, and that it is still correct once it has been torn out of its context.

Docsbook does two things toward that. It **emits machine-readable markup** describing the questions and procedures your page already contains, on a single toggle. And it **writes and enforces content by a set of rules** aimed at the passage, not the page — those rules are the part that actually moves the outcome, and they are on [Content rules for answer engines](./content-rules.md).

This page covers what an answer engine needs, what Docsbook supplies without being asked, and what is left for you.

<!-- widget:cards -->

- [Structured answers](./structured-answers.md) — every schema.org type Docsbook emits, what triggers it, the exact Markdown shape, real emitted JSON-LD, and what happens when the markup comes out wrong
- [Content rules for answer engines](./content-rules.md) — the numbered rules Docsbook writes by, what each one does to an answering agent, and which are enforced automatically rather than advised

<!-- /widget -->

## What does an answer engine need from a page?

Four things, in this order. The first two are structural and Docsbook handles them; the last two are what you write.

| Need | Why the engine has it | Who supplies it |
|---|---|---|
| The text arrives without JavaScript | Retrieval crawlers fetch HTML; content painted by a browser script is not in the fetch | Docsbook — pages are server-rendered static HTML |
| The passage is scored on its own | Google runs a passage ranking system to "identify individual sections or 'passages' of a web page" ([Google](https://developers.google.com/search/docs/appearance/ranking-systems-guide)) | You — a section that only makes sense after the three above it loses |
| The answer is in the opening sentence | Models use information best at the start or end of a context and degrade in the middle ([Liu et al., TACL](https://arxiv.org/abs/2307.03172)) | You |
| One liftable fact — a number, a limit, a definition | Statistics, quotations and cited sources measurably raised visibility in generative answers ([GEO, KDD 2024](https://arxiv.org/abs/2311.09735)) | You |

Markup is nowhere on that list, and that ordering is deliberate. Markup describes content; it does not create it.

## What does Docsbook emit automatically?

Every documentation page carries one `<script type="application/ld+json">` block holding a schema.org `@graph`. Three objects are in it on every page, whatever your settings: an `Organization` for the project owner, a `TechArticle` for the page itself, and a `BreadcrumbList` built from the same canonical URL the page's `<link rel="canonical">` uses.

Turning **AEO** on in the admin **SEO / GEO** tab adds three more, each only when the page genuinely contains the matching content:

- **`FAQPage`** — when the page has an FAQ section or a question-shaped H3. Up to 20 questions, each answer capped at 1,000 characters.
- **`HowTo`** — when a heading starting "How to" (or the Russian "Как") is followed by a numbered list of at least three steps. Up to 5 procedures per page, 20 steps each.
- **`speakable`** — a `SpeakableSpecification` inside the `TechArticle` naming `.tldr`, the first article paragraph, and the H1, in that order of preference.

A page with no FAQ gets no `FAQPage`, and a two-step procedure gets no `HowTo`. That is the design, not a gap: Google's structured data policy says "Don't mark up content that is not visible to readers of the page", and breaking it risks a manual action that removes rich-result eligibility ([Google](https://developers.google.com/search/docs/appearance/structured-data/sd-policies)). The exact triggers, thresholds and emitted JSON are on [Structured answers](./structured-answers.md).

AEO is a toggle on every plan. The agents that apply the writing rules for you are a paid capability — see [pricing](https://docsbook.io/pricing).

## Why this is the right way (evidence)

| Rule Docsbook follows | Why it works on the machine consuming it | Source |
|---|---|---|
| Emit JSON-LD, not microdata | "Google recommends using JSON-LD for structured data if your site's setup allows it" | [Google, intro to structured data](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data) |
| Emit markup only for content that is on the page | "Don't mark up content that is not visible to readers of the page" — violating it can trigger a manual action | [Google, structured data guidelines](https://developers.google.com/search/docs/appearance/structured-data/sd-policies) |
| Emit `BreadcrumbList` on every page | Breadcrumb is one of the rich results Google still supports, and the trail "indicates the page's position in the site hierarchy" | [Google, breadcrumb](https://developers.google.com/search/docs/appearance/structured-data/breadcrumb), [search gallery](https://developers.google.com/search/docs/appearance/structured-data/search-gallery) |
| Point `speakable` at the summary, not the whole page | Google's guidance is to mark "key points" rather than entire articles, roughly two to three sentences | [Google, speakable](https://developers.google.com/search/docs/appearance/structured-data/speakable) |
| Treat the passage, not the page, as the unit | Google's passage ranking system scores individual sections of a page | [Google, ranking systems guide](https://developers.google.com/search/docs/appearance/ranking-systems-guide) |
| Never promise a snippet or a citation | A 2026 survey of 45 GEO studies found "no reviewed technique shows a stable, longitudinal, cross-platform causal effect on organic discoverability" | [Martinez, arXiv 2607.14035](https://arxiv.org/abs/2607.14035) |

## Limits and open questions

- **Google no longer shows FAQ or How-to rich results, and we will not pretend otherwise.** Google removed the How-to rich result in September 2023 — "no longer shown in search results, on both desktop and mobile devices" — and restricted FAQ to well-known government and health sites at the same time. FAQ was then deprecated outright: Google's own update log records "This feature will no longer appear in Google Search starting May 7, 2026" and the documentation was removed on 15 June 2026 ([Google documentation updates](https://developers.google.com/search/updates)). Neither type appears in the current [supported rich results gallery](https://developers.google.com/search/docs/appearance/structured-data/search-gallery). What `FAQPage` and `HowTo` still do is make the Q&A and the procedure explicit to anything that parses JSON-LD. What they no longer do is produce a Google rich result. If a vendor tells you otherwise, ask for the date on their source.
- **You cannot mark up your way into a featured snippet.** Asked how to mark a page as a featured snippet, Google answers "You can't. Google systems determine whether a page would make a good featured snippet for a user's search request, and if so, elevates it" ([Google, featured snippets](https://developers.google.com/search/docs/appearance/featured-snippets)). Featured snippets are won by the prose. That is why [Content rules](./content-rules.md) is the longer page of the two.
- **`speakable` is a beta with a narrow gate.** Google's implementation is "in beta and subject to change", limited to news publishers, and serves "users in the U.S. that have Google Home devices set to English" ([Google, speakable](https://developers.google.com/search/docs/appearance/structured-data/speakable)). A documentation site is not a news publisher, so treat the markup as a correct declaration of which part of the page is the summary, not as a route into a smart speaker.
- **Under question: other voice assistants.** Earlier versions of this page said Amazon Alexa reads `speakable` markup. We could not find a primary Amazon source stating that, and schema.org publishes no list of consumers. What is verifiable: `speakable` is a schema.org property, Google documents one beta use of it, and nothing else is documented by its vendor. Treat any claim about Alexa and `speakable` as unproven.
- **Under question: whether AI answer engines read JSON-LD at all.** No model vendor — OpenAI, Anthropic, Google, Perplexity — publishes a statement that its retrieval pipeline parses schema.org markup. Third-party analyses correlate JSON-LD with citation, but correlation on crawled pages cannot separate markup from the site quality that usually accompanies it. Until a vendor documents it, the honest position is that JSON-LD removes ambiguity for anything that chooses to parse it, and buys nothing measurable that we can show you.
- **Custom domains do not get AEO markup.** A workspace served on its own domain renders through a different path that emits a bare `TechArticle` only — no `BreadcrumbList`, no `FAQPage`, no `HowTo`, no `speakable`, and the AEO toggle has no effect there. On `*.docsbook.io` addresses the full graph is emitted. This is a known gap, not a configuration you can change.
- **Nothing in Docsbook validates the markup it emits.** There is no schema linter in the pipeline and `audit_geo` does not inspect JSON-LD. Check a page with Google's Rich Results Test or the Schema Markup Validator after you turn AEO on — [Structured answers](./structured-answers.md) explains what a failure looks like.

## Related

- [Structured answers](./structured-answers.md) — the emitted types, triggers and real JSON-LD
- [Content rules for answer engines](./content-rules.md) — the rules that actually move the outcome
- [SEO](../seo/README.md) — meta tags, sitemap, canonical URLs and `noindex`
- [GEO](../geo/README.md) — the TL;DR block the `speakable` selector prefers, and citation by assistants
- [llms.txt](../geo/llms-txt.md) — the site-level index for AI crawlers
- [How Docsbook proves what it claims](../evidence.md) — the evidence rule these pages follow
