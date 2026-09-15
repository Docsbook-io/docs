---
title: "Set chat system prompt"
description: "Set a custom system prompt for the AI chatbot."
---

# Set chat system prompt

<!-- widget:mcp access=write -->

## set_chat_system_prompt

Set a custom system prompt for the AI chatbot. Injected with high priority after the default system prompt. REQUIRES PRO or higher. BEFORE CHANGING THIS, call `docsbook_expert` with what you are trying to achieve: it names the reading that should decide the value, so the setting is a conclusion rather than a guess. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `system_prompt` | string | yes | Custom system prompt text. Pass empty string to clear. |

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
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"set_chat_system_prompt","arguments":{"workspace_id":"<workspace_id>","system_prompt":"<system_prompt>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/set_chat_system_prompt

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/set_chat_system_prompt' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"workspace_id":"<workspace_id>","system_prompt":"<system_prompt>"}}'
```

<!-- /widget -->
