---
title: "Read search trends"
description: "The last three months of relative search interest for up to 5 terms charted against each other, plus the queries rising fastest around them and where in the world the interest…"
---

# Read search trends

<!-- widget:mcp access=read price-millicents=6000 -->

## read_search_trends

The last three months of relative search interest for up to 5 terms charted against each other, plus the queries rising fastest around them and where in the world the interest sits. Direction, which no other reading here has: a phrase with steady volume and a falling trend is a page worth writing once, the same volume rising is a page worth writing now — and relatedQueries_rising is the only place in this product that says what people STARTED asking about a topic recently. Routes from questions like: is interest in this topic growing or dying · what are people suddenly asking about this · is this term seasonal · «растёт или падает интерес к теме» · «о чём вдруг начали спрашивать» · «сезонный ли это запрос». Not: The values are RELATIVE interest, 0-100, normalised to the peak of this call's own series — never a count of searches and never comparable with another call's numbers. The absolute monthly figure is read_keyword_demand, the exact phrasings people type are read_search_suggestions, and the last point of any series is marked isPartial because its week is still filling. Example: Chart the last three months of interest in "openapi docs" against "swagger ui" worldwide, and show what is rising around them. Pass `workspace_id` whenever the answer will be quoted later: it is what files the reading in that project's history with a `call_id`, and only a `call_id` (or a URL) is accepted as the source of a figure on an audit finding — the tool's own name is not a source. One call fetches at most 20 results and costs $0.0600.

| Field | Type | Required | Description |
|---|---|---|---|
| `terms` | string[] | yes | Up to 5 search terms to chart against each other, e.g. ["openapi docs", "swagger ui"] — values are relative to the highest point across the terms in THIS call. |
| `country` | string | no | Two-letter country code to scope interest to ("US", "DE", "GB"). Omit for worldwide, which also changes which regional breakdown comes back. |
| `time_range` | string | no | One of exactly: "now 1-H", "now 4-H", "now 1-d", "now 7-d", "today 1-m", "today 3-m", "today 5-y", "all". There is no 12-month value; any other string is rejected. Defaults to "today 3-m". |
| `workspace_id` | string | no | The project this reading is FOR. 🔴 Pass it whenever the answer will be QUOTED later: it is what files the call in that project's history with a `call_id`, and a `call_id` is the only thing an opportunity accepts as the source of a demand figure (`demand_source`). Nothing about the project is sent to the site being read. Omitted, the reading still comes back — it simply lands in no history, so nothing afterwards can point at it. Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |

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
    "name": "read_search_trends",
    "arguments": {
      "terms": []
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"read_search_trends","arguments":{"terms":[]}}}'
```

<!-- /widget -->
