---
title: "Update ui settings"
description: "Show or hide one interface element of the docs site — the header search button, sidebar search, collapsible top-level sidebar folders (sidebar_collapse_top_folders: «сверни папки…"
---

# Update ui settings

<!-- widget:mcp access=write price-millicents=1 -->

## update_ui_settings

Show or hide one interface element of the docs site — the header search button, sidebar search, collapsible top-level sidebar folders (sidebar_collapse_top_folders: «сверни папки первого уровня»), the copy-page menu and its entries, previous/next links, breadcrumbs, scroll-to-top, page feedback, the 'was this helpful' bar, edit-on-GitHub, the Ask AI buttons (header, outline, on selection), copy-as-markdown, and where the language and theme switchers sit. Also the HOME-PAGE LANDING switches (home_hide_sidebar, home_hide_outline, home_hide_chrome, home_landing_typography), which strip the sidebar, the outline and the article chrome (breadcrumbs, 'Updated', rating bar, prev/next) off the site's FRONT PAGE ONLY and give its sections landing-page scale so it can read as a landing page — use them for 'make the home page a landing page', «сделай главную посадочной», «убери сайдбары на главной». There is no full-width/edge-to-edge switch: the front page always sits in the same reading column as every other page. And the SITE FOOTER (whether it exists, its layout, its copyright text, its call-to-action button, and whether it shows the social icons and a theme picker) — 'add a footer', 'put a copyright line at the bottom', «добавь футер». Pass only the toggles the user mentioned; the rest are untouched. NOT header links or folder tabs — and NOT the footer's LINK COLUMNS, which are update_navigation's footer_columns. NOT colours or fonts (update_branding). All toggles available on FREE plan.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `show_search_button` | boolean | no | The search button in the site header. |
| `show_search_in_sidebar` | boolean | no | The search box at the top of the left sidebar. |
| `sidebar_collapse_top_folders` | boolean | no | First-level sidebar folders become collapsible rows (chevron + name, fold on click, open by themselves around the current page) like second-level folders, instead of always-open uppercase section headings. Their pages stay flush left — no indent and no guide line, which remain the look of the second level. Off by default. |
| `show_copy_page_button` | boolean | no | — |
| `show_copy_skills_url` | boolean | no | Show "Copy Skills.md URL" in the Copy page dropdown |
| `show_view_as_markdown` | boolean | no | Show "View as Markdown" in the Copy page dropdown |
| `show_open_in_chatgpt` | boolean | no | Show "Open in ChatGPT" in the Copy page dropdown |
| `show_open_in_claude` | boolean | no | Show "Open in Claude" in the Copy page dropdown |
| `show_open_in_cursor` | boolean | no | Show "Open in Cursor" in the Copy page dropdown |
| `show_open_in_windsurf` | boolean | no | Show "Open in Windsurf" in the Copy page dropdown |
| `show_connect_vscode` | boolean | no | Show "Connect to VSCode" in the Copy page dropdown |
| `show_connect_mcp` | boolean | no | Show "Connect MCP" in the Copy page dropdown — copies a prompt that installs this project's MCP server into any agent |
| `show_prev_next_buttons` | boolean | no | — |
| `show_breadcrumbs` | boolean | no | — |
| `home_hide_sidebar` | boolean | no | HOME PAGE ONLY: hide the left navigation rail on the site's front page (its top-level README/index), on desktop — the mobile drawer stays. Every other page keeps its sidebar. It also makes the front page a landing rather than the first doc: it leaves the sidebar tree, and the subheader's "Overview" tab opens the next page instead and is not highlighted on the front page (give the front page its own tab with update_navigation subheader_folders kind:"page" if the owner wants one). |
| `home_hide_outline` | boolean | no | HOME PAGE ONLY: hide the right-hand "On this page" outline on the site's front page. |
| `home_hide_chrome` | boolean | no | HOME PAGE ONLY: remove the article chrome from the front page — the breadcrumb/copy-page bar, the "Updated" line, the "Was this page helpful?" bar and the previous/next links — so it reads as a landing page, not as page one of a manual. |
| `home_landing_typography` | boolean | no | HOME PAGE ONLY: landing-page scale for the front page's sections — each h2 becomes a large section title with air above it and the paragraph under it reads as that section's lead. Pair it with hero/stats/cards widgets in the README. |
| `show_scroll_to_top` | boolean | no | — |
| `show_page_feedback` | boolean | no | — |
| `show_content_feedback` | boolean | no | — |
| `show_edit_on_github` | boolean | no | — |
| `show_ask_ai_button` | boolean | no | Show AI chat button (AI must be enabled separately) |
| `show_ask_ai_header` | boolean | no | — |
| `show_ask_ai_outline` | boolean | no | — |
| `show_ask_ai_on_selection` | boolean | no | Show floating Ask AI button when user selects text in the docs (AI must be enabled separately) |
| `show_ask_docs_button` | boolean | no | Floating "Ask Docs" pill pinned to the page's bottom-right corner |
| `show_copy_markdown` | boolean | no | — |
| `language_in_header` | boolean | no | — |
| `theme_in_header` | boolean | no | — |
| `language_sidebar_toggle` | boolean | no | — |
| `github_edit_base` | string | no | Base URL for Edit on GitHub links |
| `footer_enabled` | boolean | no | Show the site footer — the band under every docs page. Off by default. It renders only once it has content: a link column (update_navigation footer_columns), footer_text, a CTA, the logo or the social icons. |
| `footer_layout` | string | no | How the footer's blocks sit: 'columns' (brand block left, link columns right), 'centered' (everything stacked down the middle) or 'minimal' (one row — text left, links and socials right). Placement only; it never turns a block off. One of: `columns`, `centered`, `minimal`. |
| `footer_text` | string | no | Free text under the footer's logo — copyright line, legal entity, postal address. Plain text: line breaks are kept, markup is not. Max 600 chars. Pass an empty string to clear it. |
| `footer_show_logo` | boolean | no | Show the site logo in the footer's brand block. |
| `footer_show_socials` | boolean | no | Show the social icons in the footer. WHICH accounts is not a footer setting — it is the workspace's social_links (update_navigation); this only decides whether the footer draws them. |
| `footer_show_theme_picker` | boolean | no | Show a three-way light / dark / system picker in the footer. |
| `footer_cta_label` | string | no | Label for an optional call-to-action button in the footer's brand block (e.g. 'Get started'). Without a label no button is drawn. Pass an empty string to remove it. |
| `footer_cta_url` | string | no | Where the footer's call-to-action button goes. Leave unset to reuse the workspace's own cta_url (see get_workspace) rather than repeating it. |

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

### Use cases

- Use it for 'hide the search button', 'remove breadcrumbs', «убери кнопку поиска».

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "update_ui_settings",
    "arguments": {
      "workspace_id": "<workspace_id>",
      "footer_layout": "columns"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"update_ui_settings","arguments":{"workspace_id":"<workspace_id>","footer_layout":"columns"}}}'
```

### REST

```bash
curl -X POST 'https://docsbook.io/api/v1/update_ui_settings' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"workspace_id":"<workspace_id>","footer_layout":"columns"}'
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
