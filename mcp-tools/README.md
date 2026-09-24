---
title: "MCP Tools"
description: "Every tool your own agent can call once it is connected to Docsbook over MCP — from Claude Code, Cursor, Codex, VS Code or any other MCP client."
---

# MCP Tools

Every tool your own agent can call once it is connected to Docsbook over MCP — from Claude Code, Cursor, Codex, VS Code or any other MCP client.

## Connect

```bash
claude mcp add --transport http docsbook https://docsbook.io/api/mcp/server
```

Your client opens a browser once, you sign in (OAuth 2.0 with PKCE), and it keeps the token. Setup for other clients and what to say first: [Tell your agent, get discovered](../get-discovered.md).

## What is on this list

Every tool below appears in your client's tool list:

- **The agent** — `docsbook_agent` takes a goal in plain words and does the whole job; `docsbook_agent_status`, `docsbook_agent_activity`, `docsbook_agent_tasks`, `docsbook_agent_reply` and `docsbook_agent_stop` watch and steer it.
- **Projects** — `get_info`, `list_workspaces`, `get_workspace`, `create_workspace`.
- **Your pages** — search, read and write them, their sources, widgets and status.
- **Your site** — branding, navigation, domain, languages, translations and the AI chat.
- **Goals** — the conversions and funnels your analytics count.
- **Docsbook's own manual** — `search_docsbook_docs`, `read_docsbook_doc`, `list_docsbook_docs`.

## More tools through `call_tool`

Webhook alerts (`register_webhook_*`), the agent's [memory folder](../brain/memory.md) (`*_context`), claim links that hand a project to its owner, and site access are callable but kept off the list so it stays short. Ask `find_tool` for one by describing it, then run it with `call_tool`.

## What the Docsbook agent adds

`docsbook_agent` works with a larger toolbox of its own — over 170 tools, including search results, keyword demand, community threads, competitor docs, reader analytics and the [expertise audit](../agent/expertise.md). You reach all of it by giving it a goal: see [AI agent writes and updates your docs](../agent/README.md).

## Cost and access

Each call has a flat price, shown on its page and charged to your balance — discovery calls such as `get_info` and `find_tool` are free. See [pricing](../plans-and-pricing.md).

The pill beside a tool in the sidebar says whether it only **reads** a project or can **change** it.

Endpoint: `https://docsbook.io/api/mcp/server`

<!-- widget:cards plain cols=2 arrow=hover -->

- [Settings](./settings/README.md) — Change one thing about the site to a value the user stated.
- [Content](./content/README.md) — Read and write the documentation itself.
- [Orientation](./orientation/README.md) — Find out what this server is, which project the user means, and — on an owner's token — what else this…
- [Goals](./goals/README.md) — Declare what a reader was supposed to do, and count who did.
- [Create](./create/README.md) — Bring a documentation site into existence.
- [Agent](./agent/README.md) — The Docsbook agent — one worker you delegate to, and the whole of "manage the documentation" on a customer's…
- [Product Help](./product-help/README.md) — The craft corpus — `docsbook_assistant` — how the work is done well, from Docsbook's published pages, with…

<!-- /widget -->
