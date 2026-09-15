---
title: "Ask docsbook"
description: "Ask a question about USING DOCSBOOK ITSELF — how a feature works, how to set something up, what a plan includes, why the product behaves a certain way, 'can Docsbook do X' — and…"
---

# Ask docsbook

<!-- widget:mcp access=read price-millicents=30000 -->

## ask_docsbook

Ask a question about USING DOCSBOOK ITSELF — how a feature works, how to set something up, what a plan includes, why the product behaves a certain way, 'can Docsbook do X' — and get back the SAME AI-generated, cited answer a reader gets from the public 'Ask AI' chat on https://docsbook.io/docs. Different from `docsbook_expert`: that one advises YOU on how to plan documentation work and runs no model; this one actually asks the question and answers it, against Docsbook's own manual. NOT for a customer's OWN documentation — that is `search`/`search_docs`/`read_doc` against their workspace. `session_id` is optional: reuse the same one across calls to keep them grouped as one conversation in this project's own chat analytics, the way a real visitor's multi-turn chat is; omit it and each call reads as a separate visitor. Any language — answers come back in whichever language the question was asked in. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `question` | string | yes | The question, in plain language, any language. |
| `session_id` | string | no | Optional: reuse the same id across calls to group them as one visitor's conversation. |

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
    "name": "ask_docsbook",
    "arguments": {
      "question": "<question>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"ask_docsbook","arguments":{"question":"<question>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/ask_docsbook

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/ask_docsbook' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"question":"<question>"}}'
```

<!-- /widget -->
