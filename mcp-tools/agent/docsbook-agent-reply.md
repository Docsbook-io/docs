---
title: "Docsbook agent reply"
description: "Talk to the Docsbook agent about a job that is still open — answer a question it asked, add something it needs (a decision, a fact it could not find, a correction), or just ask…"
---

# Docsbook agent reply

<!-- widget:mcp access=write price-millicents=3 -->

## docsbook_agent_reply

Talk to the Docsbook agent about a job that is still open — answer a question it asked, add something it needs (a decision, a fact it could not find, a correction), or just ask it something about how the job is going ('how far is the API reference pass', 'did you find the auth docs'). You do not have to wait for it to ask first: send text any time the job is open and it picks the job back up with the whole exchange in front of it, replying in its next report — read `docsbook_agent_status` or `docsbook_agent_activity` after to see what it said. Only for a job that is still open; a finished one is finished, start a new one with `docsbook_agent`.

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
  -H 'Authorization: Bearer YOUR_MCP_OAUTH_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"docsbook_agent_reply","arguments":{"task_id":"<task_id>","text":"<text>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### POST /api/v1/docsbook_agent_reply

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `task_id` | string | yes | The job to reply to. |
| `text` | string | yes | What you want to tell the agent, in your own words. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/docsbook_agent_reply' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"task_id":"<task_id>","text":"<text>"}'
```

<!-- /widget -->
