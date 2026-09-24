---
title: "Approve translation"
description: "Approve a draft translation, moving it to status 'published'."
---

# Approve translation

<!-- widget:api -->

## POST /api/v1/approve_translation

Approve a draft translation, moving it to status 'published'. REQUIRES PRO or higher.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/approve_translation`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `translation_id` | number | no | Translation row ID |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/approve_translation' \
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
