---
title: "Connect source"
description: "Connect a repository, a website or a single page as a SOURCE OF TRUTH for this documentation — what `list_sources` then lists and `read_source` reads, and what an agent armed…"
---

# Connect source

<!-- widget:mcp access=write price-millicents=800 -->

## connect_source

Connect a repository, a website or a single page as a SOURCE OF TRUTH for this documentation — what `list_sources` then lists and `read_source` reads, and what an agent armed with `enable_agent` watches.
Use it when the docs are about a product whose code or site this project cannot currently read: connecting the repository is what turns 'the docs claim X' into something checkable.
A GitHub repository is PROVED readable before anything is stored — publicly, or with a GitHub authorisation this project already holds — so this never leaves behind a source that quietly reads nothing. A private repository nobody has authorised yet comes back as REPO_UNREADABLE with the one thing that fixes it (the owner grants repository access once, in their panel); connect it anyway is not an option this tool offers.
`note` is the owner's own words about why the source is connected and is read as instruction by everything that later reads it — say what it is for ('the API server the reference pages describe'), not what it is.
REQUIRES a read-write MCP token.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `url` | string | yes | The address to connect: 'https://github.com/acme/api', 'https://acme.com', or one page of it. |
| `note` | string | no | What this source is for, in the owner's words — read as instruction by every tool that later reads the source. |
| `label` | string | no | What to call it in the list. Defaults to the repository or host name. |

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
    "name": "connect_source",
    "arguments": {
      "url": "<url>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"connect_source","arguments":{"url":"<url>"}}}'
```

<!-- /widget -->
