---
title: "Get project doc outline"
description: "List every markdown page in the workspace with a short summary (title, heading count, char count) plus its lifecycle — `status`, `version` and `agentMayBuildFrom`."
---

# Get project doc outline

<!-- widget:mcp access=read price-millicents=800 -->

## get_project_doc_outline

List every markdown page in the workspace with a short summary (title, heading count, char count) plus its lifecycle — `status`, `version` and `agentMayBuildFrom`. An INVENTORY, not a search: NOT the way to answer a question or find the page about something — that is `search_project_docs`. Building this list downloads and parses every page of the site (slow on a large one), and a list of titles answers nothing by itself. Use it for 'what does this documentation cover', to pick a folder for a NEW page, or after `search_project_docs` found nothing. It is also the REVIEW BOARD for documentation that is governed by status: `status: 'review'` lists what is waiting on a human, `status: 'generated'` what a machine wrote that nobody has read. `counts` always describes the whole prefix, not the filtered rows, so 'four of ninety pages are approved' is one call. Statuses: generated (A machine wrote this page and no human has read it yet.) · draft (Someone is still writing it. Not ready to be read as settled.) · review (Waiting for a human to read it and decide.) · approved (A human read this version and signed off. Safe to build work from.) · locked (Frozen on purpose. Agents may read it and build from it, but may not rewrite it.) · deprecated (Superseded. Kept so its links keep working, not to be relied on.) · archived (History. Neither built from nor edited.)

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `path_prefix` | string | no | Optional: restrict to pages under this path prefix. |
| `status` | string | no | Optional: only pages at this lifecycle status. `counts` still covers them all. One of: `generated`, `draft`, `review`, `approved`, `locked`, `deprecated`, `archived`. |

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
    "name": "get_project_doc_outline",
    "arguments": {
      "status": "generated"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_project_doc_outline","arguments":{"status":"generated"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### GET /api/v1/get_project_doc_outline

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `path_prefix` | string | no | Optional: restrict to pages under this path prefix. |
| `status` | string | no | Optional: only pages at this lifecycle status. `counts` still covers them all. One of: `generated`, `draft`, `review`, `approved`, `locked`, `deprecated`, `archived`. |

#### Request

```bash
curl 'https://docsbook.io/api/v1/get_project_doc_outline?status=generated' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->
