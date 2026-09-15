---
title: "Get issue"
description: "Read ONE GitHub issue on this project's repository in full — its complete body, its STATUS in plain words, and WHAT CAME OF IT: the comments, the agent and run that filed it when…"
---

# Get issue

<!-- widget:mcp access=read -->

## get_issue

Read ONE GitHub issue on this project's repository in full — its complete body, its STATUS in plain words, and WHAT CAME OF IT: the comments, the agent and run that filed it when a machine did, and the pull requests written against it (`resulted_in`). The body is where a hypothesis gets written down — what was observed, why it was thought to matter, what done would look like; `resulted_in` is whether anybody acted on it. Read together they are this project's record of "we thought X, we did Y"; read apart, the first is a wish. Use it before acting on an issue listed by list_issues (acting on a 280-character preview is how you do the wrong half of a request) and on any row search_prior_work returned. ALWAYS state whether it is open or closed when you cite it: a closed issue is a decision somebody already took. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `number` | number | yes | The issue number, e.g. 42. |

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
    "name": "get_issue",
    "arguments": {
      "number": 0
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_issue","arguments":{"number":0}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/get_issue

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/get_issue' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"number":0}}'
```

<!-- /widget -->
