---
title: "List goals"
description: "The goals and funnels defined for this workspace, with what each one MATCHES."
---

# List goals

<!-- widget:api -->

## GET /api/v1/list_goals

The goals and funnels defined for this workspace, with what each one MATCHES. A goal is a named thing you want a reader to do; a funnel is an ordered list of goals. Free on every plan: defining measurement is not the paid part. Every project has the standing goal — be found, on Google and in AI answers (`standing_goal` here, `be_found` as a `goal_key`) — without declaring anything; these are the owner's EXTRAS, reader actions on the site.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/list_goals`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |

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
| `goals` | object[] | — |
| `funnels` | object[] | — |
| `max_funnel_steps` | number | — |

### Use cases

- Call this before creating anything — a goal whose name already exists is refused, and a funnel step refers to a goal by name.

### Limitations

- 🔴 AN EMPTY LIST IS NOT A MISSING GOAL.
- Never ask the owner to declare a goal, and never create a page-view goal to stand in for being found: decompose the standing goal instead (list_opportunities, add_direction).

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/list_goals' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Response

```json
{
  "ok": true,
  "result": {
    "workspace_id": 0,
    "goals": [],
    "funnels": [],
    "max_funnel_steps": 0
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
