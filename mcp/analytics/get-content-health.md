---
title: "Get content health"
description: "Per-page health score 0-100 (PRO), combining dead-end exits and negative feedback so the owner of a large doc set does not have to cross-reference several reports by hand."
---

# Get content health

<!-- widget:mcp access=read price-millicents=4000 -->

## get_content_health

Per-page health score 0-100 (PRO), combining dead-end exits and negative feedback so the owner of a large doc set does not have to cross-reference several reports by hand. Lower score = fix sooner. Pages people leave from after succeeding are exempt from the penalty.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `period` | string | no | Time range (default: 7d) |
| `limit` | integer | no | Max rows (default 100-200) |

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
    "name": "get_content_health",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_content_health","arguments":{}}}'
```

<!-- /widget -->
