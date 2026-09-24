---
title: "Create funnel"
description: "Define an ORDERED route through the docs, as a list of goal names."
---

# Create funnel

<!-- widget:api -->

## POST /api/v1/create_funnel

Define an ORDERED route through the docs, as a list of goal names. Order is the whole point: a visit counts as reaching step N only if it hit steps 1..N in sequence, so a reader who lands on step 3 first is not counted. Two rules the validator enforces and you should follow when proposing one: start BROAD (most docs readers arrive deep from search or an AI answer, and a narrow step 1 excludes the majority of traffic before measuring anything), and end on a REAL OUTCOME (a funnel ending on a scroll measures attention, not results). `window_hours` bounds how long after step 1 a later step still counts; omit it to use the visit itself, which is the honest default for docs.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/create_funnel`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `key` | string | no | Machine name, e.g. 'evaluation'. |
| `steps` | string[] | no | Goal names, in order. Between 2 and 8. Create the goals first with create_goal. |
| `label` | string | no | Human label. Defaults to the key. |
| `window_hours` | number | no | Conversion window in hours. Clamped to what the plan retains — a window longer than your history can never complete. |

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
| `funnel` | object | — |
| `issues` | object[] | — |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/create_funnel' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

### Response

```json
{
  "ok": true,
  "result": {
    "workspace_id": 0,
    "funnel": {},
    "issues": []
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
