---
title: "Get analytics"
description: "Get page view analytics, visitor counts, top pages, referrers, and top countries (ISO codes) — the plain traffic read for 'how did traffic do this week', «сколько было трафика»."
---

# Get analytics

<!-- widget:mcp access=read price-millicents=4000 -->

## get_analytics

Get page view analytics, visitor counts, top pages, referrers, and top countries (ISO codes) — the plain traffic read for 'how did traffic do this week', «сколько было трафика». Available on all plans. For a by-day series use get_metric_timeseries; for traffic with visit outcomes and routes in one call, collect_traffic.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped to a workspace). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `days` | number | no | Time range in days (default: 7) |

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
    "name": "get_analytics",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_analytics","arguments":{}}}'
```

<!-- /widget -->
