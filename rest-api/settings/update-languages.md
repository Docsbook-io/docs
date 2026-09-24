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

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/update_languages' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
