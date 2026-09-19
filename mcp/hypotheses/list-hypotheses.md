---
title: "List hypotheses"
description: "WHAT THIS PROJECT BELIEVES WILL WORK, AND WHAT IT FOUND OUT — every claim somebody wrote down here, what it predicted, and how it was judged."
---

# List hypotheses

<!-- widget:mcp access=read price-millicents=800 -->

## list_hypotheses

WHAT THIS PROJECT BELIEVES WILL WORK, AND WHAT IT FOUND OUT — every claim somebody wrote down here, what it predicted, and how it was judged. Free on every plan. 🔴 READ THIS BEFORE PROPOSING A CHANGE. A `rejected` row is this project having ALREADY TRIED your idea and measured nothing — proposing it again with the same confidence is the single most expensive mistake available here, and the row that prevents it is sitting in this list with the figures in `result`. 🔴 AND READ IT FOR WHAT IS OWED. A row whose `state` is `due` has a prediction, a change that shipped, and a date that has arrived, with nobody having said whether it worked. Take the reading named in `metric`, write what it showed into `result`, and judge it with edit_hypothesis. A board that says "measuring" about something nobody is measuring is worse than an empty one. 🔴 AND READ `kind` ON EVERY ROW BEFORE YOU CITE IT. `forecast` is a claim written BEFORE the change, argued from a goal and sized by something published outside this project — the only kind that predicted anything. `reconstruction` was written afterwards about a change that already shipped, to pay the board's `unmeasured` debt: honest, useful, and not evidence that this project forecasts anything. `counts.forecasts` is the figure that says which sort of store this is. Each row carries `text` (the claim, in the owner's words), `kind`, `goal_key` (the goal it argues for — the standing goal `be_found` unless narrowed or the owner's own), `direction_key` + `opportunity_key` (the opportunity it was drawn from), `because` (why the claim exists — the opportunity is not won, and the cause), `source_url` (where the IDEA came from) with `source_claim` (the one fact that page reports), `evidence` (the observation on THIS project it rests on — the trace), `baseline` (what the deciding reading said BEFORE the change — the figure the verdict is compared against), `expected_effect` (what it should buy, written BEFORE the change — that is what makes it a forecast), `metric` (the reading that decides it, the same tool and subject that produced `baseline`), `change`, `check_at`, `result`, `verdict`, `next_key` (the hypothesis this one led to) and `overdue_days`. `gap` names the one thing to do about this store — a verdict owed, nothing written at all, forecasts arguing for no goal or quoting no source, a rejection that taught nobody anything.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `state` | string | no | Which ones. `all` (the default) — everything, due-first. `open` — not yet judged. `due` — the check date has arrived and no verdict was recorded; these are the ones to act on. `verified` — judged, with the verdict and the figures; read these before proposing a change somebody already measured. One of: `all`, `open`, `due`, `verified`. |
| `limit` | number | no | Cap the rows returned. Default 50. |

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
    "name": "list_hypotheses",
    "arguments": {
      "state": "all"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_hypotheses","arguments":{"state":"all"}}}'
```

<!-- /widget -->
