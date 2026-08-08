---
title: "AI-Powered Translations"
description: "How Docsbook auto-translates documentation with Claude AI — incremental re-translation, resumable runs with progress, cached delivery, and zero translation files to maintain."
---

# AI Translations

How Docsbook automatically translates your documentation using Claude AI.

## How It Works

1. You enable a language in [Translation Settings](./settings).
2. Docsbook fetches your markdown files from GitHub.
3. Each file is sent to **Claude** (by Anthropic) for translation.
4. Translated pages are cached for fast delivery.
5. When you edit a page and re-translate it, only the sections you changed are sent to Claude — the rest are reused from cache.

No manual work. No translation files to maintain. No YAML keys.

Enabling a language translates your whole site once. After that, pushing to GitHub does **not** re-translate anything on its own: readers keep seeing the last translation until it is re-run. Ask your AI agent to re-translate a page, or replace a specific translation yourself with the MCP translation tools — see [Translation Settings](./settings).

## Long Runs Resume Where They Stopped

A large site takes more than one pass to translate. Docsbook runs the job in chunks and keeps a cursor, so a run that hits a time limit picks up from the next untranslated page instead of starting over or stalling.

- **Changed pages go first.** When a re-translation is scoped to the pages a commit touched, those are translated ahead of the rest of the site — the pages you just edited come back first.
- **A run continues on its own.** Every couple of minutes a background runner resumes any job that still has pages left.
- **Interrupted runs are recovered.** If a run dies mid-way, it is picked up automatically rather than sitting unfinished.

You do not need to re-click anything to keep a long translation moving.

## Watching Progress

The **Languages** card in the Translation tab shows what a running job is doing:

- A progress bar and a **35/80** counter — pages handled out of pages in the run.
- **Stopped** on a language whose last run did not finish. Hover it to see why: the AI budget ran out, a provider quota was hit, or the run failed.

When a run stops on budget, the remaining pages are translated on a later run once the budget refreshes — nothing you already paid for is lost.

## What Gets Translated

| Translated | Not translated |
|---|---|
| Body text | Code blocks |
| Headings | Inline code (`like this`) |
| Tables | URLs and links |
| Image alt text | File paths |
| Sidebar navigation labels | Technical identifiers |
| Page titles and meta descriptions | — |

Code is intentionally left in the original language — it should stay consistent regardless of the reader's locale.

## Translation Cache

Translations are cached per page per language, keyed to the file's content hash on GitHub.

- Every visit serves the cached translation instantly.
- After you change a page, readers keep getting the previous translation until you re-translate it — they are never dropped back to the original language.
- Cached translations persist even if you temporarily disable a language.

This means re-enabling a language that was previously active is instant — no re-translation needed.

Because the cache is keyed by content, re-translating is cheap: a page is split into sections, and only the sections whose text actually changed are sent to Claude. Fixing a typo costs one section, not a whole page.

## Translation Quality

Claude produces high-quality technical documentation translations — the same model that powers Claude.ai, trained on a large corpus of technical writing in dozens of languages.

### Why Claude Outperforms Generic Translation

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

### Quality at Scale

Human translators cost $0.10–$0.30 per word. A 50-page documentation site is typically 25,000–40,000 words. That's $2,500–$12,000 per language — before you account for updates.

With Docsbook, translation is included in your plan. Re-translating an updated page is a click, and you are only charged for the sections that actually changed. No invoices. No turnaround time. No coordination overhead.

## SEO Impact of Translations

Every translated language version is a fully separate set of URLs, indexed independently by Google.

```
docsbook.io/{user}/{repo}        → ranks for English queries
docsbook.io/{user}/{repo}/es     → ranks for Spanish queries
docsbook.io/{user}/{repo}/de     → ranks for German queries
```

Docsbook automatically adds `hreflang` tags to every page, which tells Google which language version to show to which audience. Without these tags, Google may show the wrong language to international visitors — or ignore translated pages entirely.

**What this means in practice:** enabling Spanish translation doesn't just serve your existing Spanish-speaking users better. It creates an entirely new set of pages that rank for Spanish-language searches your English docs never would have appeared in. You're multiplying your search surface area by the number of languages you publish.

A documentation site that was ranking for 500 English queries now ranks for 500 queries in each additional language — passively, without any extra content work.

## Writing Tips for Better AI Translation

Clear source content produces better translations. Follow these guidelines:

- **Use short, direct sentences.** Long compound sentences lose nuance in translation.
- **Avoid idioms.** "It's a piece of cake" doesn't translate literally. Say "It's simple."
- **Use ISO date format.** Write `2024-03-25`, not "March 25th" — dates are interpreted differently across locales.
- **Keep code comments in English.** They're excluded from translation but should be readable by all developers.
- **Use consistent terminology.** If you call something a "workspace" in one place, don't call it a "project" in another.

---

> **Go global without the translation overhead.**
> [Enable translations →](https://docsbook.io/connect)

See also: [Translation Settings →](./settings)
