---
title: "List opportunities"
description: "WHAT THERE IS TO WIN HERE, AND HOW MUCH OF IT IS WON — the standing goal (be found, on Google and in AI answers) decomposed for this project into DIRECTIONS, each an audience and…"
---

# List opportunities

<!-- widget:mcp access=read price-millicents=800 -->

## list_opportunities

WHAT THERE IS TO WIN HERE, AND HOW MUCH OF IT IS WON — the standing goal (be found, on Google and in AI answers) decomposed for this project into DIRECTIONS, each an audience and the searches it makes with a target, and under each the OPPORTUNITIES: one search or question, how many people make it, where we stand, who wins it today, what winning is worth. Free on every plan. 🔴 READ THIS BEFORE WRITING A HYPOTHESIS. A claim drawn from an opportunity can say what SHARE of the goal it addresses; a claim drawn from the hour's reading cannot, however well it turns out — and every reading finds something wrong, so a project working from readings alone produces an endless supply of true, small, unrankable ideas. The opportunities are that ranking, with a number and a source on each row. 🔴 NO DIRECTION AT ALL IS THE FINDING, and on a new project it will be — the standing goal has not been decomposed yet. Build one this hour: add_direction for the audience, add_opportunity per search or question, configure_mentions so the searches are watched. Each direction carries `goal_key` and `goal_label` (the standing goal unless the owner named their own), `title`, `question`, `target` (what reaching it looks like, in the owner's words), `status`, `review_at`, `progress` (how many opportunities, the audience behind them, how much is being worked, how much is won) and its `opportunities`. `scope`, `method`, `baseline` and `target_metric` are the trace — yours, not the owner's. Each opportunity: What people look for (`intent`): The search or the question, in the words they actually use. How many (`demand`): How many people look for it, and how often — with where that figure came from. Where we stand (`current`): What these docs show that person today: nothing, the wrong page, a page nobody can quote. Who wins it today (`competitor`): Who the search or the assistant sends them to instead — and what gives them the slot. The move (`action`): What we would do about it, from a short list of things a documentation site can actually do. What it is worth (`potential`): What winning it buys: the people it brings in, the price comparison it wins, the support question it retires. Status (`state`): To win, planned, in progress, won, didn't work, or passed — derived from the changes made against it. Plus `state`/`state_label`, the hypotheses pointed at it, and `evidence` — the call ids and URLs behind it. 🔴 `demand_unknown` IS NOT ZERO DEMAND. It counts the rows nobody could measure, and the totals beside it exclude those rows — so a `demand_total` sitting next to a large `demand_unknown` is a floor, not a figure. `gap` names the one thing to do about this store.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `status` | string | no | Which directions. Default `all`. One of: `all`, `open`, `reached`, `abandoned`. |
| `include_opportunities` | boolean | no | Include every opportunity on every direction. Default true — the opportunities ARE the direction; without them this is a list of intentions. |

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
    "name": "list_opportunities",
    "arguments": {
      "status": "all"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_opportunities","arguments":{"status":"all"}}}'
```

<!-- /widget -->
