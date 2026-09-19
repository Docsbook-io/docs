---
title: "Configure source"
description: "Change or disconnect one of this project's connected sources (see `list_sources`): rename it, rewrite the `note` every tool reads as instruction, pause it, or remove it."
---

# Configure source

<!-- widget:mcp access=write price-millicents=800 -->

## configure_source

Change or disconnect one of this project's connected sources (see `list_sources`): rename it, rewrite the `note` every tool reads as instruction, pause it, or remove it.
Pausing (`enabled: false`) keeps the row and stops every tool and agent from reading it — the move for a repository that has moved or a site that is being rebuilt. `disconnect: true` deletes it, along with any GitHub authorisation attached to it.
Identify the source by `source_id` from list_sources, or by `match` (a word from its label or URL). REQUIRES a read-write MCP token.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `source_id` | number | no | The source's id from list_sources. |
| `match` | string | no | Part of its label or URL, when you do not have the id (e.g. 'acme/api'). |
| `note` | string | no | Replace what this source is for. Read as instruction by everything that reads the source. |
| `label` | string | no | Rename it in the list. |
| `enabled` | boolean | no | false pauses the source: it stays connected and nothing reads it. |
| `disconnect` | boolean | no | true removes the source entirely, with any GitHub authorisation attached to it. |

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
    "name": "configure_source",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"configure_source","arguments":{}}}'
```

<!-- /widget -->
