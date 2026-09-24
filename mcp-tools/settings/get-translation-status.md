---
title: "Get translation status"
description: "How each enabled language stands against the source RIGHT NOW: pages current / behind / missing / manual, the percentage, whether a run is in flight and how far along, and what…"
---

# Get translation status

<!-- widget:mcp access=read price-millicents=3 -->

## get_translation_status

How each enabled language stands against the source RIGHT NOW: pages current / behind / missing / manual, the percentage, whether a run is in flight and how far along, and what the last run did — including which agent run started it. Coverage is null (never 0) when the source repository could not be read.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `languages` | string[] | no | ISO codes to report on (default: every language switched on for this project) |

### Returns

| Field | Type | Description |
|---|---|---|
| `…` | … | Per enabled language: pages current / behind / missing / manual, percentage, whether a run is in flight, and what the last run did. |

### Use cases

- Call this BEFORE run_translation_pass: a language already level with the source costs money to re-translate and changes nothing.

### Limitations

- REQUIRES PRO or higher.

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "get_translation_status",
    "arguments": {
      "workspace_id": "<workspace_id>"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer YOUR_MCP_OAUTH_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_translation_status","arguments":{"workspace_id":"<workspace_id>"}}}'
```

### REST

```bash
curl 'https://docsbook.io/api/v1/get_translation_status?workspace_id=%3Cworkspace_id%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Result

```json
{
  "…": "<…>"
}
```

<!-- /widget -->
