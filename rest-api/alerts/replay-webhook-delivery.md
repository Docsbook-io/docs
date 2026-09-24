---
title: "Replay webhook delivery"
description: "Replay a webhook delivery by creating a new pending row with the same payload and running the worker (PRO)."
---

# Replay webhook delivery

<!-- widget:api -->

## POST /api/v1/replay_webhook_delivery

Replay a webhook delivery by creating a new pending row with the same payload and running the worker (PRO).

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/replay_webhook_delivery`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `delivery_id` | integer | no | — |

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
| `original_delivery_id` | number | — |
| `new_delivery_id` | number | — |
| `worker_result` | object | — |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/replay_webhook_delivery' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

### Response

```json
{
  "ok": true,
  "result": {
    "ok": true,
    "original_delivery_id": 0,
    "new_delivery_id": 0,
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
