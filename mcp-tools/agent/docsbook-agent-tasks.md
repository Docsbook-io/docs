---
title: "Docsbook agent tasks"
description: "Every job this account has given the Docsbook agent, newest first — what was asked for, what is running now, what finished and how."
---

# Docsbook agent tasks

<!-- widget:mcp access=read price-millicents=3 -->

## docsbook_agent_tasks

Every job this account has given the Docsbook agent, newest first — what was asked for, what is running now, what finished and how. Narrow to one project with workspace_id.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Only this project's jobs. Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `limit` | number | no | How many, 1-100. Default 20. |

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "docsbook_agent_tasks",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"docsbook_agent_tasks","arguments":{}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### GET /api/v1/docsbook_agent_tasks

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `workspace_id` | string | no | Only this project's jobs. Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `limit` | number | no | How many, 1-100. Default 20. |

#### Request

```bash
curl 'https://docsbook.io/api/v1/docsbook_agent_tasks' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->
