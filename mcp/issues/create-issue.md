---
title: "Create issue"
description: "File a GitHub issue on this project's repository."
---

# Create issue

<!-- widget:mcp access=write price-millicents=2000 -->

## create_issue

File a GitHub issue on this project's repository. THIS IS HOW A FINDING OUTLIVES THE CONVERSATION — when you have audited, diagnosed or measured something and found work worth doing, write it down here rather than only in your answer. One call per issue; do not batch several findings into one.
Body: what you observed (with the evidence you actually collected), why it matters for this project, and what done looks like.
Call list_issues first and skip anything that duplicates an open issue.
Label it with the stage of work it belongs to when one fits: observe, understand, discover, decide, plan, execute, measure, verify, learn, coordinate.
Returns the created issue's number and link — report those verbatim, never a link you built yourself. REQUIRES a read-write MCP token.

**Every issue carries an impact contract, and this call refuses without a valid one.** The four `impact_*` fields below say what number the work is expected to move and by how much; they are written into the issue body as a `docsbook-impact` block, so the claim is readable on GitHub and is scored later by code rather than by a model — `get_issue_thread` returns the share of the predicted move that actually happened.

The figures are checked before anything is filed, and four things are rejected outright:

- an outcome that is not one of the thirteen;
- a missing `impact_unit`, or one that is really a number;
- an `impact_target` equal to its `impact_baseline` — that predicts nothing and could not come out false;
- a predicted move smaller than the noise the reading itself carries, which no later reading could confirm.

Read the baseline with a tool before you write it. An invented baseline is the one error here that cannot be corrected afterwards, because the whole comparison hangs off it.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `title` | string | yes | The finding itself, not its category. |
| `body` | string | no | Markdown body: what you observed (with evidence), why it matters here, what done looks like. |
| `labels` | string[] | no | Labels to attach, e.g. ['measure']. Labels that do not exist yet are created by GitHub. |
| `impact_metric` | string | yes | Which of the thirteen outcomes this issue moves: `support_load`, `upkeep_time`, `manual_checks`, `ai_spend`, `broken_pages`, `time_to_answer`, `ai_citations`, `new_markets`, `organic_traffic`, `conversion`, `first_visit_bounce`, `repeat_readers`, `hands_on_time`. |
| `impact_unit` | string | yes | What the two figures below count, stated once: `visits/30d`, `%`, `questions/week`, `seconds`. |
| `impact_baseline` | number | yes | What that number says today. Read it with a tool; do not estimate it. |
| `impact_target` | number | yes | What it should say once this is done, in the same unit. |
| `impact_check_at` | string | no | `YYYY-MM-DD` — the day the reading gets taken. Optional on an issue, required on a pull request opened through `write_docs`. |
| `impact_source` | string | no | Where you read the baseline: a tool name, a URL, a query. |

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
    "name": "create_issue",
    "arguments": {
      "title": "<title>",
      "impact_metric": "organic_traffic",
      "impact_unit": "visits/30d",
      "impact_baseline": 1240,
      "impact_target": 1600,
      "impact_check_at": "2026-10-18"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"create_issue","arguments":{"title":"<title>","impact_metric":"organic_traffic","impact_unit":"visits/30d","impact_baseline":1240,"impact_target":1600,"impact_check_at":"2026-10-18"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/create_issue

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/create_issue' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"title":"<title>","impact_metric":"organic_traffic","impact_unit":"visits/30d","impact_baseline":1240,"impact_target":1600,"impact_check_at":"2026-10-18"}}'
```

<!-- /widget -->
