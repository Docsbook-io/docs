---
title: "Update ui settings"
description: "Show or hide one interface element of the docs site — the header search button, sidebar search, the copy-page menu and its entries, previous/next links, breadcrumbs,…"
---

# Update ui settings

<!-- widget:mcp access=write -->

## update_ui_settings

Show or hide one interface element of the docs site — the header search button, sidebar search, the copy-page menu and its entries, previous/next links, breadcrumbs, scroll-to-top, page feedback, the 'was this helpful' bar, edit-on-GitHub, the Ask AI buttons (header, outline, on selection), copy-as-markdown, and where the language and theme switchers sit. Also the HOME-PAGE LANDING switches (home_hide_sidebar, home_hide_outline, home_wide_content), which strip the sidebar, the outline and the column width off the site's FRONT PAGE ONLY so it can read as a landing page — use them for 'make the home page a landing page', 'full-width main page', «сделай главную посадочной», «убери сайдбары на главной». And the SITE FOOTER (whether it exists, its layout, its copyright text, its call-to-action button, and whether it shows the social icons and a theme picker) — 'add a footer', 'put a copyright line at the bottom', «добавь футер». Pass only the toggles the user mentioned; the rest are untouched. Use it for 'hide the search button', 'remove breadcrumbs', «убери кнопку поиска». NOT header links or folder tabs — and NOT the footer's LINK COLUMNS, which are update_navigation's footer_columns. NOT colours or fonts (update_branding). All toggles available on FREE plan. BEFORE CHANGING THIS, call `docsbook_expert` with what you are trying to achieve: it names the reading that should decide the value, so the setting is a conclusion rather than a guess. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | yes | Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `show_search_button` | boolean | no | The search button in the site header. |
| `show_search_in_sidebar` | boolean | no | The search box at the top of the left sidebar. |
| `show_copy_page_button` | boolean | no | — |
| `show_copy_skills_url` | boolean | no | Show "Copy Skills.md URL" in the Copy page dropdown |
| `show_view_as_markdown` | boolean | no | Show "View as Markdown" in the Copy page dropdown |
| `show_open_in_chatgpt` | boolean | no | Show "Open in ChatGPT" in the Copy page dropdown |
| `show_open_in_claude` | boolean | no | Show "Open in Claude" in the Copy page dropdown |
| `show_open_in_cursor` | boolean | no | Show "Open in Cursor" in the Copy page dropdown |
| `show_open_in_windsurf` | boolean | no | Show "Open in Windsurf" in the Copy page dropdown |
| `show_connect_vscode` | boolean | no | Show "Connect to VSCode" in the Copy page dropdown |
| `show_prev_next_buttons` | boolean | no | — |
| `show_breadcrumbs` | boolean | no | — |
| `home_hide_sidebar` | boolean | no | HOME PAGE ONLY: hide the left navigation rail on the site's front page (its top-level README/index), on desktop — the mobile drawer stays. Every other page keeps its sidebar. |
| `home_hide_outline` | boolean | no | HOME PAGE ONLY: hide the right-hand "On this page" outline on the site's front page. |
| `home_wide_content` | boolean | no | HOME PAGE ONLY: let the front page's content run the full window width instead of the fixed reading column. |
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
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"update_ui_settings","arguments":{"workspace_id":"<workspace_id>","footer_layout":"columns"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/update_ui_settings

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/update_ui_settings' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"workspace_id":"<workspace_id>","footer_layout":"columns"}}'
```

<!-- /widget -->
