---
title: "Get issue thread"
description: "Read the comments on one GitHub issue or pull request, in order, with its impact contract and how much of the predicted move has actually happened."
---

# Get issue thread

<!-- widget:mcp access=read price-millicents=800 -->

## get_issue_thread

Read the comments on one GitHub issue or pull request, in order, with its impact contract and how much of the predicted move has actually happened. Call it BEFORE replying to anything on a record — the question may already have been answered, and a reply repeating an existing one is worse than silence. `impact.achieved_percent` is computed by code: quote it, never recompute it.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `number` | integer | yes | The issue or pull request number. |

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
    "name": "get_issue_thread",
    "arguments": {
      "number": 0
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_issue_thread","arguments":{"number":0}}}'
```

<!-- /widget -->
