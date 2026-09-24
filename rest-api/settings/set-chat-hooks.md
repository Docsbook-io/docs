---
title: "Set chat hooks"
description: "Set pre-, post-, and streaming webhook URLs for the AI chatbot."
---

# Set chat hooks

<!-- widget:api -->

## POST /api/v1/set_chat_hooks

Set pre-, post-, and streaming webhook URLs for the AI chatbot. Pass empty string to clear an individual hook.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/set_chat_hooks`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `pre_url` | string | no | Pre-LLM hook URL — receives {question, session_id, workspace_id}, may return {block, reason} or {inject_context} |
| `post_url` | string | no | Post-LLM hook URL — fire-and-forget POST with {question, answer, tool_calls, latency_ms} |
| `streaming_url` | string | no | Streaming events webhook URL — fire-and-forget SSE-style events |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `status` | string | — |
| `workspace_id` | number | — |
| `ai_chat_pre_hook_url` | string | null | — |
| `ai_chat_post_hook_url` | string | null | — |
| `ai_chat_streaming_webhook_url` | string | null | — |

### Limitations

- REQUIRES the PRO plan or above.

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/set_chat_hooks' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

### Response

```json
{
  "ok": true,
  "result": {
    "status": "<status>",
    "workspace_id": 0,
    "ai_chat_pre_hook_url": "<ai_chat_pre_hook_url>",
    "ai_chat_post_hook_url": "<ai_chat_post_hook_url>",
    "ai_chat_streaming_webhook_url": "<ai_chat_streaming_webhook_url>"
  },
  "duration_ms": 0
}
```

### Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |

<!-- /widget -->
