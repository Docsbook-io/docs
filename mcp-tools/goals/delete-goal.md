---
title: "Delete goal"
description: "Archive a goal by name."
---

# Delete goal

<!-- widget:mcp access=write price-millicents=1 -->

## delete_goal

Archive a goal by name. Archived rather than destroyed, because a funnel step pointing at it would otherwise vanish — and a funnel that silently loses a step reports a BETTER conversion rate than the real one.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `key` | string | yes | The goal's name. |

### Returns

| Field | Type | Description |
|---|---|---|
| `workspace_id` | number | — |
| `archived` | string | The goal's key. |

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "delete_goal",
    "arguments": {
      "key": "<key>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"delete_goal","arguments":{"key":"<key>"}}}'
```

### REST

```bash
curl -X POST 'https://docsbook.io/api/v1/delete_goal' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"key":"<key>"}'
```

### Result

```json
{
  "workspace_id": 0,
  "archived": "<archived>"
}
```

<!-- /widget -->
