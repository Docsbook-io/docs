---
title: "Update navigation"
description: "Update every curated link on the docs site: header links, social links, FOOTER link columns, folder navigation tabs, left-sidebar page/folder icons, and sidebar label overrides."
---

# Update navigation

<!-- widget:mcp access=write price-millicents=1 -->

## update_navigation

Update every curated link on the docs site: header links, social links, FOOTER link columns, folder navigation tabs, left-sidebar page/folder icons, and sidebar label overrides. Available on all plans including FREE. Whether the footer is SHOWN (and its layout, copyright text and CTA) is update_ui_settings — this tool owns what is IN it.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped to a workspace). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `header_links` | object[] | no | Links shown in the docs header. Full replacement of the set — pass the complete desired list, not a delta. `color` is a hex background that renders the link as a filled button: give it to the workspace's call-to-action link (cta_url from get_workspace / update_branding) and leave it unset on the rest, so exactly one header item reads as the CTA. |
| `social_links` | object | no | — |
| `subheader_folders` | object[] | no | Where each top-level folder of the docs is PLACED. A folder normally has one of two placements, and these flags are how you choose between them: • SUBHEADER TAB — a top-level section in the category strip under the header (`inSubheader: true`, `hiddenInSidebar: true`). Selecting the tab scopes the left sidebar to that folder's pages; outside the tab they stay out of the sidebar tree. This is the normal, deliberate arrangement for a LARGE section — a blog, a changelog, a guides or reference set — and it is NOT a misconfiguration waiting to be tidied up. • SIDEBAR FOLDER — an ordinary folder in the main sidebar tree (`showInSidebar: true`, `hiddenInSidebar` unset, `inSubheader: false`). No tab; readers expand it in the sidebar. get_workspace reports the resolved choice per folder as `placement` ("subheader_tab" \| "sidebar_tree" \| "subheader_tab_and_sidebar_tree" \| "hidden") — read that instead of re-deriving it from the three booleans. HOW THE THREE COMBINE — two questions, not three settings: (1) is there a tab? `inSubheader`, and nothing else; removing a tab never puts its pages back in the sidebar. (2) are the pages in the ROOT sidebar tree — the tree shown when no tab is active? `showInSidebar` must be true AND `hiddenInSidebar` must not be; `hiddenInSidebar` also drops them from Previous/Next, which `showInSidebar: false` does not. Inside an active tab neither flag applies: a tab always scopes the sidebar to its own folder. COMBINATIONS THAT MEAN NOTHING: `showInSidebar: false` together with `hiddenInSidebar: true` (the root tree already excludes the folder for either reason — the only added effect is Previous/Next); `showInSidebar: true` with `hiddenInSidebar: true` (contradictory, `hiddenInSidebar` wins); any `hiddenInSidebar` on a "Getting Started" folder (ignored — it can never be hidden this way). `inSubheader: false` with no root-tree placement leaves the pages reachable only by direct URL or search. PAGE TABS — a tab can also be ONE PAGE instead of a folder: `kind: "page"`, `folderPath` = the page's path (`introduction` or "" for the site's front page, `guides/setup` for any other). Clicking it opens that page; it never scopes the sidebar. `hiddenInSidebar: true` takes the page out of the left sidebar (`showInSidebar` is ignored for pages). Typical use: the front page as its own tab (`{kind:"page", folderPath:"introduction", label:"Home", showInSidebar:true, beforeOverview:true}`) on a site whose home page hides the sidebar. ORDER — tabs render in array order AFTER the built-in "Overview" tab; `beforeOverview: true` puts an entry to the LEFT of Overview instead. When the home page hides its sidebar (update_ui_settings home_hide_sidebar), the front page is a landing, not part of Overview: Overview opens the first sidebar page after it, is not highlighted on the front page, and the front page leaves the sidebar tree. 🔴 DO NOT "FIX" A TAB'S `hiddenInSidebar`. Setting it to false on a folder that is a tab repairs nothing: the tab stays, and every page of that folder is MERGED into the root sidebar tree, so the sidebar grows by the whole section and the same pages are reachable twice. Change it only when the owner asks for it. |
| `sidebar_icons` | object[] | no | Icons shown next to pages/folders in the left sidebar. Full replacement of the set — pass the complete desired list, not a delta. |
| `footer_columns` | object[] | no | The footer's link columns (max 6). Full replacement of the set — pass the complete desired list, not a delta; read the current one from get_workspace `footerColumns`. The footer must also be enabled (update_ui_settings footer_enabled) before a reader sees any of this. Do NOT put social profiles here — they are social_links above, which the footer renders as icons. |
| `page_labels` | object[] | no | Sidebar label overrides. An override changes ONLY the text in the sidebar — never the page's address and never its position in the tree, so no link breaks and nothing is reordered. Use this for 'rename this page in the navigation'; renaming the file itself is a write_docs move, which changes the address (the old one keeps working through the site's redirect map, but links and citations to it become second-hand). Labels are derived from file names, so every README.md renders as "Introduction" — this is how several of them get told apart. Overridden labels are still offered for translation, so a renamed page stays localized. Full replacement of the set — pass the complete desired list, not a delta (read the current one from get_workspace `pageLabels`). |

<!-- /widget -->

## `social_links` fields

| Field | Type | Required | Description |
|---|---|---|---|
| `github` | string | no | — |
| `twitter` | string | no | — |
| `linkedin` | string | no | — |
| `youtube` | string | no | — |
| `slack` | string | no | — |

## Call it

<!-- widget:code-group -->

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "update_navigation",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"update_navigation","arguments":{}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### POST /api/v1/update_navigation

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped to a workspace). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `header_links` | object[] | no | Links shown in the docs header. Full replacement of the set — pass the complete desired list, not a delta. `color` is a hex background that renders the link as a filled button: give it to the workspace's call-to-action link (cta_url from get_workspace / update_branding) and leave it unset on the rest, so exactly one header item reads as the CTA. |
| `social_links` | object | no | — |
| `subheader_folders` | object[] | no | Where each top-level folder of the docs is PLACED. A folder normally has one of two placements, and these flags are how you choose between them: • SUBHEADER TAB — a top-level section in the category strip under the header (`inSubheader: true`, `hiddenInSidebar: true`). Selecting the tab scopes the left sidebar to that folder's pages; outside the tab they stay out of the sidebar tree. This is the normal, deliberate arrangement for a LARGE section — a blog, a changelog, a guides or reference set — and it is NOT a misconfiguration waiting to be tidied up. • SIDEBAR FOLDER — an ordinary folder in the main sidebar tree (`showInSidebar: true`, `hiddenInSidebar` unset, `inSubheader: false`). No tab; readers expand it in the sidebar. get_workspace reports the resolved choice per folder as `placement` ("subheader_tab" \| "sidebar_tree" \| "subheader_tab_and_sidebar_tree" \| "hidden") — read that instead of re-deriving it from the three booleans. HOW THE THREE COMBINE — two questions, not three settings: (1) is there a tab? `inSubheader`, and nothing else; removing a tab never puts its pages back in the sidebar. (2) are the pages in the ROOT sidebar tree — the tree shown when no tab is active? `showInSidebar` must be true AND `hiddenInSidebar` must not be; `hiddenInSidebar` also drops them from Previous/Next, which `showInSidebar: false` does not. Inside an active tab neither flag applies: a tab always scopes the sidebar to its own folder. COMBINATIONS THAT MEAN NOTHING: `showInSidebar: false` together with `hiddenInSidebar: true` (the root tree already excludes the folder for either reason — the only added effect is Previous/Next); `showInSidebar: true` with `hiddenInSidebar: true` (contradictory, `hiddenInSidebar` wins); any `hiddenInSidebar` on a "Getting Started" folder (ignored — it can never be hidden this way). `inSubheader: false` with no root-tree placement leaves the pages reachable only by direct URL or search. PAGE TABS — a tab can also be ONE PAGE instead of a folder: `kind: "page"`, `folderPath` = the page's path (`introduction` or "" for the site's front page, `guides/setup` for any other). Clicking it opens that page; it never scopes the sidebar. `hiddenInSidebar: true` takes the page out of the left sidebar (`showInSidebar` is ignored for pages). Typical use: the front page as its own tab (`{kind:"page", folderPath:"introduction", label:"Home", showInSidebar:true, beforeOverview:true}`) on a site whose home page hides the sidebar. ORDER — tabs render in array order AFTER the built-in "Overview" tab; `beforeOverview: true` puts an entry to the LEFT of Overview instead. When the home page hides its sidebar (update_ui_settings home_hide_sidebar), the front page is a landing, not part of Overview: Overview opens the first sidebar page after it, is not highlighted on the front page, and the front page leaves the sidebar tree. 🔴 DO NOT "FIX" A TAB'S `hiddenInSidebar`. Setting it to false on a folder that is a tab repairs nothing: the tab stays, and every page of that folder is MERGED into the root sidebar tree, so the sidebar grows by the whole section and the same pages are reachable twice. Change it only when the owner asks for it. |
| `sidebar_icons` | object[] | no | Icons shown next to pages/folders in the left sidebar. Full replacement of the set — pass the complete desired list, not a delta. |
| `footer_columns` | object[] | no | The footer's link columns (max 6). Full replacement of the set — pass the complete desired list, not a delta; read the current one from get_workspace `footerColumns`. The footer must also be enabled (update_ui_settings footer_enabled) before a reader sees any of this. Do NOT put social profiles here — they are social_links above, which the footer renders as icons. |
| `page_labels` | object[] | no | Sidebar label overrides. An override changes ONLY the text in the sidebar — never the page's address and never its position in the tree, so no link breaks and nothing is reordered. Use this for 'rename this page in the navigation'; renaming the file itself is a write_docs move, which changes the address (the old one keeps working through the site's redirect map, but links and citations to it become second-hand). Labels are derived from file names, so every README.md renders as "Introduction" — this is how several of them get told apart. Overridden labels are still offered for translation, so a renamed page stays localized. Full replacement of the set — pass the complete desired list, not a delta (read the current one from get_workspace `pageLabels`). |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/update_navigation' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

<!-- /widget -->
