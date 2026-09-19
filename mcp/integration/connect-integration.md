---
title: "Connect integration"
description: "GET THE LINK THAT CONNECTS AN APP — GitHub, Slack, Discord, Notion, a calendar, anything in the catalogue — and what connecting it would let this project's agents do."
---

# Connect integration

<!-- widget:mcp access=write price-millicents=800 -->

## connect_integration

GET THE LINK THAT CONNECTS AN APP — GitHub, Slack, Discord, Notion, a calendar, anything in the catalogue — and what connecting it would let this project's agents do. 🔴 THIS DOES NOT CONNECT ANYTHING, and must not be reported as if it had: authorising an app needs the owner's own browser session, which no API call can stand in for. Give them the `connect_url` and say in one line what it unlocks; they open it, and the next `list_agent_jobs` shows the account attached. Call this the moment a request depends on an app that `list_agent_jobs` reports as not connected, rather than reporting the request as impossible.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `connector` | string | yes | The connector id from `list_agent_jobs`.integrations — e.g. 'github', 'slack', 'discord'. |

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
    "name": "connect_integration",
    "arguments": {
      "connector": "<connector>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"connect_integration","arguments":{"connector":"<connector>"}}}'
```

<!-- /widget -->
