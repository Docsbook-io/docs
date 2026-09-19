---
title: "Configure mentions"
description: "Choose what the mention checks watch on one engine: turn the daily check on or off, and set the queries (up to 5) — the exact words a reader would type or ask."
---

# Configure mentions

<!-- widget:mcp access=write price-millicents=800 -->

## configure_mentions

Choose what the mention checks watch on one engine: turn the daily check on or off, and set the queries (up to 5) — the exact words a reader would type or ask. Queries a workspace does NOT rank for are the point: those are the ones Search Console can never report on. Use get_mentions to read what the checks found.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped to a workspace). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `surface` | string | yes | Which engine this arms: ai_overview (Google's AI answer), google or bing (the results page). One of: `ai_overview`, `google`, `bing`. |
| `enabled` | boolean | no | Whether the daily check runs. Queries are kept either way. |
| `queries` | string[] | no | The queries to check, up to 5. Replaces the saved list. |
| `cron_expression` | string | no | 5-field UTC cron for the check. Defaults to a daily early-morning slot. |

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
    "name": "configure_mentions",
    "arguments": {
      "surface": "ai_overview"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"configure_mentions","arguments":{"surface":"ai_overview"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/configure_mentions

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped to a workspace). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `surface` | string | yes | Which engine this arms: ai_overview (Google's AI answer), google or bing (the results page). One of: `ai_overview`, `google`, `bing`. |
| `enabled` | boolean | no | Whether the daily check runs. Queries are kept either way. |
| `queries` | string[] | no | The queries to check, up to 5. Replaces the saved list. |
| `cron_expression` | string | no | 5-field UTC cron for the check. Defaults to a daily early-morning slot. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/configure_mentions' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"surface":"ai_overview"}'
```

<!-- /widget -->
