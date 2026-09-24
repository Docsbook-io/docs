---
title: "Docsbook agent reply"
description: "Talk to the Docsbook agent about a job that is still open — answer a question it asked, add something it needs (a decision, a fact it could not find, a correction), or just ask…"
---

# Docsbook agent reply

<!-- widget:api -->

## POST /api/v1/docsbook_agent_reply

Talk to the Docsbook agent about a job that is still open — answer a question it asked, add something it needs (a decision, a fact it could not find, a correction), or just ask it something about how the job is going ('how far is the API reference pass', 'did you find the auth docs'). You do not have to wait for it to ask first: send text any time the job is open and it picks the job back up with the whole exchange in front of it, replying in its next report — read `docsbook_agent_status` or `docsbook_agent_activity` after to see what it said. Only for a job that is still open; a finished one is finished, start a new one with `docsbook_agent`.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/docsbook_agent_reply`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `task_id` | string | no | The job to reply to. |
| `text` | string | no | What you want to tell the agent, in your own words. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/docsbook_agent_reply' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
