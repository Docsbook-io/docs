---
title: "Docs Skills — AI Agent Skills for Documentation"
description: "An open catalog of four SKILL.md files that extend Claude, Cursor, Copilot, and Codex with Docsbook-aware capabilities for analysing, creating, managing and automating documentation. Install them locally, discover them at runtime through MCP, or have Docsbook run one for you."
---

# Docs Skills

`docs-skills` is an open catalog of SKILL.md files for AI agents. Each skill teaches an agent how to do one of the four jobs documentation work comes in: find what is wrong with docs that exist, create docs that do not, decide what a page should say and what the site around it should do, or make any of that keep happening on its own.

The catalog lives at [github.com/Docsbook-io/docs-skills](https://github.com/Docsbook-io/docs-skills).

### What is a Skill?

A **Skill** is a reusable workflow — a set of Guardrails, Steps, and Acceptance Criteria encoded in a SKILL.md file. Think of it as a QA Checklist: you apply it in any project, with any agent (Claude Code, Cursor, Copilot, Codex). It does not carry project-specific context.

A **Subagent** is an executor: it has a pinned model, specific tools, priorities, and an autonomous work plan. Subagents live in [docs-subagents](https://github.com/Docsbook-io/docs-subagents). They are built for a specific context and are not meant to be reused across projects.

**Rule of thumb:** "Would this workflow be useful in another project?" — yes → skill, no → subagent.

## The four skills

Documentation work is four jobs, and every request lands in one of them. The catalog is four orchestrator skills, one per job, and they hand off to each other rather than overlapping: `docs-analyze` finds a gap and hands it to `docs-create`; `docs-create` writes to `docs-manage`'s rules; `docs-manage` executes what `docs-analyze` diagnosed; `docs-automate` makes any of it recur.

| Skill | Category | The question it answers |
|---|---|---|
| `docs-analyze` | analysis | Something is wrong. Find it from real numbers, say what it costs in plain language, and fix it — including the gap no number shows: the audiences and use cases the docs never address. |
| `docs-create` | creation | The docs do not exist yet. Make them — from a site, a repo, another platform, or an idea. |
| `docs-manage` | management | What should this page say, and what should the site around it do? |
| `docs-automate` | automation | Make it keep happening without anyone remembering. |

All four are available on every plan, including Free.

## Three consumption modes

### Local install

Copy SKILL.md files into your agent's local skill directory:

```bash
npx skills add Docsbook-io/docs-skills --skill '*'          # the whole catalog
npx skills add Docsbook-io/docs-skills --skill docs-analyze  # one skill
```

The installer detects Claude Code, Cursor, and Cline layouts and writes to `.claude/skills/`, `.cursor/rules/`, or `AGENTS.md` as appropriate. Add `-a claude-code -a cursor` to target specific agents. Skills work offline once installed.

### Runtime discovery via MCP

If the agent is connected to the Docsbook MCP server, it can discover skills on demand:

```typescript
find_skill({ query: "audit my docs for SEO" })
```

The tool returns matching SKILL.md entries with a `raw_url` field. The agent fetches the file directly from GitHub and follows its instructions. No local install required.

### Have Docsbook run it for you

The two modes above both end with *your* agent executing the skill, which needs it to be connected here, to have picked a workspace, and to be willing to spend twenty tool calls. On PRO and above there is a third mode: ask Docsbook to run the skill instead.

```typescript
run_docs_analyze({ request: "why is our quickstart getting impressions but no clicks?" })
// → { run_id: "run_…", state: "queued" }

get_agent_run({ run_id: "run_…" })
// → state, live progress, and once it finishes the report and what changed
```

One tool per skill — `run_docs_analyze`, `run_docs_create`, `run_docs_manage`, `run_docs_automate` — each running against your workspace with the full administrative toolset the skill was written for. The job takes minutes, so the call returns a run identifier rather than a result; read it with `get_agent_run`. `run_docs_analyze` changes nothing and works with a read-only token; the other three commit pages or settings and need a read-write one. See [MCP Server](./mcp.md#handing-over-the-whole-job).

## Skills vs Subagents

| | Skill | Subagent |
|---|---|---|
| Analogy | QA Checklist | Jira ticket |
| Contains | Workflow, Guardrails, Acceptance Criteria | Pinned model, tools, plan |
| Reusable | Yes — any project | No — specific context |
| Works in | Claude Code, Cursor, Copilot, Codex | Claude Code (agent system) |
| Install | `npx skills add Docsbook-io/docs-skills --skill '*'` | `npx docs-subagents install` |

## Catalog page

Browse the full catalog at [docsbook.io/skills](https://docsbook.io/skills), with install snippets and prompts for each skill.

## Pricing

The catalog and the `find_skill` MCP tool are available on **all plans**, including Free — installing a skill locally and running it with your own agent costs nothing here. Individual skills may invoke MCP tools that require a paid plan. Having Docsbook run a skill for you (`run_docs_*`) is a **PRO** capability, because the work runs on our machines and our AI budget.

## Related

- [MCP Server](./mcp.md) — How `find_skill` is exposed to agents, and how `run_docs_*` runs a skill for you.
- [llms.txt](./llms-txt.md) — The other discovery surface for AI clients.
- [docs-subagents](https://github.com/Docsbook-io/docs-subagents) — subagents for autonomous doc automation.
- [markdown-lsp](https://github.com/Docsbook-io/markdown-lsp) — open-source LSP parser for Markdown that powers local doc-graph search.
