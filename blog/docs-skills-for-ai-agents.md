---
title: "docs-skills: Modular Capabilities for AI Agents on Your Docs"
description: "What docs-skills are, why Claude Code and Cursor use them, and how the open-source catalog lets agents understand any documentation site. The new layer between MCP and your content."
---

# docs-skills: Modular Capabilities for AI Agents

In 2026, AI agents do not just read documentation — they take actions on it. They publish a docs site, fix broken links, generate `llms.txt`, write missing pages, audit accessibility. The way they know how to do these actions is through "skills" — packaged, discoverable, declarative capability descriptions.

This post explains what skills are, why Docsbook ships an open-source catalog of 25 of them, and how this fits between MCP and your content.

## TL;DR

- A "skill" is a `SKILL.md` file with frontmatter that describes a capability — what it does, when to trigger it, what tools it needs
- AI agents (Claude Code, Cursor) read skills and execute them autonomously
- [docs-skills](https://github.com/Docsbook-io/docs-skills) is an open-source catalog of 25 skills for documentation
- Docsbook MCP exposes `find_skill` so agents discover skills by query at runtime
- You can install skills locally (`npx docs-skills install`) or use them through MCP

## What a skill looks like

A minimal `SKILL.md`:

```markdown
---
name: docs-pr-check
description: Validate documentation changes in a pull request — check for broken links, missing frontmatter, accessibility issues, and SEO regressions. Use when reviewing docs PRs.
category: automation
requires_plan: free
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

The frontmatter is the contract. The body is the prompt.

## Why this matters for documentation

Three problems skills solve:

### 1. Discoverability of capabilities

Without skills, an AI agent reading your docs MCP has to guess what to do. With skills, the agent calls `find_skill("audit my docs")` and gets a SKILL.md with exact instructions.

### 2. Modular reuse

A skill written for one project works on any project. The `docs-pr-check` skill applies to any docs repo. The `docs-tune-ai-chat` skill applies to any Docsbook workspace.

### 3. Composition

Skills can chain. The `docs-analyze` skill orchestrates 10 sub-skills (`docs-seo`, `docs-accessibility`, `docs-i18n`, etc.) into a single audit run. This composition is declarative in the SKILL.md.

## The docs-skills catalog

[docs-skills](https://github.com/Docsbook-io/docs-skills) is an open-source catalog of 25 skills across five categories:

| Category | Skills |
|---|---|
| **analysis** (11) | docs-analyze, docs-seo, docs-accessibility, docs-i18n, docs-style-tone, docs-structure-templates, docs-content-types, docs-audience, docs-navigation-linking, docs-media, docs-maintenance |
| **creation** (4) | docs-create, docs-create-interactive, docs-detect-source, docs-from-site |
| **publishing** (3) | docs-publish, docs-setup-workspace, docs-generate-agents-md |
| **automation** (6) | docs-enable-translation, docs-pr-check, docs-tune-ai-chat, docs-stale-watcher, docs-release-announce, docs-translate-webhook |
| **observability** (1) | docs-gap-finder |

Each skill is a standalone `SKILL.md` in the GitHub repo. Some chain to others.

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

## Related reading

- [MCP server for documentation](./mcp-server-for-documentation.md) — the layer below skills
- [How to get docs cited by ChatGPT](./how-to-get-docs-cited-by-chatgpt.md)
- [llms.txt: the complete guide](./llms-txt-guide.md)
- [AI documentation platforms compared (2026)](./ai-docs-platform-comparison.md)

---

Docsbook ships docs-skills support — `find_skill` MCP tool plus local install. [Connect from Claude Code →](https://docsbook.io/mcp)
