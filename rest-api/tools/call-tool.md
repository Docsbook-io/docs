---
title: "Call any tool by name"
description: "Call a tool by name, over plain REST — no MCP client, no JSON-RPC transport, no OAuth dance."
---

# Call any tool by name

<!-- widget:api -->

## POST /api/v1/tools/{tool}

Call a tool by name, over plain REST — no MCP client, no JSON-RPC transport, no OAuth dance. The request is dispatched into the exact same server your own MCP-connected agent reaches, so it is billed and logged identically: the same per-call price off the workspace balance and the same row in the event feed, marked `api` rather than `mcp` so call history can tell the two apart.

Every tool this reaches also has its own path in this reference, with a real `GET` (reads) or `POST` (changes) and its typed arguments — prefer those. This dispatch-by-name form is for a caller that holds the tool name in a variable rather than a literal. A name your key does not reach answers `404 TOOL_NOT_FOUND`, never a partial result, and is never billed.

The workspace is resolved from the API key, so there is no project to name in the body.

This is the dispatch-by-name form, for a caller that holds the tool name in a variable. Every tool also has its own documented path below, with its real argument schema.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `tool` | string | yes | The tool's name, exactly as `GET /api/mcp/tools` reports it. |
| `args` | object | no | The tool's own arguments, exactly as an MCP client would send them. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | string | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/{tool}' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"period":"30d"}}'
```

### Response

```json
{
  "ok": true,
  "result": "<result>",
  "duration_ms": 0
}
```

### Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `400` | `args` was not a JSON object. |
| `401` | Missing or invalid API key. |
| `404` | `TOOL_NOT_FOUND` — this server serves no tool by that name. Never billed: the call never reached a tool. |

<!-- /widget -->
