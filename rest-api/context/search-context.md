---
title: "Search context"
description: "HAS THIS ORGANIZATION ALREADY BEEN HERE?"
---

# Search context

<!-- widget:api -->

## GET /api/v1/search_context

HAS THIS ORGANIZATION ALREADY BEEN HERE? — search the folder by words, and get back the files that match with a short extract each. Free. CALL IT BEFORE PROPOSING ANYTHING. A match in `hypotheses/` with a verdict is this customer having already tried your idea and measured what it did; a match in `decisions/` is the owner having already settled it. Proposing either again is the single most expensive thing a run can do, because it looks like work. ⚡ Extracts are short and metered by design — this is for finding the file, not for reading it. Open what matches with read_context.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/search_context`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `query` | string | yes | Words to look for, in any language — at least three characters. |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/search_context?query=%3Cquery%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
