---
title: "Get tool call"
description: "ONE recorded call, whole: the exact arguments it was given and the exact answer it returned."
---

# Get tool call

<!-- widget:mcp access=read price-millicents=800 -->

## get_tool_call

ONE recorded call, whole: the exact arguments it was given and the exact answer it returned. Free on every plan. Use it when a series row or a search hit is worth reading rather than counting — what a reading actually SAID is the thing a later comparison is about. Long arguments and long answers are stored truncated (the marker says how much was dropped), and anything keyed like a secret was redacted before it was ever written, so a key cannot be read back out of here.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `call_id` | integer | yes | The `call_id` from list_tool_calls or search_tool_calls. |

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
    "name": "get_tool_call",
    "arguments": {
      "call_id": 0
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_tool_call","arguments":{"call_id":0}}}'
```

<!-- /widget -->
