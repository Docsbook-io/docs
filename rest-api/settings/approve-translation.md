---
title: "Approve translation"
description: "Approve a draft translation, moving it to status 'published'."
---

# Approve translation

<!-- widget:api -->

## POST /api/v1/approve_translation

Approve a draft translation, moving it to status 'published'.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/approve_translation`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `translation_id` | number | no | Translation row ID |

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
| `translation` | object | — |

### Limitations

- REQUIRES PRO or higher.

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/approve_translation' \
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
    "translation": {}
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
