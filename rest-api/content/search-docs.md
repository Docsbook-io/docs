---
title: "Search docs"
description: "LITERAL-string search over the workspace's documentation files — for an exact token you already know: an error message, a CLI flag, a config key, a regex, a file path."
---

# Search docs

<!-- widget:api -->

## GET /api/v1/search_docs

LITERAL-string search over the workspace's documentation files — for an exact token you already know: an error message, a CLI flag, a config key, a regex, a file path. In 'text' mode on a project with a semantic index the literal matches are fused with the index's meaning matches (`engine: "hybrid"`), so a section worded differently still surfaces; without an index it matches words only (`engine: "literal"`). Still NOT for a question or a topic ('where do we describe…', 'find the page about…', «где у нас описано», «найди в документации») — that is `search_project_docs`, which takes the whole question, splits it into its parts and ranks pages by MEANING; do not hunt for an answer here mode by mode. Modes: 'text' (default — full-text with snippets, hybrid when indexed), 'grep' (regex), 'symbol' (fuzzy heading match), 'paths' (glob over file paths). Returns numbered hits {n, title, headingPath, snippet, url}: 280-character snippets, not pages — call read_project_doc for the whole page before editing it. Available to any token regardless of read/write scope.

**Price** — $0.00009 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/search_docs`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `query` | string | yes | What to find. For 'text'/'grep' a phrase or pattern; for 'symbol' a heading hint; for 'paths' a glob. |
| `mode` | string | no | Search mode (default 'text'). |
| `path_prefix` | string | no | Optional: restrict 'text'/'grep' results to files under this path prefix. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `mode` | string | text \| grep \| symbol \| paths. |
| `docs_language` | string | null | — |
| `count` | number | — |
| `results` | object[] | { n, title, headingPath, snippet, url, path }. |
| `note` | string | — |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/search_docs?query=%3Cquery%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Response

```json
{
  "ok": true,
  "result": {
    "mode": "<mode>",
    "docs_language": "<docs_language>",
    "count": 0,
    "results": [],
    "note": "<note>"
  },
  "duration_ms": 0
}
```

### Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |

<!-- /widget -->
