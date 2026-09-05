---
title: "Enable a language, pick the model, and set the URL shape"
description: "The configuration surface for translation: source language, enabled languages, translation model, when passes run, where the language switcher appears, and the URL of every locale."
tldr: "Enable languages in the Float Widget → Translation tab; Docsbook quotes the run before you confirm. Your source language is auto-detected from the repository README and can never be a translation target. Translated pages live at https://<user>.docsbook.io/<lang>/<repo>/<path> — the locale is always a path segment, never a subdomain."
---

# Translation settings

This page is the configuration surface: which languages exist, which model translates them, when passes run, where readers switch language, and what every translated URL looks like. How a pass actually works is [AI translations](./ai-translations.md); whether the result is good is [Translation quality and SEO](./quality.md).

Automatic translation and the translation workflow controls are part of the paid plan — see [Pricing](https://docsbook.io/pricing). A free project can *view* everything on this page, and its source language is still detected automatically when the project connects. What it cannot do is **change** any of it: enabled languages and the source language are one plan-gated group, so a free project is refused on both, as it is on the translation mode and on starting a pass.

## What can be configured

| Setting | What it does |
|---|---|
| Default (source) language | The language your docs are already written in. Never a translation target. |
| Enabled languages | Which languages your docs are additionally published in. |
| Translation model | Which AI model performs the translation. Separate from your chat model. |
| Translation mode | `auto`, `manual` or `external` — what starts a pass. |
| Language switcher | Whether readers see the selector in the sidebar, the header, or both. |

## Your project's source language

Docsbook detects the language your documentation is written in rather than asking you. When a project connects, it reads the repository README, strips code fences, inline code, images, links and HTML from it, and runs a language identifier over what is left.

The rules that matter:

- **Under 50 characters of prose after stripping, or no confident answer, falls back to `en`** and is recorded with low confidence, so the panel can label it *best guess — please confirm* rather than presenting a guess as a detection. A confident detection is recorded at high confidence and labelled *auto-detected*. Setting it yourself relabels it *set by you* and pins it.
- **The detector recognises exactly the fifteen codes Docsbook supports.** A README in a language outside that set falls through to the `en` fallback.
- **The source language can never be enabled as a translation target.** It is dropped from `enabled_languages` if you pass it, and a translation pass skips it explicitly — before it even checks whether the language is enabled — with the reason `is_source_language`. This is a structural guard, not a UI validation: a stale database row or a direct API call cannot make a project pay to translate English into English.
- **English is not special.** A project whose docs are written in German gets the mirror image of everything above.

## Enabling a language

1. Open your docs site.
2. Float Widget → **Translation** tab.
3. Check the language you want.
4. Confirm the dialog. The pass starts in the background.

If the language switcher is already on your site, opening it and pressing **Activate languages** goes to the same tab. That entry point appears only for you as the owner, or in admin preview — never for readers.

Enabling a language does not itself translate anything at the API level: `update_languages` sets the set, and `run_translation_pass` (or the mode's own trigger) does the work. In the panel the two are joined for you, so checking a box does start a pass.

### The dialog quotes the run first

Before anything is spent, the confirmation dialog shows how many pages are not yet translated out of the total, the estimated cost, and the balance remaining. If the run does not fit, it says what share of the docs your balance covers and offers a top-up — and **Translate what fits** is a real option: the pages that fit are translated now and the rest are picked up automatically when the balance allows.

The estimate is priced on the model you selected, so the quote and the charge describe the same model. That has to be said explicitly because it was once not true: the estimate priced one model while the run used another.

### Choosing the translation model

**Settings ▸ Translations ▸ Translation Model** picks the model, and it is deliberately a different setting from the model your reader chat runs on — translating prose and answering a question with tools are different jobs, and a measurement that moves one has no business moving the other.

Pick nothing and you get the default marked `(default)` in the picker, currently **GPT-5.6 Luna**. Each option shows its price per 1M tokens, so a cheaper model stretches the balance over more pages and a stronger one is one click away when a language reads badly. Only models in Docsbook's catalog are honoured in managed mode, because spend is billed at the model's published price and an unrecognised model would be charged at a rate you were never shown.

If you bring your own translation API key, the model becomes a free-text field on that card and the run is billed by your own provider instead of your project balance. Bringing your own key does not unlock translation on a free project: the gate is a plan decision, not a cost one.

## Choose when translations run

| Mode | What triggers a pass |
|---|---|
| **Auto** | A push that changes a documented page re-queues that page in every enabled language. |
| **Manual** | Nothing starts by itself; you press **Translate now** or ask an agent. |
| **External webhook** | Nothing starts by itself; Docsbook emits `translation.needed` and your own pipeline decides. |

On **Auto**, Docsbook polls your repository rather than reacting to a webhook: a workspace is looked at roughly every 15 minutes, and only four workspaces are examined per tick, so expect a catch-up to begin within about that window rather than the instant you push. Pages that have fallen *behind* are translated before pages that were never translated at all — a stale translation is actively telling your reader something your docs no longer say, while a missing one falls back to the original and merely fails to help.

Agents set the mode with the `set_translation_mode` MCP tool:

```typescript
// auto: Docsbook follows new commits and re-translates the pages they changed
set_translation_mode({ workspace_id: 42, mode: "auto" })

// external: nothing runs here; your pipeline listens for translation.needed
set_translation_mode({ workspace_id: 42, mode: "external", external_webhook_url: "https://example.com/hooks/translate" })
```

In `external` mode you receive a `translation.needed` event, run your own pipeline, and post the result back with `upload_translation`. Setting `external` without ever having supplied a webhook URL is refused rather than silently accepted.

## Language switcher placement

The switcher can appear in the sidebar, in the header, or in both. Header placement is a workspace flag of its own; the sidebar can additionally be set to show the switcher on mobile only, so a wide desktop header carries it and the narrow layout does not repeat it.

| Placement | Best for |
|---|---|
| Header | More visible; better when an international audience is the point |
| Sidebar | Saves header space when the header is already full |

Pick one. Showing the same control twice on the same screen is noise. Configure it in [Header options](../design/layout/header.md) or [Sidebar control](../design/layout/sidebar.md).

A site with no enabled languages shows no switcher at all, rather than a control with one entry in it.

## The URL of a translated page

The locale is **always a path segment, never a subdomain**. There is no `https://fr.docsbook.io/…`, and a bare language subdomain is served as a 404 on purpose so it cannot become a second address for the same content.

```text
https://<user>.docsbook.io/<repo>/<path>          → your source language
https://<user>.docsbook.io/fr/<repo>/<path>       → French
https://<user>.docsbook.io/ja/<repo>/<path>       → Japanese
```

On a custom domain the repository segment disappears and the locale keeps its place at the front:

```text
https://docs.example.com/<path>                   → your source language
https://docs.example.com/fr/<path>                → French
```

Two consequences worth knowing:

- **A workspace with a custom domain is canonical on that domain**, not on its `docsbook.io` mirror — for translated pages as well as originals. Mixing the two would publish a page whose `hreflang` neighbours point somewhere its own canonical does not.
- **`/en/…` exists but is not a separate page.** English is served identically at `/<repo>/<path>` and `/en/<repo>/<path>`, and the prefixed form declares the unprefixed one as its canonical, so the pair collapses into one indexable page instead of competing with itself.

Some Docsbook-hosted sites — the product's own docs and showcase projects — are served on the apex with the locale after the repository segment (`https://docsbook.io/<repo>/fr/<path>`). Docsbook builds the canonical and `hreflang` for those from the same function that routes them, so the URL it advertises is always the one that answers with a 200 rather than a redirect.

## Turning a language off

Uncheck it in the Translation tab, or use the switch on that language's own page. No confirmation is asked, because nothing is destroyed:

- Stored translations are kept. Turning the language back on does not pay again for pages that have not changed — only new and edited pages are translated, so re-enabling a previously used language is close to instant and close to free.
- That language's reporting page is kept too, so "should I turn this back on?" is answerable from the readers and cost it already had.
- Readers on the disabled locale's URL are sent to your source-language version.

## Limits

- **Fifteen codes, no regional variants.** `pt` covers Brazil and Portugal with one page set; `zh` covers Simplified and Traditional with one. The stored language column allows five characters, so codes like `pt-BR` are storable, but nothing in the product produces or serves them.
- **Auto mode is a poll, not a webhook.** A push is picked up at the next scan, and with a busy fleet the wait between scans for one workspace can exceed 15 minutes. If nothing has scanned your project in about an hour, the per-language panel calls the scan overdue rather than pretending it is on schedule.
- **The language switcher is the only reader-facing language control.** Docsbook does not redirect readers by `Accept-Language` and does not geo-route them; a reader who has expressed no preference gets the site's configured default.
- **Model choice is per workspace, not per language.** You cannot translate Japanese on a stronger model than Polish within one project.

## Related

- [AI translations](./ai-translations.md) — what a pass does to a page, and what is protected from the model
- [Translation quality and SEO](./quality.md) — coverage, freshness, corrections, `hreflang` and canonicals
- [Header layout and navigation](../design/layout/header.md) — putting the switcher in the header
- [Sidebar layout and configuration](../design/layout/sidebar.md) — putting it in the sidebar instead
- [Visitor countries report](../analytics/reports/countries.md) — which regions arrive that you do not translate for yet
