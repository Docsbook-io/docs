---
title: "List webhook deliveries"
description: "List delivery attempts for a webhook with status and response code (PRO)."
---

# List webhook deliveries

<!-- widget:api -->

## GET /api/v1/list_webhook_deliveries

List delivery attempts for a webhook with status and response code (PRO).

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/list_webhook_deliveries`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `webhook_id` | integer | yes | — |
| `limit` | integer | no | Max rows (default 50). |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `webhook_id` | number | — |
| `deliveries` | object[] | { id, status, attempts, response_code, response_body, created_at, delivered_at }. |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/list_webhook_deliveries?webhook_id=0' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Response

```json
{
  "ok": true,
  "result": {
    "webhook_id": 0,
    "deliveries": []
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
