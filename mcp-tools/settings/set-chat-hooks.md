---
title: "Set chat hooks"
description: "Set pre-, post-, and streaming webhook URLs for the AI chatbot."
---

# Set chat hooks

<!-- widget:mcp access=write price-millicents=1 -->

## set_chat_hooks

Set pre-, post-, and streaming webhook URLs for the AI chatbot. Pass empty string to clear an individual hook.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `pre_url` | string | no | Pre-LLM hook URL — receives {question, session_id, workspace_id}, may return {block, reason} or {inject_context} |
| `post_url` | string | no | Post-LLM hook URL — fire-and-forget POST with {question, answer, tool_calls, latency_ms} |
| `streaming_url` | string | no | Streaming events webhook URL — fire-and-forget SSE-style events |

### Returns

| Field | Type | Description |
|---|---|---|
| `status` | string | — |
| `workspace_id` | number | — |
| `ai_chat_pre_hook_url` | string | null | — |
| `ai_chat_post_hook_url` | string | null | — |
| `ai_chat_streaming_webhook_url` | string | null | — |

### Limitations

- REQUIRES the PRO plan or above.

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "set_chat_hooks",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"set_chat_hooks","arguments":{"workspace_id":"<workspace_id>"}}}'
```

### REST

```bash
curl -X POST 'https://docsbook.io/api/v1/set_chat_hooks' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"workspace_id":"<workspace_id>"}'
```

### Result

```json
{
  "status": "<status>",
  "workspace_id": 0,
  "ai_chat_pre_hook_url": "<ai_chat_pre_hook_url>",
  "ai_chat_post_hook_url": "<ai_chat_post_hook_url>",
  "ai_chat_streaming_webhook_url": "<ai_chat_streaming_webhook_url>"
}
```

<!-- /widget -->
