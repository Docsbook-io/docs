---
title: "Configure source"
description: "Change or disconnect one of this project's connected sources (see `list_sources`): rename it, rewrite the `note` every tool reads as instruction, pause it, or remove it."
---

# Configure source

<!-- widget:api -->

## POST /api/v1/configure_source

Change or disconnect one of this project's connected sources (see `list_sources`): rename it, rewrite the `note` every tool reads as instruction, pause it, or remove it. Pausing (`enabled: false`) keeps the row and stops every tool and agent from reading it — the move for a repository that has moved or a site that is being rebuilt. `disconnect: true` deletes it, along with any GitHub authorisation attached to it. Identify the source by `source_id` from list_sources, or by `match` (a word from its label or URL).

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/configure_source`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `source_id` | number | no | The source's id from list_sources. |
| `match` | string | no | Part of its label or URL, when you do not have the id (e.g. 'acme/api'). |
| `note` | string | no | Replace what this source is for. Read as instruction by everything that reads the source. |
| `label` | string | no | Rename it in the list. |
| `enabled` | boolean | no | false pauses the source: it stays connected and nothing reads it. |
| `disconnect` | boolean | no | true removes the source entirely, with any GitHub authorisation attached to it. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `source` | object | { id, kind, label, url, note, status, is_private, has_authorization } — absent when `disconnect: true` was passed. |
| `disconnected` | object | { id, label, url } — present only on disconnect. |
| `note` | string | — |

### Limitations

- REQUIRES a read-write MCP token.

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/configure_source' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

### Response

```json
{
  "ok": true,
  "result": {
    "source": {},
    "disconnected": {},
    "note": "<note>"
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
