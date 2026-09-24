---
title: "Replay webhook delivery"
description: "Replay a webhook delivery by creating a new pending row with the same payload and running the worker (PRO)."
---

# Replay webhook delivery

<!-- widget:api -->

## POST /api/v1/replay_webhook_delivery

Replay a webhook delivery by creating a new pending row with the same payload and running the worker (PRO).

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/replay_webhook_delivery`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `delivery_id` | integer | no | — |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/replay_webhook_delivery' \
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
