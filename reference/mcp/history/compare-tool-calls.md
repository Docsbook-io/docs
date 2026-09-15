---
title: "Compare tool calls"
description: "TWO READINGS OF THE SAME INSTRUMENT, and what moved between them."
---

# Compare tool calls

<!-- widget:mcp access=read -->

## compare_tool_calls

TWO READINGS OF THE SAME INSTRUMENT, and what moved between them. Free on every plan. This is the measurement — the thing you do instead of asserting that a change worked. Two ways to call it. Name a `tool` (and a `subject`, when the reading was scoped to a page or a heading) and it takes the newest recorded reading and the nearest one at least `baseline_age` old — 'today against a week ago' is `{ tool: "get_analytics", baseline_age: "7d" }`. Or name two `call_id`s exactly. 🔴 TAKE THE READING FIRST. It compares what is already in the ledger; it runs nothing. If the newest reading predates the change you are measuring, call the read tool again and then compare — otherwise you are comparing two readings of the world before you touched it. Answers with every numeric field that MOVED (before, after, delta, and a percentage that is null — never ∞ or 100 — when the baseline was zero), what appeared, what went away, and how many fields did not move at all, which is the denominator that stops one moved number from reading as 'everything changed'. Timestamp fields are excluded: they differ on every pair by construction. It reports NO verdict, on purpose. Two readings a week apart are two facts. Docs traffic moves on its own, an index re-crawls, a holiday happens — whoever asked knows what else was going on and this tool does not. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `tool` | string | no | The instrument, e.g. 'get_analytics'. Required unless you pass both call ids. |
| `subject` | string | no | Scope the series to a page, heading, host or query. Omit for the reading of the whole site. |
| `baseline_age` | string | no | How old the baseline should be at least — '7d', '24h', '4w'. Default 7d. Never picks one YOUNGER than this; it falls back to the oldest reading there is and says so. |
| `call_id` | integer | no | The later reading, by id. |
| `baseline_call_id` | integer | no | The earlier reading, by id. |

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
    "name": "compare_tool_calls",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"compare_tool_calls","arguments":{}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/compare_tool_calls

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/compare_tool_calls' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{}}'
```

<!-- /widget -->
