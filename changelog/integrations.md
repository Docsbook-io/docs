---
title: "What changed in Docsbook Integrations, and in which release"
description: "Every release that touched Integrations: the apps, sources and delivery channels your project is wired to, the accounts behind each one, and the occasions a connector can wake your agent for."
---

# What changed in Docsbook Integrations, and in which release

Everything that shipped in **Integrations**. This is the Integrations slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG).

## NEW - 19.09.2026

### Changed

- **Every screen in the panel now carries a Visit Website button in its top-right corner**, opening your published documentation in a new tab. Checking what a reader actually sees after changing a setting stops being a retyped address, so nobody ships a change to a live site on the assumption that it looked right. `Integrations`
- **Connect MCP moved to that same corner, beside Visit Website, as an outline button.** It sat next to the section title, where it read as a label rather than something to press; the top-right corner is where the panel keeps the things you can do from the screen you are on. `Integrations`

## NEW - 18.09.2026

### Added

- **Integrations is now one grid of everything this project is wired to**, with a card per connector and a detail page behind it. It used to be three tabs — Connectors, MCP and Webhooks — each holding a different *kind* of the same thing, so "what is this project connected to?" was a question you had to ask three times and add up yourself; now it is one screen and one glance, and a connector that has stopped working sorts to the top of it. `Integrations`
- **Connect Google Calendar, GitHub, Slack, Google Workspace, Telegram, Notion, Linear, Jira, Intercom, Zendesk, GitLab, Sentry, Figma or HubSpot** — and search 2 500 more by name. Your documentation can be written from the places the work actually happens instead of from whatever somebody remembered to paste, so a release, a merged pull request or a repeated support question reaches the docs without anybody carrying it there. `Integrations`
- **More than one account per service.** Two GitHub organisations, three Slack workspaces and somebody's personal Drive can all feed one project, each renamed to something your team recognises, paused, reconnected or removed on its own — so nobody has to choose which half of the truth to connect. `Integrations`
- **Every connector's page says what the agent can DO with it and what changes on the other side.** Each tool is listed in plain words, anything that can post or write carries a `Writes` badge, and the MCP section says how the same calls reach an agent working in your editor rather than in the panel — so you can tell what you are granting before you grant it, instead of finding out from a changelog later. `Integrations`
- **Triggers: 29 occasions a connector can wake the agent for**, written for documentation rather than copied from a vendor's event list — code landing on a branch, a release published, a pull request merged, an API spec changed, a question nobody answered in Slack, a launch three days out on the calendar. Documentation stops depending on somebody remembering, and starts happening because something moved. `Integrations`
- **A trigger that cannot fire yet says so on its own card.** Eight deliver today (GitHub and connected sources); the rest are listed, unarmable, with the reason. An armed trigger that silently never fires is indistinguishable from a quiet week, so the ones that would be silent are never offered as though they worked. `Integrations`

### Changed

- **Sources moved into Integrations**, a card per kind — repositories, Mintlify, GitBook, Notion, Zendesk and the rest. They used to sit behind a settings tab, which is why almost nobody found them: what your docs may READ and what your project is CONNECTED TO are the same question, and it is now answered in one place. `Integrations`
- **Paste as many addresses at once as you like** when connecting a source, one per line, with a preview of where each one will be filed before you commit. A project's docs are written from its repository *and* its pricing page *and* its API reference, and connecting them one dialog at a time is how a source list ends up with a single row in it. `Integrations`
- **Yours and Discover** split the section in two: what you have wired up, and what you could. A connector that is broken stays under Yours rather than disappearing at the moment it needs attention. `Integrations`

## NEW - 27.07.2026

### Fixed

- The `MCP Server` card in the `Integrations` tab now renders with its plan badge and upgrade footer instead of a bare blurred panel. `Integrations`

## NEW - 14.07.2026

### Added

- `MCP Server` card in the `Integrations` tab — copy your workspace's MCP endpoint alongside the API key. `Integrations`

## NEW - 06.07.2026

### Added

- `Integrations` panel — view, copy, and reset your workspace's API key from the `/chat` avatar menu or admin profile menu. `Integrations`

## Related

- [Full Docsbook changelog](../CHANGELOG.md) — every release, across every section
- [Sources](../ai-chat/sources.md) — the addresses your agent is allowed to read
- [Changelogs by panel section](./README.md) — the same releases, cut by where they landed
- [Changelogs by outcome](./outcomes/README.md) — the same releases, cut by the number they move

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: add the entry to the general changelog with its component tag and rerun the script. -->
