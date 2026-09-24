---
title: "List pending translations"
description: "List draft translations awaiting approval for a workspace."
---

# List pending translations

<!-- widget:mcp access=read price-millicents=800 -->

## list_pending_translations

List draft translations awaiting approval for a workspace. REQUIRES PRO or higher.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |

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
    "name": "list_pending_translations",
    "arguments": {
      "workspace_id": "<workspace_id>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_pending_translations","arguments":{"workspace_id":"<workspace_id>"}}}'
```

<!-- /widget -->
