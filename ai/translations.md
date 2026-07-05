---
title: "AI Translations — 15 Languages With SEO"
description: "Translate documentation into 15 languages with separate SEO indexing, auto-detected reader language, and a switcher in sidebar or header."
---

# AI Translations

Docsbook translates documentation into 15 languages. Each language is rendered as a separate route, indexed independently by Google, and served with the correct `hreflang` tags.

## Supported languages

```text
EN, ES, FR, DE, PT, IT, RU, ZH, JA, KO, AR, HI, TR, PL, NL
```

## Reader experience

- **Language switcher** — placed in the sidebar or in the header, configurable per workspace.
- **Auto-detect** — the reader's preferred language is detected from `Accept-Language` and from the page body via `franc`. If a translated version exists, Docsbook serves it on first load.
- **Per-language URLs** — Google indexes each language as a distinct page, which compounds organic traffic across markets.

## Translation modes

Set the mode with the `set_translation_mode` MCP tool (requires Pro or Business).

```typescript
// auto: Docsbook translates with its built-in AI provider
set_translation_mode({ workspace_id: 42, mode: "auto" })

// external: drafts are posted to your webhook for human or pipeline review
set_translation_mode({ workspace_id: 42, mode: "external" })
```

In `external` mode you receive a `translation.needed` webhook, run your own pipeline, and post the result back with `upload_translation`.

## Providers

Translations run through OpenRouter by default. You can plug in your own provider and API key — the same configuration as for AI Chat applies.

## Limits

| Plan | AI translations |
|---|---|
| Free | Not available |
| Pro | Included |
| Business | Included, higher monthly limit than Pro |

A translation is counted per source page version. If the English page changes, the translated copy is marked stale and needs to be regenerated.

## Pricing

AI Translations require **Pro** (monthly, 7-day free trial) or **Business** (monthly, 14-day free trial, higher limit).

## Related

- [Translation Settings](../translation/settings.md) — Enable languages and configure the switcher.
- [AI Translations Guide](../translation/ai-translations.md) — Step-by-step setup and review flow.
