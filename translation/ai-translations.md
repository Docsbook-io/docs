---
title: "What a Docsbook translation pass does to a page"
description: "What triggers a pass, how a page is chunked, exactly what is protected from the model and by which mechanism, how a stale translation is detected, and what happens when a run fails halfway."
tldr: "Docsbook renders your Markdown to HTML, splits it at heading boundaries into chunks capped at 9,000 characters, extracts code blocks and inline code into placeholders restored byte-for-byte, and translates the rest at temperature 0. Chunks are cached by content hash, so editing one section re-translates only that section. A page where any chunk failed is served for that request but never stored."
---

# AI translations

A translation pass takes the Markdown already in your repository, renders it exactly as the live page renders it, splits it, translates the human-readable parts, and stores the result per page per language. There are no translation files, no message keys and no export step. This page is the mechanism, at the level of what the code actually does.

## What starts a pass

Five things, and every run records which one it was — so the panel can say *Triggered by commit a1b2c3d* rather than attributing a push to you.

| Trigger | What causes it |
|---|---|
| `language_enabled` | You switched a language on. |
| `commit` | Auto mode's scanner found the repository head has moved. |
| `manual` | You pressed **Translate now**, or someone else did from the dashboard. |
| `agent` | An agent called `run_translation_pass`. The agent's key and run id are written on the job row. |
| The resume runner | Every 2 minutes a cron tick reaps runs whose heartbeat has been silent for 15 minutes, frees their locks, and drives up to three live jobs that have been idle for 90 seconds. |

The scanner only looks at a workspace it has not looked at for 15 minutes, and only four workspaces per tick, ordered by whoever has gone longest without a scan. It short-circuits when the repository head is unchanged — and the watermark it compares against is only advanced when *every* enabled language was found in sync at that commit, so a run that halted on budget cannot freeze a workspace at a partial translation and never be looked at again.

A pass never starts more than **three languages at once**, worst first: each run is minutes of billed model work, and an agent step that opened ten of them would spend a month's budget on one trigger. The rest are reported as `over_language_cap` and picked up next time, which is the honest version of "not now".

## How a page is chunked

The unit of translation is not the page. It is a section.

1. Your Markdown is preprocessed and rendered through the **same pipeline the live page uses**, including your widget blocklist. Translation therefore sees the page a reader sees, not a second interpretation of the source.
2. The rendered HTML is split at `<h2>` and `<h3>` boundaries. Content before the first heading becomes its own leading chunk.
3. A chunk longer than **9,000 characters** is split again — but only at top-level block boundaries (`</p>`, `</li>`, `</table>`, `</pre>`, `</figure>`, `</h1>`…`</h6>`), so a fragment is never cut mid-tag.
4. Each chunk is hashed by its own content. The hash plus the language is the cache key.
5. Chunks are translated at most **3 at a time**, each with a 30-second upstream timeout, and concatenated back in order.

Two things fall out of that design, and they are the whole reason it is built this way:

- **Editing one paragraph re-translates one section.** Every other chunk's hash is untouched, so it is served from cache. A typo fix costs a section, not a page. The split — how many chunks were reused against how many were sent to the model — is recorded once per page on the spend ledger, so the saving is a measured number rather than a claim.
- **Terminology cannot drift on text you did not touch.** An unedited section is byte-identical to the last time it was translated, because it is literally the same cached string.

Requests are sent at **temperature 0**, and the output-token budget is computed from the input length rather than reserved flat — with a multiplier of 2.6, chosen because Cyrillic and CJK cost far more tokens per character than the English source and a 1.5× budget returned truncated pages.

## What is protected from the model

There are two different kinds of protection here, and conflating them is how documentation ends up promising more than the code delivers.

### Protected structurally — the model never sees it

| Element | Mechanism |
|---|---|
| Fenced code blocks | Extracted before the request and replaced with `__CODE_BLOCK_N__`; restored byte-for-byte afterwards. |
| Inline code (`` `like this` ``) | Same extraction, same byte-for-byte restore. |
| Frontmatter keys and values | Never reach the model at all: translation runs on rendered HTML, and frontmatter was consumed at render time. |
| Widget markers (`<!-- widget:name -->`) | Also never reach the model: widgets are expanded into HTML by the render pipeline before chunking. There is no marker left to corrupt. The visible text *inside* a widget — a card's title, for example — is prose, and is translated. |

These are guarantees. A model cannot alter, reflow or "translate" a code sample it was never given.

### Protected by instruction — verify these, do not assume them

The prompt tells the model, as absolute rules, not to translate or modify HTML tags, attributes, class names, ids, `href` values or data attributes, not to change the HTML structure, not to translate code identifiers and variable names, not to add commentary, and to reproduce `__CODE_BLOCK_N__` placeholders exactly. That is a strong instruction to a model running at temperature 0, and it holds in practice — but it is an instruction, not a mechanism, and the honest word for that is *usually*.

Three consequences worth knowing:

- **Links keep their targets.** `href` is an attribute, and attributes are on the do-not-touch list. Link *text* is prose and is translated.
- **Heading anchors stay in the source language.** Heading `id` attributes are set before translation and instructed to be left alone, so a deep link into an English heading anchor keeps working on the translated page.
- **Image `alt` text is not translated.** It is an HTML attribute, and the rule that protects `href` protects `alt` with it. If accessible alt text in the reader's language matters to you, that is a gap, not a feature.

### Translated as sets, not one at a time

Navigation labels are translated as one group in a single request that must return the same number of labels in the same order; a malformed or mismatched response keeps the originals rather than guessing. If every returned label is identical to the original — the signature of a translation that did not happen — the result is discarded rather than cached, so the next attempt can try again instead of locking in English labels forever. A page's title and description are translated together as a pair, so the two can never drift out of sync.

## How an outdated translation is detected

By comparison against git, not by a status flag.

Every stored translation row keeps `source_hash` — the **git blob SHA of the source file at the moment it was translated**. Coverage is computed by reading the repository tree at HEAD and comparing, per path:

| State | Meaning |
|---|---|
| `current` | A machine translation exists and its stored SHA equals the file's SHA at HEAD. |
| `behind` | A machine translation exists, but of an older version of that page. |
| `missing` | The page exists in the repository and has never been translated into this language. |
| `manual` | Hand-written or uploaded. Freshness is the author's call, so it is never counted as behind. |
| `orphaned` | A translation whose source file no longer exists at HEAD. |

Coverage is `(current + manual) / total`, and a language is *in sync* when `behind` and `missing` are both zero. When the repository cannot be read, coverage is **null — never a confident zero**, and every surface reports "unknown" rather than painting a healthy language red.

The `status = 'outdated'` column in the database is deliberately not used for this. Nothing in the product writes it automatically, so it reads zero on every workspace; a freshness check built on it would report perfect health forever.

A pass ordered by this comparison translates **behind before missing**. A stale translation is actively telling a reader something your docs no longer say; a missing one falls back to the original and merely fails to help.

## The review and approve flow

There are three origins a stored translation can have, and they are treated differently on purpose.

| Origin | Written by | Served to readers | Overwritten by a later pass |
|---|---|---|---|
| `docsbook_ai` | A translation pass | Yes | Yes |
| `manual_upload` | You, through the panel editor or `upload_translation` | [Read this first](./quality.md#can-i-correct-a-translation-and-will-the-correction-survive) | **No** — an automatic pass will not replace it |
| `external_api` | Your own pipeline in `external` mode | [Read this first](./quality.md#can-i-correct-a-translation-and-will-the-correction-survive) | **No** |

Uploads land as **draft** by default. `list_pending_translations` returns the drafts, `approve_translation` moves one to published, and editing a translation's content marks the row as a manual upload so a later pass leaves it alone. In `external` mode the loop is: Docsbook emits `translation.needed` when a page is about to be translated, your pipeline does the work, and `upload_translation` posts the result back.

**Machine translations do not enter this queue.** A pass writes rows with status `auto`, not `draft`, so `list_pending_translations` never lists them. The approve flow is a gate on translations coming *in* from outside, not a human review step in front of the AI output. If you want AI output reviewed before readers see it, `external` mode is the shape that does that; the default `auto` mode publishes as it goes.

## What happens when a run fails

Every failure mode below is a deliberate decision to serve the original rather than store something broken.

| Failure | What happens |
|---|---|
| The model hits its output-token ceiling (`finish_reason: length`) | Treated as a hard failure and **refused**, not stored. A truncated chunk once meant half a page cached as the translation forever. |
| The model returns empty content | Also a hard failure. An empty string that propagated as success is how 808 blank translation rows once accumulated on one project. |
| One chunk fails | The page is assembled with the original text for that chunk and served **for that request only**. It is not written to Redis, not written to Postgres, and not indexed. |
| The assembled page is blank while the source is not | Not stored; the source is served instead. |
| A chunk failed recently | A 10-minute negative cache prevents a retry stampede. The next visit after it expires re-translates only the missing chunks. |
| The provider returns 402/403 on Docsbook's shared key | A global halt is set for **4 hours** and every pending run stops immediately rather than hammering an exhausted account. Workspaces with their own key are unaffected. |
| Your own key's quota is exhausted | Only your project's run fails. Somebody else's exhausted quota never halts you, and yours never halts them. |
| The project's spend budget is exhausted | The run is halted with that reason in words, and the remaining pages are translated on a later run once the balance allows. Nothing already paid for is lost. |
| The invocation is killed mid-run | The job keeps a cursor and a heartbeat. The 2-minute runner reaps a job silent for 15 minutes, frees its lock, and restarts it from the next untranslated page. |

A partially completed run is normal, not an error state: a large site takes more than one invocation, each invocation walks as far as its wall clock allows, and the next tick continues. What you should never see is a page half in English and half in another language, because that assembly is exactly what the code refuses to persist.

While a page has no translation yet, the reader is served the original — with no spinner, no error, and no banner promising a translation this request is not producing. Where only an older translation exists, the reader gets that older translation immediately rather than being dropped back to the original: readable content in the right language beats waiting.

## Limits

- **Terminology consistency has no glossary behind it.** There is no term base, no do-not-translate list you can supply, and no cross-page consistency check. What consistency exists comes from temperature 0, from unedited sections being served verbatim from cache, and from labels and title/description being translated as sets. Two different pages using the same term were translated independently, and may not agree.
- **"Do not translate identifiers" is an instruction, not a guarantee.** Code inside fences and backticks is mechanically safe. A bare identifier written as ordinary prose — a parameter name in a sentence, with no backticks — is protected only by the prompt. Writing identifiers in backticks is the single highest-value thing you can do for your own translations.
- **Image `alt` text stays in the source language.** See above; this is a consequence of protecting HTML attributes wholesale.
- **A cached translation was rendered under the widget blocklist in force when it was written.** Switching a widget off does not rewrite pages already translated; they pick it up on their next pass. Re-keying the cache on the blocklist would re-translate every page of every language for a presentation toggle.
- **Auto mode reacts to a poll, not to your push.** See [Translation settings](./settings.md#choose-when-translations-run).

## Related

- [Translation settings](./settings.md) — enabling a language, the model, the mode, and locale URLs
- [Translation quality and SEO](./quality.md) — what is measured, how to correct a translation, `hreflang`, and what search engines do with translated pages
- [Visitor countries report](../analytics/reports/countries.md) — which regions arrive that you do not translate for yet
