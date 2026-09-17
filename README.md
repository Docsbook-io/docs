---
title: "Docsbook documentation: goals, experiments, and what they measured"
description: "Docsbook turns a business goal into researched opportunities and experiments that each carry an expected number and a date. Start here, then pick the guide for the job you are doing."
tldr: "Docsbook takes one stated business goal, researches the evidence behind it, and turns it into an experiment with a predicted number and date, then reports on that date whether the experiment hit that number."
---

<!-- widget:hero -->

**Docsbook documentation**

# Give your agent a goal. Get back an opportunity, a number, and a verdict.

Say where you want the business to get to. Docsbook researches what is actually there, sizes the opportunity from evidence, and turns it into experiments that each carry a number they are expected to hit — then reads, on the date, whether they hit it. It runs inside the agent you already use, and everything it writes lands in your own repository as a commit you review.

- [Quick start](./quick-start.md) {rocket}
- [How it works](./overview.md) {compass}
- [MCP server](./agent-ready/mcp.md) {terminal}
- [Pricing](./pricing.md) {credit-card}

> ![Claude](https://docsbook.io/agents/claude.svg) ![OpenAI](https://docsbook.io/agents/openai.svg) ![Cursor](https://docsbook.io/agents/cursor.svg) **Onboard your agent** — Set up Docsbook for me. Fetch https://docsbook.io/get-started.md and follow it.
>
> Paste one prompt into Claude Code, Cursor, Codex or any client that speaks MCP. It connects the server itself, writes a Docsbook rule into its own memory file, and takes a first project live.

<!-- /widget -->

<!-- widget:cards cols=2 -->

## What people bring it

- [Be found](./seo/README.md) — "More qualified organic traffic." Read as clicks and impressions per intent. {search}
- [Be recommended](./geo/README.md) — "Be named when assistants answer my category." Read as citations across a fixed question set. {sparkles}
- [Turn readers into customers](./analytics/reports/goals-and-funnels.md) — "Make more readers reach the product." Read as goal completions per page. {git-fork}
- [Open a new market](./translation/README.md) — "Reach people in another language." Read as traffic and rank per locale. {languages}

<!-- /widget -->

## The loop, in eight stages

The stage most tools skip is the fifth: writing down what should change, and by when, **before** doing the work. Without it the seventh stage has nothing to compare against.

<!-- widget:stepper -->

### Goal

One sentence from you — the outcome you want, not a brief or a backlog.

### Research

Six classes of evidence: what your product does, the demand around it, who ranks for it, what assistants answer, what your readers searched for and did not find.

### Opportunity

One row per thing people look for: how many of them, what your docs show them today, who gets the click instead, and what winning it is worth.

### Hypothesis

Competing ways to take the same opportunity, each argued from the readings rather than from a checklist.

### Expected effect

The number it is expected to hit and the date it will be read on — written down before any page exists.

### Experiment

The change is written into your repository as a commit or a pull request you review like any other.

### Actual result

On the date, the reading is taken and compared with the number written beforehand. Confirmed or rejected.

### Learning

A rejection counts: what it eliminated is kept, so the next bet does not repeat it.

<!-- /widget -->

The experiments run on documentation because it is the surface an agent can change without asking anyone for access, and the one whose effect is readable from outside — search indexes it, assistants quote it, buyers decide on it, and every page reports its own traffic, referrals and failed searches.

## The surface they run on

Four stages, and an experiment can be read at any of them. Pick the one you are asking about.

<!-- widget:journey cols=2 -->

### Publish

Source to a public URL, in about five minutes.

- [Quick start](./quick-start.md) {rocket}
- [Guides](./guides/README.md) {book-open}
- [Custom domain](./guides/advanced/custom-domain.md) {globe}

### Get found

What ships for search engines without configuring anything.

- [SEO](./seo/README.md) {search}
- [llms.txt](./geo/llms-txt.md) {file-text}

### Get quoted

What makes a passage an assistant can cite.

- [GEO](./geo/README.md) {sparkles}
- [AEO](./aeo/README.md) {message-square-quote}
- [AI chat](./ai-chat/README.md) {message-circle}

### Measure

Which pages were read, and where readers stopped.

- [Analytics](./analytics/README.md) {bar-chart-3}
- [Goals and funnels](./analytics/reports/goals-and-funnels.md) {target}
- [Page feedback](./ai-chat/feedback.md) {thumbs-up}

<!-- /widget -->

## Start in one conversation

There is no signup flow in front of it. Point the agent you already work in at one endpoint and say where you want to go.

```bash
claude mcp add --transport http docsbook https://docsbook.io/api/mcp/server
```

Codex, Cursor, Windsurf, Cline and any other MCP client use the same endpoint — see [MCP server](./agent-ready/mcp.md) for each. Would rather see the surface first? [Publish a site in about five minutes](./quick-start.md).

<!-- widget:cards cols=3 plain -->

## Start here

- [Overview](./overview.md) — What Docsbook does, and what it costs {compass}
- [Quick start](./quick-start.md) — Source to public URL {rocket}
- [Concepts](./basics.md) — Workspace, balance, indexing {box}
- [Use cases](./use-cases.md) — The jobs teams hire docs for {target}
- [How we prove it](./evidence.md) — The evidence rule every page follows {scale}

## Run the loop from your agent

- [MCP server](./agent-ready/mcp.md) — Connect the agent you already use {plug}
- [MCP tools reference](./mcp/README.md) — Every tool and its price class {list}
- [Docs skills](./agent-ready/skills.md) — SKILL.md files any agent can load {graduation-cap}
- [Source of truth](./agent-ready/source-of-truth.md) — The graph an agent navigates {network}
- [MCP security](./agent-ready/mcp-security.md) — Auth model and token scopes {shield}

## Publish, brand and translate

- [Guides](./guides/README.md) — Create and manage a site {book-open}
- [Content and setup](./content/README.md) — Sources, indexing, GitHub link {settings-2}
- [Design and branding](./design/README.md) — Name, colour, fonts, layout {palette}
- [Custom domain](./guides/advanced/custom-domain.md) — One CNAME, SSL automatic {globe}
- [Private docs](./guides/advanced/sso.md) — Shared password or your own SSO {lock}
- [Translation](./translation/README.md) — 15 languages, indexed separately {languages}

## Reference

- [Pricing](./pricing.md) — What is metered, and what is not {credit-card}
- [FAQ](./faq.md) — Cost, sync, privacy, data ownership {help-circle}
- [REST API](./rest-api/README.md) — Call your docs chat from your backend {code}
- [Webhooks](./reference/webhooks.md) — Event catalogue and payload schemas {bell}
- [Content widgets](./content/features/widgets.md) — Cards, steps and callouts in Markdown {layout-grid}
- [Changelog](./CHANGELOG.md) — What shipped, and what it was meant to buy {history}
- [Blog](./blog/README.md) — AI search, docs SEO, comparisons {newspaper}

<!-- /widget -->

## Documentation running on Docsbook

Every site below is live and readable without signing in.

<!-- widget:showcase cols=3 -->

- [Cursor](https://docsbook-websites.docsbook.io/cursor) — Documentation for the AI code editor {color:#1a1a1a}

  ![Cursor documentation built with Docsbook](https://docsbook.io/gallery-cursor-light.png)

- [ClickHouse](https://docsbook-websites.docsbook.io/clickhouse) — Column-oriented database for real-time analytics {color:#faff69}

  ![ClickHouse documentation built with Docsbook](https://docsbook.io/gallery-clickhouse-light.png)

- [Discord Developers](https://docsbook-websites.docsbook.io/discord-developers/) — Build bots, Activities, and apps on Discord {color:#5865F2}

  ![Discord Developers documentation built with Docsbook](https://docsbook.io/gallery-discord-developers-light.png)

- [Ramp](https://docsbook-websites.docsbook.io/ramp) — Developer API for the finance platform 70,000+ businesses run on {color:#d7f942}

  ![Ramp documentation built with Docsbook](https://docsbook.io/gallery-ramp-light.png)

- [n8n](https://docsbook-websites.docsbook.io/n8n) — Workflow automation platform for technical teams {color:#ea4b71}

  ![n8n documentation built with Docsbook](https://docsbook.io/gallery-n8n-light.png)

- [Runway API](https://docsbook-websites.docsbook.io/runway-api) — Generative video, image, and audio behind one HTTP API {color:#0e0e0e}

  ![Runway API documentation built with Docsbook](https://docsbook.io/gallery-runway-api-light.png)

<!-- /widget -->

[See every site in the showcase →](https://docsbook.io/showcase)

Support: [support@docsbook.io](mailto:support@docsbook.io) or the [Docsbook Discord](https://discord.gg/baqUCdwrag).

<!-- widget:cta -->

**Ready when you are**

## Give your agent a goal

Ask one question and you get a researched answer about your own market — whether or not you ever run anything it suggests.

[Start free — no credit card](https://docsbook.io/start) · [Connect your agent](./agent-ready/mcp.md)

<!-- /widget -->
