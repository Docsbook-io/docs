---
title: "Get translation"
description: "Get the translation for a specific source path and language."
---

# Get translation

<!-- widget:api -->

## GET /api/v1/get_translation

Get the translation for a specific source path and language. REQUIRES PRO or higher.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/get_translation`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `source_path` | string | yes | Source document path |
| `language` | string | yes | Target language code |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/get_translation?source_path=%3Csource_path%3E&language=%3Clanguage%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
