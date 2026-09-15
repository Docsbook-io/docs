---
title: "Mark path as funnel step"
description: "Add a documentation PAGE to a funnel as its next step, creating the page goal if it does not exist yet."
---

# Mark path as funnel step

<!-- widget:mcp access=write price-millicents=2000 -->

## mark_path_as_funnel_step

Add a documentation PAGE to a funnel as its next step, creating the page goal if it does not exist yet. The shortcut for 'this page is part of the route readers should take' — it saves creating a goal and then editing the funnel. Creates the funnel too if the name is new. Note the broad-entry rule: if this is the FIRST step of a new funnel you will get a warning, because a single page as step 1 excludes every reader who arrived deep. BEFORE FILING THIS, call `docsbook_expert` with the outcome you want: it says whether this is the thing worth doing first and what it would move, so the backlog is ranked rather than merely long. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `path` | string | yes | The doc path, e.g. '/docs/quickstart'. |
| `funnel` | string | yes | Funnel name to append the step to. Created if it does not exist. |
| `position` | number | no | 0-based index to insert at. Appends when omitted. |

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
    "name": "mark_path_as_funnel_step",
    "arguments": {
      "path": "<path>",
      "funnel": "<funnel>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"mark_path_as_funnel_step","arguments":{"path":"<path>","funnel":"<funnel>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/mark_path_as_funnel_step

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/mark_path_as_funnel_step' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"path":"<path>","funnel":"<funnel>"}}'
```

<!-- /widget -->
