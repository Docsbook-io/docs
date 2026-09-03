---
title: "AI translations: publish your docs in 15 languages"
description: "Docsbook translates docs into 15 languages, gives each its own indexable URL and hreflang tags, and re-translates a page when its source commit changes."
---

# AI Translations

Docsbook AI Translations translate your documentation into **15 languages**. Each language is rendered as its own route, indexed independently by Google, and served with the correct `hreflang` tags — so a translated page competes in its own market rather than as a duplicate of the English one.

## Which languages does Docsbook translate into?

Docsbook supports 15 target languages, and a page can be translated into any subset of them:

```text
EN, ES, FR, DE, PT, IT, RU, ZH, JA, KO, AR, HI, TR, PL, NL
```

Enabling a language does not translate anything by itself — it makes the language available, and the mode below decides when a page is actually translated.

## Reader experience

- **Language switcher** — placed in the sidebar or in the header, configurable per workspace.
- **Auto-detect** — the reader's preferred language is detected from `Accept-Language` and from the page body via `franc`. If a translated version exists, Docsbook serves it on first load.
- **Per-language URLs** — Google indexes each language as a distinct page, which compounds organic traffic across markets.

## Which translation mode should I use?

Use `auto` when you want every push translated without asking, and `external` when a human or your own pipeline must approve the wording first. Set the mode with the `set_translation_mode` MCP tool, or in the workspace settings.

```typescript
// auto: Docsbook translates with its built-in AI provider, and follows new
// commits — pages changed by a push are re-translated without being asked
set_translation_mode({ workspace_id: 42, mode: "auto" })

// external: drafts are posted to your webhook for human or pipeline review
set_translation_mode({ workspace_id: 42, mode: "external" })
```

In `external` mode you receive a `translation.needed` webhook, run your own pipeline, and post the result back with `upload_translation`.

## Which model translates the pages?

Translations run through OpenRouter by default, with their own model setting under **Settings ▸ Translations** — separate from the two chat models, so the model that translates is not forced to be the model that answers readers.

You can also bring your own provider, API key and model for translations. That configuration is separate from AI Chat's bring-your-own-key setting, with its own key and model choice, so different providers (or models) can run each.

## What does translating a page draw on?

Each translated page version calls a model, and that call draws on the balance of the project it belongs to. Serving an already-translated page does not: the reader's visit, the `hreflang` tags and the language switcher cost nothing to run.

A translation is counted **per source page version**. If the English page changes, its translated copies are stale until they are redone — automatically in `auto` mode, on request in `manual` and `external`. A repository with 40 pages and 5 languages is therefore 200 translated page versions on the first run, and only the changed pages after that.

Two consequences worth planning around:

- **Enable languages deliberately.** Each extra language multiplies the work done on every push.
- **A large restructuring commit re-translates everything it touched.** Renaming a heading across 40 pages is 40 re-translations per language.

Current amounts are on the [Docsbook pricing page](https://docsbook.io/pricing).

## Next steps

Enable one language in [Translation settings](../translation/settings.md) and push a change — the first translated route appears on the next index rebuild.

## Related

- [Translation settings](../translation/settings.md) — enable languages and configure the switcher.
- [AI translations guide](../translation/ai-translations.md) — step-by-step setup and review flow.
- [SEO](../content/features/seo.md) — how a language's URLs enter the sitemap, and why an untranslated one does not.
- [Webhooks](../webhooks.md) — `translation.needed`, `translation.completed` and `translation.outdated` events.
