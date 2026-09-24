---
title: "Docsbook agent tasks"
description: "Every job this account has given the Docsbook agent, newest first — what was asked for, what is running now, what finished and how."
---

# Docsbook agent tasks

<!-- widget:api -->

## GET /api/v1/docsbook_agent_tasks

Every job this account has given the Docsbook agent, newest first — what was asked for, what is running now, what finished and how. Narrow to one project with workspace_id.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/docsbook_agent_tasks`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `limit` | number | no | How many, 1-100. Default 20. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | string | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/docsbook_agent_tasks' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Response

```json
{
  "ok": true,
  "result": "<result>",
  "duration_ms": 0
}
```

### Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |

<!-- /widget -->
