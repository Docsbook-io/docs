---
title: "Grant repo access"
description: "Whether Docsbook can COMMIT to a GitHub repository — and, when it cannot, the one URL that fixes it."
---

# Grant repo access

<!-- widget:mcp access=write -->

## grant_repo_access

Whether Docsbook can COMMIT to a GitHub repository — and, when it cannot, the one URL that fixes it.
Call this BEFORE `write_docs` on any project whose site is served from a repository Docsbook does not host, and call it whenever a write comes back NO_GITHUB_ACCESS. It writes nothing and needs no GitHub authorisation of its own.
🔴 `can_write: true` is not the whole answer — read `works_unattended`. A repository reachable only through a signed-in browser session cannot be published to by an agent, a schedule or an MCP client, which is every caller on this side of the wire: that case reports `route: "your_session"` and still carries a `fix`.
The fix is always the same shape and the owner does it once, on GitHub's own screen: install the Docsbook GitHub App on the repository with "Contents: Read and write". That authorisation belongs to the repository rather than to a session, so it keeps working at 03:00. Nothing this tool or any other can do grants it — hand the URL to the person and stop.
`repo` is optional: omitted, it answers for the repository this project already publishes to. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `repo` | string | no | Repository as 'owner/name'. Defaults to the one this project publishes to. |

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
    "name": "grant_repo_access",
    "arguments": {}
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"grant_repo_access","arguments":{}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/grant_repo_access

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/grant_repo_access' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{}}'
```

<!-- /widget -->
