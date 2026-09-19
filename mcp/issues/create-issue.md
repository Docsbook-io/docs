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

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `title` | string | yes | The finding itself, not its category. |
| `body` | string | no | Markdown body: what you observed (with evidence), why it matters here, what done looks like. |
| `labels` | string[] | no | Labels to attach, e.g. ['measure']. Labels that do not exist yet are created by GitHub. |
| `impact_metric` | string | yes | Which of the thirteen outcomes this issue moves. One of: `support_load`, `upkeep_time`, `manual_checks`, `ai_spend`, `broken_pages`, `time_to_answer`, `ai_citations`, `new_markets`, `organic_traffic`, `conversion`, `first_visit_bounce`, `repeat_readers`, `hands_on_time`. |
| `impact_unit` | string | yes | What the two figures below COUNT, stated once: 'visits/30d', '%', 'questions/week', 'seconds'. |
| `impact_baseline` | number | yes | What that number says TODAY. Read it with a tool — an invented baseline is the one error here that cannot be corrected later, because the whole comparison hangs off it. |
| `impact_target` | number | yes | What it should say once this is done, in the same unit. A target equal to the baseline, or a move smaller than the reading's own noise, is refused. |
| `impact_check_at` | string | no | YYYY-MM-DD — the day the reading gets taken. |
| `impact_source` | string | no | Where you read the baseline — a tool name, a URL, a query. |

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
      "impact_metric": "support_load",
      "impact_unit": "<impact_unit>",
      "impact_baseline": 0,
      "impact_target": 0
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"create_issue","arguments":{"title":"<title>","impact_metric":"support_load","impact_unit":"<impact_unit>","impact_baseline":0,"impact_target":0}}}'
```

<!-- /widget -->
