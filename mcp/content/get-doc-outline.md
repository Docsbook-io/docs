---
title: "Get doc outline"
description: "List every markdown page in the workspace with a short summary (title, heading count, char count) plus its lifecycle — `status`, `version` and `agentMayBuildFrom`."
---

# Get doc outline

<!-- widget:mcp access=read price-millicents=800 -->

## get_doc_outline

List every markdown page in the workspace with a short summary (title, heading count, char count) plus its lifecycle — `status`, `version` and `agentMayBuildFrom`. Use it to discover what pages exist before searching or writing. It is also the REVIEW BOARD for documentation that is governed by status: `status: 'review'` lists what is waiting on a human, `status: 'generated'` what a machine wrote that nobody has read. `counts` always describes the whole prefix, not the filtered rows, so 'four of ninety pages are approved' is one call. Statuses: generated (A machine wrote this page and no human has read it yet.) · draft (Someone is still writing it. Not ready to be read as settled.) · review (Waiting for a human to read it and decide.) · approved (A human read this version and signed off. Safe to build work from.) · locked (Frozen on purpose. Agents may read it and build from it, but may not rewrite it.) · deprecated (Superseded. Kept so its links keep working, not to be relied on.) · archived (History. Neither built from nor edited.) This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

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
    "name": "get_doc_outline",
    "arguments": {
      "status": "generated"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_doc_outline","arguments":{"status":"generated"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/get_doc_outline

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/get_doc_outline' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"status":"generated"}}'
```

<!-- /widget -->
