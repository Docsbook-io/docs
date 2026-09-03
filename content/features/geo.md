---
title: "GEO: make your documentation quotable by AI assistants"
description: "What Docsbook adds to a page so a generative engine can quote it and attribute it to you — TL;DR block, visible update date and author schema."
tldr: "Turn GEO on in the admin SEO / GEO tab. Docsbook injects a TL;DR block after the H1 (from `tldr:` frontmatter or the first paragraph, 280 characters), shows a visible Updated date, and switches JSON-LD author to a full Person object."
---

# GEO — Generative Engine Optimization

Docsbook GEO is the set of page-level signals that help a generative engine — Perplexity, ChatGPT Search, Google AI Overviews, Claude — quote your documentation **and attribute the quote to you**. Toggle **GEO** on in the admin **SEO / GEO** tab and every page in the workspace gets them on the next render.

GEO is about being cited in a generated answer. Its two neighbours cover different surfaces: [SEO](./seo.md) is about ranking in a list of blue links, and [AEO](./aeo.md) is about the answer box and voice assistants, which are built from explicit `FAQPage` and `HowTo` markup.

## What does Docsbook add to a page when GEO is on?

Three things, all of them visible in the page's HTML: a TL;DR block after the H1, a visible last-modified date at the end of the article, and an author in the JSON-LD that is a real person rather than a company.

### TL;DR block at the top

A short summary is injected right after the H1 as a styled `<aside class="tldr">` block, capped at **280 characters**. Docsbook picks its text in this order:

1. An explicit `tldr:` field in the page's frontmatter, used as written.
2. Otherwise, the first paragraph after the H1, truncated cleanly at a word boundary. In this case the TL;DR block *replaces* that paragraph rather than repeating it, so the same sentence never appears twice in a row.

A first paragraph shorter than 40 characters yields no TL;DR at all, because a fragment is worse than nothing. This is the block most assistants read first, and — through [AEO](./aeo.md) — the first thing a voice assistant reads aloud.

### Visible last-modified date

A line reading *Updated 25 May 2026* appears at the end of each article, wrapped in a real `<time dateTime="...">` element so a parser gets the machine value as well as the human one. The date comes from the last commit that touched the file in your GitHub repository, so it cannot drift from reality the way a hand-typed date does.

Treat freshness as hygiene rather than as a lever: how heavily any given model weights a date varies by model and changes between versions. A page with no date at all is the case worth avoiding.

### Author attribution as `Person` schema

With GEO on, the page's JSON-LD switches `author` from a generic `Organization` reference to a full `Person` object:

```json
{
  "@type": "Person",
  "name": "Jane Doe",
  "url": "https://github.com/janedoe",
  "sameAs": ["https://github.com/janedoe"]
}
```

Docsbook takes the name from explicit `author:` and `authorUrl:` frontmatter, and otherwise from the last git author of that file on GitHub.

### Semantic HTML

The article body is wrapped in `<article>` with descriptive structure, and the TL;DR block exposes `role="note"` — read by assistive technology and by parsers alike.

## How do I make a page more likely to be quoted?

Write each section so it survives being read alone. An engine retrieves and ranks **passages**, not pages: a section that only makes sense after the three above it is scored without them and loses before a reader ever sees it.

- **Name the subject in full inside every section.** "To rotate it, call…" is unretrievable — nothing in it says which product, or that the thing being rotated is an API key.
- **Answer in the first sentences after the heading**, then elaborate. "Before we get into rotation, it's worth understanding…" is the answer arriving too late.
- **One question per section.** A section answering three competes weakly for all three.
- **Phrase a heading as the reader's question where the section answers one** — `## How do I rotate an API key?` beats `## Key rotation`. Do not force question form onto reference tables and API listings; they are not questions.
- **Write an explicit `tldr:`** with a one- or two-sentence direct answer, rather than relying on the extracted first paragraph.
- **Give something extractable**: a limit, a timeout, a price, a version, or a one-sentence definition. Concrete numbers are what a model lifts verbatim.
- **Set `author:` and `authorUrl:`** when the page has subject-matter authority worth attributing.
- **Apply the quote test.** Paste a section into an empty file. If it no longer says what it is about, rewrite it.

Two warnings, both measured rather than assumed. **Never invent a number, a limit or a quotation** to make a passage quotable — a wrong figure repeated by an assistant is worse than no answer. And **do not strip a page down for quotability**: rewriting a body to be tighter removes the synonym variety that made it match varied questions, and in a controlled study that kind of body-only rewrite reduced top-20 retrieval presence by about 9%. Add the definition and the number alongside your prose; do not replace the prose with them.

## How much does GEO actually move?

Honestly: less than any vendor implies, and Docsbook will not quote you a citation-rate lift.

What has been measured in controlled work ([GEO, KDD 2024](https://arxiv.org/abs/2311.09735), 10,000 queries) is that adding quotations, statistics and cited sources raises how much of a generated answer is attributed to a source — while keyword stuffing scored *below* the unmodified baseline. A 2026 survey of 45 studies ([arXiv 2607.14035](https://arxiv.org/abs/2607.14035)) found those gains hold only for pages that were already retrieved, and that most method-and-domain combinations did not replicate on an independent benchmark.

So: the strong, uncontested part is structural — self-contained passages, the subject named, the answer first. The TL;DR block, the date and the author schema sit in the moderate-to-weak tiers. They are cheap, they are honest, and they are worth having. They are not a citation strategy on their own.

Measure the traces instead of the claim: crawler hits from assistant user agents in your Docsbook analytics, and referral traffic arriving from assistant domains. And repeat a check before believing it — the same prompt on the same engine returns substantially different sources run to run.

## How to enable GEO

1. Open your workspace admin panel (FloatWidget) → **SEO / GEO** tab.
2. Toggle **GEO — Generative Engine Optimization** on.
3. The change applies to every page in the workspace on the next render.

## Next steps

Turn GEO on, then add a `tldr:` line to the five pages you most want quoted — those two edits are the whole first pass.

## Related

- [SEO](./seo.md) — ranking in classical search results.
- [AEO](./aeo.md) — answer boxes, rich results and voice assistants.
- [llms.txt](../../ai/llms-txt.md) — the site-level index for AI crawlers, and what its evidence is worth.
- [AI Chat](../../ai/chat.md) — the assistant that answers on your own site.
