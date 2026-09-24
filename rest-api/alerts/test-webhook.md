---
title: "Test webhook"
description: "Send a test ping to a registered webhook and run the delivery worker immediately (Free)."
---

# Test webhook

<!-- widget:api -->

## GET /api/v1/test_webhook

Send a test ping to a registered webhook and run the delivery worker immediately (Free).

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/test_webhook`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `webhook_id` | integer | yes | Webhook id to test. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | — |
| `delivery_id` | number | — |
| `worker_result` | object | — |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/test_webhook?webhook_id=0' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Response

```json
{
  "ok": true,
  "result": {
    "ok": true,
    "delivery_id": 0,
    "worker_result": {}
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
