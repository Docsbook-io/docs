---
title: "Remove hypothesis"
description: "RETIRE a hypothesis that should never have been written."
---

# Remove hypothesis

<!-- widget:mcp access=write price-millicents=2000 -->

## remove_hypothesis

RETIRE a hypothesis that should never have been written. Free on every plan. 🔴 THIS IS NOT HOW ONE GETS FINISHED. A claim you actually tested is closed with edit_hypothesis's `verdict` — including when the verdict is `rejected` because nothing moved. A retired hypothesis and a judged one are indistinguishable to the next run, so retiring what you measured destroys the finding and leaves the project looking like it never tested anything. Use this when the claim was a mistake, or when what it was about is gone: the page was deleted, the feature was cancelled. Archived rather than destroyed, so the key stays taken and writing it again revives the row with its original date.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `key` | string | yes | The hypothesis's handle, from list_hypotheses. |

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
    "name": "remove_hypothesis",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"remove_hypothesis","arguments":{"key":"<key>"}}}'
```

<!-- /widget -->
