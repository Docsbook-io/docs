---
title: "Approve translation"
description: "Approve a draft translation, moving it to status 'published'."
---

# Approve translation

<!-- widget:mcp access=write price-millicents=2000 -->

## approve_translation

Approve a draft translation, moving it to status 'published'. REQUIRES PRO or higher.

| Field | Type | Required | Description |
|---|---|---|---|
| `translation_id` | number | yes | Translation row ID |

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
    "name": "approve_translation",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"approve_translation","arguments":{"translation_id":0}}}'
```

<!-- /widget -->
