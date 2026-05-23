---
title: "MCP Server — Control Docsbook From Claude"
description: "Manage workspaces, branding, AI chat, translations, analytics, and webhooks from Claude Code over a standard MCP HTTP transport."
---

# MCP Server

Docsbook ships a Model Context Protocol (MCP) server. Connect Claude Code or any MCP-compatible client and manage every aspect of your docs without leaving the editor.

## What MCP is

The Model Context Protocol is an open standard for exposing tools, resources, and prompts to AI agents over a typed RPC interface. The Docsbook MCP server exposes around 40 tools covering the full product surface.

## Endpoint

```text
https://docsbook.io/api/mcp/server
```

Authentication is OAuth 2.0 Authorization Code with PKCE. Bearer tokens are returned to the client and refreshed transparently.

## Install in Claude Code

```bash
claude mcp add --transport http docsbook https://docsbook.io/api/mcp/server
```

The first call opens a browser tab for OAuth. After consent, the tools become available inside Claude Code.

## Tool categories

| Category | Examples |
|---|---|
| Workspace | `list_workspaces`, `create_workspace`, `get_workspace` |
| Branding & UI | `update_branding`, `update_ui_settings`, `update_navigation` |
| AI chat | `get_chat_system_prompt`, `set_chat_system_prompt`, `set_chat_hooks` |
| Doc graph | `get_doc_graph`, `read_doc_sections`, `reindex_doc_graph` |
| Translations | `set_translation_mode`, `list_pending_translations`, `approve_translation` |
| Analytics | `get_analytics`, `get_ai_usage`, `get_failed_searches` |
| Webhooks | `register_webhook_*`, `list_webhooks`, `replay_webhook_delivery` |
| Skills | `find_skill` |

## Plan gating

Each tool declares a minimum plan. The server returns a structured error when a tool is called below the required tier.

| Plan | Available tool groups |
|---|---|
| Free | Workspace, branding, UI, navigation, analytics (24h), `find_skill` |
| PRO | + AI settings, SEO, domain, languages, chat hooks, translations, deeper analytics |
| PRO+ | + Doc graph (`get_doc_graph`, `read_doc_sections`, `reindex_doc_graph`), page journeys, `query_events` |

## Learn more

The full product page lives at [docsbook.io/mcp](https://docsbook.io/mcp), with copy-pasteable install snippets for Claude Code, Cursor, and Cline.

## Related

- [Chat Hooks](./chat-hooks.md) — Configure pre/post-LLM hooks via MCP.
- [Docs Skills](./skills.md) — Discover SKILL.md files through `find_skill`.
- [Webhooks](../webhooks.md) — Register event handlers from MCP.
