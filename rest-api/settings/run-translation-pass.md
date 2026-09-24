---
title: "Run translation pass"
description: "Start a REAL translation catch-up run for one or more languages: the same batch the panel's 'Translate now' starts, with pages that are behind translated before pages that are…"
---

# Run translation pass

<!-- widget:api -->

## POST /api/v1/run_translation_pass

Start a REAL translation catch-up run for one or more languages: the same batch the panel's 'Translate now' starts, with pages that are behind translated before pages that are missing. Answers with the job id per language as soon as the runs are open — the pages themselves land over the following minutes and are visible in Translations. It NEVER discards existing translations (that is the owner's 'Re-translate everything'). Every call translates that site chrome for every language asked about — INCLUDING the ones it reports as skipped — so a project whose pages are all current is repaired by an ordinary call.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/run_translation_pass`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `languages` | string[] | no | ISO codes to bring level (default: every language switched on for this project) |
| `force` | boolean | no | Run even for a language coverage says is already level with the source (default false) |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `…` | … | The job id started per language — pages land over the following minutes. |

### Limitations

- Languages already level with the source are skipped unless force=true, a language with a live run is left alone, and at most 3 languages are started per call.
- 🔴 THIS IS ALSO THE CALL FOR 'the pages are translated but the MENU / breadcrumbs / header buttons / tabs / suggested questions are still in English'.
- Do NOT reach for force=true to fix English chrome: force re-runs every page in the repo and costs real money to rewrite a few dozen short strings.
- REQUIRES PRO or higher.

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/run_translation_pass' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

### Response

```json
{
  "ok": true,
  "result": {
    "…": "<…>"
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
