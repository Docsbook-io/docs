---
title: "Get work board"
description: "HOW THE WORK ON THIS PROJECT IS GOING — every issue and pull request in the column its state earns, with what each one is linked to and whether it turned out to be worth doing."
---

# Get work board

<!-- widget:mcp access=read price-millicents=6000 -->

## get_work_board

HOW THE WORK ON THIS PROJECT IS GOING — every issue and pull request in the column its state earns, with what each one is linked to and whether it turned out to be worth doing. Free on every plan. 🔴 CALL THIS FIRST IN ANY SESSION THAT IS GOING TO CHANGE SOMETHING. It answers the three questions that decide what you may do: what is already in flight (never open a second pull request for an issue whose first is still open), what is waiting on the OWNER rather than on you, and what merged without anybody being able to say whether it worked. Four columns: `planned` (an issue with no pull request yet), `in_review` (a pull request is open — it merges itself under auto-merge, or waits for the owner under human review), `measuring` (merged, and the reading that judges it is not in yet), `done` (judged, or closed). 🔴 READ `outcome` ON EVERY DONE CARD. `unmeasured` means a change shipped with no hypothesis attached, so nothing can say what it did — that is the debt this board exists to make visible, and paying it (add_hypothesis, link_work) outranks starting anything new. `confirmed` and `rejected` are real answers; `pending` means the wait is still on. `review_mode` says what happens to the NEXT change you write: `auto` merges it in the same call, `manual` opens it and stops. Either way a pull request is always opened — the mode decides only whether it lands. The owner sets it on their panel; do not work around it. `loose_hypotheses` are claims nothing on the board tests, and `gap` names the one thing to do about the board itself.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `limit` | number | no | How many issues and pull requests to read from GitHub, 1-100. Default 50 of each. |

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
    "name": "get_work_board",
    "arguments": {}
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_work_board","arguments":{}}}'
```

<!-- /widget -->
