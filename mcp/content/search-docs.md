---
title: "Search docs"
description: "Search the workspace's documentation content and return verbatim, citable sections — the call for 'where do we describe…', 'find the page about…', «где у нас описано», «найди в…"
---

# Search docs

<!-- widget:mcp access=read price-millicents=30000 -->

## search_docs

Search the workspace's documentation content and return verbatim, citable sections — the call for 'where do we describe…', 'find the page about…', «где у нас описано», «найди в документации». Modes: 'text' (default — full-text with snippets), 'grep' (regex), 'symbol' (fuzzy heading match), 'paths' (glob over file paths). Returns numbered hits {n, title, headingPath, snippet, url}: 280-character snippets, not pages — call read_doc for the whole page before editing it. Available to any token regardless of read/write scope.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `query` | string | yes | What to find. For 'text'/'grep' a phrase or pattern; for 'symbol' a heading hint; for 'paths' a glob. |
| `mode` | string | no | Search mode (default 'text'). One of: `text`, `grep`, `symbol`, `paths`. |
| `path_prefix` | string | no | Optional: restrict 'text'/'grep' results to files under this path prefix. |

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
    "name": "search_docs",
    "arguments": {
      "query": "<query>",
      "mode": "text"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"search_docs","arguments":{"query":"<query>","mode":"text"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### GET /api/v1/search_docs

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `query` | string | yes | What to find. For 'text'/'grep' a phrase or pattern; for 'symbol' a heading hint; for 'paths' a glob. |
| `mode` | string | no | Search mode (default 'text'). One of: `text`, `grep`, `symbol`, `paths`. |
| `path_prefix` | string | no | Optional: restrict 'text'/'grep' results to files under this path prefix. |

#### Request

```bash
curl 'https://docsbook.io/api/v1/search_docs?query=%3Cquery%3E&mode=text' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->
