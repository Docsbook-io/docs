---
title: "Your product's second brain: docs, sources and memory"
description: "One brain of your product: your pages, the code and sites they describe, what the agent learned and your skills. You, your agent, readers and agents can ask it."
---

# Your product's second brain

Docsbook keeps everything it knows about your product in one place — your pages, the code and sites behind them, what its agent has learned — and lets you, your agent, your readers and their AI agents ask it.

The brain has four parts:

- **Your pages** — searchable by meaning and by exact words, and drawn as a map on **Analytics ▸ Graph**.
- **[Sources](./sources.md)** — the repositories, websites, specs and files your docs describe.
- **[Memory](./memory.md)** — one folder per organization of what the agent has learned about your product.
- **[Skills](./skills.md)** — your house instructions for how the agent works, and where.

## What's on from day one

These work on a new project with nothing to set up:

- **Search by exact words** over every page, kept in step with your docs.
- **Your site's own repository** as a source, plus the **Product website** you set in **Settings ▸ General**.
- **The agent's folder**, which fills as the agent works and is counted on **Overview ▸ Docsbook agent**.
- **A public [MCP server](./mcp-server.md)** that your readers' AI agents can query without an account.

<!-- widget:callout type=info -->

**Search by meaning is one switch.** Turn on **Enable semantic search** on the **Semantic Search** card in **Settings ▸ Agent** — it is part of [Pro](../plans-and-pricing.md), and on a trial it unlocks once a card is on file. Until then, every search answers by exact words.

<!-- /widget -->

## What the agent does on its own

The agent keeps the brain current, checks your pages against the code, adds what it learns on every run, and answers from it.

<!-- widget:cards cols=2 -->

- Keeps the index in step — No rebuild button: with search by meaning on, the index follows your docs by itself. {refresh-cw}

  - **Watches:** every page Docsbook publishes, and your GitHub branch for commits pushed outside Docsbook.
  - **Changes:** re-embeds only the sections that changed, and redraws the map.
  - **Shows:** **Last updated** on the **Semantic Search** card, and a `content.indexed` event listing the pages added, modified and removed.

- [Catches pages the code outgrew](./sources.md) — It reads your connected sources instead of trusting old pages. {git-compare}

  - **Watches:** your docs finishing a re-index, and — once a day — your MCP server, OpenAPI spec or SDK.
  - **Changes:** fixes what the source plainly contradicts and proposes the rest.
  - **Shows:** which claims were wrong and for how long, reported in your **Inbox**.

- [Writes down what it learns](./memory.md) — What one run works out, the next run starts from. {brain}

  - **Watches:** every run lists the folder first, and checks before it stops that it filed what it learned.
  - **Changes:** records facts, your decisions, open questions and claims under test — each claim with a date to re-check.
  - **Shows:** entries per folder on **Overview ▸ Docsbook agent**, and how many are due a second look.

- [Answers from it](./mcp-server.md) — Every door reaches the same brain. {messages-square}

  - **Watches:** a question from you, a reader, a reader's agent or your backend.
  - **Changes:** searches by meaning first, then reads the matching pages before it answers.
  - **Shows:** one row per run or chat turn on **Activity ▸ Agent runs**, marked with the door it came through.

<!-- /widget -->

The ready-made cards behind the second loop, from [Triggers](../agent/triggers.md):

- **Find pages the code outgrew** — wakes when your docs changed and finished re-indexing, so it needs search by meaning on.
- **MCP sync**, **OpenAPI sync**, **SDK sync** — daily, each against one machine-readable surface.
- **Find pages that contradict** — weekly, for two pages telling a reader two different things.

The rules behind all four loops sit on the **Freshness** axis of the **Trust & evidence** family in the [expertise catalog](../agent/expertise.md): a page that was true is not a page that is true.

## Who can ask it?

The same brain answers through six doors:

| Who | Where | How |
|---|---|---|
| You | The admin chat in the panel | Ask in your own words; it searches pages, sources and the folder |
| You, from your editor | Claude Code, Cursor or Codex, over [your MCP connection](../get-discovered.md) | `ask_project_docs` for a cited answer, `search_project_docs` for pages by meaning |
| The Docsbook agent | Every run and every trigger | Reads the folder, the sources and the pages before it writes |
| Your readers | The [AI chat](../ai-chat/README.md) on your site (Pro) | Answers from your published pages |
| Your readers' agents | The [public MCP server](./mcp-server.md) | `search_<slug>_docs` and `read_<slug>_doc`, no account needed |
| Your backend | `POST /api/v1/chat` with your API key (Pro) | Returns `answer` and the `refs` it drew on — see the [chat API](../ai-chat/api.md) |

## How fresh is the brain?

A page Docsbook publishes reaches the index within minutes. A push made straight to GitHub is noticed at the next five-minute branch check when search by meaning is on, and within the hour when it is off.

| Search | What keeps it current | Plan |
|---|---|---|
| By exact words | Every page Docsbook publishes; an hourly pass catches pushes made on GitHub | Every plan |
| By meaning | Every page Docsbook publishes, your branch checked for new commits every five minutes, and an hourly pass as a safety net | Pro, with **Semantic Search** on |

Only the sections that changed are re-embedded. That cost comes from the project's AI balance — or your own AI key — and shows next to **Last updated**; indexing stops when the balance runs out rather than running into overage.

## See it working

- **Overview ▸ Docsbook agent** — how many entries the agent filed in each folder, when it last learned something, and what is due a second look.
- **Analytics ▸ Graph** — the map of pages, headings and links; the **Search by meaning…** box lights the sections that answer a question.
- **Settings ▸ Agent** — the **Semantic Search** card, with **Last updated** and what the last run cost.
- **Integrations** — each source's addresses, marked "read by the agent" or "not read yet".
- **Activity ▸ Agent runs** — every run and chat turn, filtered by door.

## Tell your agent

Say it in your own words:

```text
Remember: we never call it a dashboard, it's the console.
Connect github.com/acme/api as a source — it's the API our reference pages describe.
Which pages say something our code no longer does? Fix what's plainly wrong.
What do you know about our pricing, and where did you learn it?
```

Send it in the admin chat, or from Claude Code, Cursor or Codex through [your MCP connection](../get-discovered.md).

## FAQ

**Can readers see my sources or the agent's memory?** No. The AI chat and the public MCP server answer from your published pages; sources and the folder stay on your side, and only a [skill](./skills.md) you place on a public door reaches readers.

**Does the brain read a private repository?** Yes, once the Docsbook GitHub App is installed on it — **Contents: read** is enough. See [Sources](./sources.md).

**What happens to the brain when I hand a project over?** The project's own memory entries and audit verdicts move to the new owner; skills and your organization-wide entries stay with you. See [Memory](./memory.md).

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [Connect a source](./sources.md) — Point the agent at the code and sites your docs describe {plug}
- [Teach it a skill](./skills.md) — Write down how your team wants the work done {sparkles}
- [Open it to readers' agents](./mcp-server.md) — Your docs as an MCP server anyone can connect {server}
- [See what it remembers](./memory.md) — The folder the agent reads before every run {brain}

<!-- /widget -->
