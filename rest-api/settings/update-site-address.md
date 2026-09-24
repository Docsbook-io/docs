---
title: "Update site address"
description: "Change the ADDRESS of the site: the <name> in <name>.docsbook.io — its path name / subdomain."
---

# Update site address

<!-- widget:api -->

## POST /api/v1/update_site_address

Change the ADDRESS of the site: the <name> in <name>.docsbook.io — its path name / subdomain. Call it when the user asks to change the site's URL or path («поменяй адрес сайта», «поменяй path name»), and when a project is still on the opaque ws-<id>-<nonce> address it was reserved with before it had a name. The name is slugged the way the create form slugs it ('Acme API' → acme-api); a taken or reserved name is REFUSED, never silently suffixed into a different URL. 🔴 THIS MOVES A LIVE URL — the old address stops serving the site, so only call it when the user asked for it. NOT the display name (update_branding custom_name), NOT a domain of their own (update_domain). Works for EVERY project, including one whose pages come from the user's own GitHub repository — the address is a Docsbook setting and no repository is renamed. Pass an empty name to clear it and fall back to the default address. Report `site_url` from the result verbatim.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/update_site_address`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `name` | string | no | The new name, as a person would write it — 'Acme API'. It becomes acme-api.docsbook.io. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/update_site_address' \
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
