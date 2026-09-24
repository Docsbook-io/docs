---
title: "Test chat hook"
description: "Send a test ping to one of the configured AI chat hooks and return status."
---

# Test chat hook

<!-- widget:api -->

## GET /api/v1/test_chat_hook

Send a test ping to one of the configured AI chat hooks and return status. REQUIRES the PRO plan or above.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/test_chat_hook`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `hook_type` | string | yes | Which hook to test |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/test_chat_hook?hook_type=%3Chook_type%3E' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
