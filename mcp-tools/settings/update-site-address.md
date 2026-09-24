---
title: "Update site address"
description: "Change the ADDRESS of the site: the <name> in <name>.docsbook.io — its path name / subdomain."
---

# Update site address

<!-- widget:mcp access=write price-millicents=1 -->

## update_site_address

Change the ADDRESS of the site: the <name> in <name>.docsbook.io — its path name / subdomain. NOT the display name (update_branding custom_name), NOT a domain of their own (update_domain). Works for EVERY project, including one whose pages come from the user's own GitHub repository — the address is a Docsbook setting and no repository is renamed. Pass an empty name to clear it and fall back to the default address. Report `site_url` from the result verbatim.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when the MCP endpoint is auto-scoped to a workspace). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `name` | string | yes | The new name, as a person would write it — 'Acme API'. It becomes acme-api.docsbook.io. |

### Use cases

- Call it when the user asks to change the site's URL or path («поменяй адрес сайта», «поменяй path name»), and when a project is still on the opaque ws-<id>-<nonce> address it was reserved with before it had a name.

### Limitations

- The name is slugged the way the create form slugs it ('Acme API' → acme-api); a taken or reserved name is REFUSED, never silently suffixed into a different URL.
- 🔴 THIS MOVES A LIVE URL — the old address stops serving the site, so only call it when the user asked for it.

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "update_site_address",
    "arguments": {
      "name": "<name>"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer YOUR_MCP_OAUTH_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"update_site_address","arguments":{"name":"<name>"}}}'
```

### REST

```bash
curl -X POST 'https://docsbook.io/api/v1/update_site_address' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"name":"<name>"}'
```

<!-- /widget -->
