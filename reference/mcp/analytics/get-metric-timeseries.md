---
title: "Get metric timeseries"
description: "One headline metric BY DAY (PRO) — the trend, not the snapshot every other analytics tool returns."
---

# Get metric timeseries

<!-- widget:mcp access=read -->

## get_metric_timeseries

One headline metric BY DAY (PRO) — the trend, not the snapshot every other analytics tool returns. Use it to answer 'is this getting worse' and to line a turn up against a release date. Days built on very few visits are flagged `thin`: read the shape, never a single point. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `period` | string | no | Time range (default: 7d) |
| `metric` | string | no | Which metric to plot (default: dead_end_rate) One of: `dead_end_rate`, `self_serve_resolution_rate`, `visits`, `success`, `dead_ends`, `median_time_to_first_value`. |

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
    "name": "get_metric_timeseries",
    "arguments": {
      "metric": "dead_end_rate"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_metric_timeseries","arguments":{"metric":"dead_end_rate"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/get_metric_timeseries

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/get_metric_timeseries' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"metric":"dead_end_rate"}}'
```

<!-- /widget -->
