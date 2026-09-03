---
title: "Translate your Docsbook documentation into 15 languages"
description: "Pick target languages, let Docsbook translate every page, serve each language on its own indexed path, and keep the cost of a re-translation predictable."
---

# Translate your documentation

Docsbook translates your documentation with an AI model and serves each language on its own path, indexed separately by search engines. You pick the languages; every published page is translated and re-translated as you edit.

Translation is the capability that spends money fastest, because every page in every enabled language is a model call. Read [what translation costs](#what-translation-costs) before you enable a second language.

## The 15 supported languages

Docsbook translates into 15 languages:

| Language | Code | Language | Code | Language | Code |
|---|---|---|---|---|---|
| English | `en` | Italian | `it` | Arabic | `ar` |
| Spanish | `es` | Russian | `ru` | Hindi | `hi` |
| French | `fr` | Chinese | `zh` | Turkish | `tr` |
| German | `de` | Japanese | `ja` | Polish | `pl` |
| Portuguese | `pt` | Korean | `ko` | Dutch | `nl` |

If you need a language that is not on this list, write to [support@docsbook.io](mailto:support@docsbook.io).

## Enable a language

1. Open your documentation while signed in.
2. Click the Float Widget → **Settings**.
3. Open **Translation Languages**.
4. Tick the languages you want.
5. Click **Save**.

Docsbook queues every published page for every language you ticked and starts translating. The language row shows a progress counter while a run is going, and marks the language **Stopped** with a reason if a run ended early.

A large run is processed in chunks and resumes on its own until it finishes, so you do not need to watch it.

## What translation costs

Translating a page calls an AI model, and every model call is charged against that project's balance. A new project starts with **$1.00** of balance.

The arithmetic that matters before you tick a box: **one enabled language multiplies your page count by one.** A 40-page site with three languages enabled is 120 translated pages on the first run, and every subsequent edit re-translates that page in all three.

Two controls keep this predictable:

- **A per-source ceiling.** In **Settings** → **Usage**, set a per-cycle ceiling on **AI Translations** specifically. When translations reach it they stop and everything else — reader answers, the editor — keeps running. See [How Docsbook charges for AI usage](../../content/setup/pricing-spec.md).
- **Manual mode.** On **Manual** or **External webhook** mode nothing re-translates by itself, so a burst of edits does not trigger a burst of spend.

Reading a translated page costs nothing. Only producing one does.

## Choose when translations update

| Mode | What triggers a translation |
|---|---|
| **Auto** | A push that changes a documented page re-queues that page in every enabled language |
| **Manual** | Nothing starts by itself; you re-run translation from the Translation tab |
| **External webhook** | Nothing starts by itself; your own system decides when |

On **Auto**, Docsbook checks your repository for new commits roughly every 15 minutes, so a catch-up starts within about that window rather than the instant you push. Pages that have fallen behind are translated before pages that were never translated at all.

On any mode you can ask your AI agent to re-translate a specific page, or re-run a language from the Translation tab.

## What readers see

A language selector appears in your site header. Translated pages live under a language prefix:

```text
docs.example.com/page        English
docs.example.com/es/page     Spanish
docs.example.com/fr/page     French
docs.example.com/de/page     German
```

Without a custom domain the same structure sits under your project path:

```text
docsbook.io/user/repo            English
docsbook.io/user/repo/es         Spanish
docsbook.io/user/repo/de/guides  German subpage
```

## What gets translated and what does not

| Translated | Left as written |
|---|---|
| Body text and headings | Code blocks |
| Image alt text | Inline code |
| Tables | URLs and link targets |
| Sidebar navigation | |

## How the translations are indexed

Each language is a separate set of pages with its own URLs, and Docsbook emits `hreflang` tags linking them to each other. Search engines index each language independently, so a reader searching in Spanish can land on your Spanish page rather than on an English one they will bounce from.

## Review and override a translation

The AI translation is a starting point, not a final draft. Idioms, product-specific jargon and cultural references are where it is weakest.

To override a page:

1. Open the **Translation** tab.
2. Download the translation for the language you want to correct.
3. Edit the markdown.
4. Upload it back.

Docsbook serves your version from then on and does not overwrite it on the next automatic pass.

## Write source pages that translate well

The quality of a translation is set by the source text. Four habits do most of the work:

**Write plain sentences.** "To install the package, run the command" translates cleanly. "Pip this bad boy and you're golden" does not.

**Avoid idioms.** "The setup takes three steps" survives translation; "it's a piece of cake" arrives as a dessert.

**Use structure.** Short paragraphs, clear headings, lists and tables give the model unambiguous units to work with.

**Keep code and code comments in English.** A translated docstring desynchronises from the code it documents.

```python
# Keep comments in English
def setup():
    """Configure the system."""
    pass
```

**Write dates in ISO format** — `2026-03-25`, not `25/03/2026`, which means two different days depending on the reader.

## Manage the language list

**Add a language:** open **Settings** → **Translation Languages**, tick it, and save. Docsbook translates the current pages into it.

**Remove a language:** untick it and save. Those pages stop being served and readers on those URLs are redirected to the default language. Nothing is deleted — the translations are kept, so turning the language back on is immediate and does not pay again for pages that have not changed.

**Change the default language:** pick from **Default Language** in the same panel. Visitors see that language first.

## See which languages readers actually use

Open Float Widget → **Analytics**. Views, visitors and top pages are reported per path, and each language sits under its own prefix (`/es`, `/fr`, `/de`), so the language breakdown falls out of the page report.

A language with translated pages and no traffic after a month is a language to untick — the pages stay stored, and you stop paying to re-translate them on every edit.

## Next steps

- [How Docsbook charges for AI usage](../../content/setup/pricing-spec.md) — set the per-source ceiling before a large run.
- [Set up a custom domain](./custom-domain.md) — every language is served under the same domain.
- [Web analytics](../../analytics/tracking/overview.md) — the per-path report that shows which languages earn their keep.
