---
title: "List docsbook docs"
description: "List EVERY page of Docsbook's own official documentation — the product's full table of contents."
---

# List docsbook docs

<!-- widget:api -->

## GET /api/v1/list_docsbook_docs

List EVERY page of Docsbook's own official documentation — the product's full table of contents. The one call that answers 'what can Docsbook do?' without having to guess a search query first: the page list is the feature list. Use it to orient yourself before advising a user what to do, to check whether a capability is documented at all, or when a `search_docsbook_docs` query came back empty and you need to know whether the topic is missing or just worded differently. 🔴 This is Docsbook the platform's own manual, not the user's documentation — that is the project's own outline tool (`get_project_doc_outline` on the signed-in server, or the branded one a public endpoint names).

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable without a token on this workspace's public MCP endpoint.

Also reachable by name at `POST /api/v1/tools/list_docsbook_docs`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `path_prefix` | string | no | Optional: only pages under this prefix, e.g. 'guides/' or 'ai/'. |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/list_docsbook_docs' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
