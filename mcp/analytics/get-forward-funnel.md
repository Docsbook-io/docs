---
title: "Get forward funnel"
description: "Step-by-step completion of the route the OWNER declared (PRO), and which transition leaks."
---

# Get forward funnel

<!-- widget:mcp access=read price-millicents=4000 -->

## get_forward_funnel

Step-by-step completion of the route the OWNER declared (PRO), and which transition leaks. Requires a configured route on the workspace; when none is set the response says so rather than inventing one — use get_reverse_funnel in that case. Steps are matched in order, so a reader who hit step 3 before step 1 is correctly not counted as having reached it.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `period` | string | no | Time range (default: 7d) |

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
    "name": "get_forward_funnel",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_forward_funnel","arguments":{}}}'
```

<!-- /widget -->
