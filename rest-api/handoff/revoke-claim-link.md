---
title: "Revoke claim link"
description: "Cancel this project's pending claim link before anyone claims it — 'take the link back', 'cancel the transfer', «отмени claim-ссылку»."
---

# Revoke claim link

<!-- widget:api -->

## POST /api/v1/revoke_claim_link

Cancel this project's pending claim link before anyone claims it — 'take the link back', 'cancel the transfer', «отмени claim-ссылку». Only a link that is still pending can be revoked: a claimed one is a completed hand-over, and the result then reports state: claimed with who took it.

**Price** — free, never metered.

Also reachable by name at `POST /api/v1/tools/revoke_claim_link`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/revoke_claim_link' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
