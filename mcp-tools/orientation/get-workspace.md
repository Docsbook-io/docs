---
title: "Get workspace"
description: "Get one project in full — every setting an update_* tool can change, its plan and capabilities, its call to action, its live site_url."
---

# Get workspace

<!-- widget:mcp access=read -->

## get_workspace

Get one project in full — every setting an update_* tool can change, its plan and capabilities, its call to action, its live site_url. Address it the way the user did: a numeric id, 'owner/repo', the repo name alone, the display name, the docs URL or the custom domain — the server resolves the name, so this is the FIRST call when the user names a project, never list_workspaces. A name matching several projects returns AMBIGUOUS_WORKSPACE with the candidates; one matching none returns WORKSPACE_NOT_FOUND with the closest.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `repo` | string | no | 'owner/repo', or anything else the user calls the project — a repo name, a display name, a docs URL, a custom domain. Resolved the same way as a textual workspace_id. |

### Returns

| Field | Type | Description |
|---|---|---|
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

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "get_workspace",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_workspace","arguments":{}}}'
```

### REST

```bash
curl 'https://docsbook.io/api/v1/get_workspace' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

### Result

```json
{
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
