---
title: "docs-skills: modular capabilities for AI agents on docs"
description: "What docs-skills are, what the open-source catalog contains, and how the layer sits between an MCP server and the documentation an agent acts on."
---

# docs-skills: modular capabilities for AI agents on docs

In 2026, AI agents do not just read documentation — they take actions on it. They publish a docs site, fix broken links, generate `llms.txt`, write missing pages, audit accessibility. The way they know how to do these actions is through "skills" — packaged, discoverable, declarative capability descriptions.

This post explains what skills are, what Docsbook's open-source catalog contains today, and how the layer fits between MCP and your content.

## TL;DR

- A "skill" is a `SKILL.md` file with frontmatter that describes a capability — what it does, when to trigger it, what tools it needs
- AI agents (Claude Code, Cursor) read skills and execute them autonomously
- [docs-skills](https://github.com/Docsbook-io/docs-skills) is an open-source catalog of four documentation skills
- Docsbook MCP exposes `find_skill` so agents discover skills by query at runtime
- You can install skills locally (`npx docs-skills install`) or use them through MCP

## What a skill looks like

A minimal `SKILL.md`:

```markdown
---
name: docs-pr-check
description: Validate documentation changes in a pull request — check for broken links, missing frontmatter, accessibility issues, and SEO regressions. Use when reviewing docs PRs.
category: automation
mode: agent
keywords: [pull request, broken links, frontmatter, review]
requires_docsbook_mcp: true
version: 1
---

# docs-pr-check

When the user opens a docs PR, run this skill to validate the change.

Steps:

1. Run `doc_search_unresolved` to find broken links in changed files
2. Verify YAML frontmatter on every new or modified `.md` file
3. Check that internal links resolve
4. Suggest improvements

Tools used: `doc_search_unresolved`, `doc_outline`, `doc_resolve_link` (Docsbook MCP)
```

The skill above is an illustration of the format, not an entry in the catalog — the four real skills are listed further down. The frontmatter fields are the ones the schema actually defines: `name`, `description`, `category`, `mode`, `keywords`, `requires_docsbook_mcp` and `version`.

The frontmatter is the contract. The body is the prompt.

## Why this matters for documentation

Three problems skills solve:

### 1. Discoverability of capabilities

Without skills, an AI agent reading your docs MCP has to guess what to do. With skills, the agent calls `find_skill("audit my docs")` and gets a SKILL.md with exact instructions.

### 2. Modular reuse

A skill written for one project works on any project. `docs-manage` is the rulebook for writing a page and running the site it lives on, and it applies to any documentation repository, on Docsbook or not.

### 3. Composition

Skills compose rather than multiply. Each one carries a `references/` directory of focused documents that it loads only when the task needs them — `docs-manage` alone holds separate references for retrieval, conversion and writing rules. The agent reads the skill, then reads the one reference that matters, instead of loading a catalogue.

## The docs-skills catalog

### What is in the docs-skills catalog?

[docs-skills](https://github.com/Docsbook-io/docs-skills) is an open-source catalog of **four** skills, each covering one job an agent does with documentation. It was previously a long list of narrow skills; it was consolidated because an agent choosing between fifty near-synonymous descriptions picks badly, and four jobs are distinguishable.

| Skill | The job it does |
|---|---|
| `docs-create` | Create documentation that did not exist — from a product website, a code repository, another docs platform you are migrating off, or nothing but a product name |
| `docs-analyze` | Find what is wrong with documentation that already exists and fix it, starting from search positions, AI-answer signals, reader behaviour and funnels |
| `docs-manage` | The rulebook for writing a page and for running the site it lives on — page type, structure, style, audience, retrieval, conversion |
| `docs-automate` | Set up the things that should keep happening without anyone remembering — drift guards, translation triggers, release announcements |

Each skill is a standalone `SKILL.md` in the GitHub repository, with a `references/` directory the agent reads on demand. The machine-readable index is `index.json` in the same repository; the counts above were read from it on 2026-09-03.

## Two ways to use skills

### Local install

```bash
npx docs-skills install
```

Copies the catalog to `.claude/skills/`, `.cursor/rules/`, or `AGENTS.md` (depending on detected tool). Works offline. Updates with `docs-skills update`.

This pattern: your tools' skills live in your repo, version-controlled.

### Runtime discovery via MCP

If you have Docsbook MCP connected, your agent calls:

```
find_skill({ query: "audit my docs for SEO and accessibility" })
```

It returns the top matching skills with `raw_url` for each `SKILL.md`. The agent fetches and follows the instructions.

This pattern: no local install, always the latest version, works across machines.

## How AI agents use skills in practice

Three real workflows we have seen:

### Workflow 1: PR review

A developer opens a PR that touches `docs/`. Their Claude Code (or Cursor) invokes `docs-pr-check`. The skill:

1. Lists changed `.md` files
2. Calls `doc_search_unresolved` on each
3. Checks frontmatter completeness
4. Reports findings as a PR comment

The developer sees the report before a human reviewer. Many docs issues never reach the team.

### Workflow 2: Stale content detection

Weekly cron in the user's setup invokes `docs-stale-watcher`. The skill:

1. Queries Docsbook analytics for pages with traffic but no edits in 90+ days
2. Cross-references with the doc graph
3. Lists candidates for refresh

The output is a backlog of pages to update — content gaps with revenue signal.

### Workflow 3: AI chat tuning

User says "my AI chat is hallucinating about feature X." Agent invokes `docs-tune-ai-chat`. The skill:

1. Calls `get_ai_questions` to see recent unanswered queries
2. Calls `get_negative_feedback` to see thumbs-down patterns
3. Identifies missing or weak content
4. Suggests a new page or system prompt change

This is the "agent improves agent" loop.

## Skills + MCP: the architecture

Skills tell the agent **what to do**. MCP tools tell the agent **how to do it**.

- A skill says "audit accessibility for every page"
- The skill body lists steps like "call `doc_list_pages`, then `doc_outline` on each"
- MCP exposes the actual tools the skill invokes

Neither is enough alone. Together they form a complete loop: discovery (find_skill) → instructions (SKILL.md) → execution (MCP tools).

## What this looks like for your own docs

If you ship a developer-facing product and you want AI agents to interact with your docs well, three steps:

1. **Publish on a platform with `llms.txt`** — Docsbook generates one automatically per workspace
2. **Expose an MCP server or rely on the platform's** — Docsbook MCP is included
3. **Install relevant docs-skills locally** — `npx docs-skills install`

After that, any agent (Claude Code, Cursor, ChatGPT with HTTP MCP) can autonomously work with your docs.

## Build your own skill

If you have a docs workflow that is not in the catalog, contribute one. The SKILL.md format is simple, the catalog is public, contributions ship in days.

A useful skill is:

- Specific (one job, done well)
- Composable (calls existing MCP tools)
- Triggered by a clear user intent
- Documented with examples

The repo has a `SKILL.md` template and a contribution guide.

Docsbook ships docs-skills support: the `find_skill` MCP tool for runtime discovery, and `npx docs-skills install` for a local copy. Publish a workspace and the MCP endpoint comes with it — the setup steps are at [docsbook.io/mcp](https://docsbook.io/mcp).

[Start free — no credit card](https://docsbook.io/start)

## Next steps

- [MCP server for documentation](./mcp-server-for-documentation.md) — the layer skills sit on top of
- [How to get your documentation cited by ChatGPT](./how-to-get-docs-cited-by-chatgpt.md) — what agents do with the docs they can read
- [llms.txt explained](./llms-txt-guide.md) — the companion file for agents that do not speak MCP
- [AI documentation platforms compared](./ai-docs-platform-comparison.md) — which platforms expose an MCP server at all
