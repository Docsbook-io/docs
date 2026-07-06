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

## Install in your AI client

The Docsbook MCP server is a remote HTTP server with OAuth — every modern MCP client can connect to it using the same endpoint.

### Claude Code

```bash
claude mcp add --transport http docsbook https://docsbook.io/api/mcp/server
```

The first call opens a browser tab for OAuth. After consent, the tools become available inside Claude Code.

### Cursor

Add the server to `~/.cursor/mcp.json` (or use **Settings → MCP & Integrations → New MCP server**):

```json
{
  "mcpServers": {
    "docsbook": {
      "url": "https://docsbook.io/api/mcp/server"
    }
  }
}
```

Reload Cursor — OAuth opens in the browser on first use.

### Codex CLI

Codex stores MCP servers in `~/.codex/config.toml`:

```toml
[mcp_servers.docsbook]
url = "https://docsbook.io/api/mcp/server"
```

### Windsurf

Edit `~/.codeium/windsurf/mcp_config.json` and refresh the Cascade panel:

```json
{
  "mcpServers": {
    "docsbook": {
      "serverUrl": "https://docsbook.io/api/mcp/server"
    }
  }
}
```

### Cline

Open **Cline → MCP Servers → Configure MCP Servers** and paste:

```json
{
  "mcpServers": {
    "docsbook": {
      "url": "https://docsbook.io/api/mcp/server",
      "transportType": "http"
    }
  }
}
```

### Gemini CLI

Add to `~/.gemini/settings.json`:

```json
{
  "mcpServers": {
    "docsbook": {
      "httpUrl": "https://docsbook.io/api/mcp/server"
    }
  }
}
```

### GitHub Copilot (VS Code)

Create `.vscode/mcp.json` inside your workspace, then enable the server from the Copilot Chat MCP picker:

```json
{
  "servers": {
    "docsbook": {
      "type": "http",
      "url": "https://docsbook.io/api/mcp/server"
    }
  }
}
```

### ChatGPT

ChatGPT supports remote MCP through **Connectors** (Pro / Business / Enterprise plans).

1. Open **ChatGPT → Settings → Connectors → Advanced → Developer mode**.
2. Click **Create** and paste the URL: `https://docsbook.io/api/mcp/server`.
3. Authorize in the browser when prompted.

## Tool categories

| Category | Examples |
|---|---|
| Workspace | `list_workspaces`, `create_workspace`, `get_workspace` |
| Branding & UI | `update_branding`, `update_ui_settings`, `update_navigation` |
| Content & search | `search_docs`, `write_docs` |
| AI chat | `get_chat_system_prompt`, `set_chat_system_prompt`, `set_chat_hooks` |
| Translations | `set_translation_mode`, `list_pending_translations`, `approve_translation` |
| Analytics | `get_analytics`, `get_ai_usage`, `get_failed_searches`, `get_page_journeys`, `get_top_visitors`, `get_visitor_activity`, `query_events` |
| Webhooks | `register_webhook_*`, `list_webhooks`, `replay_webhook_delivery` |
| Skills | `find_skill` |

## Searching and editing documentation content

There are two ways to work with your docs content from an agent:

- **Hosted, via MCP tokens** — `search_docs` (Free plan and up, read-only, works with any connected token regardless of its scope) and `write_docs` (Free+, requires a token authorized with **read-write** scope; commits one or more files as a single atomic git commit). These run against the Docsbook-hosted repository directly, no local checkout needed.
- **Local, via `markdown-lsp`** — for an agent working directly on your checked-out files, [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) exposes richer LSP-style `doc_*` tools (outline, fuzzy headings, full-text, link references, resolve links) by running `npx markdown-lsp <subcommand> ./docs` on the agent's machine. See [Source of Truth](./source-of-truth.md) for the tool list and rationale.

Use `search_docs`/`write_docs` when the agent only has an MCP connection (no local checkout); use `markdown-lsp` when the agent already has the repo on disk and wants deeper graph navigation.

## Plan gating

Each tool declares a minimum plan. The server returns a structured error when a tool is called below the required tier.

| Plan | Available tool groups |
|---|---|
| Free | Workspace, branding, UI, navigation, analytics (24h), `find_skill`, `search_docs`, `write_docs` (with a read-write token) |
| PRO | + AI settings, SEO, languages, chat hooks, translations, deeper analytics |
| PRO+ | + page journeys, top visitors + visitor activity drill-down, `query_events` |
| Business | + custom domain, webhooks, bring-your-own AI/translation API key |

## Learn more

The full product page lives at [docsbook.io/mcp](https://docsbook.io/mcp), with an interactive install selector for Claude Code, Cursor, Codex, Windsurf, Cline, Gemini CLI, GitHub Copilot, and ChatGPT.

## Related

- [Chat Hooks](./chat-hooks.md) — Configure pre/post-LLM hooks via MCP.
- [Docs Skills](./skills.md) — Discover SKILL.md files through `find_skill`.
- [Webhooks](../webhooks.md) — Register event handlers from MCP.
