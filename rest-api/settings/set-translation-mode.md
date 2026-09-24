---
title: "Set translation mode"
description: "Set the translation workflow mode for a workspace: 'auto' (Docsbook AI), 'manual' (drafts via API), or 'external' (forward to webhook)."
---

# Set translation mode

<!-- widget:api -->

## POST /api/v1/set_translation_mode

Set the translation workflow mode for a workspace: 'auto' (Docsbook AI), 'manual' (drafts via API), or 'external' (forward to webhook). REQUIRES PRO or higher.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/set_translation_mode`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `mode` | string | no | Translation workflow mode One of: `auto`, `manual`, `external`. |
| `external_webhook_url` | string | no | Webhook URL (required for 'external' mode, empty string clears) |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/set_translation_mode' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"mode":"auto"}'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
