---
title: "Grant repo access"
description: "Whether Docsbook can COMMIT to a GitHub repository — and, when it cannot, the one URL that fixes it."
---

# Grant repo access

<!-- widget:api -->

## POST /api/v1/grant_repo_access

Whether Docsbook can COMMIT to a GitHub repository — and, when it cannot, the one URL that fixes it.
Call this BEFORE `write_docs` on any project whose site is served from a repository Docsbook does not host, and call it whenever a write comes back NO_GITHUB_ACCESS. It writes nothing and needs no GitHub authorisation of its own.
🔴 `can_write: true` is not the whole answer — read `works_unattended`. A repository reachable only through a signed-in browser session cannot be published to by an agent, a schedule or an MCP client, which is every caller on this side of the wire: that case reports `route: "your_session"` and still carries a `fix`.
The fix is always the same shape and the owner does it once, on GitHub's own screen: install the Docsbook GitHub App on the repository with "Contents: Read and write". That authorisation belongs to the repository rather than to a session, so it keeps working at 03:00. Nothing this tool or any other can do grants it — hand the URL to the person and stop.
`repo` is optional: omitted, it answers for the repository this project already publishes to.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/grant_repo_access`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `repo` | string | no | Repository as 'owner/name'. Defaults to the one this project publishes to. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/grant_repo_access' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
