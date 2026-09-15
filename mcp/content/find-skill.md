---
title: "Find skill"
description: "Search the Docsbook docs-skills catalog (Docsbook-io/docs-skills) for a skill matching the user's request."
---

# Find skill

<!-- widget:mcp access=read anonymous -->

## find_skill

Search the Docsbook docs-skills catalog (Docsbook-io/docs-skills) for a skill matching the user's request. Returns matching SKILL.md files with raw_url — read the skill via WebFetch and follow its steps. Use it when the user wants a repeatable, multi-step workflow. NOT the first move for a request a tool here answers directly — create_workspace, write_docs, update_*, register_webhook_<event>, get_* — call that tool. This tells you what is here, not what to do with it. If you have not already asked `docsbook_expert` what the user actually wants done, ask it — one call returns the ordered steps with the tool on each, and it changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `query` | string | yes | Free-text description of what the user wants, e.g. 'enable auto-translation' or 'create AGENTS.md'. |
| `filters` | object | no | — |

<!-- /widget -->

## `filters` fields

| Field | Type | Required | Description |
|---|---|---|---|
| `category` | string | no | Restrict matches to a single skill category. One of: `analysis`, `creation`, `publishing`, `automation`, `observability`. |
| `requires_plan` | string | no | Restrict matches to skills available on this plan. One of: `free`, `pro`, `business`. |
| `max_results` | integer | no | Maximum number of matches to return (1-20). Default 5. |

## Call it

<!-- widget:code-group -->

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "find_skill",
    "arguments": {
      "query": "<query>"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"find_skill","arguments":{"query":"<query>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/find_skill

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/find_skill' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"query":"<query>"}}'
```

<!-- /widget -->
