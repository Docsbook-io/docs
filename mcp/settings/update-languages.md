---
title: "Update languages"
description: "Set the languages the site is served in — the call for 'we need docs in Spanish and German', «нужна документация на испанском»."
---

# Update languages

<!-- widget:mcp access=write price-millicents=2000 -->

## update_languages

Set the languages the site is served in — the call for 'we need docs in Spanish and German', «нужна документация на испанском». REQUIRES PRO plan. `enabled_languages` REPLACES the whole set, so pass the existing languages plus the new ones (read them from get_workspace first). Enabling a language does not translate anything by itself: run_translation_pass starts the first pass, and later passes follow the workspace's translation mode. Supported codes: en, es, fr, de, pt, it, ru, zh, ja, ko, ar, hi, tr, pl, nl. Translated pages are served at https://<username>.docsbook.io/<lang>/<repo>/<path> — language is always a PATH SEGMENT under the user subdomain, never a subdomain itself (never https://<lang>.docsbook.io/). `default_language` is the docs' own source language (auto-detected from the repo README when the project is connected) — it is silently dropped from `enabled_languages` if included, since the docs are already written in it and there is nothing to translate.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `enabled_languages` | string[] | no | ISO language codes to enable |
| `default_language` | string | no | Default language code |

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
    "name": "update_languages",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"update_languages","arguments":{"workspace_id":"<workspace_id>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### POST /api/v1/update_languages

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `enabled_languages` | string[] | no | ISO language codes to enable |
| `default_language` | string | no | Default language code |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/update_languages' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"workspace_id":"<workspace_id>"}'
```

<!-- /widget -->
