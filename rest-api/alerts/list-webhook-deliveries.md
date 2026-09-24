---
title: "List webhook deliveries"
description: "List delivery attempts for a webhook with status and response code (PRO)."
---

# List webhook deliveries

<!-- widget:api -->

## GET /api/v1/list_webhook_deliveries

List delivery attempts for a webhook with status and response code (PRO).

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/list_webhook_deliveries`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `webhook_id` | integer | yes | — |
| `limit` | integer | no | Max rows (default 50). |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/list_webhook_deliveries?webhook_id=0' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
