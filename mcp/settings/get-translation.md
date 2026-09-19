---
title: "Get translation"
description: "Get the translation for a specific source path and language."
---

# Get translation

<!-- widget:mcp access=read price-millicents=800 -->

## get_translation

Get the translation for a specific source path and language. REQUIRES PRO or higher.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `source_path` | string | yes | Source document path |
| `language` | string | yes | Target language code |

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
    "name": "get_translation",
    "arguments": {
      "workspace_id": "<workspace_id>",
      "source_path": "<source_path>",
      "language": "<language>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_translation","arguments":{"workspace_id":"<workspace_id>","source_path":"<source_path>","language":"<language>"}}}'
```

<!-- /widget -->
