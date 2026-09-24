---
title: "Documentation translation: your docs in 15 languages"
description: "Translate Docsbook docs into Spanish, German, Japanese and 11 more languages, each with its own URLs, hreflang and sitemap entries, kept in step by your agent."
---

# Your docs in 15 languages

Turn a language on and Docsbook publishes your docs in it at their own URLs, with the signals search engines need to show each reader the right language.

| Language | Code | Language | Code | Language | Code |
|---|---|---|---|---|---|
| English | `en` | Spanish | `es` | French | `fr` |
| German | `de` | Portuguese | `pt` | Italian | `it` |
| Russian | `ru` | Chinese | `zh` | Japanese | `ja` |
| Korean | `ko` | Arabic | `ar` | Hindi | `hi` |
| Turkish | `tr` | Polish | `pl` | Dutch | `nl` |

One of the 15 is the language your docs are written in (**Default Language** in **Settings ▸ General**); translations go into the others. Docs written in another language? **Translate into English** gives you the version most readers and answer engines meet first.

## Turn a language on

Tell your agent: "Translate our docs into German and Japanese." It switches the languages on with `update_languages`, and the first translation pass starts right away, home page first.

Readers then get a language switcher in the sidebar footer (**Customize ▸ Left sidebar ▸ Language Toggle**), and you can add one to the header with **Customize ▸ Header ▸ Language in Header**. Translations live in Docsbook, not in your repository, which stays in its source language.

## Keep translations in step with your edits

Out of the box, a language is translated once, when you turn it on. To keep it level with every edit, pick one of these:

| Option | What happens after you change a page |
|---|---|
| **Translate into …** card in **Triggers** | The agent brings that language level after each docs change, pages readers open first; one card per language |
| `auto` mode | Docsbook checks your repository about every 15 minutes and translates new and changed pages itself |
| `external` mode | Docsbook notifies your webhook which pages need translating; your translator sends them back with `upload_translation` |
| `manual` mode | Nothing runs by itself; you upload translations and publish them with `approve_translation` |

<!-- widget:callout type=note -->

The **Translate into …** cards wake only when your docs are re-indexed, so they fire only with **Enable semantic search** on in **Settings ▸ Agent ▸ Semantic Search** (Pro; during the trial, once a card is on file). The modes don't need it: `auto` follows your repository on its own. Set a mode with `set_translation_mode`.

<!-- /widget -->

## Per-language URLs and SEO

The language code is the first part of the path: `docs.acme.com/de/quickstart`, while the source-language page keeps `docs.acme.com/quickstart`.

- **Canonical and `hreflang`** — each translated page is its own canonical page and lists every language it exists in, plus `x-default`.
- **Titles and descriptions** — the translated `<title>` and meta description come from the translated page.
- **Sitemap** — every translated page gets its own entry.
- **No duplicates** — a language URL for a page not translated yet shows the original and points search engines at it.
- **Interface** — search, buttons and page actions ship in all 15 languages; your menu labels, tabs and suggested questions are translated with the pages.

## Review translations yourself

Every translation can be read, replaced or approved from your agent, with these tools:

- **`get_translation_status`** — per language: pages current, behind and missing, and any run in progress
- **`run_translation_pass`** — catches up to three languages now, skipping any already level with the source
- **`list_pending_translations`** and **`approve_translation`** — the drafts waiting for you, and publishing one
- **`upload_translation`** — adds or replaces one page's translation, as a draft by default
- **`get_translation`** and **`delete_translation`** — read or remove a single translated page

Ask in plain words: "Which German pages are behind?" See the [MCP tools reference](../mcp-tools/README.md) for every argument.

## What it costs

Translations are part of **Pro**, and the 14-day trial includes them; recording your docs' own language is free on every plan. Translating runs on your project's AI balance, and a page is only re-translated when its source changed ([Plans and pricing](../plans-and-pricing.md)).

To pay your AI provider directly, ask the panel chat for the **Bring your own Translations API key** card. It takes a key from OpenRouter, OpenAI, Google Gemini, Anthropic or Vercel AI Gateway.

## FAQ

<!-- widget:accordion -->

### Does Docsbook translate my code samples?

No. Code blocks and inline code are kept exactly as written, so every command still runs when a reader copies it.

### Can a person approve translations before readers see them?

Yes. In `manual` mode, uploaded translations wait as drafts until you publish them with `approve_translation`.

### Do translated pages need their own files in my repository?

No. Docsbook stores them, and your repository keeps only the source language.

<!-- /widget -->

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [Triggers](../agent/triggers.md) — The Translate cards and the rest of the catalog {bot}
- [Custom domain](./custom-domain.md) — Serve every language on your own domain {globe}
- [Search engines see you](../seo/README.md) — How translated pages feed your rankings {search-check}
- [Plans and pricing](../plans-and-pricing.md) — What Pro includes {credit-card}

<!-- /widget -->
