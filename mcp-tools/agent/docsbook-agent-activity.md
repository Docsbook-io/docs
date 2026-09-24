---
title: "Docsbook agent activity"
description: "WATCH THE DOCSBOOK AGENT WORK — the ordered timeline of what a job has actually done, step by step, while it is still running."
---

# Docsbook agent activity

<!-- widget:mcp access=write anonymous price-millicents=800 -->

## docsbook_agent_activity

WATCH THE DOCSBOOK AGENT WORK — the ordered timeline of what a job has actually done, step by step, while it is still running. Every line is one action: a page read, a page written, a translation pass, a file it edited, a site it fetched, a report it posted — with the time, how long it took, and whether it worked. USE THIS INSTEAD OF GUESSING. `docsbook_agent_status` says what state a job is in; this says what it has been DOING, so a caller asked 'what is it doing right now' has real lines to read back rather than a plausible story. Poll it: pass `after` with the `next_after` from the previous answer and you get only what happened since, which is what a live view is made of. It reports actions, never method: the playbooks and the reasoning behind them are part of the service, so a step that consulted them says exactly that and no more.

| Field | Type | Required | Description |
|---|---|---|---|
| `task_id` | string | yes | The job to watch — the id docsbook_agent returned. |
| `after` | number | no | Resume from here: the `next_after` of your last call. Omit to start at the beginning. |
| `limit` | number | no | How many steps, 1-200. Default 50. |

<!-- /widget -->

## Call it

<!-- widget:code-group -->

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "docsbook_agent_activity",
    "arguments": {
      "task_id": "<task_id>"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"docsbook_agent_activity","arguments":{"task_id":"<task_id>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### POST /api/v1/tools/docsbook_agent_activity

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/docsbook_agent_activity' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"task_id":"<task_id>"}}'
```

<!-- /widget -->
