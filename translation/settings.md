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
4. Check the language you want to enable.
5. Confirm in the dialog that appears — translation then starts in the background.

Translation typically takes **1–5 minutes** for small repositories, up to 30 minutes for large ones.

### Before You Confirm

Turning a language on opens a confirmation dialog so you know the cost before you commit to it. It shows:

- **Pages to translate** — how many pages are not yet translated, out of the total. If everything is already translated, it says so and enabling costs nothing.
- **Estimated cost** — what the run is expected to cost, or *Billed to your own API key* if you brought your own provider.
- **Budget left** — how much of your AI budget (or translation limit) remains.

If the run does not fit in what is left, the dialog says what percentage of the docs your budget covers and offers an upgrade. You can still press **Translate what fits** — the pages that fit are translated now, and the rest are picked up automatically once your budget refreshes.

### Following a Running Translation

While a run is in progress, the language row shows a progress bar and a **35/80** counter (pages handled out of pages in the run). A language whose last run did not finish is marked **Stopped**; hover it to see the reason — budget exhausted, provider quota, or a failure. Long runs resume on their own, in chunks, until every page is done.

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

Uncheck the language in the Translation tab → Save. No confirmation is asked, because nothing is destroyed.

Visitors on that language's URL are automatically redirected to the English version.

**Turning a language off never deletes what is already translated**, and turning it back on does not pay again for pages that have not changed — only new or edited pages are translated. Re-enabling a language you previously used is effectively instant and free. You can experiment with languages without risking a second bill.

---

> **Reach a global audience without hiring translators.**
> [Upgrade to Pro →](https://docsbook.io/connect)

See also: [How AI Translations work →](./ai-translations)
