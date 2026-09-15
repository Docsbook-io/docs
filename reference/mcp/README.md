---
title: "MCP Tools"
description: "Point an agent at your documentation and it can read it, write it, measure it and watch it — over MCP, the protocol Claude, Cursor, Windsurf and VS Code already speak."
---

# MCP Tools

Point an agent at your documentation and it can read it, write it, measure it and watch
it — over MCP, the protocol Claude, Cursor, Windsurf and VS Code already speak.

## Connect

```bash
claude mcp add --transport http docsbook https://docsbook.io/api/mcp/server
```

Authentication is OAuth 2.0 + PKCE: your client opens a browser once, you approve, and
the token is stored by the client. Nothing to paste.

Every tool below is also callable as a plain HTTP request, at the same price — each page
shows both forms, and the REST one comes with a form you can send from the page.

## Start with the expert

`docsbook_expert` is the first call to make for any documentation request, however
narrow, in any language. It is an **expert, not a runner**: one round trip returns how to
think about the request, the steps in order with the tool on each, what to carry between
them, what makes the answer wrong — and it runs none of it. `workspace_id` is optional,
because most of what it knows is true of documentation work rather than of one project.

## What a call costs

A flat price per call, decided by what serving it costs — reading a row, scanning the
event warehouse, leaving the network, running a model — and charged to your project's
balance. Each tool's page names its own price; the classes behind them are on the
[pricing page](https://docsbook.io/pricing). A call refused for an empty balance says so.

## READ and WRITE

The pill beside each tool in the sidebar says whether it only reads your project or can
change it. A handful of tools are marked **no token needed** — those are the ones your
own readers reach through the public endpoint on your published site.

Endpoint: `https://docsbook.io/api/mcp/server`

<!-- widget:cards cols=2 -->

- [Opportunities](./opportunities/README.md) — What there is to WIN for this project against the standing goal — be found, on Google and in AI answers —…
- [Hypotheses](./hypotheses/README.md) — A WAY TO WIN an opportunity, written before the change and judged after it — what this project believes will…
- [Memory](./memory/README.md) — This project's BRIEF — what it aims at, what nobody has answered yet, and what is known about it.
- [Settings](./settings/README.md) — Change one thing about the site to a value the user stated.
- [Product Help](./product-help/README.md) — Ask a real question about USING DOCSBOOK ITSELF and get back the same answer a reader gets from the public…
- [Evidence](./evidence/README.md) — The rows behind a judgement, gathered in code — no model, nothing to disbelieve.
- [History](./history/README.md) — What this server was already asked here, and what it answered — the record that turns every read into a…
- [Content](./content/README.md) — Read and write the documentation itself.
- [Research](./research/README.md) — What the outside world says — threads, job postings, reviews, profiles, a rival's docs, a page as a browser…
- [Goals](./goals/README.md) — Declare what a reader was supposed to do, and count who did.
- [Issues](./issues/README.md) — Work that outlives the conversation, on the project's GitHub repository.
- [Create](./create/README.md) — Bring a documentation site into existence.
- [Agent](./agent/README.md) — The one agent — `docsbook_expert` — an expert that tells you how to do the work and does none of it.
- [Analytics](./analytics/README.md) — What readers, searchers and the assistant actually did.
- [Orientation](./orientation/README.md) — Find out what this server is, and which project the user means.
- [Work](./work/README.md) — How the work on this project is going — the board, and what each piece of it is connected to.
- [Alerts](./alerts/README.md) — Outbound notifications when something happens on the site.

<!-- /widget -->
