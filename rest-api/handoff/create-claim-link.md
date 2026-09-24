---
title: "Create claim link"
description: "Mint a CLAIM LINK that hands this project to whoever opens it — 'give this site to the client', 'transfer ownership', «отдай документацию клиенту», «сделай claim-ссылку»."
---

# Create claim link

<!-- widget:api -->

## POST /api/v1/create_claim_link

Mint a CLAIM LINK that hands this project to whoever opens it — 'give this site to the client', 'transfer ownership', «отдай документацию клиенту», «сделай claim-ссылку». The link is single-use and expires (default 7 days, up to 30). The recipient opens it, signs in to Docsbook (GitHub or email — no account needed beforehand), confirms, and the project moves onto THEIR account: its pages, its public address and whatever trial is still on it all stay exactly as they are, and you lose access to it at that moment. One live link per project — calling again returns the same URL with its expiry pushed out (reused: true). If the project was already claimed, the result says so (state: claimed, claimed_by) instead of failing. Typical flow: create_workspace → write_docs (or docsbook_agent) → create_claim_link → send claim_url to the business, verbatim. Moving the docs into the recipient's own GitHub repository is their own later step, from Settings in the panel — it needs their GitHub token, so no tool here does it.

**Price** — free, never metered.

Also reachable by name at `POST /api/v1/tools/create_claim_link`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `expires_in_days` | integer | no | How long the link stays claimable, in days (default 7, max 30). Also pushes out the expiry of an already-pending link. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/create_claim_link' \
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
