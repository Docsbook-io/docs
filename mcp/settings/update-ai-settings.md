---
title: "Update ai settings"
description: "Configure the AI chatbot."
---

# Update ai settings

<!-- widget:mcp access=write price-millicents=2000 -->

## update_ai_settings

Configure the AI chatbot. REQUIRES PRO plan. Returns upgrade info for FREE workspaces.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `ai_enabled` | boolean | no | Enable or disable the AI chatbot |
| `ai_provider` | string | no | One of: `openrouter`, `openai`, `gemini`, `anthropic`. |
| `ai_api_key` | string | no | API key for the AI provider |
| `custom_questions` | string[] | no | Suggested questions in the AI chat |

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
    "name": "update_ai_settings",
    "arguments": {
      "workspace_id": "<workspace_id>",
      "ai_provider": "openrouter"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"update_ai_settings","arguments":{"workspace_id":"<workspace_id>","ai_provider":"openrouter"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### POST /api/v1/update_ai_settings

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `ai_enabled` | boolean | no | Enable or disable the AI chatbot |
| `ai_provider` | string | no | One of: `openrouter`, `openai`, `gemini`, `anthropic`. |
| `ai_api_key` | string | no | API key for the AI provider |
| `custom_questions` | string[] | no | Suggested questions in the AI chat |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/update_ai_settings' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"workspace_id":"<workspace_id>","ai_provider":"openrouter"}'
```

<!-- /widget -->
