---
title: "List inbox messages"
description: "WHAT THIS PROJECT'S OWNER AND AGENT HAVE WRITTEN TO EACH OTHER."
---

# List inbox messages

<!-- widget:mcp access=read price-millicents=800 -->

## list_inbox_messages

WHAT THIS PROJECT'S OWNER AND AGENT HAVE WRITTEN TO EACH OTHER. Free on every plan. 🔴 CALL THIS BEFORE send_inbox_message ASKS THE SAME THING TWICE. Every letter carries `thread` — the turns under it, oldest first, each one `owner` or `agent` — which is where the owner's answer to your question actually is. `status: "unanswered"` (the default) is your own questions nobody has written back to; `status: "answered"` is what came back, so you can act on it; `status: "all"` includes reports and the letters the OWNER started, newest first. ⚡ A letter the owner wrote (`origin: "owner"`) is them asking YOU for something — read those first when you are deciding what to do next.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `status` | string | no | Default `unanswered` — your own question letters the owner has not written back to yet. One of: `unanswered`, `answered`, `all`. |
| `limit` | integer | no | Max rows (default 50), newest first. |

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
    "name": "list_inbox_messages",
    "arguments": {
      "status": "unanswered"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_inbox_messages","arguments":{"status":"unanswered"}}}'
```

<!-- /widget -->
