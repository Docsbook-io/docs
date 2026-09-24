---
title: "Get chat system prompt"
description: "Get the current custom AI chat system prompt for a workspace."
---

# Get chat system prompt

<!-- widget:api -->

## GET /api/v1/get_chat_system_prompt

Get the current custom AI chat system prompt for a workspace. REQUIRES PRO or higher.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/get_chat_system_prompt`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/get_chat_system_prompt' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
