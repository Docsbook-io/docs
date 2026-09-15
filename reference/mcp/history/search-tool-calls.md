---
title: "Search tool calls"
description: "FIND a recorded call by what is inside it — a page it was about, a word in the answer, an error it returned."
---

# Search tool calls

<!-- widget:mcp access=read -->

## search_tool_calls

FIND a recorded call by what is inside it — a page it was about, a word in the answer, an error it returned. Free on every plan. Ranked by WHERE the words were found, not by date: a call whose SUBJECT is /pricing outranks fifty whose answers merely list /pricing among their rows, which is the whole difference between this and grepping a log. Every word must appear somewhere (AND, not OR). The query takes filters inline — `tool:get_analytics path:/pricing since:14d failed:true source:cron` — and everything else is treated as words. An unknown `key:value` is searched as two words rather than silently dropped. Reach for it when you know WHAT you are looking for and not when it was taken: 'when did we last audit GEO on the pricing page', 'which reading first showed zero AI citations', 'what failed yesterday'. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `query` | string | yes | Words to find, plus optional inline filters: tool:, path:, since:, failed:, source:. |
| `limit` | integer | no | Max hits. Default 20. |

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
    "name": "search_tool_calls",
    "arguments": {
      "query": "<query>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"search_tool_calls","arguments":{"query":"<query>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/search_tool_calls

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/search_tool_calls' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"query":"<query>"}}'
```

<!-- /widget -->
