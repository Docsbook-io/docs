---
title: "Find widget"
description: "Search the Docsbook widget catalog for an interactive UI widget matching the user's request."
---

# Find widget

<!-- widget:mcp access=read anonymous -->

## find_widget

Search the Docsbook widget catalog for an interactive UI widget matching the user's request. Returns matching widget ids and summaries. Use this to discover available widgets (e.g. 'dark mode toggle', 'analytics chart', 'search bar'). After finding a widget, use the returned resourceUri to read its HTML bundle via the ui:// resource.

| Field | Type | Required | Description |
|---|---|---|---|
| `query` | string | yes | Free-text description of what the user wants, e.g. 'dark mode toggle' or 'analytics dashboard'. |
| `mode` | string | no | Restrict matches to widgets available in this mode (admin or user). One of: `admin`, `user`. |

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
    "name": "find_widget",
    "arguments": {
      "query": "<query>",
      "mode": "admin"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"find_widget","arguments":{"query":"<query>","mode":"admin"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### GET /api/v1/find_widget

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `query` | string | yes | Free-text description of what the user wants, e.g. 'dark mode toggle' or 'analytics dashboard'. |
| `mode` | string | no | Restrict matches to widgets available in this mode (admin or user). One of: `admin`, `user`. |

#### Request

```bash
curl 'https://docsbook.io/api/v1/find_widget?query=%3Cquery%3E&mode=admin' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->
