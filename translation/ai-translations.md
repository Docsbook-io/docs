---
title: "How Docsbook translates your documentation with AI"
description: "What the translation pipeline does to a page: which parts it sends to the model, what it leaves alone, how runs resume, and why re-translating a typo is cheap."
---

# AI Translations

Docsbook translates your documentation with Claude, page by page, straight from the Markdown in your repository. There are no translation files, no keys and no export step: you switch a language on, and translated pages appear on their own URLs. Each translation run spends your project's balance; serving a translated page afterwards does not.

## How AI translation works

1. You enable a language in [Translation Settings](./settings.md).
2. Docsbook fetches your markdown files from GitHub.
3. Each file is sent to **Claude** (by Anthropic) for translation.
4. Translated pages are cached for fast delivery.
5. When you edit a page and re-translate it, only the sections you changed are sent to Claude — the rest are reused from cache.

No manual work. No translation files to maintain. No YAML keys.

Enabling a language translates your whole site once. After that, on the **Auto** mode Docsbook follows your repository: a push that changes a documented page puts that page back in the queue for every enabled language, checked for roughly every 15 minutes. On **Manual** and **External webhook** nothing starts by itself. To correct a specific translation by hand, ask your AI agent to re-translate a page or use the MCP translation tools — see [Translation Settings](./settings.md).

## Long runs resume where they stopped

A large site takes more than one pass to translate. Docsbook runs the job in chunks and keeps a cursor, so a run that hits a time limit picks up from the next untranslated page instead of starting over or stalling.

- **Changed pages go first.** When a re-translation is scoped to the pages a commit touched, those are translated ahead of the rest of the site — the pages you just edited come back first.
- **A run continues on its own.** Every couple of minutes a background runner resumes any job that still has pages left.
- **Interrupted runs are recovered.** If a run dies mid-way, it is picked up automatically rather than sitting unfinished.

You do not need to re-click anything to keep a long translation moving.

## Watching progress

The **Languages** card in the Translation tab shows what a running job is doing:

- A progress bar and a **35/80** counter — pages handled out of pages in the run.
- **Stopped** on a language whose last run did not finish. Hover it to see why: the project's balance ran out, a provider quota was hit, or the run failed.

When a run stops on balance, the remaining pages are translated on a later run once the balance allows — nothing you already paid for is lost.

## What gets translated, and what does not

| Translated | Not translated |
|---|---|
| Body text | Code blocks |
| Headings | Inline code (`like this`) |
| Tables | URLs and links |
| Image alt text | File paths |
| Sidebar navigation labels | Technical identifiers |
| Page titles and meta descriptions | — |

Code is intentionally left in the original language — it should stay consistent regardless of the reader's locale.

## Translation cache

Translations are cached per page per language, keyed to the file's content hash on GitHub.

- Every visit serves the cached translation instantly.
- After you change a page, readers keep getting the previous translation until you re-translate it — they are never dropped back to the original language.
- Cached translations persist even if you temporarily disable a language.

This means re-enabling a language that was previously active is instant — no re-translation needed.

Because the cache is keyed by content, re-translating is cheap: a page is split into sections, and only the sections whose text actually changed are sent to Claude. Fixing a typo costs one section, not a whole page.

## Translation quality

Docsbook translates with Claude, the same model family behind Claude.ai. What that buys over a general-purpose translator is context: the surrounding page, the code around a sentence, and the terms your docs already use.

### How Claude differs from generic machine translation

Generic machine translation (Google Translate, DeepL) is built for general-purpose text. Developer documentation has a different structure: imperative commands, technical terms, code-adjacent prose, and precision-critical instructions where a mistranslation causes a broken setup.

Claude understands context. It knows that "run the command" means `ejecuta el comando`, not `corre el comando`, and that a parameter name should stay in English even when the surrounding sentence is in French. It preserves meaning across sentence restructuring — not just word-for-word substitution.

**Works best for:**
- Step-by-step guides
- API documentation
- FAQs
- Configuration references

**May need manual review for:**
- Brand-specific terminology
- Cultural references or idioms
- Highly domain-specific jargon

### How the "Saved" figure is calculated

Human translation agencies typically bill per word, which breaks down as a measure the moment a language has no whitespace-delimited words to count — Chinese and Japanese, most notably. Docsbook prices the counterfactual per 1,000 characters instead, a measure that works the same way in every language, and that rate is printed beside the "Saved" figure on your Translations dashboard. It is a comparison against a price list, not money you had and kept: nobody was paid either amount.

What a Docsbook run actually costs comes off your project's balance, and only the sections that changed are sent to the model. Re-translating an updated page is a click, with no invoice, no turnaround time and no coordination.

## What translation does to search

Every translated language version of your Docsbook site is a fully separate set of URLs, indexed independently by Google.

```text
docsbook.io/{user}/{repo}        → English pages
docsbook.io/{user}/{repo}/es     → Spanish pages
docsbook.io/{user}/{repo}/de     → German pages
```

Docsbook automatically adds `hreflang` tags to every page, which tells Google which language version to show to which audience. Without these tags, Google may show the wrong language to international visitors — or ignore translated pages entirely.

**What this means in practice:** enabling Spanish translation does not only serve your existing Spanish-speaking readers. It creates a separate set of pages, in Spanish, that a Spanish-language query can match at all — something an English-only page cannot do however well it ranks. Whether those pages are found is decided by the same things that decide it for your English pages; translation only makes them eligible.

Which regions arrive without a translation waiting for them is a question the [visitor countries report](../analytics/reports/countries.md) answers directly.

## Review and override a translation

The AI translation is a starting point, not a final draft. Idioms, product-specific jargon and cultural references are where it is weakest.

To override a page:

1. Open the **Translation** tab.
2. Download the translation for the language you want to correct.
3. Edit the markdown.
4. Upload it back.

Docsbook serves your version from then on and does not overwrite it on the next automatic pass.

## Writing tips for better AI translation

Clear source content produces better translations. Follow these guidelines:

- **Use short, direct sentences.** Long compound sentences lose nuance in translation.
- **Avoid idioms.** "It's a piece of cake" doesn't translate literally. Say "It's simple."
- **Use ISO date format.** Write `2024-03-25`, not "March 25th" — dates are interpreted differently across locales.
- **Keep code comments in English.** They're excluded from translation but should be readable by all developers.
- **Use consistent terminology.** If you call something a "workspace" in one place, don't call it a "project" in another.

## Related

- [Translation settings](./settings.md) — switching a language on, the cost quote before a run, and per-language results
- [Visitor countries report](../analytics/reports/countries.md) — which countries read a translation and which do not
- [Sidebar layout and configuration](../design/layout/sidebar.md) — showing the language switcher to readers
