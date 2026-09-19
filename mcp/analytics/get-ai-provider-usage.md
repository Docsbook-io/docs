---
title: "Get ai provider usage"
description: "Docsbook's OWN OpenRouter account balance and account-wide AI spend for the last 7 and 30 days — not one workspace's wallet (use get_ai_usage for that)."
---

# Get ai provider usage

<!-- widget:mcp access=read price-millicents=4000 -->

## get_ai_provider_usage

Docsbook's OWN OpenRouter account balance and account-wide AI spend for the last 7 and 30 days — not one workspace's wallet (use get_ai_usage for that). Returns provider_balance (purchased/spent/remaining credits, or available:false with why when no OpenRouter key is configured in this environment) and usage.last_7d/last_30d (raw provider cost vs what was billed to customers, by category, so margin is a subtraction). For checking spend health before or during a background job, not for a customer-facing answer.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Workspace ID (billing context for this call only; the figures returned are account-wide). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |

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
    "name": "get_ai_provider_usage",
    "arguments": {
      "workspace_id": "<workspace_id>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_ai_provider_usage","arguments":{"workspace_id":"<workspace_id>"}}}'
```

<!-- /widget -->
