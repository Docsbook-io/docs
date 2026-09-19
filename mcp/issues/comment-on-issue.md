---
title: "Comment on issue"
description: "Reply on a GitHub issue or pull request — the conversation ON the record, where the question was asked."
---

# Comment on issue

<!-- widget:mcp access=read price-millicents=800 -->

## comment_on_issue

Reply on a GitHub issue or pull request — the conversation ON the record, where the question was asked. Use it when you finish work a record asked for (say what you did, with the numbers), when you were handed a comment to answer, and when you disagree with something written there. A reply that exists only in your answer is read once and lost; the thread stays unanswered.
Say the thing. Do not restate the record back at the reader, and do not promise to do something later — either do it now and report it, or say why it cannot be done. REQUIRES a read-write MCP token.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `number` | integer | yes | The issue or pull request number. |
| `body` | string | yes | Markdown. What you are actually saying — evidence and figures, not a summary. |

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
    "name": "comment_on_issue",
    "arguments": {
      "number": 0,
      "body": "<body>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"comment_on_issue","arguments":{"number":0,"body":"<body>"}}}'
```

<!-- /widget -->
