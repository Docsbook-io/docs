---
title: "Search stackoverflow threads"
description: "Up to 15 Stack Overflow questions naming a product or library, with view count, answer count and whether any answer was accepted — unanswered-and-viewed is the exact shape of a…"
---

# Search stackoverflow threads

<!-- widget:mcp access=read price-millicents=15000 -->

## search_stackoverflow_threads

Up to 15 Stack Overflow questions naming a product or library, with view count, answer count and whether any answer was accepted — unanswered-and-viewed is the exact shape of a documentation gap. A question with 4,000 views and zero accepted answers is a page our docs should have and do not, stated by a real reader rather than inferred. Routes from questions like: what stack overflow questions mention our product · find unanswered questions about this library · «какие вопросы про наш продукт есть на stack overflow» · «найди вопросы без ответа про эту библиотеку». Not: It searches Stack Overflow specifically. Broader open-web developer discussion is your own client's web search (this server has none); a specific question URL you already have is read_rendered_page. Example: Find Stack Overflow questions mentioning our npm package, with view and answer counts. Pass `workspace_id` whenever the answer will be quoted later: it is what files the reading in that project's history with a `call_id`, and only a `call_id` (or a URL) is accepted as the source of a figure on an audit finding — the tool's own name is not a source. One call fetches at most 15 results and costs $0.1500.

| Field | Type | Required | Description |
|---|---|---|---|
| `query` | string | yes | Product or library name to search Stack Overflow questions for, e.g. the npm package name. |
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
    "name": "search_stackoverflow_threads",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"search_stackoverflow_threads","arguments":{"query":"<query>"}}}'
```

<!-- /widget -->
