---
title: "Docsbook agent status"
description: "What the Docsbook agent is doing on a job, and what came of it — status, progress, the exchange so far, and the result once it is done."
---

# Docsbook agent status

<!-- widget:api -->

## GET /api/v1/docsbook_agent_status

What the Docsbook agent is doing on a job, and what came of it — status, progress, the exchange so far, and the result once it is done. `needs_owner` in the result means it asked you something and is waiting: answer with `docsbook_agent_reply`. It reports what it CHANGED and what that should move; it does not hand back the method it used.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/docsbook_agent_status`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `task_id` | string | yes | The id docsbook_agent returned. |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/docsbook_agent_status?task_id=%3Ctask_id%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
