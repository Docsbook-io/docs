---
title: "Mark path as funnel step"
description: "Add a documentation PAGE to a funnel as its next step, creating the page goal if it does not exist yet."
---

# Mark path as funnel step

<!-- widget:api -->

## POST /api/v1/mark_path_as_funnel_step

Add a documentation PAGE to a funnel as its next step, creating the page goal if it does not exist yet. The shortcut for 'this page is part of the route readers should take' — it saves creating a goal and then editing the funnel. Creates the funnel too if the name is new. Note the broad-entry rule: if this is the FIRST step of a new funnel you will get a warning, because a single page as step 1 excludes every reader who arrived deep.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/mark_path_as_funnel_step`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `path` | string | no | The doc path, e.g. '/docs/quickstart'. |
| `funnel` | string | no | Funnel name to append the step to. Created if it does not exist. |
| `position` | number | no | 0-based index to insert at. Appends when omitted. |

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
| `goal` | string | — |
| `issues` | object[] | — |
| `unchanged` | string | — |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/mark_path_as_funnel_step' \
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
    "goal": "<goal>",
    "issues": [],
    "unchanged": "<unchanged>"
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
