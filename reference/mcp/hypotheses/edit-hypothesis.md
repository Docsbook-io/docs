---
title: "Edit hypothesis"
description: "JUDGE a hypothesis with what the reading showed, move its date, or correct it."
---

# Edit hypothesis

<!-- widget:mcp access=write -->

## edit_hypothesis

JUDGE a hypothesis with what the reading showed, move its date, or correct it. Free on every plan. 🔴 JUDGING IS THE POINT. `result` is what was measured — the pair, with the denominator, not a rate on its own — and `verdict` is which way it went. **"Nothing distinguishable" is `rejected`, not a missing verdict**: the claim predicted an effect and none appeared, and that is the most valuable row this store produces, because it is what stops the same change being made again with the same confidence. 🔴 TOO EARLY IS NOT A VERDICT. If the honest wait has not passed, move the date with `check_in_days` instead of judging. A verdict recorded on a week's own variance is a wrong answer that will be quoted for a year. Pass an empty string in `verdict` to RETRACT one — a reading taken against the wrong baseline has to be retractable, and the row goes back to `testing` rather than to untested, because the change was still made. After a verdict: add_memory the RULE it taught (not the figure — figures expire, 'this class of change does nothing here' does not), and — when it was rejected — add_hypothesis for the successor and put its key in `next_key`. A rejection that names nothing next is a dead end nobody learned from. Corrections happen in place rather than remove-and-re-add, and here that is load-bearing: "written before the change, judged after it" is the entire claim a hypothesis rests on, and a re-created row cannot make it. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `key` | string | yes | The hypothesis's handle, from list_hypotheses. |
| `text` | string | no | Replacement claim. Omit to keep it. |
| `kind` | string | no | Correct which sort of row this is. forecast: Written BEFORE the change, to decide it. Argued from a goal that is not being reached, and sized by something published outside this project. This is the only kind that can be cited later as a prediction. reconstruction: Written about a change that ALREADY shipped, to pay the board's `unmeasured` debt. Honest and useful — but nobody predicted it, so `expected_effect` here is what we NOW think it should have done, and it must never be counted as a forecast. 🔴 Moving a row from `reconstruction` to `forecast` after the fact is the one edit that makes the store lie: it says somebody predicted this, and nobody did. One of: `forecast`, `reconstruction`. |
| `status` | string | no | Where this stands. DERIVED from what you write — a verdict makes it verified whatever you pass, and retracting one puts it back to testing — so pass it only to say "testing" before a change is linked. untested: Written down, not yet tested — no change has been made against it. The next move is an issue naming the change, then a pull request linked to both, then a `check_at` date for the reading. testing: A change is out and the verdict waits on the date in `check_at`. Do not judge it early: a reading taken before the honest wait measures the week's own variance, not the change. verified: Judged — `verdict` says which way and `result` says what was measured. Read these before proposing the same change again with the same confidence. One of: `untested`, `testing`, `verified`. |
| `verdict` | string | no | `confirmed` or `rejected` — this judges it. Pass an empty string to RETRACT a verdict. 'Nothing distinguishable' is `rejected`. |
| `result` | string | no | What happened, in the owner's words — 'now on Google's first page for this search; the AI answer still names a competitor'. The pair with its denominator and call ids goes in `evidence`. Pass an empty string to clear it. |
| `goal_key` | string | no | The goal this argues for — the standing goal `be_found`, a branch, or one of the owner's own. Checked against that list; a name matching nothing is refused with the list. Empty string clears it. |
| `direction_key` | string | no | The direction this claim was drawn from. Checked against the directions here. Empty string clears it. |
| `opportunity_key` | string | no | The opportunity inside that direction. Empty string clears it. |
| `because` | string | no | Why this claim exists: the goal is not being reached, on which reading, and the cause. Empty string clears it. |
| `source_url` | string | no | Replacement source — the page outside this product the idea came from. Empty string clears it. |
| `source_claim` | string | no | The one fact that page reports. Empty string clears it. |
| `evidence` | string | no | Replacement evidence — the observation on THIS project. Empty string clears it. |
| `baseline` | string | no | The before-reading, when the row was written without one or quoted it wrongly. 🔴 Only before the result is in: a baseline edited afterwards is the same forgery as an edited forecast, moved to the field nobody thinks to check. Empty string clears it. |
| `expected_effect` | string | no | Replacement forecast. 🔴 Only before the reading is taken: rewriting this after the result is how a description becomes a prediction, and nothing downstream can tell. |
| `metric` | string | no | Replacement reading. Empty string clears it. |
| `change` | string | no | What was done to test it. Empty string clears it. |
| `check_in_days` | number | no | Move the check this many days from NOW — the safe way to reschedule, with no date arithmetic on your side. |
| `check_at` | string | no | Move it to an absolute instant instead. |
| `next_key` | string | no | The hypothesis this one led to. Empty string clears it. |

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
    "name": "edit_hypothesis",
    "arguments": {
      "key": "<key>",
      "kind": "forecast",
      "status": "untested"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"edit_hypothesis","arguments":{"key":"<key>","kind":"forecast","status":"untested"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/edit_hypothesis

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/edit_hypothesis' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"key":"<key>","kind":"forecast","status":"untested"}}'
```

<!-- /widget -->
