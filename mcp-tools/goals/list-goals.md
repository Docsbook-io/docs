---
title: "List goals"
description: "The goals and funnels defined for this workspace, with what each one MATCHES."
---

# List goals

<!-- widget:mcp access=read price-millicents=3 -->

## list_goals

The goals and funnels defined for this workspace, with what each one MATCHES. A goal is a named thing you want a reader to do; a funnel is an ordered list of goals. Free on every plan: defining measurement is not the paid part. Every project has the standing goal — be found, on Google and in AI answers (`standing_goal` here, `be_found` as a `goal_key`) — without declaring anything; these are the owner's EXTRAS, reader actions on the site.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |

### Returns

| Field | Type | Description |
|---|---|---|
| `workspace_id` | number | — |
| `goals` | object[] | — |
| `funnels` | object[] | — |
| `max_funnel_steps` | number | — |

### Use cases

- Call this before creating anything — a goal whose name already exists is refused, and a funnel step refers to a goal by name.

### Limitations

- 🔴 AN EMPTY LIST IS NOT A MISSING GOAL.
- Never ask the owner to declare a goal, and never create a page-view goal to stand in for being found: decompose the standing goal instead (list_opportunities, add_direction).

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "list_goals",
    "arguments": {}
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer YOUR_MCP_OAUTH_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_goals","arguments":{}}}'
```

### REST

```bash
curl 'https://docsbook.io/api/v1/list_goals' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Result

```json
{
  "workspace_id": 0,
  "goals": [],
  "funnels": [],
  "max_funnel_steps": 0
}
```

<!-- /widget -->
