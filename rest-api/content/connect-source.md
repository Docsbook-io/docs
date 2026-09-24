---
title: "Connect source"
description: "Connect a repository, a website or a single page as a SOURCE OF TRUTH for this documentation — what `list_sources` then lists and `read_source` reads, and what an agent armed…"
---

# Connect source

<!-- widget:api -->

## POST /api/v1/connect_source

Connect a repository, a website or a single page as a SOURCE OF TRUTH for this documentation — what `list_sources` then lists and `read_source` reads, and what an agent armed with `enable_agent` watches.
Use it when the docs are about a product whose code or site this project cannot currently read: connecting the repository is what turns 'the docs claim X' into something checkable.
A GitHub repository is PROVED readable before anything is stored — publicly, or with a GitHub authorisation this project already holds — so this never leaves behind a source that quietly reads nothing. A private repository nobody has authorised yet comes back as REPO_UNREADABLE with the one thing that fixes it (the owner grants repository access once, in their panel); connect it anyway is not an option this tool offers.
`note` is the owner's own words about why the source is connected and is read as instruction by everything that later reads it — say what it is for ('the API server the reference pages describe'), not what it is.
REQUIRES a read-write MCP token.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/connect_source`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `url` | string | no | The address to connect: 'https://github.com/acme/api', 'https://acme.com', or one page of it. |
| `note` | string | no | What this source is for, in the owner's words — read as instruction by every tool that later reads the source. |
| `label` | string | no | What to call it in the list. Defaults to the repository or host name. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/connect_source' \
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
