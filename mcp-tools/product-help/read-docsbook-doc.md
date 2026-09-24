---
title: "Read docsbook doc"
description: "Read ONE page of DOCSBOOK'S OWN official documentation in full, verbatim, by the `path` from a `search_docsbook_docs` hit (e.g."
---

# Read docsbook doc

<!-- widget:mcp access=read anonymous price-millicents=3 -->

## read_docsbook_doc

Read ONE page of DOCSBOOK'S OWN official documentation in full, verbatim, by the `path` from a `search_docsbook_docs` hit (e.g. 'guides/advanced/custom-domain.md'). Use it when the search snippet is not enough to act on: step-by-step setup, the exact list of options a setting takes, what a limit actually is, what a plan actually includes. Reading the page before you answer is the difference between telling a user which switch to flip and inventing one. 🔴 This is Docsbook the PLATFORM's own manual, not the user's documentation — that is the project's own read-page tool (`read_project_doc` on the signed-in server, or the branded one a public endpoint names).

| Field | Type | Required | Description |
|---|---|---|---|
| `path` | string | yes | Path in the official docs, from a search_docsbook_docs hit, e.g. 'ai/chat.md'. |

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "read_docsbook_doc",
    "arguments": {
      "path": "<path>"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"read_docsbook_doc","arguments":{"path":"<path>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### GET /api/v1/read_docsbook_doc

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `path` | string | yes | Path in the official docs, from a search_docsbook_docs hit, e.g. 'ai/chat.md'. |

#### Request

```bash
curl 'https://docsbook.io/api/v1/read_docsbook_doc?path=%3Cpath%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->
