---
title: "Grant repo access"
description: "Whether Docsbook can COMMIT to a GitHub repository — and, when it cannot, the one URL that fixes it."
---

# Grant repo access

<!-- widget:mcp access=write price-millicents=3 -->

## grant_repo_access

Whether Docsbook can COMMIT to a GitHub repository — and, when it cannot, the one URL that fixes it. It writes nothing and needs no GitHub authorisation of its own. The fix is always the same shape and the owner does it once, on GitHub's own screen: install the Docsbook GitHub App on the repository with "Contents: Read and write". That authorisation belongs to the repository rather than to a session, so it keeps working at 03:00. Nothing this tool or any other can do grants it — hand the URL to the person and stop. `repo` is optional: omitted, it answers for the repository this project already publishes to.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `repo` | string | no | Repository as 'owner/name'. Defaults to the one this project publishes to. |

### Returns

| Field | Type | Description |
|---|---|---|
| `repo` | string | owner/name, as asked about. |
| `can_write` | boolean | — |
| `route` | string | `github_app`, `docsbook_account`, `your_session` or `none` — which credential answered. |
| `works_unattended` | boolean | Whether a run with nobody signed in can publish here. `your_session` is false. |
| `detail` | string | — |
| `fix` | object | null | { action, url } — the one thing that changes the answer. |
| `is_this_projects_repo` | boolean | — |
| `hint` | string | — |

### Use cases

- Call this BEFORE `write_docs` on any project whose site is served from a repository Docsbook does not host, and call it whenever a write comes back NO_GITHUB_ACCESS.

### Limitations

- 🔴 `can_write: true` is not the whole answer — read `works_unattended`.
- A repository reachable only through a signed-in browser session cannot be published to by an agent, a schedule or an MCP client, which is every caller on this side of the wire: that case reports `route: "your_session"` and still carries a `fix`.

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
  -H 'Authorization: Bearer YOUR_MCP_OAUTH_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"grant_repo_access","arguments":{}}}'
```

### REST

```bash
curl -X POST 'https://docsbook.io/api/v1/grant_repo_access' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

### Result

```json
{
  "repo": "<repo>",
  "can_write": true,
  "route": "<route>",
  "works_unattended": true,
  "detail": "<detail>",
  "fix": "<fix>",
  "is_this_projects_repo": true,
  "hint": "<hint>"
}
```

<!-- /widget -->
