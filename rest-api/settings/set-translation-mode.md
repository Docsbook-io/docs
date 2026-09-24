---
title: "Set translation mode"
description: "Set the translation workflow mode for a workspace: 'auto' (Docsbook AI), 'manual' (drafts via API), or 'external' (forward to webhook)."
---

# Set translation mode

<!-- widget:api -->

## POST /api/v1/set_translation_mode

Set the translation workflow mode for a workspace: 'auto' (Docsbook AI), 'manual' (drafts via API), or 'external' (forward to webhook).

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/set_translation_mode`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `mode` | string | no | Translation workflow mode One of: `auto`, `manual`, `external`. |
| `external_webhook_url` | string | no | Webhook URL (required for 'external' mode, empty string clears) |

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
| `translation_mode` | string | — |
| `external_translation_webhook_url` | string | null | — |

### Limitations

- REQUIRES PRO or higher.

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/set_translation_mode' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"mode":"auto"}'
```

### Response

```json
{
  "ok": true,
  "result": {
    "status": "<status>",
    "workspace_id": 0,
    "translation_mode": "<translation_mode>",
    "external_translation_webhook_url": "<external_translation_webhook_url>"
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
