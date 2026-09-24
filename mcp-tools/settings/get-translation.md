---
title: "Get translation"
description: "Get the translation for a specific source path and language."
---

# Get translation

<!-- widget:mcp access=read price-millicents=3 -->

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
  -H 'Authorization: Bearer YOUR_MCP_OAUTH_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_translation","arguments":{"workspace_id":"<workspace_id>","source_path":"<source_path>","language":"<language>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### GET /api/v1/get_translation

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `source_path` | string | yes | Source document path |
| `language` | string | yes | Target language code |

#### Request

```bash
curl 'https://docsbook.io/api/v1/get_translation?workspace_id=%3Cworkspace_id%3E&source_path=%3Csource_path%3E&language=%3Clanguage%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->
