---
title: "List content widgets"
description: "List the widgets that can be embedded directly in documentation markdown (as opposed to find_widget, which covers interactive widgets rendered in the AI chat)."
---

# List content widgets

<!-- widget:mcp access=read anonymous price-millicents=3 -->

## list_content_widgets

List the widgets that can be embedded directly in documentation markdown (as opposed to find_widget, which covers interactive widgets rendered in the AI chat). Returns, for each widget, what it renders, when to use it, the exact markdown contract it expects, and a copy-pasteable example — and, above them, `writing_style`: how the PROSE between the widgets reads (one- or two-line paragraphs, identifiers in inline code, concepts linked where they are named, bold only where the eye lands) with a page that shows it. Widgets the workspace owner switched off in the admin panel are NOT listed — their markers render as plain markdown, so writing one would produce a page that silently looks unchanged. Call this before writing or editing a docs page that would benefit from a card grid, an accordion, or any other rich content block — the catalog is the live source of truth, so never guess a widget name or syntax.

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | no | Return only this widget (e.g. 'cards'). Omit to list every content widget. |
| `workspace_id` | string | no | Workspace whose widget settings apply. Omit when the token is scoped to a single repo — that workspace is used. Only affects which widgets are switched off; the markdown contract is the same everywhere. Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |

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
    "name": "list_content_widgets",
    "arguments": {}
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_content_widgets","arguments":{}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### GET /api/v1/list_content_widgets

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `name` | string | no | Return only this widget (e.g. 'cards'). Omit to list every content widget. |
| `workspace_id` | string | no | Workspace whose widget settings apply. Omit when the token is scoped to a single repo — that workspace is used. Only affects which widgets are switched off; the markdown contract is the same everywhere. Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |

#### Request

```bash
curl 'https://docsbook.io/api/v1/list_content_widgets' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->
