---
title: "Revoke claim link"
description: "Cancel this project's pending claim link before anyone claims it — 'take the link back', 'cancel the transfer', «отмени claim-ссылку»."
---

# Revoke claim link

<!-- widget:api -->

## POST /api/v1/revoke_claim_link

Cancel this project's pending claim link before anyone claims it — 'take the link back', 'cancel the transfer', «отмени claim-ссылку».

**Price** — free, never metered.

Also reachable by name at `POST /api/v1/tools/revoke_claim_link`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | — |
| `workspace_id` | number | — |
| `state` | string | revoked — or claimed, when the hand-over had already completed. |
| `revoked` | number | How many pending links were cancelled (one, by construction). |

### Limitations

- Only a link that is still pending can be revoked: a claimed one is a completed hand-over, and the result then reports state: claimed with who took it.

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/revoke_claim_link' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Response

```json
{
  "ok": true,
  "result": {
    "ok": true,
    "workspace_id": 0,
    "state": "<state>",
    "revoked": 0
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
