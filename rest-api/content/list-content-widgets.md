---
title: "List content widgets"
description: "List the widgets that can be embedded directly in documentation markdown (as opposed to find_widget, which covers interactive widgets rendered in the AI chat)."
---

# List content widgets

<!-- widget:api -->

## GET /api/v1/list_content_widgets

List the widgets that can be embedded directly in documentation markdown (as opposed to find_widget, which covers interactive widgets rendered in the AI chat). Returns, for each widget, what it renders, when to use it, the exact markdown contract it expects, and a copy-pasteable example — and, above them, `writing_style`: how the PROSE between the widgets reads (one- or two-line paragraphs, identifiers in inline code, concepts linked where they are named, bold only where the eye lands) with a page that shows it. Widgets the workspace owner switched off in the admin panel are NOT listed — their markers render as plain markdown, so writing one would produce a page that silently looks unchanged.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable without a token on this workspace's public MCP endpoint.

Also reachable by name at `POST /api/v1/tools/list_content_widgets`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `name` | string | no | Return only this widget (e.g. 'cards'). Omit to list every content widget. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `syntax` | string | — |
| `rules` | string[] | — |
| `where_to_use` | string | — |
| `widgets` | object[] | { name, summary, use_when, markdown_contract, example }. |
| `disabled_widgets` | string[] | — |
| `disabled_note` | string | — |

### Use cases

- Call this before writing or editing a docs page that would benefit from a card grid, an accordion, or any other rich content block — the catalog is the live source of truth, so never guess a widget name or syntax.

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/list_content_widgets' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Response

```json
{
  "ok": true,
  "result": {
    "syntax": "<syntax>",
    "rules": [],
    "where_to_use": "<where_to_use>",
    "widgets": [],
    "disabled_widgets": [],
    "disabled_note": "<disabled_note>"
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
