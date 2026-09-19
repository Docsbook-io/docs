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
