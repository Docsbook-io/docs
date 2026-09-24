---
title: "Create claim link"
description: "Mint a CLAIM LINK that hands this project to whoever opens it — 'give this site to the client', 'transfer ownership', «отдай документацию клиенту», «сделай claim-ссылку»."
---

# Create claim link

<!-- widget:api -->

## POST /api/v1/create_claim_link

Mint a CLAIM LINK that hands this project to whoever opens it — 'give this site to the client', 'transfer ownership', «отдай документацию клиенту», «сделай claim-ссылку». The recipient opens it, signs in to Docsbook (GitHub or email — no account needed beforehand), confirms, and the project moves onto THEIR account: its pages, its public address and whatever trial is still on it all stay exactly as they are, and you lose access to it at that moment. One live link per project — calling again returns the same URL with its expiry pushed out (reused: true). If the project was already claimed, the result says so (state: claimed, claimed_by) instead of failing. Typical flow: create_workspace → write_docs (or docsbook_agent) → create_claim_link → send claim_url to the business, verbatim. Moving the docs into the recipient's own GitHub repository is their own later step, from Settings in the panel — it needs their GitHub token, so no tool here does it.

**Price** — free, never metered.

Also reachable by name at `POST /api/v1/tools/create_claim_link`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `expires_in_days` | integer | no | How long the link stays claimable, in days (default 7, max 30). Also pushes out the expiry of an already-pending link. |

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
| `state` | string | pending — a link is live; claimed — the project already moved to the account in claimed_by. |
| `claim_url` | string | The link to send to the recipient, verbatim. Present while state is pending. |
| `expires_at` | string | — |
| `reused` | boolean | true when the project already had a pending link — the same URL, with its expiry pushed out. |
| `single_use` | boolean | — |
| `claimed_at` | string | — |
| `claimed_by` | object | { name, email } of the account that claimed it. |
| `next_step` | string | — |

### Limitations

- The link is single-use and expires (default 7 days, up to 30).

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/create_claim_link' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

### Response

```json
{
  "ok": true,
  "result": {
    "ok": true,
    "workspace_id": 0,
    "state": "<state>",
    "claim_url": "<claim_url>",
    "expires_at": "<expires_at>",
    "reused": true,
    "single_use": true,
    "claimed_at": "<claimed_at>",
    "claimed_by": {},
    "next_step": "<next_step>"
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
