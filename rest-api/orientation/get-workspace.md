---
title: "Get workspace"
description: "Get one project in full — every setting an update_* tool can change, its plan and capabilities, its call to action, its live site_url."
---

# Get workspace

<!-- widget:api -->

## GET /api/v1/get_workspace

Get one project in full — every setting an update_* tool can change, its plan and capabilities, its call to action, its live site_url. Address it the way the user did: a numeric id, 'owner/repo', the repo name alone, the display name, the docs URL or the custom domain — the server resolves the name, so this is the FIRST call when the user names a project, never list_workspaces. A name matching several projects returns AMBIGUOUS_WORKSPACE with the candidates; one matching none returns WORKSPACE_NOT_FOUND with the closest.

**Price** — free, never metered.

Also reachable by name at `POST /api/v1/tools/get_workspace`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `repo` | string | no | 'owner/repo', or anything else the user calls the project — a repo name, a display name, a docs URL, a custom domain. Resolved the same way as a textual workspace_id. |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/get_workspace' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
