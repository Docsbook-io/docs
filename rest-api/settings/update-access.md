---
title: "Update access"
description: "Make a workspace private and configure its unlock method (password and/or bring-your-own SSO/OIDC identity provider — Google Workspace, Entra ID, Okta)."
---

# Update access

<!-- widget:api -->

## POST /api/v1/update_access

Make a workspace private and configure its unlock method (password and/or bring-your-own SSO/OIDC identity provider — Google Workspace, Entra ID, Okta). Available on every plan. Anonymous readers of a private workspace must unlock it with the password or sign in via SSO before seeing any content; the owner always has access. This is the call for internal documentation — a team wiki, specs, decision records — that must not be readable by strangers. Pair it with the page lifecycle (`set_doc_status`, `get_doc_outline`) when the corpus is engineering documentation agents build from.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/update_access`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `visibility` | string | no | Whether the workspace requires unlocking to read One of: `public`, `private`. |
| `password` | string | no | Shared unlock password (min 8 chars), or null to remove password unlock |
| `sso` | string | no | Bring-your-own OIDC identity provider config, or null to remove SSO unlock |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/update_access' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"visibility":"public"}'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
