---
title: "Run translation pass"
description: "Start a REAL translation catch-up run for one or more languages: the same batch the panel's 'Translate now' starts, with pages that are behind translated before pages that are…"
---

# Run translation pass

<!-- widget:mcp access=write price-millicents=2000 -->

## run_translation_pass

Start a REAL translation catch-up run for one or more languages: the same batch the panel's 'Translate now' starts, with pages that are behind translated before pages that are missing. Answers with the job id per language as soon as the runs are open — the pages themselves land over the following minutes and are visible in Translations. Languages already level with the source are skipped unless force=true, a language with a live run is left alone, and at most 3 languages are started per call. It NEVER discards existing translations (that is the owner's 'Re-translate everything'). REQUIRES PRO or higher.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `languages` | string[] | no | ISO codes to bring level (default: every language switched on for this project) |
| `force` | boolean | no | Run even for a language coverage says is already level with the source (default false) |

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
    "name": "run_translation_pass",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"run_translation_pass","arguments":{"workspace_id":"<workspace_id>"}}}'
```

<!-- /widget -->
