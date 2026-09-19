---
title: "Unregister webhook"
description: "Remove a webhook by its id (Free)."
---

# Unregister webhook

<!-- widget:mcp access=write price-millicents=2000 -->

## unregister_webhook

Remove a webhook by its id (Free). Caller must own the workspace.

| Field | Type | Required | Description |
|---|---|---|---|
| `webhook_id` | integer | yes | Webhook id (from list_webhooks). |

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
    "name": "unregister_webhook",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"unregister_webhook","arguments":{"webhook_id":0}}}'
```

<!-- /widget -->
