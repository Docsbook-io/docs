---
title: "Search reddit threads"
description: "Up to 30 Reddit posts and comments mentioning a product, with the subreddit, upvotes and comment count — the complaint and comparison threads that never reach our own analytics."
---

# Search reddit threads

<!-- widget:mcp access=read price-millicents=6000 -->

## search_reddit_threads

Up to 30 Reddit posts and comments mentioning a product, with the subreddit, upvotes and comment count — the complaint and comparison threads that never reach our own analytics. A reader who asked r/webdev instead of our chat is a reader our own AI-question logs cannot see at all; this is the off-site half of "what do people actually ask". Routes from questions like: what does reddit say about this product · find complaints about this tool on reddit · «что говорят про продукт на реддите» · «найди жалобы на этот продукт». Not: It searches Reddit specifically. Open-web search across everywhere is your own client's web search (this server has none); a specific thread URL you already have is read_rendered_page. Example: Find what Reddit says about "docsbook alternative" — posts and comments, most relevant first. Pass `workspace_id` whenever the answer will be quoted later: it is what files the reading in that project's history with a `call_id`, and only a `call_id` (or a URL) is accepted as the source of a figure on an audit finding — the tool's own name is not a source. One call fetches at most 30 results and costs $0.0600.

| Field | Type | Required | Description |
|---|---|---|---|
| `query` | string[] | yes | Product name or phrase to search for across Reddit, e.g. "docsbook alternative" or the product's own name. |
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
    "name": "search_reddit_threads",
    "arguments": {
      "query": []
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"search_reddit_threads","arguments":{"query":[]}}}'
```

<!-- /widget -->
