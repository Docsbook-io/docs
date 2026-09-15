---
title: "List tool calls"
description: "THE HISTORY OF WHAT THIS SERVER WAS ASKED about this project — every metered call, with the arguments it was given and the answer it gave back."
---

# List tool calls

<!-- widget:mcp access=read price-millicents=800 -->

## list_tool_calls

THE HISTORY OF WHAT THIS SERVER WAS ASKED about this project — every metered call, with the arguments it was given and the answer it gave back. Free on every plan. 🔴 THIS IS HOW YOU MEASURE ANYTHING HERE. Any read tool is a snapshot instrument: call it today, call it again after you change something, and the two rows are a before and an after. So BEFORE you change a page, a setting, a nav or a prompt, take the reading you intend to be judged by — and before you claim a change worked, look for the reading that was taken beforehand. A recommendation made without looking at what was already tried here is the most expensive mistake available to you. The answer groups into `series`: one series is one TOOL on one SUBJECT, and a subject is a page, a heading, a host, a search query or the whole site — normalised, so a reading taken with `path: "/Quick-Start/"` and one taken with `page: "quick-start"` are the same series and can be compared. Each series says how many readings exist, when the newest was taken and when the one before it was, which is exactly what decides whether a comparison is available today. Then `compare_tool_calls` puts two readings side by side, `get_tool_call` reads one whole, and `search_tool_calls` finds one by what is IN it. No verdict at any step: two readings a week apart are a pair of facts, not cause and effect. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `tool` | string | no | Only this tool's calls, e.g. 'get_analytics'. |
| `subject` | string | no | Only calls about this page, heading ('/quick-start#install'), host or query. A page also matches its own headings; a heading matches only itself. |
| `kind` | string | no | Only the tools in one named group — the same two groups the Overview cards draw. One of: `analytics`, `seo`. |
| `since` | string | no | How far back, as '24h', '7d', '4w'. Default: everything kept. |
| `failed_only` | boolean | no | Only the calls that errored. A series of failures looks exactly like a healthy one when you only count rows. |
| `group` | boolean | no | Group into snapshot series (default true). Pass false for a flat, newest-first call list. |
| `limit` | integer | no | Max series (or calls, ungrouped). Default 25. |

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
    "name": "list_tool_calls",
    "arguments": {
      "kind": "analytics"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_tool_calls","arguments":{"kind":"analytics"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/list_tool_calls

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/list_tool_calls' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"kind":"analytics"}}'
```

<!-- /widget -->
