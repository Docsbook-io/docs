---
title: "Get route patterns"
description: "The 2-4 page SEQUENCES readers actually walk (PRO), with how often each ends well."
---

# Get route patterns

<!-- widget:mcp access=read price-millicents=4000 -->

## get_route_patterns

The 2-4 page SEQUENCES readers actually walk (PRO), with how often each ends well. Top-pages reports cannot distinguish an intended journey from three unrelated landings — this can. A frequent route that keeps ending badly is a NAVIGATION defect (the next page readers need is not the one you link to), not a page-quality problem, so rewriting the pages will not fix it.

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
    "name": "get_route_patterns",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_route_patterns","arguments":{}}}'
```

<!-- /widget -->
