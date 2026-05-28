# Skills catalog — reference

`docs-skills` is an open catalog of [SKILL.md](https://github.com/Docsbook-io/docs-skills) files for AI agents, extending the Docsbook MCP. This is **part of Docsbook as a product**, not a separate project: the catalog, the marketing page `/skills`, the MCP tool `find_skill`, and the Docsbook MCP server itself evolve as a single unit.

> **Full catalog reference:** [raw.githubusercontent.com/Docsbook-io/docs-skills/main/README.md](https://raw.githubusercontent.com/Docsbook-io/docs-skills/refs/heads/main/README.md) — description of all skills, frontmatter schema, CLI, consumption modes. This is the canonical source; when developing any features related to skills, start here.

27 skills in 6 categories: `analysis`, `creation`, `automation`, `observability`, `publishing`, `planning`.

## Skill vs Subagent Architecture

Skills и субагенты — разные уровни экосистемы:

| Артефакт | Аналогия | Содержит | Пакет |
|---|---|---|---|
| Skill (SKILL.md) | QA Checklist — регламент | Workflow, Guardrails, MCP Tools, Acceptance Criteria | [docs-skills](https://github.com/Docsbook-io/docs-skills) |
| Subagent (.md) | Jira тикет — исполнитель | Pinned модель, инструменты, приоритеты, план, коллаборация | [docs-subagents](https://github.com/Docsbook-io/docs-subagents) |
| Plugin | Сборка | Subagents + MCP + hook, одна команда | [docs-claude-plugins](https://github.com/Docsbook-io/docs-claude-plugins) |

Правило: "Пригодится ли этот текст в другом проекте?" → да = skill, нет = subagent.

## Discovery surfaces

| Surface | URL / API | Source |
|---|---|---|
| Marketing catalog | `docsbook.io/skills` (SSG, 1h ISR) | `raw.githubusercontent.com/Docsbook-io/docs-skills/main/index.json` |
| Detail page | `docsbook.io/skills/[name]` (SSG) | `raw_url` of each SKILL.md, rendered via the main markdown pipeline |
| MCP tool | `find_skill(query, filters)` | same `index.json`, Redis 5 min + etag |
| llms.txt | Link in `docsbook.io/llms.txt` | — |

## Two consumption modes for users

1. **Local install** — `npx docs-skills install` copies SKILL.md into `.claude/skills/` / `.cursor/rules/` / `AGENTS.md`. Works offline.
2. **Runtime discovery** — the agent is already connected to Docsbook MCP → calls `find_skill("audit my docs")` → reads the SKILL.md via `raw_url`. No local installation required.

## Skill categories

- **analysis** (11): `docs-accessibility`, `docs-analyze`, `docs-audience`, `docs-content-types` …
- **automation** (7): `docs-enable-translation`, `docs-pr-check`, `docs-release-announce`, `docs-stale-watcher`, `docs-sync` …
- **creation** (4): `docs-create`, `docs-create-interactive`, `docs-detect-source`, `docs-from-site`
- **publishing** (3): `docs-generate-agents-md`, `docs-publish`, `docs-setup-workspace`
- **observability** (1): `docs-gap-finder`
- **planning** (1): `docs-strategy-plan`

## Implementation files

- `src/lib/skills-index.ts` — loading `index.json` for marketing pages (ISR 1h)
- `src/lib/skills/find.ts` — `find_skill` MCP tool (Redis 300s + etag revalidation, keyword match with weights name×3 / description×2 / keywords×2)
- `src/app/skills/page.tsx` — catalog with filters (category / plan / keyword search)
- `src/app/skills/[name]/page.tsx` — detail page with SKILL.md, install + MCP snippets
- `src/proxy.ts` — `skills` is reserved as a subdomain, `/skills/*` is excluded from user-rewrite
