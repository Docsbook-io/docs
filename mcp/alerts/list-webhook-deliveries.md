---
title: "List webhook deliveries"
description: "List delivery attempts for a webhook with status and response code (PRO)."
---

# List webhook deliveries

<!-- widget:mcp access=read price-millicents=4000 -->

## list_webhook_deliveries

List delivery attempts for a webhook with status and response code (PRO).

| Field | Type | Required | Description |
|---|---|---|---|
| `webhook_id` | integer | yes | — |
| `limit` | integer | no | Max rows (default 50). |

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
    "name": "list_webhook_deliveries",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_webhook_deliveries","arguments":{"webhook_id":0}}}'
```

<!-- /widget -->
