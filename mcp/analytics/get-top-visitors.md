---
title: "Get top visitors"
description: "Most active anonymous visitors in the period, ranked by pageview count (PRO)."
---

# Get top visitors

<!-- widget:mcp access=read price-millicents=4000 -->

## get_top_visitors

Most active anonymous visitors in the period, ranked by pageview count (PRO). Returns hashed `visitor_id` (stable across sessions, derived from salted IP), pageview count, first/last seen, and country. Use a returned `visitor_id` with `get_visitor_activity` to drill into a single visitor's full event history.

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
    "name": "get_top_visitors",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_top_visitors","arguments":{}}}'
```

<!-- /widget -->
