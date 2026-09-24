---
title: "List sources"
description: "List the sources this documentation is connected to — the repositories and websites its owner registered as its sources of truth, plus the repository the site is built from."
---

# List sources

<!-- widget:mcp access=read price-millicents=3 -->

## list_sources

List the sources this documentation is connected to — the repositories and websites its owner registered as its sources of truth, plus the repository the site is built from. Returns { sources: [{ id, kind, label, url, note, status, origin }] }; `note` is the owner's own words about why that source is connected — treat it as instruction. Read one with `read_source`. Every other row's `origin` is `source` and its `id` is a number. An empty list means nothing is connected: say so rather than inventing a repository or a domain. `private: true` on a row means GitHub will not serve that repository without credentials. It is a READING fact — attach an authorisation, expect no anonymous link to it to work — and it says nothing about whether the published site is public: whether anyone outside can read the DOCS is `visibility` on the workspace, and a private repository serving a fully indexed public site is an ordinary Docsbook setup.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |

### Returns

| Field | Type | Description |
|---|---|---|
| `sources` | object[] | { id, kind, label, url, note, status, last_read_at, origin }. `origin` is `workspace_repo` or `site_source` when `id` is null, `source` otherwise. |
| `hint` | string | — |

### Use cases

- Call this BEFORE writing or updating documentation and before judging whether something documented is still true: a connected source is a fact you can go and read, and reading beats recalling.

### Limitations

- `id` is a string, not a number, for two kinds of row that were never 'connected' by hand — it equals `origin`: `workspace_repo` is the repository the docs are built from (read it with `read_source source_id: "workspace_repo"`; arm a commit trigger on it with `enable_agent`'s `watch_source_id: "workspace_repo"`, no need to `connect_source` it first); `site_source` is the legacy single URL set in Branding (readable, but not a repository — it cannot be a commit trigger).

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "list_sources",
    "arguments": {}
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer YOUR_MCP_OAUTH_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_sources","arguments":{}}}'
```

### REST

```bash
curl 'https://docsbook.io/api/v1/list_sources' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Result

```json
{
  "sources": [],
  "hint": "<hint>"
}
```

<!-- /widget -->
