---
title: "Set translation mode"
description: "Set the translation workflow mode for a workspace: 'auto' (Docsbook AI), 'manual' (drafts via API), or 'external' (forward to webhook)."
---

# Set translation mode

<!-- widget:mcp access=write price-millicents=2000 -->

## set_translation_mode

Set the translation workflow mode for a workspace: 'auto' (Docsbook AI), 'manual' (drafts via API), or 'external' (forward to webhook). REQUIRES PRO or higher.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `mode` | string | yes | Translation workflow mode One of: `auto`, `manual`, `external`. |
| `external_webhook_url` | string | no | Webhook URL (required for 'external' mode, empty string clears) |

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
    "name": "set_translation_mode",
    "arguments": {
      "workspace_id": "<workspace_id>",
      "mode": "auto"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"set_translation_mode","arguments":{"workspace_id":"<workspace_id>","mode":"auto"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/set_translation_mode

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `mode` | string | yes | Translation workflow mode One of: `auto`, `manual`, `external`. |
| `external_webhook_url` | string | no | Webhook URL (required for 'external' mode, empty string clears) |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/set_translation_mode' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"workspace_id":"<workspace_id>","mode":"auto"}'
```

<!-- /widget -->
