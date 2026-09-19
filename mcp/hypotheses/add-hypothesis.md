---
title: "Add hypothesis"
description: "WRITE DOWN A WAY TO WIN AN OPPORTUNITY, BEFORE YOU MAKE THE CHANGE — what you will try, what it should buy, and the published page that says why anybody expects it to work."
---

# Add hypothesis

<!-- widget:mcp access=write price-millicents=2000 -->

## add_hypothesis

WRITE DOWN A WAY TO WIN AN OPPORTUNITY, BEFORE YOU MAKE THE CHANGE — what you will try, what it should buy, and the published page that says why anybody expects it to work. Free on every plan. 🔴 WRITTEN FOR THE OWNER, AND REFUSED WHEN IT IS NOT. `text` (the claim), `because` (why now), `expected_effect` (what it should buy, by when), `source_claim` (the one fact the source reports) and `result` are the row on the owner's screen: plain words, no call ids, tool names, file paths, metric dumps or jargon they would have to look up. Say it as the business would: "Using the words readers actually search with — 'virtual card' — on the card page gets it shown on Google for those searches within 30 days, up from absent today." The trace — the `call_id`, the tool, the figure as measured — goes in `evidence`, `baseline`, `metric` and `change`, which the owner never reads and which you MUST fill. 🔴 A HYPOTHESIS IS NOT AN IDEA YOU HAD. It is the end of a chain, and this call REFUSES a `forecast` that is missing a link: **`because`** — why this claim exists now: the opportunity is not won, on this reading (`call_id` in `evidence`), and here is the cause; **`source_url` + `source_claim`** — the page outside this product that says how this class of problem is solved, and the ONE fact it reports; **`baseline`** — what the deciding reading says RIGHT NOW, with its figure; then `expected_effect` SIZED FROM THAT FACT, and `metric`, the reading that decides it. `goal_key` is inherited — the direction's goal, or the standing goal `be_found` — and never something to ask the owner for. 🔴 DRAW IT FROM AN OPPORTUNITY. `direction_key` + `opportunity_key` (from list_opportunities) are what make the claim a SHARE of something rather than an improvement to a page: the verdict later reads as 'this took the 110 searches a month behind that row' instead of 'this page got better'. 🔴 TAKE THE BEFORE-READING BEFORE YOU MAKE THE CHANGE. A verdict is a COMPARISON, and its before-half stops being obtainable the moment the change ships — no later run can recover it. Call the tool you are about to name in `metric`, and write what it returned into `baseline` WITH THE FIGURE, the tool, the call id and the date. Then `expected_effect` is what that same reading should say afterwards, in the owner's words and with a number, by a date. Both are refused without a number in them: "should improve" cannot come out false, and a claim that cannot come out false is not a hypothesis. 🔴 WHAT COUNTS AS A SOURCE: a page you actually opened, about the PROBLEM rather than about this product — an article, a competitor's page, a standard, a write-up with numbers. Search the problem, not our name. `source_claim` is what that page states — the mechanism, or the size and the timescale it measured — and it is the part an address cannot fake. NEVER this project's own pull request, commit or issue: that is the change the claim is about, and the call refuses it. Found nothing is an honest answer — say which queries you tried and file it as a `reconstruction`, or not at all. 🔴 `kind: "reconstruction"` IS THE HONEST ESCAPE HATCH, and it is not a lesser row. Use it when the change ALREADY SHIPPED and you are paying the board's `unmeasured` debt: it needs `because` and no source, because nobody consulted one. What it may never do is pass for a prediction — that is exactly what the field exists to stop. Then: create_issue for the work, link_work to tie them together, write_docs with `hypothesis` to make the change — `check_in_days` on this call already dated the look-back. get_work_board shows the result moving through its columns. Relay the warnings — a hypothesis with no expected effect or no metric is the half-written kind that cannot be judged later, and those the call says rather than refusing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `key` | string | yes | Short machine handle, e.g. 'quickstart_token_step'. Lowercase and underscores; it is what edit_hypothesis and link_work name this claim by. |
| `text` | string | yes | The claim, stated so it could turn out false and written for the owner — what we will try and what it buys, no tool names, call ids or file paths. One claim per hypothesis — hard limit 600 characters, and a longer one is refused rather than truncated; the reasoning goes in `because` and `expected_effect`. Example: "Readers leave /quick-start at step 3 because it assumes an API token step 1 never mentions — adding the token step cuts the page's dead-end rate from 62% to under 40% within 14 days". |
| `kind` | string | no | Default `forecast`. forecast: Written BEFORE the change, to decide it. Argued from a goal that is not being reached, and sized by something published outside this project. This is the only kind that can be cited later as a prediction. reconstruction: Written about a change that ALREADY shipped, to pay the board's `unmeasured` debt. Honest and useful — but nobody predicted it, so `expected_effect` here is what we NOW think it should have done, and it must never be counted as a forecast. One of: `forecast`, `reconstruction`. |
| `goal_key` | string | no | The goal this argues for. Optional on a forecast: it inherits the direction's goal when `direction_key` is given, and otherwise the standing goal `be_found` (found on Google and in AI answers) that every project has. Name one only to narrow it — `found_in_search` / `cited_by_ai` — or to argue for one of the owner's own (list_goals, or a `goal` line in list_memory). Checked against that list; a name matching nothing is refused with the list of the ones that do. Never ask the owner for a goal. |
| `direction_key` | string | no | The direction this claim was drawn FROM, from list_opportunities. Checked against the directions here; a name matching nothing is refused with the list. Without it the claim argues for a goal without saying what SHARE of that goal it addresses — which is the difference between "it worked" and "it took 2% of what was on the table". |
| `opportunity_key` | string | no | The opportunity inside that direction, from its `opportunities`. Needs `direction_key`: an opportunity key is only unique inside its direction. |
| `because` | string | no | REQUIRED: why this claim exists NOW, for the owner — the opportunity is not won, what we saw, and the cause: 'our card page never uses the words readers search with, so Google does not show it for them'. The `call_id` of the reading goes in `evidence`, not here. |
| `source_url` | string | no | REQUIRED on a forecast: the page OUTSIDE this product that says how this class of problem is solved — an article, a forum thread, a search results page, a competitor's page, a spec. NOT this project's own pull request, commit or issue: that is the change, not its origin, and it is refused. Not `evidence` either; that is the observation on this site. |
| `source_claim` | string | no | REQUIRED on a forecast: the ONE fact the page at `source_url` actually reports — the mechanism it names, or the size and timescale it measured — quoted plainly for the owner. Build `expected_effect` from this number rather than from one you liked. A URL can be pasted without opening it; this field cannot. |
| `evidence` | string | no | The observation on THIS project it rests on: the `call_id` of the reading, the page path, the query. What makes the idea apply HERE. Hard limit 1200 characters — quote the reading, do not transcribe it. |
| `baseline` | string | no | REQUIRED on a forecast: the deciding reading AS IT STANDS NOW, taken with the tool you name in `metric`, before the change — the figure, the tool, the call id and the date. "62% of visits to /quick-start ended as dead ends (get_visit_outcomes /quick-start, call_id 455, 2026-09-13)". Must contain a number: "traffic is low" is an impression, and the reading taken on the check date needs something to be compared with. The one field that becomes unobtainable once the change ships. |
| `expected_effect` | string | no | What the change should BUY, and by when — written NOW, before it, for the owner, with a number in the same unit as `baseline` and its size taken from `source_claim`: 'shown on Google for this search within 30 days, up from absent', 'named in the AI answer for 1 of the 5 questions we watch within 30 days, from 0'. Not 'it should help', and not a tool's output. |
| `metric` | string | no | The reading that decides it: the tool and the subject. 'get_visit_outcomes /quick-start', 'compare_tool_calls against call 8123'. |
| `change` | string | no | What is being done to test it, in prose. The pull request itself is attached with link_work, not named here. |
| `check_in_days` | number | no | Days from now until the reading is due — the preferred form, resolved against this server's clock. 14 is the honest wait for anything read from traffic, rankings or citations. |
| `check_at` | string | no | An absolute instant instead ('2026-10-01'). Only for a date somebody actually named — otherwise use check_in_days, because you do not reliably know today's date. |
| `status` | string | no | Where this stands. DERIVED from what you write — a verdict makes it verified whatever you pass, and retracting one puts it back to testing — so pass it only to say "testing" before a change is linked. untested: Written down, not yet tested — no change has been made against it. The next move is an issue naming the change, then a pull request linked to both, then a `check_at` date for the reading. testing: A change is out and the verdict waits on the date in `check_at`. Do not judge it early: a reading taken before the honest wait measures the week's own variance, not the change. verified: Judged — `verdict` says which way and `result` says what was measured. Read these before proposing the same change again with the same confidence. One of: `untested`, `testing`, `verified`. |
| `result` | string | no | What happened, for the owner: 'now on Google's first page for this search, up from absent' — the pair with its call ids goes in `evidence`. Only when you are recording a hypothesis that has ALREADY been tested. |
| `verdict` | string | no | File it already judged. Only with a `result`; a verdict with nothing behind it cannot be re-checked. One of: `confirmed`, `rejected`. |
| `next_key` | string | no | The hypothesis this one leads to, by key — how a rejection turns into the next attempt instead of a dead end. |

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
    "name": "add_hypothesis",
    "arguments": {
      "key": "<key>",
      "text": "<text>",
      "kind": "forecast",
      "status": "untested",
      "verdict": "confirmed"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"add_hypothesis","arguments":{"key":"<key>","text":"<text>","kind":"forecast","status":"untested","verdict":"confirmed"}}}'
```

<!-- /widget -->
