---
title: "Read project doc"
description: "Read ONE documentation page in full — its complete markdown, title and repo path."
---

# Read project doc

<!-- widget:mcp access=read price-millicents=3 -->

## read_project_doc

Read ONE documentation page in full — its complete markdown, title and repo path. THE step between finding a page and editing it: read it here, change the text, then write_docs the whole file back. Takes the repo path search_docs and get_doc_outline use ('guides/setup.md') or the URL slug the analytics tools return ('guides/setup'); a near-miss with a single candidate is resolved for you (`resolvedFrom` says so), several candidates are listed to choose from. Use it for 'fix the command on the installation page', 'show me the quickstart', «покажи страницу», «поправь строку на странице». Changes nothing; available to any token. The result carries `lifecycle`: the page's `status`, its `version`, and `agent_may_build_from`. 🔴 When that is false the page is NOT a source of truth — a machine drafted it, or a human has not signed it off, or it was superseded. Read it, quote it as a draft, but do not generate work from it, do not cite it as a decision, and say which status it is in. `set_doc_status` is how it gets approved.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `path` | string | yes | The page: a repo file path ('reference/README.md') or its URL slug ('reference/introduction'). |

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "read_project_doc",
    "arguments": {
      "path": "<path>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"read_project_doc","arguments":{"path":"<path>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### GET /api/v1/read_project_doc

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `path` | string | yes | The page: a repo file path ('reference/README.md') or its URL slug ('reference/introduction'). |

#### Request

```bash
curl 'https://docsbook.io/api/v1/read_project_doc?path=%3Cpath%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->
