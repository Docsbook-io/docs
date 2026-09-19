---
title: "Crawl competitor docs"
description: "Up to 50 pages of a rival's documentation, JavaScript-rendered and returned as clean Markdown — the corpus, not one page of it."
---

# Crawl competitor docs

<!-- widget:mcp access=read price-millicents=25000 -->

## crawl_competitor_docs

Up to 50 pages of a rival's documentation, JavaScript-rendered and returned as clean Markdown — the corpus, not one page of it. Our own crawler stops at 30 plain-HTTP pages and returns nothing for a page a client framework renders; a competitor's whole docs site is exactly the shape that defeats both limits at once. Routes from questions like: what does our competitor's documentation actually say · map their docs site · «что у конкурента в документации» · «собери всю доку конкурента». Not: It fetches the corpus. Reading ONE page you already have a URL for, including a JS-heavy one, is read_rendered_page — cheaper and faster for a single page. Not only rivals: it is also the reader for a docs site you are migrating OFF (Mintlify, GitBook, ReadMe) when the pages are needed before run_docs_create. Example: Crawl https://docs.rivalproduct.com and return its documentation pages as Markdown. Pass `workspace_id` whenever the answer will be quoted later: it is what files the reading in that project's history with a `call_id`, and only a `call_id` (or a URL) is accepted as the source of a figure on an audit finding — the tool's own name is not a source. One call fetches at most 50 pages and costs $0.2500.

| Field | Type | Required | Description |
|---|---|---|---|
| `url` | string | yes | Entry URL of the competitor's documentation, e.g. https://docs.rivalproduct.com |
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
    "name": "crawl_competitor_docs",
    "arguments": {
      "url": "<url>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"crawl_competitor_docs","arguments":{"url":"<url>"}}}'
```

<!-- /widget -->
