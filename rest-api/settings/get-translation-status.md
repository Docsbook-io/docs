---
title: "Get translation status"
description: "How each enabled language stands against the source RIGHT NOW: pages current / behind / missing / manual, the percentage, whether a run is in flight and how far along, and what…"
---

# Get translation status

<!-- widget:api -->

## GET /api/v1/get_translation_status

How each enabled language stands against the source RIGHT NOW: pages current / behind / missing / manual, the percentage, whether a run is in flight and how far along, and what the last run did — including which agent run started it. Call this BEFORE run_translation_pass: a language already level with the source costs money to re-translate and changes nothing. Coverage is null (never 0) when the source repository could not be read. REQUIRES PRO or higher.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/get_translation_status`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `languages` | string[] | no | ISO codes to report on (default: every language switched on for this project) |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/get_translation_status' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
