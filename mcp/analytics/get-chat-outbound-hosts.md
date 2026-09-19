---
title: "Get chat outbound hosts"
description: "Where the assistant's answers actually SEND people — destination hosts ranked by clicks, with the workspace's configured target page marked (PRO)."
---

# Get chat outbound hosts

<!-- widget:mcp access=read price-millicents=800 -->

## get_chat_outbound_hosts

Where the assistant's answers actually SEND people — destination hosts ranked by clicks, with the workspace's configured target page marked (PRO). Answers 'is the chat driving anyone to our pricing/demo page, or is it handing readers to GitHub and to vendors'. `kind` is only target / code / other: a competitor of THIS workspace's owner is not something the server can know, so the ranked list is what lets the owner recognise one. Zero rows with live conversations means answers are ending the conversation instead of forwarding it.

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
    "name": "get_chat_outbound_hosts",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_chat_outbound_hosts","arguments":{}}}'
```

<!-- /widget -->
