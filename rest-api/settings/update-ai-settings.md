---
title: "Update ai settings"
description: "Configure the AI chatbot."
---

# Update ai settings

<!-- widget:api -->

## POST /api/v1/update_ai_settings

Configure the AI chatbot. REQUIRES PRO plan. Returns upgrade info for FREE workspaces.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/update_ai_settings`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `ai_enabled` | boolean | no | Enable or disable the AI chatbot |
| `ai_provider` | string | no | One of: `openrouter`, `openai`, `gemini`, `anthropic`, `vercel-ai-gateway`. |
| `ai_api_key` | string | no | API key for the AI provider |
| `custom_questions` | string[] | no | Suggested questions in the AI chat |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/update_ai_settings' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"ai_provider":"openrouter"}'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
