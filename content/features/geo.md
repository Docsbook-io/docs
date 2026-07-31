---
title: "GEO — Generative Engine Optimization in Docsbook"
description: "Make your documentation citable by Perplexity, ChatGPT Search, Google AI Overviews and Claude. TL;DR blocks, visible last-modified date, author attribution and semantic markup built into Docsbook."
tldr: "Enable GEO in the SEO / GEO admin tab. Docsbook auto-injects a TL;DR block at the top of each page, shows a visible 'Updated' date, adds Person/Author to JSON-LD and serves semantic HTML — the patterns AI search engines prefer when citing sources."
---

# GEO — Generative Engine Optimization

In 2025 a growing share of developers ask Perplexity, ChatGPT Search, Google AI Overviews and Claude instead of typing a query into Google. These engines summarize answers and cite their sources — and the way your docs are structured directly controls whether they get picked.

GEO is the practice of writing and marking up content so that generative engines find it easy to extract, attribute and quote.

## What Docsbook does when GEO is enabled

Toggle **GEO** on in the admin **SEO / GEO** tab. Once enabled, every documentation page gets:

### TL;DR block at the top

A short summary is injected right after the H1 as a styled `<aside class="tldr">` block. Source order:

1. If your markdown frontmatter contains an explicit `tldr:` field — that string is used verbatim (up to 280 characters).
2. Otherwise — Docsbook extracts the first paragraph after the H1 and truncates it cleanly to fit. In this case the TL;DR block *replaces* that paragraph rather than repeating it, so the same sentence never appears twice in a row.

This is the snippet that most AI engines pick when summarizing your page.

### Visible last-modified date

A line like *“Updated May 25, 2026”* appears at the end of each article, with a proper `<time dateTime="...">` element. AI models weight freshness heavily — pages without a visible date often get skipped in favour of dated competitors.

The date comes from the last commit that touched the file in your GitHub repository.

### Author attribution as `Person` schema

The page's JSON-LD switches `author` from a generic `Organization` reference to a full `Person` object:

```json
{
  "@type": "Person",
  "name": "Jane Doe",
  "url": "https://github.com/janedoe",
  "sameAs": ["https://github.com/janedoe"]
}
```

Source order: explicit `author:` and `authorUrl:` in frontmatter, otherwise the last git author from GitHub.

### Semantic HTML

Article body is wrapped in `<article>` with descriptive structure. The TL;DR block exposes `role="note"` for assistive tech and AI parsers alike.

## How to make a page more citable

A few authoring patterns dramatically increase how often a page gets quoted:

- **Add an explicit `tldr:` frontmatter** with a 1–2 sentence direct answer to the page's main question. Don't rely on auto-extraction if you can write something tighter.
- **Lead with a direct answer**, then expand. AI models scan the first 200–300 characters most aggressively.
- **Use short, self-contained sentences** with concrete numbers and dates — these are easier to pull out as a quote.
- **Set `author:` and `authorUrl:` in frontmatter** when the page has subject-matter authority worth attributing.
- **Keep H2/H3 headings phrased as questions or imperatives** ("How to configure webhooks", "What is a workspace?") — they match how users phrase queries.

## How to enable

1. Open your workspace admin panel (FloatWidget) → **SEO / GEO** tab.
2. Toggle **GEO — Generative Engine Optimization** on.
3. The change applies to all pages in this workspace immediately on next render.

## Related

- [SEO Optimization](./seo) — classical search engine optimization
- [AEO — Answer Engine Optimization](./aeo) — featured snippets and voice
- [llms.txt for AI agents](../../ai/llms-txt)
