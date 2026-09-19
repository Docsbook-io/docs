---
title: "Get dead end pages"
description: "Pages where readers gave up, ranked (PRO)."
---

# Get dead end pages

<!-- widget:mcp access=read price-millicents=4000 -->

## get_dead_end_pages

Pages where readers gave up, ranked (PRO). THIS is the 'what should I rewrite first' list: each row is a page that dead-end visits ended on. Rows flagged `terminal_success` are pages people leave from because they got what they needed (e.g. copied a snippet) — do not 'fix' those.

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
    "name": "get_dead_end_pages",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_dead_end_pages","arguments":{}}}'
```

<!-- /widget -->
