---
title: "Get workspace"
description: "Get one project in full — every setting an update_* tool can change, its plan and capabilities, its call to action, its live site_url."
---

# Get workspace

<!-- widget:mcp access=read -->

## get_workspace

Get one project in full — every setting an update_* tool can change, its plan and capabilities, its call to action, its live site_url. Address it the way the user did: a numeric id, 'owner/repo', the repo name alone, the display name, the docs URL or the custom domain — the server resolves the name, so this is the FIRST call when the user names a project, never list_workspaces. A name matching several projects returns AMBIGUOUS_WORKSPACE with the candidates; one matching none returns WORKSPACE_NOT_FOUND with the closest.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `repo` | string | no | 'owner/repo', or anything else the user calls the project — a repo name, a display name, a docs URL, a custom domain. Resolved the same way as a textual workspace_id. |

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
    "name": "get_workspace",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_workspace","arguments":{}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### GET /api/v1/get_workspace

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `workspace_id` | string | no | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `repo` | string | no | 'owner/repo', or anything else the user calls the project — a repo name, a display name, a docs URL, a custom domain. Resolved the same way as a textual workspace_id. |

#### Request

```bash
curl 'https://docsbook.io/api/v1/get_workspace' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->
