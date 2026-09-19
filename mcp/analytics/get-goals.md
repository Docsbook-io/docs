---
title: "Get goals"
description: "Completions per goal over the window, plus the daily series behind them (PRO)."
---

# Get goals

<!-- widget:mcp access=read price-millicents=800 -->

## get_goals

Completions per goal over the window, plus the daily series behind them (PRO). Counted per VISIT, not per event — a scroll goal fires several times for one reader and counting events would report one person as five conversions. `value_cents` is null, never 0, when the owner declared no value: 'worth nothing' and 'nobody said' are different claims and only one belongs in a revenue figure.

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
    "name": "get_goals",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_goals","arguments":{}}}'
```

<!-- /widget -->
