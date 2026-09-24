---
title: "Docsbook agent activity"
description: "WATCH THE DOCSBOOK AGENT WORK — the ordered timeline of what a job has actually done, step by step, while it is still running."
---

# Docsbook agent activity

<!-- widget:api -->

## POST /api/v1/docsbook_agent_activity

WATCH THE DOCSBOOK AGENT WORK — the ordered timeline of what a job has actually done, step by step, while it is still running. Every line is one action: a page read, a page written, a translation pass, a file it edited, a site it fetched, a report it posted — with the time, how long it took, and whether it worked. `docsbook_agent_status` says what state a job is in; this says what it has been DOING, so a caller asked 'what is it doing right now' has real lines to read back rather than a plausible story. Poll it: pass `after` with the `next_after` from the previous answer and you get only what happened since, which is what a live view is made of. It reports actions, never method: the playbooks and the reasoning behind them are part of the service, so a step that consulted them says exactly that and no more.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable without a token on this workspace's public MCP endpoint.

Also reachable by name at `POST /api/v1/tools/docsbook_agent_activity`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `task_id` | string | no | The job to watch — the id docsbook_agent returned. |
| `after` | number | no | Resume from here: the `next_after` of your last call. Omit to start at the beginning. |
| `limit` | number | no | How many steps, 1-200. Default 50. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | string | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### Use cases

- USE THIS INSTEAD OF GUESSING.

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/docsbook_agent_activity' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
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
