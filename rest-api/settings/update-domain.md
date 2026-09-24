---
title: "Update domain"
description: "Set or remove a custom domain (e.g."
---

# Update domain

<!-- widget:api -->

## POST /api/v1/update_domain

Set or remove a custom domain (e.g. docs.yourcompany.com). REQUIRES BUSINESS plan.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/update_domain`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `custom_domain` | string | no | Custom domain name, or empty string to remove |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/update_domain' \
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
