---
title: "Remove memory"
description: "RETIRE a line this project remembers."
---

# Remove memory

<!-- widget:mcp access=write price-millicents=2000 -->

## remove_memory

RETIRE a line this project remembers. Free on every plan. Archived rather than destroyed, like a goal and for the same reason: a rule that simply vanished is indistinguishable from one that was never written, and the next run re-derives it. Retire a line when it stopped being TRUE or stopped deciding anything — not because it is inconvenient for what you are about to recommend.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `key` | string | yes | The line's handle, from list_memory. |

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
    "name": "remove_memory",
    "arguments": {
      "key": "<key>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"remove_memory","arguments":{"key":"<key>"}}}'
```

<!-- /widget -->
