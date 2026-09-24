---
title: "Call tool"
description: "Run a tool this connection serves but tools/list does not name — the webhook alert registrars ('notify us when traffic drops'), the agent's folder, giving a finished project away…"
---

# Call tool

<!-- widget:mcp access=read -->

## call_tool

Run a tool this connection serves but tools/list does not name — the webhook alert registrars ('notify us when traffic drops'), the agent's folder, giving a finished project away (create_claim_link / revoke_claim_link), changing who may SEE the site. Find the name with find_tool first: a match marked `call: "call_tool"` is one of these, and calling it by name fails inside your own client, which offers only what tools/list named. Pass `name` and that tool's own `arguments` (find_tool's `accepts` lists the fields); the call is billed, scoped and logged exactly as a direct call would be, and the answer is the tool's own, unchanged. A name your client DOES list needs no hop — call that one directly.

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | yes | The tool to run, exactly as find_tool named it — e.g. 'create_claim_link'. |
| `arguments` | object | no | That tool's own arguments, as an object. Omit for a tool that takes none. |

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
    "name": "call_tool",
    "arguments": {
      "name": "<name>"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer YOUR_MCP_OAUTH_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"call_tool","arguments":{"name":"<name>"}}}'
```

<!-- /widget -->
