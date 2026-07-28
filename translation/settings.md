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

## Keeping Translations Current

The **Translation Activity** panel, on the same Translation tab, is where you check and fix the state of your translations.

At the top are three numbers:

- **Coverage** — of every page in your docs across every language you enabled, how much is translated and still matches your source.
- **Needs attention** — pages that have no translation at all, plus pages whose translation has fallen behind the source. Untranslated pages are the ones your readers see in the original language, so they are counted first.
- **Spend** — what translation cost over the period your plan retains.

Below them is a table with one row per page in your documentation. Each row shows a language chip per language, coloured by what your reader actually gets:

- **Up to date** — the translation matches the page's current content in your repository.
- **Outdated** — the page changed in git and its translation has not caught up yet.
- **Not translated** — no translation exists, so readers see the original language.
- **Edited** — a hand-written or uploaded translation. Automatic runs leave these alone.

Pages whose source file was renamed or deleted upstream are marked **No longer in the repository**.

You can **search** for a page by path, and filter the table **by language** or **by state** — for example, to list only what is outdated. A live progress bar appears while a translation run is going, and if a run stopped early, why it stopped (budget spent or provider quota reached).

### Fixing a page

- **Retranslate from the row** — the button on each row translates that page into the language that needs it. Pages already up to date are skipped and cost you nothing.
- **Open a page** — clicking a row replaces the panel with that page's detail view: every language with its state, and the option to view your source text side by side with the translation. Use the back arrow to return to the table.
- **Edit a translation by hand** — in the detail view, `Edit` lets you correct the translated text directly. A translation you edit is marked as hand-written, so later automatic runs will not overwrite it.

Re-translating is how a page that has fallen behind gets caught up. Editing a page in GitHub does not re-translate it by itself.

## Disabling a Language

Uncheck the language in the Translation tab → Save.

Visitors on that language's URL are automatically redirected to the English version. Cached translations are kept — re-enabling is instant.

---

> **Reach a global audience without hiring translators.**
> [Upgrade to Pro →](https://docsbook.io/connect)

See also: [How AI Translations work →](./ai-translations)
