---
title: "List context"
description: "WHAT THIS ORGANIZATION'S FOLDER ALREADY HOLDS — every file's path, title and date, with no contents."
---

# List context

<!-- widget:api -->

## GET /api/v1/list_context

WHAT THIS ORGANIZATION'S FOLDER ALREADY HOLDS — every file's path, title and date, with no contents. FIRST CALL OF EVERY RUN, before reading anything and before deciding anything. Free. The folder is what previous runs worked out about this customer and never had to work out again: product/ — What is this business, what does it charge, what does it never claim? audience/ — Who reads these docs, what job are they on, what do they arrive already knowing? conventions/ — How must a page read here — voice, terms this product uses and never uses, structure? memory/ — What would the next run otherwise work out again from scratch? decisions/ — What did the owner settle, when, and what does it close? hypotheses/ — What might be true, what reading decides it, and by when? questions/ — What could not be worked out here, and who can answer it? playbooks/ — How is this kind of work done well HERE — what was tried, what held? Two levels: a file at `product/pricing.md` is true of the whole organization, one at `projects/41/product/pricing.md` is true of project 41 and overrides it — so one agent serving six projects of one company learns what they share exactly once. Reading the folder whole is not a step in any job, and the store stops it anyway. ⚡ `overdue: true` on a file is work somebody owes today — a claim whose check-in date has passed, or a question that has been waiting. Those outrank starting anything new.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/list_context`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `folder` | string | no | One folder only. Omitted lists all eight, which is what a run starting up wants. |
| `include_retired` | string | no | Also list what was retired — a rejected claim is the expensive half of what a project knows. Off by default. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | string | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### Limitations

- 🔴 This answers WHAT IS THERE, deliberately without a word of what it says: open the two or three that bear on the job with read_context.

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/list_context' \
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
