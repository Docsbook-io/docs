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

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

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

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/get_info' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Response

```json
{
  "ok": true,
  "result": {
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
  },
  "duration_ms": 0
}
```

### Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |

<!-- /widget -->
