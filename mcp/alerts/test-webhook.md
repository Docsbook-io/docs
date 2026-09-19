---
title: "Test webhook"
description: "Send a test ping to a registered webhook and run the delivery worker immediately (Free)."
---

# Test webhook

<!-- widget:mcp access=read price-millicents=6000 -->

## test_webhook

Send a test ping to a registered webhook and run the delivery worker immediately (Free).

| Field | Type | Required | Description |
|---|---|---|---|
| `webhook_id` | integer | yes | Webhook id to test. |

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
    "name": "test_webhook",
    "arguments": {
      "webhook_id": 0
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"test_webhook","arguments":{"webhook_id":0}}}'
```

<!-- /widget -->
