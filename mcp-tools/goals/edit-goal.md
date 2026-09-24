---
title: "Edit goal"
description: "CORRECT a goal that already exists — its label, what one completion is worth, or what it matches — without breaking it."
---

# Edit goal

<!-- widget:mcp access=write price-millicents=1 -->

## edit_goal

CORRECT a goal that already exists — its label, what one completion is worth, or what it matches — without breaking it. A funnel step refers to a goal BY KEY, so archiving the goal breaks every funnel naming it, and a funnel that loses a step reports a BETTER conversion rate than the real one. And `created_at` is when this project started measuring the thing: a re-create resets it, so four months of history reads as a goal created today. A different name is a different goal. Pass only what changes. Warnings come back in `issues` and are worth relaying verbatim.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `key` | string | yes | The goal's name, from list_goals. Not editable — see the description. |
| `kind` | string | no | page = a pageview of a path. event = one of the events the docs emit (see get_analytics event names). section = a heading/anchor came into view — THIS is how a 'scrolled as far as pricing' goal works, and it needs no new tracking. outbound = a click leaving for a host (matched by host, so query strings do not matter). One of: `page`, `event`, `section`, `outbound`. |
| `match` | string | no | New matcher: a path for 'page', an event name for 'event', an anchor for 'section', a host for 'outbound'. |
| `match_path` | string | no | New scope. Pass an empty string to clear it and count the goal everywhere. |
| `label` | string | no | New human label. |
| `value_usd` | number | no | What ONE completion is worth, in dollars. Pass 0 to clear it — which switches money figures OFF for this goal rather than reporting it as worthless. |

### Returns

| Field | Type | Description |
|---|---|---|
| `workspace_id` | number | — |
| `goal` | object | — |
| `issues` | object[] | — |

### Limitations

- 🔴 Not the same as deleting it and creating it again, which was the only route until 2026-09-12 and silently cost two things every time.
- The KEY cannot be changed here, deliberately — funnels, MCP callers and the owner's own notes all point at it, and a rename leaves all of them pointing at nothing.

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "edit_goal",
    "arguments": {
      "key": "<key>",
      "kind": "page"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"edit_goal","arguments":{"key":"<key>","kind":"page"}}}'
```

### REST

```bash
curl -X POST 'https://docsbook.io/api/v1/edit_goal' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"key":"<key>","kind":"page"}'
```

### Result

```json
{
  "workspace_id": 0,
  "goal": {},
  "issues": []
}
```

<!-- /widget -->
