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
| AI chat | `get_chat_system_prompt`, `set_chat_system_prompt`, `set_chat_hooks` |
| Translations | `set_translation_mode`, `list_pending_translations`, `approve_translation` |
| Analytics | `get_analytics`, `get_ai_usage`, `get_failed_searches`, `get_page_journeys`, `get_top_visitors`, `get_visitor_activity`, `query_events` |
| Webhooks | `register_webhook_*`, `list_webhooks`, `replay_webhook_delivery` |
| Skills | `find_skill` |

## Doc graph search runs locally

Graph search over your docs (outline, fuzzy headings, full-text, link references, resolve links) is **not** a hosted MCP tool. It runs on the agent's machine via the [`docs-claude-plugins`](https://github.com/Docsbook-io/docs-claude-plugins) package — install once with `/plugin install docs-sync@docs-claude-plugins` and the bundled `markdown-lsp` MCP server exposes the LSP-style `doc_*` tools to Claude Code. See [Source of Truth](./source-of-truth.md) for the tool list and rationale.

## Plan gating

Each tool declares a minimum plan. The server returns a structured error when a tool is called below the required tier.

| Plan | Available tool groups |
|---|---|
| Free | Workspace, branding, UI, navigation, analytics (24h), `find_skill` |
| PRO | + AI settings, SEO, domain, languages, chat hooks, translations, deeper analytics |
| PRO+ | + page journeys, top visitors + visitor activity drill-down, `query_events` |

## Learn more

The full product page lives at [docsbook.io/mcp](https://docsbook.io/mcp), with an interactive install selector for Claude Code, Cursor, Codex, Windsurf, Cline, Gemini CLI, GitHub Copilot, and ChatGPT.

## Related

- [Chat Hooks](./chat-hooks.md) — Configure pre/post-LLM hooks via MCP.
- [Docs Skills](./skills.md) — Discover SKILL.md files through `find_skill`.
- [Webhooks](../webhooks.md) — Register event handlers from MCP.
