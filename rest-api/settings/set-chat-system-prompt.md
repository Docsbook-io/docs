---
title: "Set chat system prompt"
description: "Set a custom system prompt for the AI chatbot."
---

# Set chat system prompt

<!-- widget:api -->

## POST /api/v1/set_chat_system_prompt

Set a custom system prompt for the AI chatbot. Injected with high priority after the default system prompt. REQUIRES PRO or higher.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/set_chat_system_prompt`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `system_prompt` | string | no | Custom system prompt text. Pass empty string to clear. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/set_chat_system_prompt' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
