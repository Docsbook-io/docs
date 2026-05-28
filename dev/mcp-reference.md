# MCP server — full tool reference

**Endpoint:** `https://docsbook.io/api/mcp/server`
**Authentication:** OAuth 2.0 Authorization Code + PKCE, Bearer tokens
**OAuth metadata:** `https://docsbook.io/.well-known/oauth-authorization-server`

### Usage with Claude Code
```
mcp add --transport http https://docsbook.io/api/mcp/server
```
After authorizing in the browser, tools become available in Claude Code.

---

## Workspace and branding

| Tool | Minimum plan | Description |
|---|---|---|
| `get_info` | Free | Information about the MCP server and its capabilities |
| `list_workspaces` | Free | List all workspaces with plan_capabilities |
| `get_workspace` | Free | Get a workspace by ID or `owner/repo` |
| `create_workspace` | Free | Create a workspace for a GitHub repo |
| `update_branding` | Free | Colors, fonts, logo, theme |
| `update_ui_settings` | Free | Show/hide UI components |
| `update_navigation` | Free | Header links, social links, folder tabs |
| `update_ai_settings` | PRO | Enable AI chat, choose provider, API key |
| `update_seo` | PRO | Enable/disable classic SEO (canonical, OG, sitemap, JSON-LD) |
| `update_geo` | PRO | Enable/disable GEO — TL;DR block, dateModified, Person/Author, semantic HTML for AI search |
| `update_aeo` | PRO | Enable/disable AEO — auto-markup FAQPage, HowTo, speakable for featured snippets and voice assistants |
| `update_domain` | PRO | Set or remove a custom domain |
| `update_languages` | PRO | Enable languages for translation |

## Documentation and content

Documentation graph search is no longer hosted. Install the `docs-sync` Claude Code plugin from [`docs-claude-plugins`](https://github.com/Docsbook-io/docs-claude-plugins) — it ships `markdown-lsp` as a local MCP server and gives the agent LSP-style tools (`doc_outline`, `doc_search_text`, `doc_search_symbols`, `doc_search_links_to`, `doc_resolve_link`, etc.) over the working tree.

## AI chat

| Tool | Minimum plan | Description |
|---|---|---|
| `get_chat_system_prompt` | PRO+ | Get the current AI chat system_prompt (also in admin panel: AI Chat → System prompt) |
| `set_chat_system_prompt` | PRO+ | Replace system_prompt (also in admin panel) |
| `set_chat_hooks` | PRO+ | Configure pre/post LLM hooks (also in admin panel: AI Chat → Advanced hooks) |
| `test_chat_hook` | PRO+ | Run a hook against test data (also in admin panel: Test button) |

## Translations (management)

| Tool | Minimum plan | Description |
|---|---|---|
| `set_translation_mode` | PRO+ | `auto` (built-in AI), `manual`, or `external` (custom webhook pipeline). Also in admin panel: Languages → Translation mode |
| `list_pending_translations` | PRO | Translations awaiting approval (also in admin panel: Languages → Pending translations) |
| `get_translation` | PRO | Get a specific translation |
| `upload_translation` | PRO+ | Upload an external translation |
| `approve_translation` | PRO+ | Approve a translation (also in admin panel: Approve in Pending list) |
| `delete_translation` | PRO+ | Delete a translation (also in admin panel: Delete in Pending list) |

## Analytics and observability

| Tool | Minimum plan | Description |
|---|---|---|
| `get_analytics` | Free | Page views, visitors, top pages, referrers |
| `get_ai_usage` | Free | AI and translation usage, limits, remaining quota |
| `get_ai_questions` | PRO | All questions users asked the AI chat |
| `get_ai_unanswered` | PRO | Questions the AI could not answer |
| `get_negative_feedback` | PRO | Pages with negative feedback (👎). Also in admin panel: Analytics → Negative feedback |
| `get_failed_searches` | PRO | Search queries with no results. Also in admin panel: Analytics → Failed searches |
| `get_popular_searches` | PRO | Top search queries. Also in admin panel: Analytics → Popular searches |
| `get_page_journeys` | PRO+ | User navigation paths between pages. Each session contains a stable `visitor_id` — can be passed to `get_visitor_activity` for details. Also in admin panel: Analytics → User journeys |
| `get_top_visitors` | PRO+ | Top active anonymous visitors for a period — `visitor_id`, view count, country, first/last seen. Entry point for drilling down into a specific visitor's activity |
| `get_visitor_activity` | PRO+ | Chronological timeline of a single visitor's actions by `visitor_id`: pageviews, feedback, cta_click, etc. with paths and details for each event. Raw IPs are not returned |
| `query_events` | PRO+ | Arbitrary query to Axiom (platform events) |

## Webhooks

All 6 operations below are available both via MCP and via the admin panel (**Webhooks** tab in `FloatWidget`).

| Tool | Description |
|---|---|
| `register_webhook_<event>` | Register a webhook (HMAC secret + URL) for one of ~15 events — see [webhooks-reference.md](webhooks-reference.md) |
| `list_webhooks` | List registered webhooks |
| `unregister_webhook` | Unregister a webhook |
| `list_webhook_deliveries` | Delivery history (status, retry, payload) |
| `replay_webhook_delivery` | Resend a specific delivery |
| `test_webhook` | Send a test payload to a URL |

## Skills discovery

| Tool | Description |
|---|---|
| `find_skill` | Find a matching SKILL.md in the `docs-skills` catalog by `query` + filters (`category`, `requires_plan`). Returns `raw_url` from which the user's agent reads the SKILL.md — see [skills-reference.md](skills-reference.md) |
