---
title: "Configure mentions"
description: "Choose what the mention checks watch on one engine: turn the daily check on or off, and set the queries (up to 5) — the exact words a reader would type or ask."
---

# Configure mentions

<!-- widget:api -->

## POST /api/v1/configure_mentions

Use get_mentions to read what the checks found.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/configure_mentions`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `surface` | string | no | Which engine this arms: ai_overview (Google's AI answer), google or bing (the results page). One of: `ai_overview`, `google`, `bing`. |
| `enabled` | boolean | no | Whether the daily check runs. Queries are kept either way. |
| `queries` | string[] | no | The queries to check, up to 5. Replaces the saved list. |
| `cron_expression` | string | no | 5-field UTC cron for the check. Defaults to a daily early-morning slot. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `surface` | string | ai_overview \| google \| bing. |
| `enabled` | boolean | — |
| `queries` | string[] | As STORED — trimmed, de-duplicated and capped at 5. |
| `cronExpression` | string | null | — |
| `lastRunAt` | string | null | — |
| `lastStatus` | string | null | — |
| `lastDetail` | string | null | — |
| `note` | string | — |

### Limitations

- Choose what the mention checks watch on one engine: turn the daily check on or off, and set the queries (up to 5) — the exact words a reader would type or ask.
- Queries a workspace does NOT rank for are the point: those are the ones Search Console can never report on.

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/configure_mentions' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"surface":"ai_overview"}'
```

### Response

```json
{
  "ok": true,
  "result": {
    "surface": "<surface>",
    "enabled": true,
    "queries": [],
    "cronExpression": "<cronExpression>",
    "lastRunAt": "<lastRunAt>",
    "lastStatus": "<lastStatus>",
    "lastDetail": "<lastDetail>",
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
