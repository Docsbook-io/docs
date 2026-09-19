---
title: "Docsbook agent status"
description: "What the Docsbook agent is doing on a job, and what came of it — status, progress, the exchange so far, and the result once it is done."
---

# Docsbook agent status

<!-- widget:mcp access=read price-millicents=800 -->

## docsbook_agent_status

What the Docsbook agent is doing on a job, and what came of it — status, progress, the exchange so far, and the result once it is done. `needs_owner` in the result means it asked you something and is waiting: answer with `docsbook_agent_reply`. It reports what it CHANGED and what that should move; it does not hand back the method it used.

| Field | Type | Required | Description |
|---|---|---|---|
| `task_id` | string | yes | The id docsbook_agent returned. |

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
    "name": "docsbook_agent_status",
    "arguments": {
      "task_id": "<task_id>"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"docsbook_agent_status","arguments":{"task_id":"<task_id>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### GET /api/v1/docsbook_agent_status

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `task_id` | string | yes | The id docsbook_agent returned. |

#### Request

```bash
curl 'https://docsbook.io/api/v1/docsbook_agent_status?task_id=%3Ctask_id%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->
