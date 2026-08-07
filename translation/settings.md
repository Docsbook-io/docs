---
title: "Translation Settings"
description: "Configure multi-language publishing in Docsbook — enable target languages, toggle the language switcher in the sidebar or header, and control translations."
---

# Translation Settings

Publish your documentation in multiple languages — automatically, with no manual work.

## Settings

| Setting | What it does |
|---|---|
| Enabled languages | Which languages to publish your docs in |
| Language switcher in sidebar | Show the language selector in the left sidebar |
| Language selector in header | Show the language selector in the top header bar |

## How to Enable

1. Requires a **Pro plan**.
2. Open your docs site.
3. Float Widget → **Translation** tab.
4. Check the languages you want to enable.
5. Save — translation starts automatically in the background.

Translation typically takes **1–5 minutes** for small repositories, up to 30 minutes for large ones.

## Supported Languages

15 core languages are available:

| Language | Code |
|---|---|
| Spanish | `es` |
| French | `fr` |
| German | `de` |
| Portuguese | `pt` |
| Italian | `it` |
| Russian | `ru` |
| Chinese | `zh` |
| Japanese | `ja` |
| Korean | `ko` |
| Arabic | `ar` |
| Hindi | `hi` |
| Turkish | `tr` |
| Polish | `pl` |
| Dutch | `nl` |
| English | `en` (default) |

## Language Switcher Placement

The language switcher can appear in the **sidebar**, the **header**, or both.

**Recommendation:** Pick one location. Showing it in both places is redundant.

| Placement | Best for |
|---|---|
| Header | More visible, better for international audiences |
| Sidebar | Saves header space when header is already full |

Configure placement in:
- [Header Options →](../design/layout/header)
- [Sidebar Control →](../design/layout/sidebar)

## URL Structure

Each language gets its own URL path:

```
docsbook.io/{username}/{repo}           → English (default)
docsbook.io/{username}/es/{repo}        → Spanish
docsbook.io/{username}/fr/{repo}        → French
```

Each language version is indexed separately by search engines, which means passive SEO traffic in every language you publish.

## Was Translating Worth It?

The **Translation impact** panel sits at the top of the same Translation tab and answers the question you actually pay for. Pick a period from the tab's interval dropdown and it reports three numbers over that window:

- **Savings** — what a human translator would have charged for the same word count, minus what the AI translation actually cost you. The translator rate is an industry estimate, not a quote you received, so read this as an order of magnitude rather than an invoice.
- **Visitors** — unique readers who landed on a translated page, with crawlers excluded.
- **Conversion** — how much better or worse readers of translated pages convert compared with readers of your original-language pages. A negative number is a real answer, not an error: it means the translated pages are reaching people who bounce, and it is worth knowing.

Below it, **Visitor Countries** and the language breakdown show where that traffic came from.

## Keeping Translations Current

Enabling a language translates your whole site once. After that, editing a page in GitHub does **not** re-translate it on its own — readers keep seeing the last translation until it is re-run. Ask your AI agent to re-translate a page, or use the MCP translation tools (`upload_translation`, `approve_translation`, `delete_translation`) to correct or replace a specific translation by hand. A translation you upload or approve is marked as hand-written, so later automatic runs leave it alone.

## Disabling a Language

Uncheck the language in the Translation tab → Save.

Visitors on that language's URL are automatically redirected to the English version. Cached translations are kept — re-enabling is instant.

---

> **Reach a global audience without hiring translators.**
> [Upgrade to Pro →](https://docsbook.io/connect)

See also: [How AI Translations work →](./ai-translations)
