---
title: "MCP server for documentation: what it is and why it wins"
description: "How Claude Code and Cursor read and edit documentation through Model Context Protocol, which tools matter, and why agents are now a traffic channel."
---

# MCP server for documentation: what it is and why it wins

Model Context Protocol (MCP) is the connector standard Anthropic released in late 2024. By mid-2026 it is supported by Claude Code, Cursor, ChatGPT, and a growing list of agents. For documentation, MCP turns your docs from a website-only asset into a programmatic surface that AI agents can read and act on.

This post explains what MCP is, what tools a docs MCP server exposes, and how Docsbook ships one.

## TL;DR

- MCP = standard way for AI agents to call external tools
- A docs MCP server exposes tools like `get_analytics`, `update_branding`, `set_chat_hooks`
- Agents discover capabilities, request OAuth, then call tools as part of their work
- Docsbook ships a managed MCP server at `docsbook.io/api/mcp/server`
- This is now a primary AI distribution channel — Mintlify measured AI coding agents at 45.3% of requests to the docs sites it hosts in March 2026, Claude Code at 25.2% and Cursor at 18.0% ([source](https://www.mintlify.com/blog/state-of-ai))

## What MCP actually is

MCP is a JSON-RPC protocol layered over HTTP (or stdio). An agent connects to an MCP server, asks "what tools do you have?", receives a typed schema, and calls tools. Authentication is OAuth 2.0 with PKCE.

The simplest way to think about it: REST API + OAuth + a discovery endpoint + tools instead of resources.

## Why documentation benefits from MCP

Three workflows:

### 1. Reading docs as structured data

Without MCP, an agent fetches an HTML page, parses it, and hopes the structure is intact. With [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) running locally (`npx markdown-lsp <subcommand> ./docs`), the agent parses the doc graph on disk and receives clean Markdown or JSON without a network round-trip.

This means agents:

- Know the full table of contents before reading
- Can read individual sections instead of full pages
- See cross-links as graph edges, not regex matches
- Get version-stable metadata

### 2. Editing docs config from the agent

A user in Claude Code can say "set my docs accent color to brand purple and add a Discord link in the footer." The agent calls `update_branding` and `update_navigation` on the MCP server. No dashboard switching, no copy-pasting, no markdown editing.

### 3. Querying docs analytics from inside the agent

"Which pages got the most failed searches last week?" — the agent calls `get_failed_searches`, sees the list, and offers to draft missing content right there.

## What tools a good docs MCP server exposes

Docsbook's MCP server exposes tools in these categories. The full list is returned by the server itself on connection — the table below is the shape, not the inventory:

| Category | Examples |
|---|---|
| Workspace | `list_workspaces`, `get_workspace`, `create_workspace` |
| Content and documentation | `search_docs`, `get_doc_outline`, `write_docs` |
| Branding | `update_branding`, `update_ui_settings`, `update_navigation` |
| AI settings | `update_ai_settings`, `set_chat_system_prompt`, `set_chat_hooks` |
| SEO and domain | `update_seo`, `update_domain` |
| Translation | `update_languages`, `set_translation_mode`, `approve_translation` |
| Analytics | `get_analytics`, `get_ai_questions`, `get_failed_searches`, `get_negative_feedback`, `get_top_visitors`, `get_visitor_activity` |
| Webhooks | `register_webhook_*`, `list_webhook_deliveries`, `test_webhook` |
| Skills | `find_skill` (queries the [docs-skills](https://github.com/Docsbook-io/docs-skills) catalog) |

## Connecting from Claude Code

```
mcp add --transport http https://docsbook.io/api/mcp/server
```

The OAuth flow opens in the browser, you authorize, the tools appear in Claude Code. No API keys to manage, no config file to edit.

Cursor uses the same MCP server with similar UX. ChatGPT and Gemini are adding HTTP MCP support through 2026.

## LSP-style tools are the underrated half (local plugin, not hosted MCP)

Most docs MCP marketing focuses on read/write — in Docsbook's case, `search_docs` to find citable sections, `get_doc_outline` to see every page's title, heading count, and size before searching or writing, and `write_docs` to commit changes (gated by OAuth consent: the customer picks read-only or read-write scope when authorizing the connection). The bigger value for agents is the LSP-style search and navigation surface — but for a working repo, that surface is better delivered as a **local Claude Code plugin** than as a hosted MCP tool. Disk-local parsing is faster, cheaper, and doesn't require the docs to be published yet.

Docsbook ships this via [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) — run it locally and the agent gains:

- `doc_outline` — heading hierarchy for a page (no bodies)
- `doc_search_symbols` — fuzzy subsequence over all headings ("oaf" → "OAuth flow")
- `doc_search_text` — full-text with snippets and exact line/col
- `doc_search_links_to` — incoming references (LSP `references`)
- `doc_resolve_link` — relative or wiki link → absolute GitHub URL with anchor
- `doc_definition` — `page#anchor` → exact source position

LSP — Language Server Protocol — is what powers go-to-definition, find-references, and symbol search in VS Code. The plugin applies the same model to your local docs tree, so an agent navigates with IDE-like precision. The hosted MCP server stays focused on workspace operations (branding, analytics, webhooks, translations) where the cloud actually owns the data.

## Why this is a real distribution channel

Three signals from 2025–2026:

1. **Mintlify telemetry.** Mintlify measured 30 days of traffic across the documentation sites it hosts — roughly 790 million requests — and reported that AI coding agents accounted for **45.3% of all requests**, with Claude Code at 25.2% and Cursor at 18.0% ([The state of agent traffic in documentation](https://www.mintlify.com/blog/state-of-ai), published 3 April 2026). Its follow-up measurement put the agent share at **66% of traffic in July 2026** ([2026 midyear report](https://www.mintlify.com/blog/state-of-docs-traffic), published 29 July 2026). That is one vendor's fleet rather than the whole web, but it is the largest published measurement of agent traffic to documentation.
2. **Anthropic dogfooding.** Anthropic's own documentation and the Claude Code docs are MCP-first.
3. **The client side is already built.** Claude Code, Cursor and ChatGPT ship MCP support, so the connector does not need adoption on the reader's side — only on yours.

If you build for developers and your audience uses Claude Code or Cursor, MCP is no longer optional infrastructure.

## What it costs to build yourself

A reasonable docs MCP server requires:

- HTTP transport + JSON-RPC framing
- OAuth 2.0 Authorization Code + PKCE flow
- Tool definitions with typed schemas
- Doc graph parsing for read tools — usually delivered as a local CLI tool like [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) rather than a hosted endpoint, because disk-local parsing is faster and cheaper
- Write access if you want config edits
- Rate limiting and audit logging

About 4–6 engineering weeks if you have not done it before. Docsbook's MCP server comes with the workspace and costs nothing to run; `markdown-lsp` is free and open source for the doc-graph read tools.

Docsbook ships a managed MCP server with OAuth, so Claude Code and Cursor read and edit your docs without you running anything. Connection details are at [docsbook.io/mcp](https://docsbook.io/mcp).

[Start free — no credit card](https://docsbook.io/start)

## Next steps

- [docs-skills: modular capabilities for AI agents](./docs-skills-for-ai-agents.md) — the layer that sits on top of MCP
- [llms.txt explained](./llms-txt-guide.md) — the companion standard for agents without MCP
- [AI documentation platforms compared](./ai-docs-platform-comparison.md) — which of the four ship an MCP server
- [How to get your documentation cited by ChatGPT](./how-to-get-docs-cited-by-chatgpt.md) — the discovery side of the same channel
