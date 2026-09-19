---
title: "Search discourse threads"
description: "Up to 40 threads from a named Discourse forum matching a search term, with reply count and age — the support-forum half of \"what do people ask\" for the tools that run one."
---

# Search discourse threads

<!-- widget:mcp access=read price-millicents=4000 -->

## search_discourse_threads

Up to 40 threads from a named Discourse forum matching a search term, with reply count and age — the support-forum half of "what do people ask" for the tools that run one. A product's own community forum is where its sharpest users already asked and often already answered the question our docs are missing; the cheapest of the three off-site question sources here, at $1/1,000. Routes from questions like: what are people asking on this product's forum · search their discourse community · «что спрашивают на форуме этого продукта» · «поищи в их discourse-комьюнити». Not: It searches ONE named Discourse instance. Finding whether a product even runs a Discourse forum at all is an open-web search in your own client first, not this tool. Example: Search discuss.python.org for threads mentioning "asyncio timeout". Pass `workspace_id` whenever the answer will be quoted later: it is what files the reading in that project's history with a `call_id`, and only a `call_id` (or a URL) is accepted as the source of a figure on an audit finding — the tool's own name is not a source. One call fetches at most 40 results and costs $0.0400.

| Field | Type | Required | Description |
|---|---|---|---|
| `instance` | string | yes | Base URL of the Discourse forum to search, e.g. https://discuss.python.org |
| `query` | string[] | yes | Free-text search terms to run against that forum's own search. |
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
    "name": "search_discourse_threads",
    "arguments": {
      "instance": "<instance>",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"search_discourse_threads","arguments":{"instance":"<instance>","query":[]}}}'
```

<!-- /widget -->
