---
title: "Find tool"
description: "Search this server's own tool catalog by what you're trying to do, in your own words — not a guessed tool name."
---

# Find tool

<!-- widget:mcp access=read -->

## find_tool

Search this server's own tool catalog by what you're trying to do, in your own words — not a guessed tool name. On a customer's own token this is what surfaces the tools this connection can already call but tools/list does not spell out one by one: the webhook alert registrars ('notify us when traffic drops'), giving a finished site away, changing who may SEE the site. The documentation tools themselves — branding, navigation, domain, languages, translations, the chat assistant, conversion goals, and writing the pages — are in tools/list directly since 2026-09-22, so call those by name without searching first. 🔴 EVERY MATCH SAYS HOW TO CALL IT, and the two ways are not interchangeable. `call: "direct"` is a name your client already lists: call it by name. `call: "call_tool"` is one it does not: run it as call_tool { name, arguments } — calling such a name directly fails INSIDE YOUR OWN CLIENT ('no such tool'), before the request ever reaches this server, because a client builds what it may call out of tools/list. Each match carries `accepts` — the fields that name takes — so the call_tool arguments can be built from this answer alone. This tool runs nothing itself. Returns matching names with a trimmed description and the family each belongs to; get_info gives the family overview when the query itself does not narrow it down.

| Field | Type | Required | Description |
|---|---|---|---|
| `query` | string | yes | What you are trying to do, in natural language — a question or a sentence, not keywords. |
| `limit` | integer | no | Max results (default 8). |

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "find_tool",
    "arguments": {
      "query": "<query>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"find_tool","arguments":{"query":"<query>"}}}'
```

<!-- /widget -->
