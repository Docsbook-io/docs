---
title: "Docsbook documentation: publish, get found, get quoted, measure."
description: "Docsbook publishes the Markdown you already have to a site search engines index and AI assistants cite, then hands your agent a goal and reports the number it moved. Start here."
status: generated
version: "0.4"
---

<!-- widget:hero size=large -->

**Docsbook documentation**

# Documentation that gets your product found, quoted and measured

Publish the Markdown you already have to a site search engines index and AI assistants cite. Then hand your agent a goal and read, on a date, the number it moved.

[Start free](https://docsbook.io/?start=1) · [Connect your agent](./agent-ready/mcp.md)

> ![Claude](https://docsbook.io/agents/claude.svg) ![OpenAI](https://docsbook.io/agents/openai.svg) ![Cursor](https://docsbook.io/agents/cursor.svg) **Onboard your agent** — Set up Docsbook for me. Fetch https://docsbook.io/get-started.md and follow it.
>
> One prompt into Claude Code, Cursor or Codex: the agent connects the server, writes a Docsbook rule into its memory file and takes a first project live.

```bash
claude mcp add --transport http docsbook https://docsbook.io/api/mcp/server
```

Codex, Cursor, Windsurf, Cline and any other MCP client use the same endpoint.

<!-- /widget -->

<!-- widget:stats cols=4 -->

- **5 min** — from a repository to a public URL
- **169** — MCP tools your docs agent can use
- **15** — languages, each indexed on its own
- **$0** — for hosting, search, analytics and a custom domain

<!-- /widget -->

<!-- widget:logos -->

**Documentation running on Docsbook**

- [Cursor](https://docsbook-websites.docsbook.io/cursor)
- [ClickHouse](https://docsbook-websites.docsbook.io/clickhouse)
- [Discord Developers](https://docsbook-websites.docsbook.io/discord-developers/)

[See every site →](https://docsbook.io/showcase)

<!-- /widget -->

## Start here

Four doors. Each one is a page you can finish in one sitting.

<!-- widget:cards icons=inline cols=4 arrow=hover -->

- [Publish a site](./quick-start.md) — From a repository, a website scan or one sentence about your product, to a public URL. {rocket}
- [Connect your agent](./agent-ready/mcp.md) — Claude Code, Cursor, Codex and any MCP client, through one endpoint. {plug}
- [Brand it](./design/README.md) — Logo, colours, fonts, header, footer and your own domain. {palette}
- [Read the numbers](./analytics/README.md) — Which pages were read, which searches found nothing, and where readers stopped. {bar-chart-3}

<!-- /widget -->

## What teams hire it for

Every goal comes with the reading it is judged by — a number, not an impression.

<!-- widget:cards icons=inline horizontal cols=2 arrow=hover -->

- [Be found](./seo/README.md) — Qualified organic traffic, read as clicks and impressions per intent. {search}
- [Be recommended](./geo/README.md) — Named when assistants answer your category, read as citations across a fixed question set. {sparkles}
- [Turn readers into customers](./analytics/reports/goals-and-funnels.md) — More readers reaching the product, read as goal completions per page. {git-fork}
- [Open a new market](./translation/README.md) — Readers in another language, read as traffic and rank per locale. {languages}

<!-- /widget -->

## Everything a docs team hires five tools for

One panel, the whole growth loop: publishing, the agent, analytics, SEO, GEO and branding — measured in the same place they are changed.

<!-- widget:bento -->

- **An agent that wakes up when your product changes** — Commits, releases, merged pull requests, labelled issues, a watched API spec, a question in Discord — every trigger points at the agent. {badge:Autonomous agent} {span:7} {crop:top-left}

  ![Triggers screen: the Docsbook agent card and its event triggers](https://docsbook.io/landing-triggers.jpg)

- **Plugs into where the answers already live** — GitHub, Slack, Google Calendar, Google Workspace — or any MCP server. It reads the channels where questions get asked and the calendar where launches are planned. {span:5} {crop:top-left}

  ![Integrations screen: GitHub, Slack, Google Calendar and Google Workspace](https://docsbook.io/landing-integrations.jpg)

- **Analytics that speak in revenue, not pageviews** — Set a call-to-action URL and an average deal size, and read Revenue, Conversion rate and Revenue per visitor next to Bounce rate — plus a live map, entry pages, headings read, and the searches that found nothing. {span:12} {side} {tags} {crop:top-right}

  - Insights
  - Graph
  - Chat
  - Agent
  - Writing
  - SEO
  - GEO
  - Socials

  ![Analytics screen: visitors, revenue, conversion rate, bounce rate and the traffic chart](https://docsbook.io/landing-analytics.jpg)

- **Be found: clicks and impressions per intent** — Views, clicks, CTR, ranking and mentions across Google, Bing and DuckDuckGo, by query and by page. Plus every in-site search, so you see what readers wanted and did not get. {badge:SEO} {span:6} {crop:top-right}

  ![SEO screen: search queries with views, and in-site searches](https://docsbook.io/landing-seo.jpg)

- **Be recommended: who ChatGPT, Perplexity and Claude cite** — AI answers, indexing and training crawls per page and per crawler. When an assistant answers your category without you, the agent reads the answer engine and fixes it. {badge:GEO} {span:6} {crop:top-right}

  ![GEO screen: AI answers per page from ChatGPT-User, Perplexity-User and Claude-Web](https://docsbook.io/landing-geo.jpg)

- **Brand it in minutes** — Logo, colours, fonts, header, footer, sidebars and your own domain — one CNAME, SSL automatic. {span:4} {crop:top-right}

  ![Customize screen: background style presets and colours](https://docsbook.io/landing-customize.jpg)

- **Ship through pull requests** — Every change is a pull request with the diff and the issues behind it. Auto-merge on, or review first. Your repository stays the source of truth. {span:4}

  ![Settings screen: the auto-merge toggle and the call-to-action URL](https://docsbook.io/landing-pull-requests.jpg)

- **AI chat that admits what it doesn't know** — Answers grounded in your pages and your real site facts. No answer in the docs? It says so and hands the reader to support. {span:4} {message-circle}

  - Custom system prompt and suggested questions
  - Pick the model for readers and for the agent
  - REST API to call the chat from your backend
  - Password or SSO for private docs

<!-- /widget -->

## How the loop runs

You name the outcome. Docsbook researches what is there, proposes the change, writes the expected number down **before** the work, and reads it on the date.

<!-- widget:journey cols=4 -->

### Goal

One sentence from you: the outcome you want, not a brief or a backlog.

- [Give your agent a goal](./agent-ready/mcp.md) {target}

### Research

What your product does, who ranks for it, what assistants answer, and what your readers searched for and did not find.

- [How we prove it](./evidence.md) {scale}

### Experiment

A change committed to your repository as a pull request, with the number it is expected to hit and the date it is read on.

- [Source of truth](./agent-ready/source-of-truth.md) {git-branch}

### Verdict

On the date, the reading is taken. Confirmed or rejected, and a rejection is kept so the next bet does not repeat it.

- [Goals and funnels](./analytics/reports/goals-and-funnels.md) {check-circle}

<!-- /widget -->

## What those sites look like

Live documentation, public and readable without signing in.

<!-- widget:showcase cols=3 -->

- [Cursor](https://docsbook-websites.docsbook.io/cursor) — Documentation for the AI code editor {color:#1a1a1a}

  ![Cursor documentation built with Docsbook](https://docsbook.io/gallery-cursor-light.png)

- [ClickHouse](https://docsbook-websites.docsbook.io/clickhouse) — Column-oriented database for real-time analytics {color:#faff69}

  ![ClickHouse documentation built with Docsbook](https://docsbook.io/gallery-clickhouse-light.png)

- [Discord Developers](https://docsbook-websites.docsbook.io/discord-developers/) — Build bots, Activities, and apps on Discord {color:#5865F2}

  ![Discord Developers documentation built with Docsbook](https://docsbook.io/gallery-discord-developers-light.png)

<!-- /widget -->

[See every site in the showcase →](https://docsbook.io/showcase)

## Explore the documentation

<!-- widget:cards plain cols=3 arrow=hover -->

## Publish

- [Quick start](./quick-start.md) — Source to public URL {rocket}
- [Content and setup](./content/README.md) — Sources, indexing, GitHub link {settings-2}
- [Custom domain](./guides/advanced/custom-domain.md) — One CNAME, SSL automatic {globe}
- [Private docs](./guides/advanced/sso.md) — Shared password or your own SSO {lock}
- [Translation](./translation/README.md) — 15 languages, indexed separately {languages}
- [Design and branding](./design/README.md) — Name, colour, fonts, layout {palette}

## Agents

- [MCP server](./agent-ready/mcp.md) — Connect the agent you already use {plug}
- [MCP tools reference](./mcp/README.md) — Every tool and its price class {list}
- [Docs skills](./agent-ready/skills.md) — SKILL.md files any agent can load {graduation-cap}
- [Source of truth](./agent-ready/source-of-truth.md) — The graph an agent navigates {network}
- [MCP security](./agent-ready/mcp-security.md) — Auth model and token scopes {shield}
- [AI chat](./ai-chat/README.md) — Answers for readers, grounded in your pages {message-circle}

## Reference

- [Concepts](./basics.md) — Workspace, balance, indexing {box}
- [Pricing](./pricing.md) — What is metered, and what is not {credit-card}
- [REST API](./rest-api/README.md) — Call your docs chat from your backend {code}
- [Webhooks](./reference/webhooks.md) — Event catalogue and payload schemas {bell}
- [Content widgets](./content/features/widgets.md) — Hero, cards, stats and steps in Markdown {layout-grid}
- [Changelog](./CHANGELOG.md) — What shipped, and what it was meant to buy {history}

<!-- /widget -->

<!-- widget:cta -->

**Ready when you are**

## Give your agent a goal

Ask one question and you get a researched answer about your own market, whether or not you run anything it suggests. Questions: [support@docsbook.io](mailto:support@docsbook.io) or the [Docsbook Discord](https://discord.gg/baqUCdwrag).

[Start free — no credit card](https://docsbook.io/?start=1) · [Connect your agent](./agent-ready/mcp.md)

<!-- /widget -->
