---
title: "Test chat hook"
description: "Send a test ping to one of the configured AI chat hooks and return status."
---

# Test chat hook

<!-- widget:api -->

## GET /api/v1/test_chat_hook

Send a test ping to one of the configured AI chat hooks and return status.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/test_chat_hook`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `hook_type` | string | yes | Which hook to test |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `status` | string | "ok" \| "error" \| "not_configured". |
| `hook_type` | string | — |
| `http_status` | number | — |
| `latency_ms` | number | — |
| `url` | string | — |
| `response_preview` | string | — |

### Limitations

- REQUIRES the PRO plan or above.

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/test_chat_hook?hook_type=%3Chook_type%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Response

```json
{
  "ok": true,
  "result": {
    "status": "<status>",
    "hook_type": "<hook_type>",
    "http_status": 0,
    "latency_ms": 0,
    "url": "<url>",
    "response_preview": "<response_preview>"
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
