---
title: "Search project docs"
description: "FIND A DOCUMENTATION PAGE — start here, and this is the FIRST call for any question about these docs."
---

# Search project docs

<!-- widget:mcp access=read price-millicents=9 -->

## search_project_docs

FIND A DOCUMENTATION PAGE — start here, and this is the FIRST call for any question about these docs. Do NOT start by listing the outline, grepping or globbing files, or opening pages one by one to look for the answer: that downloads and reads the whole site, takes many times longer and answers worse than one call here. Searches the project's documentation by MEANING (embeddings over a pre-built vector index), which finds the right page far more often than literal keyword matching: 'how do I reset a password' lands on a page titled 'Recovering account access', which a word search misses entirely. Use it for any natural-language question — «где написано про…», 'where do we explain X', 'which page covers Y' — and before writing anything, so you edit the page that exists instead of adding a second one about the same thing. A LONG query is welcome, and usually better than a short one: paste the user's whole request, several questions at once included. It is split into its parts, each part searched on its own and the results merged, so a request that asks about four things returns a page for each instead of one blurred average of all four. Cheap and repeatable: the index is built once, ahead of time, so a call here is one lookup against vectors that already exist. Always answers: a project with no vector index yet is searched by full text instead, and `mode` ('semantic' | 'lexical') says which engine replied — no plan is required either way. Returns hits {n, title, headingPath, url, path}, best first — each with a similarity `score` (semantic) or a `snippet` (lexical); call the matching read-page tool on `path` for the whole page — `read_project_doc` on the signed-in server, the read tool this same tools/list names on the public one. Prefer search_docs only when you need a LITERAL string — an error message, a CLI flag, a regex, a file path.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `query` | string | yes | What you are looking for, in natural language — a question or a phrase, not keywords. |
| `limit` | integer | no | Max results (default 8). |

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "search_project_docs",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"search_project_docs","arguments":{"query":"<query>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### GET /api/v1/search_project_docs

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `query` | string | yes | What you are looking for, in natural language — a question or a phrase, not keywords. |
| `limit` | integer | no | Max results (default 8). |

#### Request

```bash
curl 'https://docsbook.io/api/v1/search_project_docs?query=%3Cquery%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->
