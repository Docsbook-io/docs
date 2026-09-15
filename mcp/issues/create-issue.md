---
title: "Create issue"
description: "File a GitHub issue on this project's repository."
---

# Create issue

<!-- widget:mcp access=write price-millicents=2000 -->

## create_issue

File a GitHub issue on this project's repository. THIS IS HOW A FINDING OUTLIVES THE CONVERSATION — when you have audited, diagnosed or measured something and found work worth doing, write it down here rather than only in your answer. One call per issue; do not batch several findings into one.
Body: what you observed (with the evidence you actually collected), why it matters for this project, and what done looks like.
Call list_issues first and skip anything that duplicates an open issue.
Label it with the stage of work it belongs to when one fits: observe, understand, discover, decide, plan, execute, measure, verify, learn, coordinate.
Returns the created issue's number and link — report those verbatim, never a link you built yourself. REQUIRES a read-write MCP token. BEFORE FILING THIS, call `docsbook_expert` with the outcome you want: it says whether this is the thing worth doing first and what it would move, so the backlog is ranked rather than merely long. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `title` | string | yes | The finding itself, not its category. |
| `body` | string | no | Markdown body: what you observed (with evidence), why it matters here, what done looks like. |
| `labels` | string[] | no | Labels to attach, e.g. ['measure']. Labels that do not exist yet are created by GitHub. |

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
    "name": "create_issue",
    "arguments": {
      "title": "<title>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"create_issue","arguments":{"title":"<title>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/create_issue

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/create_issue' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"title":"<title>"}}'
```

<!-- /widget -->
