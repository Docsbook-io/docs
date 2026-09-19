---
title: "Update access"
description: "Make a workspace private and configure its unlock method (password and/or bring-your-own SSO/OIDC identity provider — Google Workspace, Entra ID, Okta)."
---

# Update access

<!-- widget:mcp access=write price-millicents=2000 -->

## update_access

Make a workspace private and configure its unlock method (password and/or bring-your-own SSO/OIDC identity provider — Google Workspace, Entra ID, Okta). Available on every plan. Anonymous readers of a private workspace must unlock it with the password or sign in via SSO before seeing any content; the owner always has access. This is the call for internal documentation — a team wiki, specs, decision records — that must not be readable by strangers. Pair it with the page lifecycle (`set_doc_status`, `get_doc_outline`) when the corpus is engineering documentation agents build from.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `visibility` | string | no | Whether the workspace requires unlocking to read One of: `public`, `private`. |
| `password` | string | no | Shared unlock password (min 8 chars), or null to remove password unlock |
| `sso` | string | no | Bring-your-own OIDC identity provider config, or null to remove SSO unlock |

<!-- /widget -->

## Call it

<!-- widget:code-group -->

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "update_access",
    "arguments": {
      "workspace_id": "<workspace_id>",
      "visibility": "public"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"update_access","arguments":{"workspace_id":"<workspace_id>","visibility":"public"}}}'
```

<!-- /widget -->
