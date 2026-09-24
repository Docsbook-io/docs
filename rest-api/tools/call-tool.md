---
title: "Call any tool by name"
description: "Call a tool by name, over plain REST — no MCP client, no JSON-RPC transport, no OAuth dance."
---

# Call any tool by name

<!-- widget:api -->

## POST /api/v1/tools/{tool}

Call a tool by name, over plain REST — no MCP client, no JSON-RPC transport, no
OAuth dance. The request is dispatched into the exact same server your own MCP-connected agent
reaches, so it is billed and logged identically: the same flat per-call price off the workspace
balance and the same row in the event feed, marked `api` rather than `mcp` so call history can
tell the two apart.

This reaches exactly the tools your API key's owner surface does — orientation, delegating a job to
`docsbook_agent` and watching it, and reading your own documentation and Docsbook's own docs. Most
of those already have their own path below (**Tools** section) with a real `GET` or `POST` and a
typed request; this dispatch-by-name form exists for the handful that do not
(`create_workspace`, `docsbook_agent`, `docsbook_agent_reply`, `docsbook_agent_stop`) and for
a caller that holds the tool name in a variable rather than a literal.

Everything else this server can do — writing documentation, translations, analytics beyond your own
project, webhooks, the product's own memory — is not reachable by name here, on purpose: since
2026-09-18 that surface belongs to `docsbook_agent`, the background worker your token can start and
watch. A tool name outside your owner surface answers `404 TOOL_NOT_FOUND`, never a partial result.

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
