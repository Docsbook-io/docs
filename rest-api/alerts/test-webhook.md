---
title: "Test webhook"
description: "Send a test ping to a registered webhook and run the delivery worker immediately (Free)."
---

# Test webhook

<!-- widget:api -->

## GET /api/v1/test_webhook

Send a test ping to a registered webhook and run the delivery worker immediately (Free).

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/test_webhook`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `webhook_id` | integer | yes | Webhook id to test. |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/test_webhook?webhook_id=0' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
