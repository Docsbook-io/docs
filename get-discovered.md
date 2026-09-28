---
title: "Tell your docs agent what you want: connect via MCP"
description: "Connect Claude Code, Cursor, Codex, VS Code or ChatGPT to the Docsbook MCP server in one line, then ask in plain words to be found on Google and cited by AI."
---

# Tell your agent, get discovered

Connect the AI agent you already work in to the Docsbook MCP server, say what you want in one sentence, and the Docsbook agent does the job end to end — so search engines find your product and AI engines cite it.

## Connect in one line

Paste this into Claude Code, Cursor, Codex or ChatGPT, and your agent connects itself:

```text
Set up Docsbook for me. Fetch https://docsbook.io/get-started.md and follow it.
```

The playbook at `docsbook.io/get-started.md` connects the server, adds one line about `docsbook_agent` to your agent's memory file (`CLAUDE.md`, `AGENTS.md`, `GEMINI.md`) and takes one project live. To tell your agent which of several projects answers which question, see [Teach your agent where your knowledge lives](./guides/teach-your-agent.md). In the panel, the **MCP** button in the chat header has **Copy prompt** for this sentence, **Copy MCP URL**, and one-click **Install in Cursor**, **Install in VS Code** and **Install in Claude Code**.

To add the server by hand, use the one endpoint every client and every project shares, `https://docsbook.io/api/mcp/server`:

<!-- widget:code-group -->

#### Claude Code

```bash
claude mcp add --transport http docsbook https://docsbook.io/api/mcp/server
```

#### Cursor

In `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "docsbook": { "url": "https://docsbook.io/api/mcp/server" } } }
```

#### Codex

```bash
codex mcp add docsbook --url https://docsbook.io/api/mcp/server
```

#### VS Code

```bash
code --add-mcp '{"name":"docsbook","type":"http","url":"https://docsbook.io/api/mcp/server"}'
```

#### Windsurf

In `~/.codeium/windsurf/mcp_config.json`:

```json
{ "mcpServers": { "docsbook": { "serverUrl": "https://docsbook.io/api/mcp/server" } } }
```

#### Gemini CLI

```bash
gemini mcp add --transport http docsbook https://docsbook.io/api/mcp/server
```

<!-- /widget -->

Chat apps take the endpoint as a connector instead:

- **Claude** (desktop app, claude.ai, and Claude Code inside them) — **Settings ▸ Connectors ▸ Add custom connector**, then paste the endpoint
- **ChatGPT** (paid plans) — **Settings ▸ Connectors ▸ Advanced ▸ Developer mode ▸ Create**, then paste the endpoint

<!-- widget:callout type=warning -->

On the Claude desktop app and on claude.ai, `claude mcp add` writes a config file those surfaces never read: the command succeeds and nothing connects. Add Docsbook as a connector there instead.

<!-- /widget -->

Your client then opens the Docsbook consent screen in the browser (in Claude Code, run `/mcp` and pick `docsbook`). Sign in, keep **Allow editing documentation** ticked for read-write access or untick it for read-only, and press **Authorize**. There's no API key to copy: the client registers itself over OAuth with PKCE.

## What to say

Say the goal and the evidence for it, not the steps, in any language. Requests like these start a job:

<!-- widget:cards cols=2 icons=inline -->

- [Be found on Google](./seo/README.md) — "Find what keeps our docs out of Google results and fix what you can." {search}
- [Be cited by AI engines](./geo/README.md) — "Check whether AI answers name us for our main questions, and fix what makes them cite someone else." {sparkles}
- [Answer your readers](./ai-chat/README.md) — "Write the pages for the questions the chat couldn't answer this week." {message-circle}
- [Keep docs true to code](./agent/README.md) — "Compare the docs with the repo and fix every page the code outgrew." {git-branch}
- [Open a new market](./site/translations.md) — "Translate the docs into Spanish and German and keep them in step." {languages}

<!-- /widget -->

The panel is the other place to say it: the chat button at the bottom right of the panel hands the same kind of job to the same agent.

## What happens after you ask?

`docsbook_agent` answers at once with a `task_id` and then works for minutes. Your agent keeps track of the job with five more tools:

| Tool | What it gives you |
|---|---|
| `docsbook_agent_activity` | Every action as it happens: pages read, pages written, sites fetched |
| `docsbook_agent_status` | The state and, once done, what it changed and what that should move; `needs_owner` means it's waiting on you |
| `docsbook_agent_reply` | Your answer, a correction or a question, while the job is open |
| `docsbook_agent_stop` | Ends the job and revokes its credential; committed work stays |
| `docsbook_agent_tasks` | Every job on your account, newest first |

Each page change is a git commit delivered as a pull request — merged at once or left for you, per **Settings ▸ General ▸ When a change goes live** ([reviewing changes](./agent/review.md)). Every run appears in **Activity ▸ Agent runs** with its full trace, and a question the agent can't settle alone lands in **Inbox**.

A run is billed to your balance: $0.10 per run plus twice what its model tokens cost, capped at $50 per run ([pricing](./pricing/plans.md)).

## What else can your connection do?

Your connection lists 55 tools. The agent is the main one, and the rest act on your projects directly:

| Group | Tools |
|---|---|
| **Orientation** | `get_info`, `list_workspaces`, `get_workspace`, `create_workspace` |
| **The agent** | `docsbook_agent` and the five tools above |
| **Read your docs** | `search_project_docs`, `read_project_doc`, `get_project_doc_outline`, `search_docs`, `ask_project_docs` |
| **Sources** | `list_sources`, `read_source`, `connect_source`, `configure_source`, `grant_repo_access` |
| **Write pages** | `write_docs`, `set_doc_status`, `list_content_widgets` |
| **Settings** | `update_branding`, `update_navigation`, `update_domain`, `update_site_address`, `update_languages`, the chat prompt and hooks, translations |
| **Goals** | `create_goal`, `list_goals`, `create_funnel`, `mark_path_as_funnel_step` |
| **Docsbook's own manual** | `search_docsbook_docs`, `read_docsbook_doc`, `list_docsbook_docs` |

Another 33 tools stay out of the list — webhook alerts, the agent's [memory folder](./brain/memory.md), hand-over links and `update_access`. `find_tool` finds one by what you want to do, and `call_tool` runs it. Every tool is in the [MCP tools reference](./mcp-tools/README.md), and every one of them, listed or not, is also a plain HTTPS endpoint in the [API reference](./rest-api/README.md).

## Is it safe to connect?

The connection acts as you, and the agent it starts works inside a fence:

- **No key to paste** — the client registers itself and you approve it in the browser, so there's no API key to copy into a config file
- **Read-only when you want it** — untick **Allow editing documentation** and the token can search and read, while every write is refused
- **The agent stays inside its job** — a run works only on the projects its task names; it can't create projects, list your other ones, change who can see a site, grant repository access or start another agent, and a write never approves a page

## FAQ

<!-- widget:accordion -->

### Which AI clients can connect?

Any MCP client that speaks streamable HTTP: Claude Code, Cursor, Codex, VS Code with Copilot, Windsurf, Gemini CLI, Cline, ChatGPT and Claude connectors.

### Do I need a separate URL for each project?

No. One endpoint serves every project on your account; name the project in your request — `owner/repo`, the site name, its URL or domain — or pass `workspace_id`.

### What does a connection cost?

Discovery calls such as `get_info`, `find_tool` and `list_workspaces` are free. Other tool calls are billed per call from your balance at twice what serving them costs — a few cents per thousand for most — and agent runs as above; see [pricing](./pricing/plans.md).

### Can my readers' agents connect too?

Yes, to a different server: every published site has its own read-only [MCP server for your readers](./brain/mcp-server.md).

<!-- /widget -->

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [Find wins fast](./find-wins-fast.md) — How the agents pick the change that moves a number {target}
- [How the agent works](./agent/README.md) — What it reads, writes and measures on its own {bot}
- [Triggers](./agent/triggers.md) — Let the agent start work without being asked {zap}
- [MCP tools reference](./mcp-tools/README.md) — Every tool your connection can call {terminal}

<!-- /widget -->
