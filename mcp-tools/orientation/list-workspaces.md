---
title: "List workspaces"
description: "List your Docsbook documentation projects — one line each: id, repo, name, live URL, plan, whether the assistant is on, and when it last published."
---

# List workspaces

<!-- widget:mcp access=read -->

## list_workspaces

List your Docsbook documentation projects — one line each: id, repo, name, live URL, plan, whether the assistant is on, and when it last published. This is the PICKER for 'which projects do I have'. When the user already NAMED the project, do not start here: pass the name to get_workspace (or as workspace_id on any tool) and the server resolves it. With `query`, returns only the projects matching a name, repo, domain or URL fragment, best match first — the fallback when a name did not resolve. For a project's full settings call get_workspace on the one you picked.

| Field | Type | Required | Description |
|---|---|---|---|
| `query` | string | no | Narrow to projects matching this — part of a name, a repo, a domain or a URL. Best match first. Omit to list everything. |
| `limit` | integer | no | Rows to return (default 50). The answer says how many matched in total. |

### Returns

| Field | Type | Description |
|---|---|---|
| `total` | number | — |
| `matched` | number | — |
| `shown` | number | — |
| `query` | string | — |
| `workspaces` | object[] | { id, repoFullName, customName, site_url, customDomain, plan, visibility, aiEnabled, lastPublishedAt, lastUsedAt, createdAt, publish_mismatch_warning?, site_url_collision_warning? }. |
| `note` | string | — |

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "list_workspaces",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_workspaces","arguments":{}}}'
```

### REST

```bash
curl 'https://docsbook.io/api/v1/list_workspaces' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Result

```json
{
  "total": 0,
  "matched": 0,
  "shown": 0,
  "query": "<query>",
  "workspaces": [],
  "note": "<note>"
}
```

<!-- /widget -->
