---
title: "Read project doc"
description: "Read ONE documentation page in full — its complete markdown, title and repo path."
---

# Read project doc

<!-- widget:api -->

## GET /api/v1/read_project_doc

Read ONE documentation page in full — its complete markdown, title and repo path. THE step between finding a page and editing it: read it here, change the text, then write_docs the whole file back. Takes the repo path search_docs and get_doc_outline use ('guides/setup.md') or the URL slug the analytics tools return ('guides/setup'); a near-miss with a single candidate is resolved for you (`resolvedFrom` says so), several candidates are listed to choose from. Changes nothing; available to any token. The result carries `lifecycle`: the page's `status`, its `version`, and `agent_may_build_from`. Read it, quote it as a draft, but do not generate work from it, do not cite it as a decision, and say which status it is in. `set_doc_status` is how it gets approved.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/read_project_doc`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `path` | string | yes | The page: a repo file path ('reference/README.md') or its URL slug ('reference/introduction'). |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | string | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### Use cases

- Use it for 'fix the command on the installation page', 'show me the quickstart', «покажи страницу», «поправь строку на странице».

### Limitations

- 🔴 When that is false the page is NOT a source of truth — a machine drafted it, or a human has not signed it off, or it was superseded.

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/read_project_doc?path=%3Cpath%3E' \
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
