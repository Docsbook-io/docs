---
title: "Find widget"
description: "Search the Docsbook widget catalog for an interactive UI widget matching the user's request."
---

# Find widget

<!-- widget:api -->

## GET /api/v1/find_widget

Search the Docsbook widget catalog for an interactive UI widget matching the user's request. Returns matching widget ids and summaries. 'dark mode toggle', 'analytics chart', 'search bar'). After finding a widget, use the returned resourceUri to read its HTML bundle via the ui:// resource.

**Price** — free, never metered.

Also reachable without a token on this workspace's public MCP endpoint.

Also reachable by name at `POST /api/v1/tools/find_widget`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `query` | string | yes | Free-text description of what the user wants, e.g. 'dark mode toggle' or 'analytics dashboard'. |
| `mode` | string | no | Restrict matches to widgets available in this mode (admin or user). |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `matches` | object[] | { id, name, summary, resourceUri, requiresPlan, modes }. |
| `index_version` | string | — |
| `index_fetched_at` | string | — |

### Use cases

- Use this to discover available widgets (e.g.

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/find_widget?query=%3Cquery%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Response

```json
{
  "ok": true,
  "result": {
    "matches": [],
    "index_version": "<index_version>",
    "index_fetched_at": "<index_fetched_at>"
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
