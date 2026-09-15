---
title: "Edit opportunity"
description: "CORRECT one opportunity — a figure that was re-measured, a competitor that moved, or a decision not to work it."
---

# Edit opportunity

<!-- widget:mcp access=write price-millicents=2000 -->

## edit_opportunity

CORRECT one opportunity — a figure that was re-measured, a competitor that moved, or a decision not to work it. Free on every plan. 🔴 THIS IS NOT WHERE A WIN IS RECORDED. Whether the opportunity was taken is the `verdict` on the hypotheses pointing at this row (edit_hypothesis), and this table deliberately has no column for it: one fact with two owners is two answers within a week. What IS decided here is `disposition` — `dropped` for "the audience is real and the fit is not", with the reason in the owner's words, so the next run reading the same demand does not re-propose it. The same rule as add_opportunity: `intent`, `current`, `competitor`, `potential`, `demand_note` and `drop_reason` are the owner's; `evidence` and `demand_source` are the trace. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `direction_key` | string | yes | The direction, from list_opportunities. |
| `key` | string | yes | The opportunity's handle. |
| `intent` | string | no | — |
| `demand_value` | number | no | — |
| `demand_unit` | string | no | — |
| `demand_source` | string | no | — |
| `demand_note` | string | no | — |
| `current` | string | no | — |
| `competitor` | string | no | — |
| `competitor_url` | string | no | — |
| `action` | string | no | One of: `create`, `rewrite`, `expand`, `structure`, `authority`, `none`. |
| `potential` | string | no | — |
| `potential_value_cents` | number | no | — |
| `evidence` | string | no | — |
| `disposition` | string | no | One of: `open`, `dropped`. |
| `drop_reason` | string | no | — |
| `position` | number | no | — |

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
    "name": "edit_opportunity",
    "arguments": {
      "direction_key": "<direction_key>",
      "key": "<key>",
      "action": "create",
      "disposition": "open"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"edit_opportunity","arguments":{"direction_key":"<direction_key>","key":"<key>","action":"create","disposition":"open"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/edit_opportunity

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/edit_opportunity' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"direction_key":"<direction_key>","key":"<key>","action":"create","disposition":"open"}}'
```

<!-- /widget -->
