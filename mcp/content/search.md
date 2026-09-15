---
title: "Search"
description: "FIND A DOCUMENTATION PAGE — start here."
---

# Search

<!-- widget:mcp access=read anonymous price-millicents=30000 -->

## search

FIND A DOCUMENTATION PAGE — start here. Searches the project's documentation by MEANING (embeddings over a pre-built vector index), which finds the right page far more often than literal keyword matching: 'how do I reset a password' lands on a page titled 'Recovering account access', which a word search misses entirely. Use it for any natural-language question — «где написано про…», 'where do we explain X', 'which page covers Y' — and before writing anything, so you edit the page that exists instead of adding a second one about the same thing. Cheap and repeatable: the index is built once, ahead of time, so a call here is one lookup against vectors that already exist. Always answers: a project with no vector index yet is searched by full text instead, and `mode` ('semantic' | 'lexical') says which engine replied — no plan is required either way. Returns hits {n, title, headingPath, url, path}, best first — each with a similarity `score` (semantic) or a `snippet` (lexical); call read_doc on `path` for the whole page. Prefer search_docs only when you need a LITERAL string — an error message, a CLI flag, a regex, a file path. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `query` | string | yes | What you are looking for, in natural language — a question or a phrase, not keywords. |
| `limit` | integer | no | Max results (default 8). |

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
    "name": "search",
    "arguments": {
      "query": "<query>"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"search","arguments":{"query":"<query>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/search

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/search' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"query":"<query>"}}'
```

<!-- /widget -->
