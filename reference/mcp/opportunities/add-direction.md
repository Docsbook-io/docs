---
title: "Add direction"
description: "OPEN A DIRECTION: decompose the standing goal — be found, on Google and in AI answers — for ONE audience of this product."
---

# Add direction

<!-- widget:mcp access=write price-millicents=2000 -->

## add_direction

OPEN A DIRECTION: decompose the standing goal — be found, on Google and in AI answers — for ONE audience of this product. Name who they are and what they look for, and say what reaching them would look like. Free on every plan. 🔴 THIS IS THE STEP THAT MAKES A CHANGE ARGUE FOR A SHARE OF SOMETHING. Without it a hypothesis argues for a goal and cannot say how much of that goal is at stake, so `confirmed` on a change addressing 2% of the audience reads exactly like `confirmed` on one addressing all of it. The sentence this exists to make sayable: *the hypothesis was confirmed and the direction is still not reached*. 🔴 WRITTEN FOR THE OWNER. `title`, `question`, `target` and `result` are printed on their screen and are REFUSED when they read as a technical note — a call id, a tool name, a file path, a metric dump. Say it as their customer would: "Organisers looking for hackathon judging tools — show up on Google and in its AI answer for their searches by November". The trace goes in `scope`, `method`, `baseline` and `target_metric`, which the owner never reads and which you MUST fill: a direction with no `target_metric` cannot come out SHORT, and coming out short is the finding. `goal_key` is optional: the standing goal `be_found` applies unless the owner declared their own (list_goals, or a `goal` line in list_memory). Do not ask the owner for a goal and do not create one to make this call work. Then add_opportunity, once per search or question: what they type, how many do (read_keyword_demand / read_search_trends / read_search_suggestions / read_serp_snapshot), where we stand, who wins it today (crawl_competitor_docs, collect_ai_citability). Then configure_mentions with the top intents, so the direction is measured by whether the docs actually show up. Then draw hypotheses FROM the opportunities: add_hypothesis with `direction_key` and `opportunity_key`. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `key` | string | yes | Short machine handle, e.g. 'hackathon_organisers'. Lowercase and underscores; opportunities and hypotheses name the direction by it. |
| `title` | string | yes | Who this audience is and what they look for, in plain words: 'Organisers evaluating AI-assisted hackathon judging', 'People paying for foreign subscriptions with a card'. Printed on the owner's screen; refused when it reads as a technical note. |
| `goal_key` | string | no | Optional. The goal this direction serves: the standing goal `be_found` by default; its branches `found_in_search` / `cited_by_ai` when it is only one of the two; or one of the owner's own from list_goals / a `goal` line in list_memory. Checked against that list. |
| `question` | string | no | The business question it answers, in one plain sentence: 'Which of the searches organisers make can these docs realistically win?' |
| `target` | string | no | REQUIRED for an agent, and written for the owner: what reaching this direction looks like, and by when — 'show up on Google and in its AI answer for these searches by November', 'be named in AI answers for 3 of the 5 questions we watch within 60 days'. Refused when technical. |
| `target_metric` | string | no | REQUIRED for an agent: the reading that judges THE DIRECTION, not any one change — the tool and the subject, the same one the baseline was taken with. Technical, not shown to the owner: 'get_mentions (google, ai_overview) on the 5 watched queries'. |
| `scope` | string | no | Technical, not shown to the owner: what was examined — which site, which competitors, which locale and market, over which dates. The half that makes the re-run comparable. |
| `method` | string | no | Technical, not shown to the owner: which readings built it, with their `call_id`s and the date. A direction nobody can reproduce is one nobody can disagree with. |
| `baseline` | string | no | Technical, not shown to the owner: where the goal stands TODAY, with the call id — '0 of 5 watched queries mention us (get_mentions, call_id 571)'. Take it now; it cannot be taken retroactively. |
| `target_value_cents` | number | no | What reaching the target is worth, in cents. Omit when nothing is priced — an invented figure here is worse than an empty column, because everything under it inherits the invention. |
| `review_in_days` | number | no | Days until the target reading is due. 30 is the honest wait for search to answer. |
| `review_at` | string | no | An absolute date instead ('2026-11-01'). Only for a date somebody named — otherwise use review_in_days. |

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
    "name": "add_direction",
    "arguments": {
      "key": "<key>",
      "title": "<title>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"add_direction","arguments":{"key":"<key>","title":"<title>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/add_direction

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/add_direction' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"key":"<key>","title":"<title>"}}'
```

<!-- /widget -->
