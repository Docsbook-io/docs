---
title: "Get visit outcomes"
description: "How visits to these docs END (PRO): success / dead end / bounce / partial, plus the dead-end rate and self-serve resolution rate."
---

# Get visit outcomes

<!-- widget:mcp access=read price-millicents=4000 -->

## get_visit_outcomes

How visits to these docs END (PRO): success / dead end / bounce / partial, plus the dead-end rate and self-serve resolution rate. A 'dead end' is a visit where someone searched, asked the AI or opened several pages and still left with nothing — the clearest evidence that the docs are failing readers. Numbers are estimates (visitors are identified by hashed IP) and rates are withheld below 30 visits; the response says so.

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
    "name": "get_visit_outcomes",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_visit_outcomes","arguments":{}}}'
```

<!-- /widget -->
