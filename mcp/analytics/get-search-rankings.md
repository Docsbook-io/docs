---
title: "Get search rankings"
description: "Get real Google Search Console positions for the docs (PRO): average position, impressions, clicks, the queries they rank for, and the 'worth improving' set (position 5-20 —…"
---

# Get search rankings

<!-- widget:mcp access=read price-millicents=4000 -->

## get_search_rankings

Get real Google Search Console positions for the docs (PRO): average position, impressions, clicks, the queries they rank for, and the 'worth improving' set (position 5-20 — already visible to Google, not yet winning the click). Use this to decide WHICH page to rewrite and for WHICH query, instead of guessing from traffic alone. Data is cached and lags ~2 days behind Google. Pass refresh=true to pull fresh data (allowed once per day; Google itself only updates daily).

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped to a workspace). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `refresh` | boolean | no | Pull fresh data from Google before returning (max once per day) |

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
    "name": "get_search_rankings",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_search_rankings","arguments":{}}}'
```

<!-- /widget -->
