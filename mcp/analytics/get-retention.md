---
title: "Get retention"
description: "W1/W4 return rate by weekly cohort (BUSINESS) — the only cohort view in the system; everything else is a snapshot."
---

# Get retention

<!-- widget:mcp access=read price-millicents=4000 -->

## get_retention

W1/W4 return rate by weekly cohort (BUSINESS) — the only cohort view in the system; everything else is a snapshot. READ THE CAVEAT: visitors are hashed IPs, so mobile networks split one reader into many and office NAT merges many into one. Report it as a trend, never a headcount. Direction depends on the section: high return is healthy for reference docs and a FAILURE for onboarding.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `period` | string | no | Time range (default: 7d) |

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
    "name": "get_retention",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_retention","arguments":{}}}'
```

<!-- /widget -->
