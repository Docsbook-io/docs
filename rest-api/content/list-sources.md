---
title: "List sources"
description: "List the sources this documentation is connected to — the repositories and websites its owner registered as its sources of truth, plus the repository the site is built from."
---

# List sources

<!-- widget:api -->

## GET /api/v1/list_sources

List the sources this documentation is connected to — the repositories and websites its owner registered as its sources of truth, plus the repository the site is built from. Returns { sources: [{ id, kind, label, url, note, status, origin }] }; `note` is the owner's own words about why that source is connected — treat it as instruction. Read one with `read_source`. Every other row's `origin` is `source` and its `id` is a number. An empty list means nothing is connected: say so rather than inventing a repository or a domain. `private: true` on a row means GitHub will not serve that repository without credentials. It is a READING fact — attach an authorisation, expect no anonymous link to it to work — and it says nothing about whether the published site is public: whether anyone outside can read the DOCS is `visibility` on the workspace, and a private repository serving a fully indexed public site is an ordinary Docsbook setup.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/list_sources`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `sources` | object[] | { id, kind, label, url, note, status, last_read_at, origin }. `origin` is `workspace_repo` or `site_source` when `id` is null, `source` otherwise. |
| `hint` | string | — |

### Use cases

- Call this BEFORE writing or updating documentation and before judging whether something documented is still true: a connected source is a fact you can go and read, and reading beats recalling.

### Limitations

- `id` is a string, not a number, for two kinds of row that were never 'connected' by hand — it equals `origin`: `workspace_repo` is the repository the docs are built from (read it with `read_source source_id: "workspace_repo"`; arm a commit trigger on it with `enable_agent`'s `watch_source_id: "workspace_repo"`, no need to `connect_source` it first); `site_source` is the legacy single URL set in Branding (readable, but not a repository — it cannot be a commit trigger).

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/list_sources' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Response

```json
{
  "ok": true,
  "result": {
    "sources": [],
    "hint": "<hint>"
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
