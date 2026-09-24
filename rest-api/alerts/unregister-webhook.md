---
title: "Unregister webhook"
description: "Remove a webhook by its id (Free)."
---

# Unregister webhook

<!-- widget:api -->

## POST /api/v1/unregister_webhook

Remove a webhook by its id (Free). Caller must own the workspace.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/unregister_webhook`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `webhook_id` | integer | no | Webhook id (from list_webhooks). |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/unregister_webhook' \
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
