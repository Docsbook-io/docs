---
title: "Update languages"
description: "Set the languages the site is served in — the call for 'we need docs in Spanish and German', «нужна документация на испанском»."
---

# Update languages

<!-- widget:api -->

## POST /api/v1/update_languages

Set the languages the site is served in — the call for 'we need docs in Spanish and German', «нужна документация на испанском». `default_language` is the docs' own source language — what the content is ALREADY written in, e.g. after writing or reading pages that are in Russian, call this with default_language: 'ru' so the site (and the Users/Activity table's "Original" language column) knows. It is free on every plan, unlike the rest of this tool: it is a fact about the docs, not a purchase. `enabled_languages` — TRANSLATING into other languages — REQUIRES PRO plan and REPLACES the whole set, so pass the existing languages plus the new ones (read them from get_workspace first). Enabling a language does not translate anything by itself: run_translation_pass starts the first pass, and later passes follow the workspace's translation mode. Supported codes: en, es, fr, de, pt, it, ru, zh, ja, ko, ar, hi, tr, pl, nl. Translated pages are served at https://<username>.docsbook.io/<lang>/<repo>/<path> — language is always a PATH SEGMENT under the user subdomain, never a subdomain itself (never https://<lang>.docsbook.io/). `default_language` is silently dropped from `enabled_languages` if included, since the docs are already written in it and there is nothing to translate.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/update_languages`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `enabled_languages` | string[] | no | ISO language codes to enable |
| `default_language` | string | no | Default language code |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `id` | number | — |
| `repoFullName` | string | 'owner/repo', or a Docsbook-hosted placeholder when the site was created from scratch. |
| `customName` | string | null | — |
| `site_url` | string | The live docs URL — report this verbatim, never build one from repoFullName. |
| `customDomain` | string | null | — |
| `plan` | string | free \| pro \| business |
| `visibility` | string | public \| private |
| `not_discoverable` | string | Present ONLY when `visibility` is private, i.e. when no crawler and no answer engine can open this site. Says what that rules out — keyword work, SERP meta, crawler-facing sitemap/llms.txt tuning, backlinks, ranking readings, being cited by ChatGPT or Perplexity — and what is worth the run instead. A private SOURCE REPOSITORY is NOT this and does not rule anything out: Docsbook serves indexed public sites from private repositories. |
| `discoverability_blocked_by` | string | Alongside `not_discoverable`: "private" (the owner's choice) or "plan_locked" (the plan lapsed and Docsbook made it private — tell the owner before doing any work). |
| `aiEnabled` | boolean | — |
| `hasApiKey` | boolean | Whether a REST bearer exists — never the key itself. |
| `hasCustomAiKey` | boolean | — |
| `hasCustomTranslationKey` | boolean | — |
| `hasPassword` | boolean | — |
| `hasSourceOfTruthGraph` | boolean | Whether the semantic index has ever been built. |
| `sso` | object | { configured: false } or { issuer, clientId, allowedDomain, configured: true }. |
| `plan_capabilities` | object | What this plan unlocks. |
| `upgrade_hint` | string | null | — |
| `cta_url` | string | null | The one page readers should end up on. |
| `cta_hint` | string | — |
| `average_product_price_cents` | number | null | — |
| `revenue_hint` | string | — |
| `site_source_url` | string | null | Where facts about the product are read from. |
| `site_source_hint` | string | — |
| `subheaderFolders` | object[] | Top-level folder placements, each carrying the `placement` it resolves to — "subheader_tab" (a tab in the category strip, its pages kept out of the root sidebar tree), "sidebar_tree" (an ordinary folder in the sidebar), "subheader_tab_and_sidebar_tree" (both) or "hidden". Read `placement` rather than re-deriving it from inSubheader / showInSidebar / hiddenInSidebar. |
| `navigation_placement_hint` | string | Present when the project has folder placements: what each one resolves to and why a tab's hiddenInSidebar is not a defect to fix. |
| `publish_mismatch_warning` | string | Present only when the live site does not show what was published. |
| `…` | … | Plus every other project setting on this row — branding colors/fonts, navigation, UI toggles, SEO/GEO/AEO flags, access rules, domain, languages — minus secrets. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/update_languages' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

### Response

```json
{
  "ok": true,
  "result": {
    "id": 0,
    "repoFullName": "<repoFullName>",
    "customName": "<customName>",
    "site_url": "<site_url>",
    "customDomain": "<customDomain>",
    "plan": "<plan>",
    "visibility": "<visibility>",
    "not_discoverable": "<not_discoverable>",
    "discoverability_blocked_by": "<discoverability_blocked_by>",
    "aiEnabled": true,
    "hasApiKey": true,
    "hasCustomAiKey": true,
    "hasCustomTranslationKey": true,
    "hasPassword": true,
    "hasSourceOfTruthGraph": true,
    "sso": {},
    "plan_capabilities": {},
    "upgrade_hint": "<upgrade_hint>",
    "cta_url": "<cta_url>",
    "cta_hint": "<cta_hint>",
    "average_product_price_cents": "<average_product_price_cents>",
    "revenue_hint": "<revenue_hint>",
    "site_source_url": "<site_source_url>",
    "site_source_hint": "<site_source_hint>",
    "subheaderFolders": [],
    "navigation_placement_hint": "<navigation_placement_hint>",
    "publish_mismatch_warning": "<publish_mismatch_warning>",
    "…": "<…>"
  },
  "duration_ms": 0
}
```

### Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |

<!-- /widget -->
