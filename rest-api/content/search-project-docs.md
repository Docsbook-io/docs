---
title: "Search project docs"
description: "FIND A DOCUMENTATION PAGE — start here, and this is the FIRST call for any question about these docs."
---

# Search project docs

<!-- widget:api -->

## GET /api/v1/search_project_docs

FIND A DOCUMENTATION PAGE — start here, and this is the FIRST call for any question about these docs. Searches the project's documentation by MEANING (embeddings over a pre-built vector index), which finds the right page far more often than literal keyword matching: 'how do I reset a password' lands on a page titled 'Recovering account access', which a word search misses entirely. A LONG query is welcome, and usually better than a short one: paste the user's whole request, several questions at once included. It is split into its parts, each part searched on its own and the results merged, so a request that asks about four things returns a page for each instead of one blurred average of all four. Cheap and repeatable: the index is built once, ahead of time, so a call here is one lookup against vectors that already exist. Always answers: a project with no vector index yet is searched by full text instead, and `mode` ('semantic' | 'lexical') says which engine replied — no plan is required either way. Returns hits {n, title, headingPath, url, path}, best first — each with a similarity `score` (semantic) or a `snippet` (lexical); call the matching read-page tool on `path` for the whole page — `read_project_doc` on the signed-in server, the read tool this same tools/list names on the public one. Prefer search_docs only when you need a LITERAL string — an error message, a CLI flag, a regex, a file path.

**Price** — $0.00009 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/search_project_docs`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `query` | string | yes | What you are looking for, in natural language — a question or a phrase, not keywords. |
| `limit` | integer | no | Max results (default 8). |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | string | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### Use cases

- Use it for any natural-language question — «где написано про…», 'where do we explain X', 'which page covers Y' — and before writing anything, so you edit the page that exists instead of adding a second one about the same thing.

### Limitations

- Do NOT start by listing the outline, grepping or globbing files, or opening pages one by one to look for the answer: that downloads and reads the whole site, takes many times longer and answers worse than one call here.

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/search_project_docs?query=%3Cquery%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Response

```json
{
  "ok": true,
  "result": "<result>",
  "duration_ms": 0
}
```

### Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |

<!-- /widget -->
