---
title: "Docsbook agent reply"
description: "Answer the Docsbook agent's question, or add something to a job it is already working on — the decision it asked for, the fact it could not find, a correction."
---

# Docsbook agent reply

<!-- widget:mcp access=write price-millicents=800 -->

## docsbook_agent_reply

Answer the Docsbook agent's question, or add something to a job it is already working on — the decision it asked for, the fact it could not find, a correction. It picks the job back up with the whole exchange in front of it. Only for a job that is still open; a finished one is finished, start a new one with `docsbook_agent`.

| Field | Type | Required | Description |
|---|---|---|---|
| `task_id` | string | yes | The job to reply to. |
| `text` | string | yes | What you want to tell the agent, in your own words. |

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
    "name": "docsbook_agent_reply",
    "arguments": {
      "task_id": "<task_id>",
      "text": "<text>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"docsbook_agent_reply","arguments":{"task_id":"<task_id>","text":"<text>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/docsbook_agent_reply

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/docsbook_agent_reply' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"task_id":"<task_id>","text":"<text>"}}'
```

<!-- /widget -->
