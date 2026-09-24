---
title: "Set chat hooks"
description: "Set pre-, post-, and streaming webhook URLs for the AI chatbot."
---

# Set chat hooks

<!-- widget:api -->

## POST /api/v1/set_chat_hooks

Set pre-, post-, and streaming webhook URLs for the AI chatbot. REQUIRES the PRO plan or above. Pass empty string to clear an individual hook.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/set_chat_hooks`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `pre_url` | string | no | Pre-LLM hook URL — receives {question, session_id, workspace_id}, may return {block, reason} or {inject_context} |
| `post_url` | string | no | Post-LLM hook URL — fire-and-forget POST with {question, answer, tool_calls, latency_ms} |
| `streaming_url` | string | no | Streaming events webhook URL — fire-and-forget SSE-style events |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/set_chat_hooks' \
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
