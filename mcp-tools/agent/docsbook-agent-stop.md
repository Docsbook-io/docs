---
title: "Docsbook agent stop"
description: "Stop a Docsbook agent job."
---

# Docsbook agent stop

<!-- widget:mcp access=write price-millicents=800 -->

## docsbook_agent_stop

Stop a Docsbook agent job. Work already committed stays — stopping is not an undo, and what landed is ordinary git history you can revert — and the agent's credential for that job is revoked immediately.

| Field | Type | Required | Description |
|---|---|---|---|
| `task_id` | string | yes | The job to stop. |
| `reason` | string | no | Why, for the record. |

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
    "name": "docsbook_agent_stop",
    "arguments": {
      "task_id": "<task_id>"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer YOUR_MCP_OAUTH_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"docsbook_agent_stop","arguments":{"task_id":"<task_id>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### POST /api/v1/tools/docsbook_agent_stop

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/docsbook_agent_stop' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"task_id":"<task_id>"}}'
```

<!-- /widget -->
