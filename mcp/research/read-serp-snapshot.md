---
title: "Read serp snapshot"
description: "The actual Google results page for up to 5 queries — organic results, the People Also Ask box, and Google's own AI Overview text with its cited sources, as rendered today."
---

# Read serp snapshot

<!-- widget:mcp access=read price-millicents=900 -->

## read_serp_snapshot

The actual Google results page for up to 5 queries — organic results, the People Also Ask box, and Google's own AI Overview text with its cited sources, as rendered today. measure_ai_visibility and discover_quotable_atoms currently reason about citability with no way to see a real SERP; this is the fetch that turns "assistants might cite us" into a dated screenshot of whether Google's own answer box already does. Routes from questions like: what does google's ai overview say about this · check the search results page for these queries · «что показывает ai overview гугла по этому запросу» · «проверь serp по этим запросам». Not: It reads what Google shows for a query. What an LLM says when asked the question directly (no search engine in between) is the job of observe_assistant_answers, not this tool. Example: Fetch the Google results page for "docsbook vs readme" — organic results, People Also Ask, and any AI Overview. Pass `workspace_id` whenever the answer will be quoted later: it is what files the reading in that project's history with a `call_id`, and only a `call_id` (or a URL) is accepted as the source of a figure on an audit finding — the tool's own name is not a source. One call fetches at most 5 events and costs $0.0090.

| Field | Type | Required | Description |
|---|---|---|---|
| `queries` | string[] | yes | Search queries to run, e.g. the exact questions a reader would type into Google about this product. |
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
    "name": "read_serp_snapshot",
    "arguments": {
      "queries": []
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"read_serp_snapshot","arguments":{"queries":[]}}}'
```

<!-- /widget -->
