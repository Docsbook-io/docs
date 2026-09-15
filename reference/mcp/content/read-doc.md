---
title: "Read doc"
description: "Read ONE documentation page in full — its complete markdown, title and repo path."
---

# Read doc

<!-- widget:mcp access=read -->

## read_doc

Read ONE documentation page in full — its complete markdown, title and repo path. THE step between finding a page and editing it: read it here, change the text, then write_docs the whole file back. Takes the repo path search_docs and get_doc_outline use ('guides/setup.md') or the URL slug the analytics tools return ('guides/setup'); a near-miss with a single candidate is resolved for you (`resolvedFrom` says so), several candidates are listed to choose from. Use it for 'fix the command on the installation page', 'show me the quickstart', «покажи страницу», «поправь строку на странице». Changes nothing; available to any token. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `path` | string | yes | The page: a repo file path ('reference/README.md') or its URL slug ('reference/introduction'). |

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
    "name": "read_doc",
    "arguments": {
      "path": "<path>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"read_doc","arguments":{"path":"<path>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/read_doc

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/read_doc' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"path":"<path>"}}'
```

<!-- /widget -->
