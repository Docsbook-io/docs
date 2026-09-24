---
title: "List docsbook docs"
description: "List EVERY page of Docsbook's own official documentation — the product's full table of contents."
---

# List docsbook docs

<!-- widget:mcp access=read anonymous price-millicents=3 -->

## list_docsbook_docs

List EVERY page of Docsbook's own official documentation — the product's full table of contents. The one call that answers 'what can Docsbook do?' without having to guess a search query first: the page list is the feature list. Use it to orient yourself before advising a user what to do, to check whether a capability is documented at all, or when a `search_docsbook_docs` query came back empty and you need to know whether the topic is missing or just worded differently. 🔴 This is Docsbook the platform's own manual, not the user's documentation — that is the project's own outline tool (`get_project_doc_outline` on the signed-in server, or the branded one a public endpoint names).

| Field | Type | Required | Description |
|---|---|---|---|
| `path_prefix` | string | no | Optional: only pages under this prefix, e.g. 'guides/' or 'ai/'. |

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "list_docsbook_docs",
    "arguments": {}
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_docsbook_docs","arguments":{}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### GET /api/v1/list_docsbook_docs

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `path_prefix` | string | no | Optional: only pages under this prefix, e.g. 'guides/' or 'ai/'. |

#### Request

```bash
curl 'https://docsbook.io/api/v1/list_docsbook_docs' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->
