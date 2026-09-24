---
title: "Test chat hook"
description: "Send a test ping to one of the configured AI chat hooks and return status."
---

# Test chat hook

<!-- widget:mcp access=read price-millicents=3 -->

## test_chat_hook

Send a test ping to one of the configured AI chat hooks and return status.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `hook_type` | string | yes | Which hook to test One of: `pre`, `post`, `streaming`. |

### Returns

| Field | Type | Description |
|---|---|---|
| `status` | string | "ok" \| "error" \| "not_configured". |
| `hook_type` | string | — |
| `http_status` | number | — |
| `latency_ms` | number | — |
| `url` | string | — |
| `response_preview` | string | — |

### Limitations

- REQUIRES the PRO plan or above.

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "test_chat_hook",
    "arguments": {
      "workspace_id": "<workspace_id>",
      "hook_type": "pre"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"test_chat_hook","arguments":{"workspace_id":"<workspace_id>","hook_type":"pre"}}}'
```

### REST

```bash
curl 'https://docsbook.io/api/v1/test_chat_hook?workspace_id=%3Cworkspace_id%3E&hook_type=pre' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Result

```json
{
  "status": "<status>",
  "hook_type": "<hook_type>",
  "http_status": 0,
  "latency_ms": 0,
  "url": "<url>",
  "response_preview": "<response_preview>"
}
```

<!-- /widget -->
