---
title: "Replay webhook delivery"
description: "Replay a webhook delivery by creating a new pending row with the same payload and running the worker (PRO)."
---

# Replay webhook delivery

<!-- widget:mcp access=write price-millicents=6000 -->

## replay_webhook_delivery

Replay a webhook delivery by creating a new pending row with the same payload and running the worker (PRO).

| Field | Type | Required | Description |
|---|---|---|---|
| `delivery_id` | integer | yes | — |

<!-- /widget -->

## Call it

<!-- widget:code-group -->

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "replay_webhook_delivery",
    "arguments": {
      "delivery_id": 0
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"replay_webhook_delivery","arguments":{"delivery_id":0}}}'
```

<!-- /widget -->
