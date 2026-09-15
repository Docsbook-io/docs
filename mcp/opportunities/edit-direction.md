---
title: "Edit direction"
description: "JUDGE a direction with the target reading, move its review date, or correct it."
---

# Edit direction

<!-- widget:mcp access=write price-millicents=2000 -->

## edit_direction

JUDGE a direction with the target reading, move its review date, or correct it. Free on every plan. 🔴 CLOSING ONE IS A SEPARATE SENTENCE FROM JUDGING THE CHANGES UNDER IT. `status: "reached"` says the docs now show up for this audience by what `target` predicted; a set of confirmed hypotheses does not say that on its own and never has. The reverse is the row this store exists to be able to write: every claim confirmed, the target still short — which means the opportunities addressed a smaller share of the audience than anybody thought, and the next direction is about the rest of it. `result` is what the re-check showed, written FOR THE OWNER: 'now on Google's first page for 2 of the 5 searches; the AI answer still names a competitor for the other 3'. The figures with their call ids go in `method`. `abandoned` is legitimate and needs the same honesty: say in `result` what changed about the audience or the market. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `key` | string | yes | The direction's handle, from list_opportunities. |
| `title` | string | no | Written for the owner. |
| `goal_key` | string | no | The goal it serves — the standing goal, a branch, or one of the owner's own. Checked against that list. |
| `question` | string | no | Written for the owner. |
| `scope` | string | no | Technical. |
| `method` | string | no | Technical. |
| `baseline` | string | no | Technical. |
| `target` | string | no | Written for the owner. |
| `target_metric` | string | no | Technical. |
| `target_value_cents` | number | no | — |
| `review_in_days` | number | no | — |
| `review_at` | string | no | — |
| `status` | string | no | `reached` only when the TARGET reading says so — not when the changes under it were confirmed. One of: `open`, `reached`, `abandoned`. |
| `result` | string | no | What the re-check showed, in the owner's words. The baseline-and-reading pair with its call ids goes in `method`. |

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
    "name": "edit_direction",
    "arguments": {
      "key": "<key>",
      "status": "open"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"edit_direction","arguments":{"key":"<key>","status":"open"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/edit_direction

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/edit_direction' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"key":"<key>","status":"open"}}'
```

<!-- /widget -->
