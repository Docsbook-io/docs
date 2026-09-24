---
title: "Create funnel"
description: "Define an ORDERED route through the docs, as a list of goal names."
---

# Create funnel

<!-- widget:mcp access=write price-millicents=1 -->

## create_funnel

Define an ORDERED route through the docs, as a list of goal names. Order is the whole point: a visit counts as reaching step N only if it hit steps 1..N in sequence, so a reader who lands on step 3 first is not counted. Two rules the validator enforces and you should follow when proposing one: start BROAD (most docs readers arrive deep from search or an AI answer, and a narrow step 1 excludes the majority of traffic before measuring anything), and end on a REAL OUTCOME (a funnel ending on a scroll measures attention, not results). `window_hours` bounds how long after step 1 a later step still counts; omit it to use the visit itself, which is the honest default for docs.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `key` | string | yes | Machine name, e.g. 'evaluation'. |
| `steps` | string[] | yes | Goal names, in order. Between 2 and 8. Create the goals first with create_goal. |
| `label` | string | no | Human label. Defaults to the key. |
| `window_hours` | number | no | Conversion window in hours. Clamped to what the plan retains — a window longer than your history can never complete. |

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
    "name": "create_funnel",
    "arguments": {
      "key": "<key>",
      "steps": []
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer YOUR_MCP_OAUTH_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"create_funnel","arguments":{"key":"<key>","steps":[]}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### POST /api/v1/create_funnel

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `key` | string | yes | Machine name, e.g. 'evaluation'. |
| `steps` | string[] | yes | Goal names, in order. Between 2 and 8. Create the goals first with create_goal. |
| `label` | string | no | Human label. Defaults to the key. |
| `window_hours` | number | no | Conversion window in hours. Clamped to what the plan retains — a window longer than your history can never complete. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/create_funnel' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"key":"<key>","steps":[]}'
```

<!-- /widget -->
