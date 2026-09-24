---
title: "Retire context"
description: "A FILE IN THIS ORGANIZATION'S FOLDER STOPPED BEING TRUE — take it out of every later run's reading."
---

# Retire context

<!-- widget:api -->

## GET /api/v1/retire_context

A FILE IN THIS ORGANIZATION'S FOLDER STOPPED BEING TRUE — take it out of every later run's reading. Free. ⚡ Retired, not deleted: a rejected claim is the expensive half of what a customer knows, and deleting it is how the same idea gets proposed again next quarter. It stays findable with `include_retired`.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/retire_context`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `path` | string | yes | Exactly as list_context printed it. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | string | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### Use cases

- Use it when the product changed under a fact, when a question got answered (write the answer into `decisions/` first), or when a file turned out to be wrong.

### Limitations

- Not for a claim you measured — that gets a `verdict`, which is a finding.

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/retire_context?path=%3Cpath%3E' \
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
