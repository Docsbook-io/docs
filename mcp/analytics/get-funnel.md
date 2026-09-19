---
title: "Get funnel"
description: "How a declared route holds up, step by step (PRO)."
---

# Get funnel

<!-- widget:mcp access=read price-millicents=4000 -->

## get_funnel

How a declared route holds up, step by step (PRO). Each step reports how many visits reached it HAVING passed every earlier step in order, the share of the previous step that continued, and the top sources and countries at that step. `leak_index` names the worst TRANSITION, which is where the route breaks — not the smallest step, which is usually just the last one. Percentages are withheld per step under 30 visits into it, so a solid step 2 still quotes a rate while a thin step 5 does not. Returns a null `report` if the workspace has not declared a funnel yet — there is no built-in default to fall back to.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `funnel` | string | no | Funnel name. Defaults to the first one declared. |
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
    "name": "get_funnel",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_funnel","arguments":{}}}'
```

<!-- /widget -->
