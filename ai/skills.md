---
title: "Docs Skills — AI Agent Skills for Documentation"
description: "An open catalog of 52 SKILL.md files that extend Claude, Cursor, Copilot, and Codex with Docsbook-aware capabilities for analysis, creation, and publishing. Understand the Skill vs Subagent architecture for autonomous doc automation."
---

# Docs Skills

`docs-skills` is an open catalog of SKILL.md files for AI agents. Each skill teaches an agent how to perform a focused documentation task — auditing SEO, generating new pages from a website, publishing to a workspace, or watching for stale content.

The catalog lives at [github.com/Docsbook-io/docs-skills](https://github.com/Docsbook-io/docs-skills).

### What is a Skill?

A **Skill** is a reusable workflow — a set of Guardrails, Steps, and Acceptance Criteria encoded in a SKILL.md file. Think of it as a QA Checklist: you apply it in any project, with any agent (Claude Code, Cursor, Copilot, Codex). It does not carry project-specific context.

A **Subagent** is an executor: it has a pinned model, specific tools, priorities, and an autonomous work plan. Subagents live in [docs-subagents](https://github.com/Docsbook-io/docs-subagents). They are built for a specific context and are not meant to be reused across projects.

**Rule of thumb:** "Would this workflow be useful in another project?" — yes → skill, no → subagent.

## Categories

52 skills are organized into 7 categories:

| Category | Count | Examples |
|---|---|---|
| analysis | 15 | `docs-analyze`, `docs-seo`, `docs-accessibility`, `docs-competitor-gap`, `docs-pricing-consistency` |
| creation | 13 | `docs-create`, `docs-ai-retrieval`, `docs-authoring-rules`, `docs-branding`, `docs-sales-conversion` |
| observability | 10 | `docs-gap-finder`, `docs-change-impact`, `docs-dead-end-hunter`, `docs-buying-blockers`, `docs-funnel-mapper` |
| automation | 7 | `docs-pr-check`, `docs-tune-ai-chat`, `docs-stale-watcher`, `docs-release-announce`, `docs-sync` |
| publishing | 3 | `docs-publish`, `docs-setup-workspace`, `docs-generate-agents-md` |
| planning | 2 | `docs-health-triage`, `docs-strategy-plan` |
| growth | 2 | `docs-rank-recovery`, `docs-audience-enricher` |

## Two consumption modes

### Local install

Copy SKILL.md files into your agent's local skill directory:

```bash
npx docs-skills install
```

The installer detects Claude Code, Cursor, and Cline layouts and writes to `.claude/skills/`, `.cursor/rules/`, or `AGENTS.md` as appropriate. Skills work offline once installed.

### Runtime discovery via MCP

If the agent is connected to the Docsbook MCP server, it can discover skills on demand:

```typescript
find_skill({ query: "audit my docs for SEO" })
```

The tool returns matching SKILL.md entries with a `raw_url` field. The agent fetches the file directly from GitHub and follows its instructions. No local install required.

## Skills vs Subagents

| | Skill | Subagent |
|---|---|---|
| Analogy | QA Checklist | Jira ticket |
| Contains | Workflow, Guardrails, Acceptance Criteria | Pinned model, tools, plan |
| Reusable | Yes — any project | No — specific context |
| Works in | Claude Code, Cursor, Copilot, Codex | Claude Code (agent system) |
| Install | `npx docs-skills install` | `npx docs-subagents install` |

## Catalog page

Browse the full catalog at [docsbook.io/skills](https://docsbook.io/skills), with install snippets and prompts for each skill.

## Pricing

The catalog and `find_skill` MCP tool are available on **all plans**, including Free. Individual skills may invoke MCP tools that require a paid plan.

## Related

- [MCP Server](./mcp.md) — How `find_skill` is exposed to agents.
- [llms.txt](./llms-txt.md) — The other discovery surface for AI clients.
- [docs-subagents](https://github.com/Docsbook-io/docs-subagents) — subagents for autonomous doc automation.
- [markdown-lsp](https://github.com/Docsbook-io/markdown-lsp) — open-source LSP parser for Markdown that powers local doc-graph search.
