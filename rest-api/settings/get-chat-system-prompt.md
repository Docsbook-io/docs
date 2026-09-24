---
title: "Get chat system prompt"
description: "Get the current custom AI chat system prompt for a workspace."
---

# Get chat system prompt

<!-- widget:api -->

## GET /api/v1/get_chat_system_prompt

Get the current custom AI chat system prompt for a workspace.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/get_chat_system_prompt`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `workspace_id` | number | — |
| `ai_chat_system_prompt` | string | null | — |

### Limitations

- REQUIRES PRO or higher.

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/get_chat_system_prompt' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Response

```json
{
  "ok": true,
  "result": {
    "workspace_id": 0,
    "ai_chat_system_prompt": "<ai_chat_system_prompt>"
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
