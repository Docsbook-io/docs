---
title: "Get issue thread"
description: "The comments on one issue or pull request, with its impact contract and how much of the predicted move has actually happened."
---

# Get issue thread

<!-- widget:mcp access=read price-millicents=6000 -->

## get_issue_thread

Read the comments on one GitHub issue or pull request, in order, together with its impact contract and how much of the predicted move has actually happened.

Call it BEFORE replying to anything on a record — the question may already have been answered, and a reply that repeats an existing one is worse than silence.

Returns `{ number, title, state, comments: [{ author, body, created_at }], impact }`. When the record carries a contract, `impact` holds the outcome it claims, its unit, the baseline, the target, the reading taken so far, the day it is checked, and:

- `achieved_percent` — the share of the predicted move that has actually happened, as a percent. 100 is exactly what was promised, 40 is two fifths of the way, negative means the number went the other way, and past 100 means the change beat its own claim. It is **computed from the figures**, not estimated: quote it as given and never recompute it.
- `state` — `waiting` before the check date, `due` once it has passed with no reading taken, `judged` once one has.
- `verdict` — `worked`, `no_distinguishable_effect`, `made_worse`, or `cannot_tell`.

`impact` is `null` when the record carries no contract. That means nothing can say whether the work succeeded — say so plainly rather than guessing a number.

Issues and pull requests share one numbering on GitHub, so `number` accepts either.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `number` | number | yes | The issue or pull request number. |

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
    "name": "get_issue_thread",
    "arguments": {
      "number": 42
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_issue_thread","arguments":{"number":42}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/get_issue_thread

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/get_issue_thread' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"number":42}}'
```

<!-- /widget -->
