---
title: "Get reverse funnel"
description: "Works BACKWARDS from visits that ended well (PRO): which entry pages lead to success and in how many steps."
---

# Get reverse funnel

<!-- widget:mcp access=read price-millicents=4000 -->

## get_reverse_funnel

Works BACKWARDS from visits that ended well (PRO): which entry pages lead to success and in how many steps. Stronger than a configured funnel because it needs no hypothesis — it reports the path readers actually found, which is often one the owner never designed. The action is to promote that entry point in the navigation.

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
    "name": "get_reverse_funnel",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_reverse_funnel","arguments":{}}}'
```

<!-- /widget -->
