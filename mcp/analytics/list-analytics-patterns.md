---
title: "List analytics patterns"
description: "Catalog of ready-made analytics patterns (visit outcomes, dead-end pages, content health, exit pages, search effectiveness, route patterns, forward/reverse funnels, zero-click…"
---

# List analytics patterns

<!-- widget:mcp access=read price-millicents=4000 -->

## list_analytics_patterns

Catalog of ready-made analytics patterns (visit outcomes, dead-end pages, content health, exit pages, search effectiveness, route patterns, forward/reverse funnels, zero-click search, frustration signals, metric trends, retention, traffic, individual visits) with the plan each needs and the metrics it reports. Call this FIRST when you don't know which analytics tool answers a question, or before composing a chart — it is cheaper than guessing.

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
    "name": "list_analytics_patterns",
    "arguments": {}
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_analytics_patterns","arguments":{}}}'
```

<!-- /widget -->
