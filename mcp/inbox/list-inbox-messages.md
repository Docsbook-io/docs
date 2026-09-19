---
title: "List inbox messages"
description: "WHAT THIS PROJECT'S AGENT HAS WRITTEN TO THE OWNER, AND WHETHER A QUESTION WAS ANSWERED."
---

# List inbox messages

<!-- widget:mcp access=read price-millicents=800 -->

## list_inbox_messages

WHAT THIS PROJECT'S AGENT HAS WRITTEN TO THE OWNER, AND WHETHER A QUESTION WAS ANSWERED. Free on every plan. 🔴 CALL THIS BEFORE send_inbox_message ASKS THE SAME THING TWICE. `status: "unanswered"` (the default) is your own open questions; each carries `questions[].answer` — `null` until the owner types one, their own words afterwards, and `answered` true once every box on the letter is filled. `status: "answered"` is what came back, so you can act on it. `status: "all"` includes reports too, newest first.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `status` | string | no | Default `unanswered` — question letters with at least one empty answer box. One of: `unanswered`, `answered`, `all`. |
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
