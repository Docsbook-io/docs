---
title: "Get info"
description: "What this Docsbook MCP server is and how to work it: the plan tiers and what each unlocks, every tool family with the rule for when it applies and how many tools it holds, how a…"
---

# Get info

<!-- widget:mcp access=read anonymous -->

## get_info

What this Docsbook MCP server is and how to work it: the plan tiers and what each unlocks, every tool family with the rule for when it applies and how many tools it holds, how a project is named on every tool, whether this token can write, and how a site is created. Call it once, first, when you have no other orientation.

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
    "name": "get_info",
    "arguments": {}
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_info","arguments":{}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### GET /api/v1/get_info

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |

#### Request

```bash
curl 'https://docsbook.io/api/v1/get_info' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->
