---
title: "Call any tool by name"
description: "Call any tool the Docsbook MCP server registers, over plain REST — no MCP client, no JSON-RPC transport, no OAuth dance."
---

# Call any tool by name

<!-- widget:api -->

## POST /api/v1/tools/{tool}

Call any tool the Docsbook MCP server registers, over plain REST — no MCP
client, no JSON-RPC transport, no OAuth dance. The request is dispatched into the exact same server
an MCP-connected agent reaches, so it is billed and logged identically: the same flat per-call price
off the workspace balance and the same row in the event feed, marked `api` rather than `mcp` so
call history can tell the two apart.

The workspace is resolved from the API key, so there is no project to name in the body.

This is the dispatch-by-name form, for a caller that holds the tool name in a variable. Every tool also has its own documented path below, with its real argument schema.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `tool` | string | yes | The tool's name, exactly as `GET /api/mcp/tools` reports it. |
| `args` | object | no | The tool's own arguments, exactly as an MCP client would send them. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/{tool}' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"period":"30d"}}'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `400` | `args` was not a JSON object. |
| `401` | Missing or invalid API key. |
| `404` | `TOOL_NOT_FOUND` — this server serves no tool by that name. Never billed: the call never reached a tool. |
