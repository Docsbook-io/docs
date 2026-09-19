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

## Two surfaces, one endpoint

Since 2026-09-18 your own connected agent and this catalog are not the same thing.

**Your token** — the one your editor holds after the OAuth step above — meets a small,
fixed surface: orientation (`get_info`, `list_workspaces`, `get_workspace`), reading your
own documentation and Docsbook's own docs, creating a project, and the five tools that
give a job to **`docsbook_agent`** and watch it. That is the whole of "manage the
documentation" from your own agent now. A handful of the tools below are also reachable
without a token at all — those are the ones your own readers reach through the public
endpoint on your published site.

**Everything else on this page** — writing documentation, translations, webhooks,
analytics beyond your own project's summary, the product's own accumulated memory — is
performed by `docsbook_agent`, the background worker Docsbook runs on your behalf. You do
not call `write_docs` yourself any more; you describe the job to `docsbook_agent`
("restructure the getting-started section around three personas"), it plans, does the
work, and reports back what it did. This page still documents every one of those tools in
full, because knowing what `docsbook_agent` *can* do is exactly how you know what to ask
it for — read them as its capability list, not as a menu your own token can dial directly.

A narrow additional slice of pure configuration (branding, navigation, the chatbot,
translation mode, mention tracking) is reachable directly by your **workspace API key**
over REST, even though it is not on your MCP token's surface — see the API Reference
section for that list and why it stops where it does.

## Start with the agent

`docsbook_agent` is the first call to make for any documentation request, however narrow,
in any language: describe the outcome, not the steps. `docsbook_agent_status` and
`docsbook_agent_tasks` watch it, `docsbook_agent_reply` answers a question it asks
mid-run, `docsbook_agent_stop` cancels it. `workspace_id` is required on all five.

## What a call costs

A flat price per call, decided by what serving it costs — reading a row, scanning the
event warehouse, leaving the network, running a model — and charged to your project's
balance. Each tool's page names its own price; the classes behind them are on the
[pricing page](https://docsbook.io/pricing). A call refused for an empty balance says so.

## READ and WRITE

The pill beside each tool in the sidebar says whether it only reads a project or can
change it. A handful of tools are marked **no token needed** — those are the ones your
own readers reach through the public endpoint on your published site.

Endpoint: `https://docsbook.io/api/mcp/server`

<!-- widget:cards cols=2 -->

- [Opportunities](./opportunities/README.md) — What there is to WIN for this project against the standing goal — be found, on Google and in AI answers —…
- [Hypotheses](./hypotheses/README.md) — A WAY TO WIN an opportunity, written before the change and judged after it — what this project believes will…
- [Memory](./memory/README.md) — This project's BRIEF — what it aims at, what nobody has answered yet, and what is known about it.
- [Settings](./settings/README.md) — Change one thing about the site to a value the user stated.
- [Evidence](./evidence/README.md) — The rows behind a judgement, gathered in code — no model, nothing to disbelieve.
- [Issues](./issues/README.md) — Work that outlives the conversation, on the project's GitHub repository.
- [History](./history/README.md) — What this server was already asked here, and what it answered — the record that turns every read into a…
- [Content](./content/README.md) — Read and write the documentation itself.
- [Research](./research/README.md) — What the outside world says — threads, job postings, reviews, profiles, a rival's docs, a page as a browser…
- [Goals](./goals/README.md) — Declare what a reader was supposed to do, and count who did.
- [Create](./create/README.md) — Bring a documentation site into existence.
- [Agent](./agent/README.md) — The Docsbook agent — one worker you delegate to, and the whole of "manage the documentation" on a customer's…
- [Product Help](./product-help/README.md) — The craft corpus — `docsbook_assistant` — how the work is done well, from Docsbook's published pages, with…
- [Analytics](./analytics/README.md) — What readers, searchers and the assistant actually did.
- [Orientation](./orientation/README.md) — Find out what this server is, and which project the user means.
- [Work](./work/README.md) — How the work on this project is going — the board, and what each piece of it is connected to.
- [Inbox](./inbox/README.md) — The owner's mailbox — a report worth a human read, or a question you cannot decide without their own words,…
- [Alerts](./alerts/README.md) — Outbound notifications when something happens on the site.

<!-- /widget -->
