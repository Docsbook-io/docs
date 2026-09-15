---
title: "Set chat hooks"
description: "Set pre-, post-, and streaming webhook URLs for the AI chatbot."
---

# Set chat hooks

<!-- widget:mcp access=write -->

## set_chat_hooks

Set pre-, post-, and streaming webhook URLs for the AI chatbot. REQUIRES the PRO plan or above. Pass empty string to clear an individual hook. BEFORE CHANGING THIS, call `docsbook_expert` with what you are trying to achieve: it names the reading that should decide the value, so the setting is a conclusion rather than a guess. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `pre_url` | string | no | Pre-LLM hook URL — receives {question, session_id, workspace_id}, may return {block, reason} or {inject_context} |
| `post_url` | string | no | Post-LLM hook URL — fire-and-forget POST with {question, answer, tool_calls, latency_ms} |
| `streaming_url` | string | no | Streaming events webhook URL — fire-and-forget SSE-style events |

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
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"set_chat_hooks","arguments":{"workspace_id":"<workspace_id>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/set_chat_hooks

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/set_chat_hooks' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"workspace_id":"<workspace_id>"}}'
```

<!-- /widget -->
