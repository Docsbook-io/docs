---
title: "Set doc status"
description: "Move ONE documentation page through its lifecycle — the call for 'this spec is approved', 'freeze this decision record', 'mark the old guide deprecated', «эту страницу…"
---

# Set doc status

<!-- widget:api -->

## POST /api/v1/set_doc_status

Move ONE documentation page through its lifecycle — the call for 'this spec is approved', 'freeze this decision record', 'mark the old guide deprecated', «эту страницу утвердили», «заморозь», «пометь устаревшей». Statuses: `generated` — A machine wrote this page and no human has read it yet. `draft` — Someone is still writing it. Not ready to be read as settled. `review` — Waiting for a human to read it and decide. `approved` — A human read this version and signed off. Safe to build work from. Agents may build from it. `locked` — Frozen on purpose. Agents may read it and build from it, but may not rewrite it. Agents may build from it. `deprecated` — Superseded. Kept so its links keep working, not to be relied on. `archived` — History. Neither built from nor edited. Each page also carries a `version`, bumped automatically by every write that changes its text. That is not a bug to work around by re-approving in the same breath — re-approve after somebody has read the new text. Not every move is legal: from each status only the ones listed for it (get_doc_outline shows where every page sits).

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/set_doc_status`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `path` | string | no | The page: a repo file path ('specs/auth.md') or its URL slug ('specs/auth'). |
| `status` | string | no | The status to move it to. One of: `generated`, `draft`, `review`, `approved`, `locked`, `deprecated`, `archived`. |
| `version` | string | no | Optional explicit version, e.g. '1.0' when a draft becomes the first real release. Omit to keep the page's current version — a status change is not an edit. |
| `note` | string | no | Why, in the approver's own words. Goes into the commit message and the change record. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `path` | string | — |
| `from` | string | The status the page was at. |
| `to` | string | — |
| `version` | string | — |
| `lifecycle` | object | The page's lifecycle after the move, in the same shape read_doc returns. |
| `unchanged` | boolean | True when the page already sat there and nothing was committed. |
| `commitSha` | string | — |
| `pullRequest` | object | — |

### Limitations

- Writes to it are refused.
- Writes to it are refused.
- 🔴 APPROVAL IS OF A VERSION, NOT OF A PAGE: editing an approved page sends it back to `review`, because the sign-off was of the text that just changed.
- 🔴 This is the only way to reach `approved` or `locked`.
- `write_docs` cannot set them, so an agent can never approve its own output as part of writing it.
- REQUIRES a read-write MCP token.

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/set_doc_status' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"status":"generated"}'
```

### Response

```json
{
  "ok": true,
  "result": {
    "path": "<path>",
    "from": "<from>",
    "to": "<to>",
    "version": "<version>",
    "lifecycle": {},
    "unchanged": true,
    "commitSha": "<commitSha>",
    "pullRequest": {}
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
