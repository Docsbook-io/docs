---
title: "Create workspace"
description: "Create a new Docsbook documentation site (workspace) — the FIRST call for 'make a docs site', 'set up documentation', «сделай документацию»."
---

# Create workspace

<!-- widget:mcp access=write -->

## create_workspace

Create a new Docsbook documentation site (workspace) — the FIRST call for 'make a docs site', 'set up documentation', «сделай документацию». Idempotent: a repository that already has a workspace is returned with already_existed: true, so no lookup is needed first. Pages come next: write_docs, which takes MANY files in one call, so a whole first site lands as one commit. GITHUB IS OPTIONAL — this is the tool for BOTH cases:
• From scratch, no GitHub at all: OMIT repo_full_name. Docsbook creates and hosts the documentation repository itself, under its own GitHub organisation, with its own credentials. The user needs no GitHub account, no connected GitHub app and no repository — never tell them to connect GitHub or bring a repo for this. Then call write_docs to publish the pages you wrote.
• From the user's OWN repository: pass repo_full_name ('owner/repo'). Use this when they point at a repository of theirs — including the git remote of the checkout they are working in, which counts as pointing at it — it is what the site READS and what its address is made of, so it must be a repository that exists on GitHub. A repository GitHub does not have, or that Docsbook cannot see, is created as a Docsbook-hosted site instead, and the result then reports a different repo_full_name than you asked for.
If a workspace for this repo already exists, returns the existing one (already_existed: true).
ALWAYS give the user `site_url` from the result verbatim; never build a link out of a GitHub username or repo name.

| Field | Type | Required | Description |
|---|---|---|---|
| `repo_full_name` | string | no | GitHub repository in 'owner/repo' format, e.g. 'acme/docs'. OMIT for a Docsbook-hosted site created from scratch — no GitHub account or repository needed. |
| `custom_name` | string | no | Display name for the site, e.g. 'Acme API'. Derive it from the product's brand or repo name — never invent one; ask the user if you cannot. It also names the hosted repository, so pass it whenever you create from scratch. |

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
    "name": "create_workspace",
    "arguments": {}
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"create_workspace","arguments":{}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### POST /api/v1/tools/create_workspace

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/create_workspace' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{}}'
```

<!-- /widget -->
