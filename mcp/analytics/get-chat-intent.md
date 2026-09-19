---
title: "Get chat intent"
description: "Conversations split by the reader's BUYING STAGE — evaluation, pricing, integration, support, bug (PRO)."
---

# Get chat intent

<!-- widget:mcp access=read price-millicents=30000 -->

## get_chat_intent

Conversations split by the reader's BUYING STAGE — evaluation, pricing, integration, support, bug (PRO). Use when asked who is deciding whether to buy, what blocks a purchase, or whether the assistant serves customers or prospects. The verdict names a competitor when readers mentioned one, which is a competitive-intelligence signal no page-level report can produce.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `period` | string | no | Time range (default: 7d) |
| `limit` | integer | no | Max rows (default 100-200) |

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
    "name": "get_chat_intent",
    "arguments": {}
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_chat_intent","arguments":{}}}'
```

<!-- /widget -->
