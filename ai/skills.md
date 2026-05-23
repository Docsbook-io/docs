---
title: "Docs Skills — AI Agent Skills for Documentation"
description: "An open catalog of 25 SKILL.md files that extend Claude, Cursor, and Cline with Docsbook-aware capabilities for analysis, creation, and publishing."
---

# Docs Skills

`docs-skills` is an open catalog of SKILL.md files for AI agents. Each skill teaches an agent how to perform a focused documentation task — auditing SEO, generating new pages from a website, publishing to a workspace, or watching for stale content.

The catalog lives at [github.com/Docsbook-io/docs-skills](https://github.com/Docsbook-io/docs-skills).

## Categories

25 skills are organized into 5 categories:

| Category | Count | Examples |
|---|---|---|
| analysis | 11 | `docs-analyze`, `docs-seo`, `docs-accessibility`, `docs-i18n`, `docs-style-tone` |
| creation | 4 | `docs-create`, `docs-create-interactive`, `docs-detect-source`, `docs-from-site` |
| publishing | 3 | `docs-publish`, `docs-setup-workspace`, `docs-generate-agents-md` |
| automation | 6 | `docs-pr-check`, `docs-tune-ai-chat`, `docs-stale-watcher`, `docs-release-announce` |
| observability | 1 | `docs-gap-finder` |

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

## Catalog page

Browse and filter the full catalog at [docsbook.io/skills](https://docsbook.io/skills). Each skill has a detail page with installation snippets and the rendered SKILL.md body.

## Pricing

The catalog and `find_skill` MCP tool are available on **all plans**, including Free. Individual skills may invoke MCP tools that require a paid plan.

## Related

- [MCP Server](./mcp.md) — How `find_skill` is exposed to agents.
- [llms.txt](./llms-txt.md) — The other discovery surface for AI clients.
