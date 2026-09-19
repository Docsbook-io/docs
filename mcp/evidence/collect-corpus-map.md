---
title: "Collect corpus map"
description: "Map the whole corpus in one call: every page with its size, heading count and depth, the top-level sections, the shortest pages, and how much of it a declared navigation entry…"
---

# Collect corpus map

<!-- widget:mcp access=read price-millicents=12000 -->

## collect_corpus_map

Map the whole corpus in one call: every page with its size, heading count and depth, the top-level sections, the shortest pages, and how much of it a declared navigation entry actually reaches. The only capability here that needs NO traffic, NO Search Console and NO history — it reads the pages and the navigation chrome, which exist from the first day. That makes it the one thing a week-old docs site can buy that returns real rows, where every reading of reader behaviour on the same workspace comes back a column of nulls. Returns an evidence record plus the `get_doc_outline` and `get_workspace` calls behind every row. Coverage is stated as what it is — a path-prefix match, so a page linked only from another page's body counts as unreached — rather than dressed up as an orphan report. Use it for 'how many pages do we have', 'which pages are stubs', 'what does navigation actually reach', 'how deep does this thing go', «сколько у нас страниц», «какие страницы пустые», «что вообще есть в навигации». It states the shape. Whether that shape is WRONG — which sections are missing, which are too deep to find, what a reader was looking for and did not get — is a judgement: ask `docsbook_expert`, which names the readings that decide it and what makes the conclusion wrong. Returns a validated `collect_corpus_map.v1` payload: an `evidence` map, the normalised `rows` behind it, and a `reproduce` block naming the exact MCP calls and arguments that produced every row — run them yourself and you get the same answer. There is no model in the path, so there are no findings, no scores and nothing to disbelieve; interpretation is what the audits charge for. Changes nothing; safe on a read-only token.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `path_prefix` | string | no | Restrict the read to pages under this path prefix, e.g. "/api". Without it the whole corpus is mapped. |

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
    "name": "collect_corpus_map",
    "arguments": {}
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"collect_corpus_map","arguments":{}}}'
```

<!-- /widget -->
