---
title: "Get info"
description: "What this Docsbook MCP server is and how to work it: the plan tiers and what each unlocks, every tool family with the rule for when it applies and how many tools it holds, how a…"
---

# Get info

<!-- widget:mcp access=read anonymous -->

## get_info

What this Docsbook MCP server is and how to work it: the plan tiers and what each unlocks, every tool family with the rule for when it applies and how many tools it holds, how a project is named on every tool, whether this token can write, and how a site is created. Call it once, first, when you have no other orientation.

### Returns

| Field | Type | Description |
|---|---|---|
| `product` | string | — |
| `description` | string | — |
| `creating_a_site` | string | — |
| `scoped_workspace` | string | — |
| `scope_hint` | string | — |
| `which_project` | string | How to name a project on any tool, when the endpoint is not scoped to one. |
| `plan_tiers` | object | free / pro / business, each with price, billing and what it includes. |
| `tools_total` | number | — |
| `tool_families` | object[] | { family, purpose } per family this server registers. |
| `token_scope` | string | — |
| `write_access` | string | — |

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

### REST

```bash
curl 'https://docsbook.io/api/v1/get_info' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Result

```json
{
  "product": "<product>",
  "description": "<description>",
  "creating_a_site": "<creating_a_site>",
  "scoped_workspace": "<scoped_workspace>",
  "scope_hint": "<scope_hint>",
  "which_project": "<which_project>",
  "plan_tiers": {},
  "tools_total": 0,
  "tool_families": [],
  "token_scope": "<token_scope>",
  "write_access": "<write_access>"
}
```

<!-- /widget -->
