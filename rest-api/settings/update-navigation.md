---
title: "Update navigation"
description: "Update every curated link on the docs site: header links, social links, FOOTER link columns, folder navigation tabs, left-sidebar page/folder icons, and sidebar label overrides."
---

# Update navigation

<!-- widget:api -->

## POST /api/v1/update_navigation

Update every curated link on the docs site: header links, social links, FOOTER link columns, folder navigation tabs, left-sidebar page/folder icons, and sidebar label overrides. Available on all plans including FREE. Whether the footer is SHOWN (and its layout, copyright text and CTA) is update_ui_settings — this tool owns what is IN it.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/update_navigation`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `header_links` | object[] | no | Links shown in the docs header. Full replacement of the set — pass the complete desired list, not a delta. `color` is a hex background that renders the link as a filled button: give it to the workspace's call-to-action link (cta_url from get_workspace / update_branding) and leave it unset on the rest, so exactly one header item reads as the CTA. |
| `social_links` | object | no | — |
| `subheader_folders` | object[] | no | Where each top-level folder of the docs is PLACED. A folder normally has one of two placements, and these flags are how you choose between them: • SUBHEADER TAB — a top-level section in the category strip under the header (`inSubheader: true`, `hiddenInSidebar: true`). Selecting the tab scopes the left sidebar to that folder's pages; outside the tab they stay out of the sidebar tree. This is the normal, deliberate arrangement for a LARGE section — a blog, a changelog, a guides or reference set — and it is NOT a misconfiguration waiting to be tidied up. • SIDEBAR FOLDER — an ordinary folder in the main sidebar tree (`showInSidebar: true`, `hiddenInSidebar` unset, `inSubheader: false`). No tab; readers expand it in the sidebar. get_workspace reports the resolved choice per folder as `placement` ("subheader_tab" \| "sidebar_tree" \| "subheader_tab_and_sidebar_tree" \| "hidden") — read that instead of re-deriving it from the three booleans. HOW THE THREE COMBINE — two questions, not three settings: (1) is there a tab? `inSubheader`, and nothing else; removing a tab never puts its pages back in the sidebar. (2) are the pages in the ROOT sidebar tree — the tree shown when no tab is active? `showInSidebar` must be true AND `hiddenInSidebar` must not be; `hiddenInSidebar` also drops them from Previous/Next, which `showInSidebar: false` does not. Inside an active tab neither flag applies: a tab always scopes the sidebar to its own folder. COMBINATIONS THAT MEAN NOTHING: `showInSidebar: false` together with `hiddenInSidebar: true` (the root tree already excludes the folder for either reason — the only added effect is Previous/Next); `showInSidebar: true` with `hiddenInSidebar: true` (contradictory, `hiddenInSidebar` wins); any `hiddenInSidebar` on a "Getting Started" folder (ignored — it can never be hidden this way). `inSubheader: false` with no root-tree placement leaves the pages reachable only by direct URL or search. PAGE TABS — a tab can also be ONE PAGE instead of a folder: `kind: "page"`, `folderPath` = the page's path (`introduction` or "" for the site's front page, `guides/setup` for any other). Clicking it opens that page; it never scopes the sidebar. `hiddenInSidebar: true` takes the page out of the left sidebar (`showInSidebar` is ignored for pages). Typical use: the front page as its own tab (`{kind:"page", folderPath:"introduction", label:"Home", showInSidebar:true, beforeOverview:true}`) on a site whose home page hides the sidebar. ORDER — tabs render in array order AFTER the built-in "Overview" tab; `beforeOverview: true` puts an entry to the LEFT of Overview instead. When the home page hides its sidebar (update_ui_settings home_hide_sidebar), the front page is a landing, not part of Overview: Overview opens the first sidebar page after it, is not highlighted on the front page, and the front page leaves the sidebar tree. 🔴 DO NOT "FIX" A TAB'S `hiddenInSidebar`. Setting it to false on a folder that is a tab repairs nothing: the tab stays, and every page of that folder is MERGED into the root sidebar tree, so the sidebar grows by the whole section and the same pages are reachable twice. Change it only when the owner asks for it. |
| `sidebar_icons` | object[] | no | Icons shown next to pages/folders in the left sidebar. Full replacement of the set — pass the complete desired list, not a delta. |
| `footer_columns` | object[] | no | The footer's link columns (max 6). Full replacement of the set — pass the complete desired list, not a delta; read the current one from get_workspace `footerColumns`. The footer must also be enabled (update_ui_settings footer_enabled) before a reader sees any of this. Do NOT put social profiles here — they are social_links above, which the footer renders as icons. |
| `page_labels` | object[] | no | Sidebar label overrides. An override changes ONLY the text in the sidebar — never the page's address and never its position in the tree, so no link breaks and nothing is reordered. Use this for 'rename this page in the navigation'; renaming the file itself is a write_docs move, which changes the address (the old one keeps working through the site's redirect map, but links and citations to it become second-hand). Labels are derived from file names, so every README.md renders as "Introduction" — this is how several of them get told apart. Overridden labels are still offered for translation, so a renamed page stays localized. Full replacement of the set — pass the complete desired list, not a delta (read the current one from get_workspace `pageLabels`). |

### `social_links` fields

| Field | Type | Required | Description |
|---|---|---|---|
| `github` | string | no | — |
| `twitter` | string | no | — |
| `linkedin` | string | no | — |
| `youtube` | string | no | — |
| `slack` | string | no | — |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

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

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/update_navigation' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

### Response

```json
{
  "ok": true,
  "result": {
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
  },
  "duration_ms": 0
}
```

### Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |

<!-- /widget -->
