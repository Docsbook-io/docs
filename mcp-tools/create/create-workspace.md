---
title: "Create workspace"
description: "Create a new Docsbook documentation site (workspace) — the FIRST call for 'make a docs site', 'set up documentation', «сделай документацию»."
---

# Create workspace

<!-- widget:mcp access=write -->

## create_workspace

Create a new Docsbook documentation site (workspace) — the FIRST call for 'make a docs site', 'set up documentation', «сделай документацию». Idempotent: a repository that already has a workspace is returned with already_existed: true, so no lookup is needed first. Pages come next: write_docs, which takes MANY files in one call, so a whole first site lands as one commit. GITHUB IS OPTIONAL — this is the tool for BOTH cases: • From scratch, no GitHub at all: OMIT repo_full_name. Docsbook creates and hosts the documentation repository itself, under its own GitHub organisation, with its own credentials. The user needs no GitHub account, no connected GitHub app and no repository — never tell them to connect GitHub or bring a repo for this. Then call write_docs to publish the pages you wrote. • From the user's OWN repository: pass repo_full_name ('owner/repo'). It is what the site READS and what its public address is made of, so it must exist on GitHub and it must belong to this Docsbook account. A repository this account has no claim on, or that GitHub does not have, is created as a Docsbook-hosted site instead, and the result then reports a different repo_full_name than you asked for, with a note saying so. If a workspace for this repo already exists, returns the existing one (already_existed: true). ALWAYS give the user `site_url` from the result verbatim; never build a link out of a GitHub username or repo name.

| Field | Type | Required | Description |
|---|---|---|---|
| `repo_full_name` | string | no | GitHub repository in 'owner/repo' format, e.g. 'acme/docs'. OMIT for a Docsbook-hosted site created from scratch — no GitHub account or repository needed. |
| `custom_name` | string | no | Display name for the site, e.g. 'Acme API'. Derive it from the product's brand or repo name — never invent one; ask the user if you cannot. It also names the hosted repository, so pass it whenever you create from scratch. |

### Returns

| Field | Type | Description |
|---|---|---|
| `already_existed` | boolean | true when this repository already had a workspace — nothing new was created. |
| `id` | number | — |
| `repoFullName` | string | 'owner/repo', or a Docsbook-hosted placeholder when the site was created from scratch. |
| `customName` | string | null | — |
| `site_url` | string | The live docs URL — report this verbatim, never build one from repoFullName. |
| `customDomain` | string | null | — |
| `plan` | string | free \| pro \| business |
| `visibility` | string | public \| private |
| `not_discoverable` | string | Present ONLY when `visibility` is private, i.e. when no crawler and no answer engine can open this site. Says what that rules out — keyword work, SERP meta, crawler-facing sitemap/llms.txt tuning, backlinks, ranking readings, being cited by ChatGPT or Perplexity — and what is worth the run instead. A private SOURCE REPOSITORY is NOT this and does not rule anything out: Docsbook serves indexed public sites from private repositories. |
| `discoverability_blocked_by` | string | Alongside `not_discoverable`: "private" (the owner's choice) or "plan_locked" (the plan lapsed and Docsbook made it private — tell the owner before doing any work). |
| `aiEnabled` | boolean | — |
| `hasApiKey` | boolean | Whether a REST bearer exists — never the key itself. |
| `hasCustomAiKey` | boolean | — |
| `hasCustomTranslationKey` | boolean | — |
| `hasPassword` | boolean | — |
| `hasSourceOfTruthGraph` | boolean | Whether the semantic index has ever been built. |
| `sso` | object | { configured: false } or { issuer, clientId, allowedDomain, configured: true }. |
| `plan_capabilities` | object | What this plan unlocks. |
| `upgrade_hint` | string | null | — |
| `cta_url` | string | null | The one page readers should end up on. |
| `cta_hint` | string | — |
| `average_product_price_cents` | number | null | — |
| `revenue_hint` | string | — |
| `site_source_url` | string | null | Where facts about the product are read from. |
| `site_source_hint` | string | — |
| `subheaderFolders` | object[] | Top-level folder placements, each carrying the `placement` it resolves to — "subheader_tab" (a tab in the category strip, its pages kept out of the root sidebar tree), "sidebar_tree" (an ordinary folder in the sidebar), "subheader_tab_and_sidebar_tree" (both) or "hidden". Read `placement` rather than re-deriving it from inSubheader / showInSidebar / hiddenInSidebar. |
| `navigation_placement_hint` | string | Present when the project has folder placements: what each one resolves to and why a tab's hiddenInSidebar is not a defect to fix. |
| `publish_mismatch_warning` | string | Present only when the live site does not show what was published. |
| `…` | … | Plus every other project setting on this row — branding colors/fonts, navigation, UI toggles, SEO/GEO/AEO flags, access rules, domain, languages — minus secrets. |

### Use cases

- Use this ONLY when they point at a repository of THEIRS — including the git remote of the checkout they are working in, which counts as pointing at it.

### Limitations

- Never pass somebody else's repository — a competitor's, a prospect's, an open-source project you are only reading: naming one does not create documentation from it, it would claim their name on a public Docsbook address.

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
  -H 'Authorization: Bearer YOUR_MCP_OAUTH_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"create_workspace","arguments":{}}}'
```

### REST

```bash
curl -X POST 'https://docsbook.io/api/v1/create_workspace' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

### Result

```json
{
  "already_existed": true,
  "id": 0,
  "repoFullName": "<repoFullName>",
  "customName": "<customName>",
  "site_url": "<site_url>",
  "customDomain": "<customDomain>",
  "plan": "<plan>",
  "visibility": "<visibility>",
  "not_discoverable": "<not_discoverable>",
  "discoverability_blocked_by": "<discoverability_blocked_by>",
  "aiEnabled": true,
  "hasApiKey": true,
  "hasCustomAiKey": true,
  "hasCustomTranslationKey": true,
  "hasPassword": true,
  "hasSourceOfTruthGraph": true,
  "sso": {},
  "plan_capabilities": {},
  "upgrade_hint": "<upgrade_hint>",
  "cta_url": "<cta_url>",
  "cta_hint": "<cta_hint>",
  "average_product_price_cents": "<average_product_price_cents>",
  "revenue_hint": "<revenue_hint>",
  "site_source_url": "<site_source_url>",
  "site_source_hint": "<site_source_hint>",
  "subheaderFolders": [],
  "navigation_placement_hint": "<navigation_placement_hint>",
  "publish_mismatch_warning": "<publish_mismatch_warning>",
  "…": "<…>"
}
```

<!-- /widget -->
