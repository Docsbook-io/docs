---
title: "Search docs"
description: "LITERAL-string search over the workspace's documentation files — for an exact token you already know: an error message, a CLI flag, a config key, a regex, a file path."
---

# Search docs

<!-- widget:mcp access=read price-millicents=9 -->

## search_docs

LITERAL-string search over the workspace's documentation files — for an exact token you already know: an error message, a CLI flag, a config key, a regex, a file path. In 'text' mode on a project with a semantic index the literal matches are fused with the index's meaning matches (`engine: "hybrid"`), so a section worded differently still surfaces; without an index it matches words only (`engine: "literal"`). Still NOT for a question or a topic ('where do we describe…', 'find the page about…', «где у нас описано», «найди в документации») — that is `search_project_docs`, which takes the whole question, splits it into its parts and ranks pages by MEANING; do not hunt for an answer here mode by mode. Modes: 'text' (default — full-text with snippets, hybrid when indexed), 'grep' (regex), 'symbol' (fuzzy heading match), 'paths' (glob over file paths). Returns numbered hits {n, title, headingPath, snippet, url}: 280-character snippets, not pages — call read_project_doc for the whole page before editing it. Available to any token regardless of read/write scope.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `query` | string | yes | What to find. For 'text'/'grep' a phrase or pattern; for 'symbol' a heading hint; for 'paths' a glob. |
| `mode` | string | no | Search mode (default 'text'). One of: `text`, `grep`, `symbol`, `paths`. |
| `path_prefix` | string | no | Optional: restrict 'text'/'grep' results to files under this path prefix. |

### Returns

| Field | Type | Description |
|---|---|---|
| `mode` | string | text \| grep \| symbol \| paths. |
| `docs_language` | string | null | — |
| `count` | number | — |
| `results` | object[] | { n, title, headingPath, snippet, url, path }. |
| `note` | string | — |

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
  -H 'Authorization: Bearer YOUR_MCP_OAUTH_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"search_docs","arguments":{"query":"<query>","mode":"text"}}}'
```

### REST

```bash
curl 'https://docsbook.io/api/v1/search_docs?query=%3Cquery%3E&mode=text' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Result

```json
{
  "mode": "<mode>",
  "docs_language": "<docs_language>",
  "count": 0,
  "results": [],
  "note": "<note>"
}
```

<!-- /widget -->
