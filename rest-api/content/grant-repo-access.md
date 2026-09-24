---
title: "Grant repo access"
description: "Whether Docsbook can COMMIT to a GitHub repository — and, when it cannot, the one URL that fixes it."
---

# Grant repo access

<!-- widget:api -->

## POST /api/v1/grant_repo_access

Whether Docsbook can COMMIT to a GitHub repository — and, when it cannot, the one URL that fixes it. It writes nothing and needs no GitHub authorisation of its own. The fix is always the same shape and the owner does it once, on GitHub's own screen: install the Docsbook GitHub App on the repository with "Contents: Read and write". That authorisation belongs to the repository rather than to a session, so it keeps working at 03:00. Nothing this tool or any other can do grants it — hand the URL to the person and stop. `repo` is optional: omitted, it answers for the repository this project already publishes to.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/grant_repo_access`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `repo` | string | no | Repository as 'owner/name'. Defaults to the one this project publishes to. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

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

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/grant_repo_access' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

### Response

```json
{
  "ok": true,
  "result": {
    "repo": "<repo>",
    "can_write": true,
    "route": "<route>",
    "works_unattended": true,
    "detail": "<detail>",
    "fix": "<fix>",
    "is_this_projects_repo": true,
    "hint": "<hint>"
  },
  "duration_ms": 0
}
```

### Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |

<!-- /widget -->
