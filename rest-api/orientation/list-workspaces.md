---
title: "List workspaces"
description: "List your Docsbook documentation projects — one line each: id, repo, name, live URL, plan, whether the assistant is on, and when it last published."
---

# List workspaces

<!-- widget:api -->

## GET /api/v1/list_workspaces

List your Docsbook documentation projects — one line each: id, repo, name, live URL, plan, whether the assistant is on, and when it last published. This is the PICKER for 'which projects do I have'. When the user already NAMED the project, do not start here: pass the name to get_workspace (or as workspace_id on any tool) and the server resolves it. With `query`, returns only the projects matching a name, repo, domain or URL fragment, best match first — the fallback when a name did not resolve. For a project's full settings call get_workspace on the one you picked.

**Price** — free, never metered.

Also reachable by name at `POST /api/v1/tools/list_workspaces`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `query` | string | no | Narrow to projects matching this — part of a name, a repo, a domain or a URL. Best match first. Omit to list everything. |
| `limit` | integer | no | Rows to return (default 50). The answer says how many matched in total. |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/list_workspaces' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
