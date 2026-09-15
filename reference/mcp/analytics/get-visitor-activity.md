---
title: "Get visitor activity"
description: "Chronological activity timeline of a single anonymous visitor (PRO)."
---

# Get visitor activity

<!-- widget:mcp access=read price-millicents=4000 -->

## get_visitor_activity

Chronological activity timeline of a single anonymous visitor (PRO). Pass a `visitor_id` returned from `get_page_journeys` or `get_top_visitors`. Returns ordered events (pageviews, page_feedback, cta_click, etc.) with paths and event-specific details (vote, query, href, …). Only events that carry server-side IP can be attributed to a visitor — pure client-side tracking events are excluded. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `visitor_id` | string | yes | Hashed visitor id (from `get_page_journeys` or `get_top_visitors`) |
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
    "name": "get_visitor_activity",
    "arguments": {
      "visitor_id": "<visitor_id>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_visitor_activity","arguments":{"visitor_id":"<visitor_id>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/get_visitor_activity

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/get_visitor_activity' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"visitor_id":"<visitor_id>"}}'
```

<!-- /widget -->
