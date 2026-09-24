---
title: "Get translation status"
description: "How each enabled language stands against the source RIGHT NOW: pages current / behind / missing / manual, the percentage, whether a run is in flight and how far along, and what…"
---

# Get translation status

<!-- widget:api -->

## GET /api/v1/get_translation_status

How each enabled language stands against the source RIGHT NOW: pages current / behind / missing / manual, the percentage, whether a run is in flight and how far along, and what the last run did — including which agent run started it. Coverage is null (never 0) when the source repository could not be read.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/get_translation_status`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `languages` | string[] | no | ISO codes to report on (default: every language switched on for this project) |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `…` | … | Per enabled language: pages current / behind / missing / manual, percentage, whether a run is in flight, and what the last run did. |

### Use cases

- Call this BEFORE run_translation_pass: a language already level with the source costs money to re-translate and changes nothing.

### Limitations

- REQUIRES PRO or higher.

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/get_translation_status' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Response

```json
{
  "ok": true,
  "result": {
    "…": "<…>"
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
