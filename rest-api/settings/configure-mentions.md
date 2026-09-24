---
title: "Configure mentions"
description: "Choose what the mention checks watch on one engine: turn the daily check on or off, and set the queries (up to 5) — the exact words a reader would type or ask."
---

# Configure mentions

<!-- widget:api -->

## POST /api/v1/configure_mentions

Choose what the mention checks watch on one engine: turn the daily check on or off, and set the queries (up to 5) — the exact words a reader would type or ask. Queries a workspace does NOT rank for are the point: those are the ones Search Console can never report on. Use get_mentions to read what the checks found.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/configure_mentions`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `surface` | string | no | Which engine this arms: ai_overview (Google's AI answer), google or bing (the results page). One of: `ai_overview`, `google`, `bing`. |
| `enabled` | boolean | no | Whether the daily check runs. Queries are kept either way. |
| `queries` | string[] | no | The queries to check, up to 5. Replaces the saved list. |
| `cron_expression` | string | no | 5-field UTC cron for the check. Defaults to a daily early-morning slot. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/configure_mentions' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"surface":"ai_overview"}'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
