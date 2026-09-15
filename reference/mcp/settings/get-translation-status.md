---
title: "Get translation status"
description: "How each enabled language stands against the source RIGHT NOW: pages current / behind / missing / manual, the percentage, whether a run is in flight and how far along, and what…"
---

# Get translation status

<!-- widget:mcp access=read price-millicents=800 -->

## get_translation_status

How each enabled language stands against the source RIGHT NOW: pages current / behind / missing / manual, the percentage, whether a run is in flight and how far along, and what the last run did — including which agent run started it. Call this BEFORE run_translation_pass: a language already level with the source costs money to re-translate and changes nothing. Coverage is null (never 0) when the source repository could not be read. REQUIRES PRO or higher. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `languages` | string[] | no | ISO codes to report on (default: every language switched on for this project) |

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
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_translation_status","arguments":{"workspace_id":"<workspace_id>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/get_translation_status

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/get_translation_status' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"workspace_id":"<workspace_id>"}}'
```

<!-- /widget -->
