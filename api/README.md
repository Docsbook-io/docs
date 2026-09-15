---
title: "Docsbook API"
description: "Everything Docsbook can do, your backend can do — with one key and a curl."
---

# Docsbook API

Everything Docsbook can do, your backend can do — with one key and a `curl`. Ask your
documentation a question and get a grounded answer with its sources; or call any tool the
Docsbook MCP server registers, without bringing an MCP client.

## Get your key

Open **Integrations** — from your avatar in the assistant's input, or your profile
dropdown in the admin panel. View it, copy it, or reset it there.

One live key per project. Resetting revokes the old one immediately, everywhere, and
there is no key history — so update your callers before you reset.

The key carries the same full access an owner has from the admin panel, including tools
that write to your documentation. Treat it as a server-side secret: never ship it in a
browser bundle or a mobile app.

## What a call costs

`POST /api/v1/chat` spends from your project's AI budget — the same wallet the Ask AI
widget on your published site spends from. There is no separate API quota.

Every other call is a tool call, charged the same flat per-call price it would cost over
MCP and written to the same event feed, marked `api` so your call history can tell the
two apart. Each tool's page names its price.

Base URL: `https://docsbook.io`

Every page below is generated from the OpenAPI document, so it describes the API that is running right now.

151 more operations call MCP tools one by one; each is documented on its own tool page under **MCP Tools**, together with the MCP call it mirrors.

<!-- widget:cards cols=2 -->

- [Chat](./chat/README.md) — Ask your documentation a question and get one grounded answer.
- [Tools](./tools/README.md) — Dispatch any MCP tool by name.

<!-- /widget -->
