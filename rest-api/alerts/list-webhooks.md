---
title: "List webhooks"
description: "List all registered webhooks for a workspace (Free)."
---

# List webhooks

<!-- widget:api -->

## GET /api/v1/list_webhooks

List all registered webhooks for a workspace (Free).

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/list_webhooks`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/list_webhooks' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
