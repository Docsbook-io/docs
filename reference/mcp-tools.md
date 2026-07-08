---
title: "MCP Tools Reference"
description: "Complete reference of Docsbook MCP tools — workspace management, content access, AI chat configuration, translations, analytics, webhooks, and skills discovery."
---

# MCP Tools Reference

This page lists every tool exposed by the Docsbook MCP server at `https://docsbook.io/api/mcp/server`. Each tool requires Bearer authentication via OAuth 2.0 + PKCE. The minimum plan column indicates the workspace tier required to call the tool; calls below that tier return a `plan_required` error.

To connect from Claude Code:

```bash
mcp add --transport http https://docsbook.io/api/mcp/server
```

## Workspace and branding

| Tool                  | Min plan | Description                                                  |
| --------------------- | -------- | ------------------------------------------------------------ |
| `get_info`            | Free     | Server capabilities, version, available tool list            |
| `list_workspaces`     | Free     | All workspaces for the authenticated user with capabilities  |
| `get_workspace`       | Free     | Fetch one workspace by ID or `owner/repo`                    |
| `create_workspace`    | Free     | Create a workspace from a GitHub repository                  |
| `update_branding`     | Free     | Colors, fonts, logo, icon, default theme                     |
| `update_ui_settings`  | Free     | Toggle header, search, feedback, copy button, breadcrumbs    |
| `update_navigation`   | Free     | Header links, social links, folder tabs                      |
| `update_ai_settings`  | PRO      | Enable AI chat, set provider and API key, model selection (bring-your-own key is Business only) |
| `update_seo`          | PRO      | SEO meta tags, sitemap, OpenGraph                            |
| `update_domain`       | Business | Attach or remove a custom domain                             |
| `update_languages`    | PRO      | Enable target languages for AI translation                   |

## Content and documentation

| Tool           | Min plan | Description                                                                                          |
| -------------- | -------- | ----------------------------------------------------------------------------------------------------- |
| `search_docs`  | Free     | Full-text/regex/heading/path search over the workspace's documentation content. Read-only — works with any token regardless of read/write scope. |
| `get_doc_outline` | Free  | List every markdown page's title, heading count, and size before searching or writing. Read-only — works with any token regardless of read/write scope. |
| `write_docs`   | Free     | Commit one or more markdown files to the workspace's docs repo in a single atomic git commit. Requires a token authorized with **read-write** scope — a read-only token is refused. |

For deeper local graph navigation (outline, fuzzy headings, link references, resolve links) while an agent has your docs checked out on disk, use [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) instead — run `npx markdown-lsp <subcommand> ./docs` to expose LSP-style `doc_*` tools on the working tree. See the [markdown-lsp README](https://github.com/Docsbook-io/markdown-lsp) for setup. `search_docs`/`write_docs` and `markdown-lsp` are complementary: the former work over the hosted MCP connection with no local checkout, the latter needs the repo on disk.

## AI chat

| Tool                      | Min plan | Description                                |
| ------------------------- | -------- | ------------------------------------------ |
| `get_chat_system_prompt`  | PRO+     | Read the workspace's chat system prompt    |
| `set_chat_system_prompt`  | PRO+     | Replace the chat system prompt             |
| `set_chat_hooks`          | PRO+     | Configure pre/post LLM hooks               |
| `test_chat_hook`          | PRO+     | Run a hook against a synthetic payload     |

## Translations

| Tool                         | Min plan | Description                                         |
| ---------------------------- | -------- | --------------------------------------------------- |
| `set_translation_mode`       | PRO+     | `auto` (built-in AI) or `external` (webhook flow)   |
| `list_pending_translations`  | PRO      | Translations awaiting approval                      |
| `get_translation`            | PRO      | Fetch one translation by language and path          |
| `upload_translation`         | PRO+     | Upload an externally-produced translation           |
| `approve_translation`        | PRO+     | Publish a pending translation                       |
| `delete_translation`         | PRO+     | Remove a translation                                |

## Analytics and observability

| Tool                    | Min plan | Description                                              |
| ----------------------- | -------- | -------------------------------------------------------- |
| `get_analytics`         | Free     | Views, visitors, top pages, referrers (period by plan)   |
| `get_ai_usage`          | Free     | AI chat and translation usage, limits, remaining quota   |
| `get_ai_questions`      | PRO      | All questions asked to the AI chat                       |
| `get_ai_unanswered`     | PRO      | Questions the AI could not answer                        |
| `get_negative_feedback` | PRO      | Pages with thumbs-down feedback                          |
| `get_failed_searches`   | PRO      | Search queries that returned zero results                |
| `get_popular_searches`  | PRO      | Top search queries by frequency                          |
| `get_page_journeys`     | PRO+     | User navigation paths between pages                      |
| `query_events`          | PRO+     | Arbitrary Axiom query over platform events               |

## Webhooks

Registering a webhook is a **Business-exclusive** capability — Free and Pro/Pro+ workspaces cannot register any webhook regardless of event type.

| Tool                         | Description                                                   |
| ---------------------------- | ------------------------------------------------------------- |
| `register_webhook_<event>`   | Register a webhook for one of ~15 events (HMAC secret + URL). Business only. |
| `list_webhooks`              | List registered webhooks for the workspace                    |
| `unregister_webhook`         | Remove a webhook subscription                                  |
| `list_webhook_deliveries`    | Delivery history with status, retry count, payload             |
| `replay_webhook_delivery`    | Re-deliver a specific past delivery                            |
| `test_webhook`               | Send a synthetic payload to a URL                              |

Event types include `content.indexed`, `translation.completed`, `chat.no_answer`, `chat.negative_feedback`, `plan.upgraded`, `usage.limit_approaching`, and others — see [Webhooks](../webhooks.md) for the full list and payload schemas.

## Skills discovery

| Tool         | Description                                                                              |
| ------------ | ---------------------------------------------------------------------------------------- |
| `find_skill` | Search the `docs-skills` catalog by `query` with optional `category` and `requires_plan` filters. Returns `raw_url` for the agent to fetch the SKILL.md directly. |

## Related

- [MCP server overview](../ai/mcp.md)
- [Webhooks reference](../webhooks.md)
- [Chat hooks](../ai/chat-hooks.md)
