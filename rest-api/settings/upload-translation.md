---
title: "Upload translation"
description: "Upload or replace a translation for a workspace document."
---

# Upload translation

<!-- widget:api -->

## POST /api/v1/upload_translation

Upload or replace a translation for a workspace document. Creates a draft by default. This is how an EXTERNAL translator returns its work: the translation webhook notifies you, you translate, you call this. Pass back the `source_blob_sha` the webhook gave you as `source_hash` and set origin 'external_api', or the freshness surfaces cannot tell which commit your translation belongs to. The language starts being served to readers as soon as the first page is uploaded — there is no separate activation step. REQUIRES PRO or higher.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/upload_translation`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `source_path` | string | no | Source document path (e.g. 'guides/quick-start.md') |
| `language` | string | no | Target language code (e.g. 'es', 'fr') |
| `content` | string | no | Translated content |
| `status` | string | no | Status (default: draft) One of: `draft`, `published`, `outdated`. |
| `source_hash` | string | no | Git blob sha (40 hex) of the SOURCE file this was translated FROM — pass the `source_blob_sha` the translation webhook delivered, verbatim. This is what makes 'is this commit translated?' answerable: without it the row records only a hash of your own output, which no commit can ever match. Omit for a hand-written translation whose freshness is a person's call. |
| `origin` | string | no | Who produced it: 'external_api' for a machine translator answering the webhook (compared against the repo like any machine translation), 'manual_upload' for a person's own words (never reported as stale). Default 'manual_upload'. One of: `manual_upload`, `external_api`. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/upload_translation' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"status":"draft","origin":"manual_upload"}'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
