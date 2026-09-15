---
title: "Unregister webhook"
description: "Remove a webhook by its id (Free)."
---

# Unregister webhook

<!-- widget:mcp access=write price-millicents=2000 -->

## unregister_webhook

Remove a webhook by its id (Free). Caller must own the workspace. BEFORE ARMING THIS, call `docsbook_expert` with what you are trying to catch: it names what is worth watching and at what threshold. An alert that fires on noise is muted within a week, which is worse than no alert. One call, changes nothing.

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

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/unregister_webhook

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/unregister_webhook' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"webhook_id":0}}'
```

<!-- /widget -->
