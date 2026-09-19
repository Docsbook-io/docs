---
title: "Search hackernews threads"
description: "Up to 50 Hacker News stories and comments mentioning a product or topic, with points and comment count — the technical-audience discussion thread, not a summary of it."
---

# Search hackernews threads

<!-- widget:mcp access=read price-millicents=140 -->

## search_hackernews_threads

Up to 50 Hacker News stories and comments mentioning a product or topic, with points and comment count — the technical-audience discussion thread, not a summary of it. HN is where a launch gets judged by exactly the ICP developer-tool docs are written for, in public, searchably, and none of it reaches our own logs. Routes from questions like: what does hacker news say about this · find our launch discussion on hn · «что говорят про это на hacker news» · «найди обсуждение запуска на hn». Not: It searches Hacker News specifically. Everywhere-at-once is your own client's web search (this server has none). Example: Search Hacker News for discussion of "docsbook" — stories and comments, most relevant first. Pass `workspace_id` whenever the answer will be quoted later: it is what files the reading in that project's history with a `call_id`, and only a `call_id` (or a URL) is accepted as the source of a figure on an audit finding — the tool's own name is not a source. One call fetches at most 50 results and costs $0.0014.

| Field | Type | Required | Description |
|---|---|---|---|
| `query` | string | yes | Product name or topic to search Hacker News stories and comments for. |
| `workspace_id` | string | no | The project this reading is FOR. 🔴 Pass it whenever the answer will be QUOTED later: it is what files the call in that project's history with a `call_id`, and a `call_id` is the only thing an opportunity accepts as the source of a demand figure (`demand_source`). Nothing about the project is sent to the site being read. Omitted, the reading still comes back — it simply lands in no history, so nothing afterwards can point at it. Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |

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
    "name": "search_hackernews_threads",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"search_hackernews_threads","arguments":{"query":"<query>"}}}'
```

<!-- /widget -->
