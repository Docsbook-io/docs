---
title: "Delete translation"
description: "Delete a translation row."
---

# Delete translation

<!-- widget:mcp access=write price-millicents=1 -->

## delete_translation

Delete a translation row. REQUIRES PRO or higher.

| Field | Type | Required | Description |
|---|---|---|---|
| `translation_id` | number | yes | Translation row ID |

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "delete_translation",
    "arguments": {
      "translation_id": 0
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer YOUR_MCP_OAUTH_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"delete_translation","arguments":{"translation_id":0}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### POST /api/v1/delete_translation

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `translation_id` | number | yes | Translation row ID |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/delete_translation' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"translation_id":0}'
```

<!-- /widget -->
