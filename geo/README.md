---
title: "GEO: what Docsbook adds so an AI assistant can quote you"
description: "The page-level signals Docsbook injects when GEO is on — TL;DR block, visible last-modified time, Person author JSON-LD — and the honest size of the effect."
tldr: "Turn GEO on in the admin SEO / GEO tab; it is not gated by plan. Docsbook injects a TL;DR block after the H1 (from `tldr:` frontmatter or the lede, capped at 280 characters), a visible Updated date inside a real time element, and switches the JSON-LD author from your organisation to a Person."
---

# GEO — Generative Engine Optimization

Docsbook GEO is the set of page-level signals that help a generative engine — Perplexity, ChatGPT search, Google AI Overviews, Claude — quote your documentation **and attribute the quote to you**. Toggle **GEO** on in the admin **SEO / GEO** tab, or call `update_geo` over MCP, and every page in the workspace carries them on the next render. It is not gated by plan — every plan has it.

GEO is about being cited inside a generated answer. Its two neighbours cover different surfaces: [SEO](../seo/README.md) is about ranking in a list of blue links, and [AEO](../aeo/README.md) is about answer boxes and voice assistants, which are built from explicit `FAQPage` and `HowTo` markup.

## What does a generative engine actually do with your page?

Not one thing — a pipeline, and each stage can drop you. A crawler fetches the page. A retriever scores **passages**, not whole documents: Google describes its passage ranking system as one that identifies "individual sections or 'passages' of a web page to better understand how relevant a page is to a search" ([Google Search Central, ranking systems guide](https://developers.google.com/search/docs/appearance/ranking-systems-guide)). A handful of surviving sources are then placed in a context window — the GEO paper's setup uses "only the top 5 sources fetched from the Google search engine for every query" ([GEO, KDD 2024](https://arxiv.org/abs/2311.09735)) — and a model writes an answer over them, choosing what to quote and whom to credit.

Two consequences follow, and everything below is downstream of them. Anything that stops you being fetched or retrieved makes the writing irrelevant. Anything that makes a *retrieved* passage easier to lift and attribute is what GEO can actually change.

## What does Docsbook add to a page when GEO is on?

Three things, all visible in the page's HTML, plus the semantic wrappers around them.

### A TL;DR block after the H1

Docsbook injects a short summary immediately after the leading H1, rendered as `<aside class="tldr" role="note" aria-label="Summary">`. The text is chosen in this order:

1. An explicit `tldr:` field in the page's frontmatter.
2. Otherwise the document's first real paragraph. Headings, blockquotes, list items, fenced code blocks and image-only lines are skipped while looking for it.

Whichever wins is cleaned before it is printed: link syntax, inline code, emphasis marks and raw HTML tags are stripped, and whitespace is collapsed. The result is capped at **280 characters**, truncated at the last word boundary if that boundary falls past the halfway mark, with trailing punctuation removed and a single ellipsis appended.

Two behaviours are worth knowing because they are what stop the block being noise:

- **A first paragraph shorter than 40 characters produces no TL;DR at all.** A fragment is worse than nothing.
- **When the TL;DR came from the lede, the lede is removed from the body.** The same sentence never appears twice in a row; when the TL;DR came from frontmatter, your opening paragraph stays exactly where you wrote it.

### A visible last-modified time

With GEO on, a line reading *Updated May 25, 2026* is rendered at the end of the article, with the date wrapped in a real `<time dateTime="…">` element so a parser gets the machine value as well as the human one. The date is the committer date of the newest commit touching that file in your repository, falling back to the author date. Docsbook caches the lookup for an hour, and if GitHub does not answer, **the line is omitted rather than guessed** — a wrong date is worse than no date.

The same commit history fills `datePublished` in the JSON-LD, from the oldest of the most recent 100 commits touching the file.

### A `Person` author in the JSON-LD

Every page carries a `TechArticle` object. Without GEO its `author` is a reference to your workspace's `Organization`. With GEO on it becomes a person:

```json
{
  "@type": "Person",
  "name": "Jane Doe",
  "url": "https://github.com/janedoe",
  "sameAs": ["https://github.com/janedoe"]
}
```

The name comes from `author:` frontmatter when you set it, otherwise from the last commit author of that file. `url` and `sameAs` are filled from `authorUrl:` frontmatter or the author's GitHub profile, and are simply absent when neither exists. If there is no name from either source, the object falls back to the `Organization` reference rather than emitting an empty `Person`.

### Semantic wrappers

The body is rendered inside `<article>`, and the TL;DR block carries `role="note"` and an accessible label — read by assistive technology and by parsers alike. With [AEO](../aeo/README.md) also on, `.tldr` is the first selector in the page's `speakable` specification, so the block a model reads first is the block a voice assistant reads aloud.

## How do I check GEO is doing anything?

Ask the MCP tool `audit_geo`. It runs no model at all — every number in it is a fetch — so it cannot invent a finding. In one call it:

- reads your `robots.txt` and checks it against **seven named assistant agents** (a dated list, currently as of 2026-08-29), separating search-index agents from training crawlers, because blocking training is a decision and blocking the search-index agent while expecting citations is usually an accident;
- fetches each sampled page **twice in the same minute** — once as a browser, once as `OAI-SearchBot` — to catch a CDN that serves a person a page and an assistant a challenge;
- checks that the body prose is present in the raw HTML (at least 200 words, no JavaScript executed);
- checks whether the page states a date at all;
- checks that `/llms.txt`, `/llms-full.txt` and `/sitemap.xml` exist.

A probe that times out or hits a 404 is recorded as **null with a reason**, never as a failure — an unreachable check lowers the number of checks, not your score.

## Why these signals and not others

| Rule | Why the stack behaves that way | Source |
|---|---|---|
| Make each section stand alone | Retrieval scores passages, not pages | [Google ranking systems guide](https://developers.google.com/search/docs/appearance/ranking-systems-guide) |
| Add quotations, statistics and cited sources | Measured to raise the share of a generated answer attributed to a source. Quotation Addition, Cite Sources and Statistics Addition are the paper's three top methods, reported at "a relative improvement of 30-40% on the Position-Adjusted Word Count metric" over a 10K-query benchmark, with the best of them at 41% | [GEO, KDD 2024](https://arxiv.org/abs/2311.09735) |
| Say who wrote it | Google asks whether pages "carry a byline, where one might be expected" and "strongly encourage[s] adding accurate authorship information" | [Creating helpful content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content) |
| Use `Person` with a `url` that identifies the author | Google's Article guidance: "Use the `Person` type for people", and link "a web page that uniquely identifies the author" | [Article structured data](https://developers.google.com/search/docs/appearance/structured-data/article) |
| Do not expect a magic file | "There are no additional requirements to appear in AI Overviews or AI Mode, nor other special optimizations necessary" | [Google AI features](https://developers.google.com/search/docs/appearance/ai-features) |
| Do not keyword-stuff | The same benchmark files Keyword Stuffing under "Non-Performing" methods, scoring **below** the unmodified baseline — and on a live engine "10% worse than the baseline" | [GEO, KDD 2024](https://arxiv.org/abs/2311.09735) |

## Limits and open questions

**How much this moves is small, and conditional.** A 2026 critical survey of 45 GEO studies concludes that the foundational gains are "valid within its experimental setting but conditional on a source already being present in a fixed context", and that "no reviewed technique shows a stable, longitudinal, cross-platform causal effect on organic discoverability or downstream behavior" ([arXiv 2607.14035](https://arxiv.org/abs/2607.14035), Nov 2023–Jul 2026 window). Docsbook will not quote you a citation-rate lift, because none is established.

**Under question: does freshness raise citation rate?** What is verifiable is that Google runs "various 'query deserves freshness' systems" for *Search ranking* ([ranking systems guide](https://developers.google.com/search/docs/appearance/ranking-systems-guide)), and that a page with no date gives a model nothing to attribute currency to. What is not verifiable is the common claim that a visible date raises how often an assistant cites you: no primary source measures it. Treat the date as hygiene, not as a lever, until someone publishes a measurement.

**Answers are not stable enough to A/B by hand.** Independent audits summarised in the same survey: Schulte et al. (2026), across four engines and 45 days, "observe daily source-level Jaccard scores of approximately 0.34–0.42"; Kirsten et al. (2026), across 4,706 queries in the US and Germany, find "page overlap across two months is 18% for AI Overviews, compared with 45% for organic Google". Run a check more than once before believing either a win or a loss.

**Version-dependent details.** The visible date renders in US English (*May 25, 2026*) whatever language the page is in. `datePublished` is derived from at most the 100 most recent commits touching the file, so on a very long-lived page it is the oldest commit *in that window*, not the true first. An author taken from git is whoever last touched the file, which may be someone who fixed a typo — set `author:` explicitly when the byline matters.

**The GEO switch does not reach a custom domain.** All three signals on this page are emitted by the Docsbook-hosted render path. A page served on your own domain gets **no TL;DR block, no visible Updated line**, and a single `TechArticle` node whose author is always a `Person` named after the repository owner's GitHub login — whether GEO is on or off, and regardless of `author:` frontmatter. Turning GEO on changes nothing a reader or a crawler sees on a custom domain today. See [SEO limits](../seo/how-it-works.md#limits-and-open-questions) for the rest of what differs there.

**What GEO cannot do.** It does not get an unindexed page indexed, does not unblock a crawler your `robots.txt` disallows, and does not make a client-side-rendered page readable. Those are [SEO](../seo/README.md) problems, and `audit_geo` reports them as critical for exactly that reason.

## Turning it on

1. Open your workspace admin panel (FloatWidget) → **SEO / GEO** tab.
2. Toggle **GEO** on. No plan gate, no per-page setup ([pricing](https://docsbook.io/pricing)).
3. Add a `tldr:` line to the five pages you most want quoted. Those two edits are the whole first pass.

## Related

- [Citation signals](./citation-signals.md) — the writing rules, each with the retrieval behaviour that justifies it.
- [llms.txt](./llms-txt.md) — the site-level machine index, and what its evidence is actually worth.
- [SEO](../seo/README.md) — indexing, canonical URLs, sitemap: the stage before any of this matters.
- [AEO](../aeo/README.md) — `FAQPage`, `HowTo` and `speakable` markup.
- [AI chat](../ai-chat/chat.md) — the assistant that answers on your own site.
- [How Docsbook proves what it claims](../evidence.md) — the rule these pages are written to.
