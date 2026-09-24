---
title: "Get info"
description: "What this Docsbook MCP server is and how to work it: the plan tiers and what each unlocks, every tool family with the rule for when it applies and how many tools it holds, how a…"
---

# Get info

<!-- widget:api -->

## GET /api/v1/get_info

What this Docsbook MCP server is and how to work it: the plan tiers and what each unlocks, every tool family with the rule for when it applies and how many tools it holds, how a project is named on every tool, whether this token can write, and how a site is created. Call it once, first, when you have no other orientation.

**Price** — free, never metered.

Also reachable without a token on this workspace's public MCP endpoint.

Also reachable by name at `POST /api/v1/tools/get_info`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/get_info' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
