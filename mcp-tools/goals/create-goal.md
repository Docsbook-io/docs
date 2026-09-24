---
title: "Create goal"
description: "Define a goal — one thing you want a reader to do."
---

# Create goal

<!-- widget:mcp access=write price-millicents=2000 -->

## create_goal

Define a goal — one thing you want a reader to do. Matched RETROACTIVELY against the history already recorded, so the numbers appear immediately rather than starting from today. Refused when it cannot ever fire (an event these docs do not emit) or when the value is 0 — a goal that never fires looks EXACTLY like a goal with 100% drop-off, and $0 reads as a measurement instead of an absent declaration. Warnings come back in `issues` and are worth relaying to the owner verbatim. Set `value_usd` only if you can defend the number; leaving it empty keeps money figures switched off rather than showing an invented one.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `key` | string | yes | Machine name, e.g. 'reached_pricing'. Lowercase and underscores; it is the handle funnels and these tools refer to the goal by. Never put a path, id or email in it. |
| `kind` | string | yes | page = a pageview of a path. event = one of the events the docs emit (see get_analytics event names). section = a heading/anchor came into view — THIS is how a 'scrolled as far as pricing' goal works, and it needs no new tracking. outbound = a click leaving for a host (matched by host, so query strings do not matter). One of: `page`, `event`, `section`, `outbound`. |
| `match` | string | yes | What to match: a path for 'page', an event name for 'event', a heading anchor for 'section' (with or without the '#'), a host for 'outbound'. |
| `match_path` | string | no | Optional scope — only count the goal on this page. Lets one event be two goals ('copied the quickstart snippet' vs 'copied the auth snippet'). |
| `label` | string | no | Human label for the dashboard. Defaults to the key. |
| `value_usd` | number | no | What ONE completion is worth, in dollars. Omit unless defensible. |

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
    "name": "create_goal",
    "arguments": {
      "key": "<key>",
      "kind": "page",
      "match": "<match>"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer YOUR_MCP_OAUTH_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"create_goal","arguments":{"key":"<key>","kind":"page","match":"<match>"}}}'
```

<!-- /widget -->
