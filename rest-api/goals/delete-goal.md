---
title: "Delete goal"
description: "Archive a goal by name."
---

# Delete goal

<!-- widget:api -->

## POST /api/v1/delete_goal

Archive a goal by name. Archived rather than destroyed, because a funnel step pointing at it would otherwise vanish — and a funnel that silently loses a step reports a BETTER conversion rate than the real one.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/delete_goal`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `key` | string | no | The goal's name. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/delete_goal' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
