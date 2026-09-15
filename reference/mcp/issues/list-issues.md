---
title: "List issues"
description: "List the GitHub issues on this project's repository — the work that is open on it, and what has been closed."
---

# List issues

<!-- widget:mcp access=read -->

## list_issues

List the GitHub issues on this project's repository — the work that is open on it, and what has been closed. Call this BEFORE create_issue: an issue that duplicates an open one is worse than no issue. Pull requests are never included. An empty list means the tracker is genuinely empty — never invent an issue number. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `state` | string | no | Which issues to return. Default 'open'. One of: `open`, `closed`, `all`. |
| `labels` | string[] | no | Only issues carrying ALL of these labels, e.g. ['measure']. |
| `limit` | number | no | How many to return, 1-100. Default 30. |

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
    "name": "list_issues",
    "arguments": {
      "state": "open"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_issues","arguments":{"state":"open"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/list_issues

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/list_issues' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"state":"open"}}'
```

<!-- /widget -->
