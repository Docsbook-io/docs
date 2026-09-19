---
title: "Upload translation"
description: "Upload or replace a translation for a workspace document."
---

# Upload translation

<!-- widget:mcp access=write price-millicents=2000 -->

## upload_translation

Upload or replace a translation for a workspace document. Creates a draft by default. This is how an EXTERNAL translator returns its work: the translation webhook notifies you, you translate, you call this. Pass back the `source_blob_sha` the webhook gave you as `source_hash` and set origin 'external_api', or the freshness surfaces cannot tell which commit your translation belongs to. REQUIRES PRO or higher.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `source_path` | string | yes | Source document path (e.g. 'guides/quick-start.md') |
| `language` | string | yes | Target language code (e.g. 'es', 'fr') |
| `content` | string | yes | Translated content |
| `status` | string | no | Status (default: draft) One of: `draft`, `published`, `outdated`. |
| `source_hash` | string | no | Git blob sha (40 hex) of the SOURCE file this was translated FROM — pass the `source_blob_sha` the translation webhook delivered, verbatim. This is what makes 'is this commit translated?' answerable: without it the row records only a hash of your own output, which no commit can ever match. Omit for a hand-written translation whose freshness is a person's call. |
| `origin` | string | no | Who produced it: 'external_api' for a machine translator answering the webhook (compared against the repo like any machine translation), 'manual_upload' for a person's own words (never reported as stale). Default 'manual_upload'. One of: `manual_upload`, `external_api`. |

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
    "name": "upload_translation",
    "arguments": {
      "workspace_id": "<workspace_id>",
      "source_path": "<source_path>",
      "language": "<language>",
      "content": "<content>",
      "status": "draft",
      "origin": "manual_upload"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"upload_translation","arguments":{"workspace_id":"<workspace_id>","source_path":"<source_path>","language":"<language>","content":"<content>","status":"draft","origin":"manual_upload"}}}'
```

<!-- /widget -->
