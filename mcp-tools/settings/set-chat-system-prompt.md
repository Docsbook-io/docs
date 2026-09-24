---
title: "Set chat system prompt"
description: "Set a custom system prompt for the AI chatbot."
---

# Set chat system prompt

<!-- widget:mcp access=write price-millicents=1 -->

## set_chat_system_prompt

Set a custom system prompt for the AI chatbot. Injected with high priority after the default system prompt. REQUIRES PRO or higher.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `system_prompt` | string | yes | Custom system prompt text. Pass empty string to clear. |

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "set_chat_system_prompt",
    "arguments": {
      "workspace_id": "<workspace_id>",
      "system_prompt": "<system_prompt>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"set_chat_system_prompt","arguments":{"workspace_id":"<workspace_id>","system_prompt":"<system_prompt>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### POST /api/v1/set_chat_system_prompt

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `system_prompt` | string | yes | Custom system prompt text. Pass empty string to clear. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/set_chat_system_prompt' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"workspace_id":"<workspace_id>","system_prompt":"<system_prompt>"}'
```

<!-- /widget -->
