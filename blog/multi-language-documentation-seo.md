---
title: "Multi-language documentation SEO: hreflang and URLs"
description: "How translated documentation earns traffic per locale — separate URLs, hreflang, when machine translation is good enough, and what breaks if you skip steps."
---

# Multi-language documentation SEO: hreflang and URLs

Most product docs in 2026 are English-only. The teams that translate properly capture organic traffic the English-only sites never see — searches in Japanese, Spanish, German, Mandarin for the same buying intent.

This post is the practical SEO guide for shipping docs in 15 languages without breaking Google or AI search.

## TL;DR

- Each language must live at a separate URL (`/ja/`, `/es/`, `/de/`)
- Add `hreflang` tags so search engines know what is a translation of what
- Use `lang` attribute on the `<html>` element
- AI translation in 2026 is good enough for docs (not for marketing copy)
- One canonical English source, AI translations on top — never duplicate sources

## The fundamental rule

**One URL per (page, language) pair.**

Wrong:

```
docs.yourcompany.com/quick-start?lang=ja
docs.yourcompany.com/quick-start (with cookies)
```

Right:

```
docs.yourcompany.com/quick-start
docs.yourcompany.com/ja/quick-start
docs.yourcompany.com/es/quick-start
```

Without separate URLs there is nothing for a search engine to index per language: one URL holds one document in its index, so whichever language it saw is the only one that can rank. Every other locale is invisible to search in its own language, no matter how good the translation is.

## hreflang setup

Each page needs `<link rel="alternate" hreflang="...">` tags pointing to every translation.

```html
<link rel="alternate" hreflang="en" href="https://docs.yourcompany.com/quick-start">
<link rel="alternate" hreflang="ja" href="https://docs.yourcompany.com/ja/quick-start">
<link rel="alternate" hreflang="es" href="https://docs.yourcompany.com/es/quick-start">
<link rel="alternate" hreflang="x-default" href="https://docs.yourcompany.com/quick-start">
```

`x-default` tells Google "if no other locale matches, show this." Usually the English version.

Docsbook generates hreflang automatically when you enable a language in Settings → Languages.

## When AI translation is good enough

Three factors:

| Content type | AI translation quality | Recommendation |
|---|---|---|
| Reference docs (API, config) | High | Use AI |
| Tutorials and how-to | High | Use AI, light human review |
| Marketing landing pages | Medium | Human review required |
| Brand copy (taglines, mission) | Low | Human translation |
| Code samples | N/A | Keep original |
| Error messages | High when terminology is consistent | Use AI |

LLM translation quality for technical content improved sharply between 2023 and 2026. For documentation specifically, machine translation has structural advantages over a human process rather than merely a price advantage:

- **Terminology consistency.** A model applies the same term to the same concept across a thousand pages; a rotating pool of human translators drifts, and the drift is invisible until a reader files a bug about it.
- **Speed.** Fifteen languages in minutes rather than a quote-and-schedule cycle per language.
- **Revision cost.** The real expense of human translation is not the first pass but every subsequent one: change a paragraph and you pay per word again, in every language. Machine translation recomputes the changed page. That is why translated docs go stale under a human pipeline and stay current under a machine one.

What humans still beat:

- Cultural localization (date formats, examples, brand voice)
- High-stakes legal copy
- Marketing taglines

For documentation, the cost-benefit tilts heavily toward AI translation in 2026.

## Each language indexed separately

Three signals matter:

1. **URL pattern** — `/ja/` subdirectory or `ja.yourdomain.com` subdomain (subdirectory is easier)
2. **hreflang tags** — bidirectional, point both directions between all versions
3. **`lang` attribute** — `<html lang="ja">` on the Japanese version
4. **Sitemap entries** — each language gets its own entry with `xhtml:link` annotations

Google then ranks each language in its respective locale's search results. A user in Japan searching in Japanese sees `/ja/`. A user in Spain searching in Spanish sees `/es/`.

## What AI search engines do with translations

Three behaviors observed:

### ChatGPT

ChatGPT will cite a translated page if the query is in that language. Asking ChatGPT "ドキュメンテーションプラットフォームを比較してください" (compare documentation platforms in Japanese) returns Japanese sources, including Japanese versions of docs.

### Perplexity

Same as ChatGPT — Perplexity strictly matches query language to source language. If you translate well, you gain a citation channel per language.

### Gemini

Google Gemini uses Google's underlying index. The same hreflang and locale signals that help Google AI Overviews help Gemini.

## How Docsbook ships multi-language

Three steps to enable a language:

1. Dashboard → Settings → Languages → select language → enable
2. AI translates the whole doc set into that language; the translation run is metered in dollars against the project's balance
3. Page appears at `/{language-code}/{path}` with hreflang and `lang` set correctly

15 languages supported: EN, ES, FR, DE, PT, IT, RU, ZH, JA, KO, AR, HI, TR, PL, NL.

You can also upload your own translations through the MCP tool `upload_translation` or the admin UI if you have a human translator.

## Translation modes

Three modes available:

- **Auto** — Docsbook AI translates everything automatically
- **Manual** — pending translations queue, you review before publishing
- **External** — webhook your own translation pipeline (your TMS, your translators)

External mode is for teams that already have a translation memory and want to keep using it. The `set_translation_mode` MCP tool flips between modes.

## Mistakes that kill multi-language SEO

- **Query parameter switching** (`?lang=ja`) — Google does not index these as separate pages
- **Cookie-based language detection** — same problem, only one URL gets indexed
- **Missing hreflang tags** — Google treats translations as duplicate content
- **One-way hreflang** — both pages must reference each other
- **No `lang` attribute** — screen readers and crawlers fall back to English

## Cost economics

Translating 200 pages to 14 additional languages:

| | DIY human translation | Docsbook AI translation |
|---|---|---|
| Cost | Per-word, quoted per language, paid again on every revision | Metered per translation run against the project balance |
| Time | Months | Hours |
| Update cost | Charged again per word whenever the source page changes | Recomputed when the source changes |
| SEO indexing | Manual hreflang setup | Automatic per locale |
| Best for | Legal, regulated and marketing copy where a human must sign off | Reference and how-to content that changes often |

Machine translation is not strictly better. It is better at the thing that kills most translation projects, which is not the first pass but the twentieth revision.

[Start free — no credit card](https://docsbook.io/start)

## Next steps

- [Documentation SEO guide](./documentation-seo-guide.md) — the single-locale foundation this page extends
- [AI search for documentation](./ai-search-documentation.md) — on-site search across locales
- [How to get your documentation cited by ChatGPT](./how-to-get-docs-cited-by-chatgpt.md) — assistants ask in many languages too
- [JSON-LD for documentation](./json-ld-for-documentation.md) — the structured data that goes on each translated page
