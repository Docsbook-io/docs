---
title: "Docsbook API"
description: "One workspace API key: the AI chat engine that answers from your documentation, your MCP owner surface (orientation, your own reads, and delegating a job to `docsbook_agent`),…"
---

# Docsbook API

One workspace API key: the AI chat engine that answers from your documentation, your
MCP owner surface (orientation, your own reads, and delegating a job to `docsbook_agent`), and a
narrow list of configuration settings — each with its own real `GET` or `POST` below.

This does not include writing documentation, translations or webhooks directly: since 2026-09-18
that catalog is reached only by delegating a job to `docsbook_agent`, the same as your own connected
MCP agent now does.

This document is generated from the running server, so every operation below is reachable right now —
nothing here 404s on the first call. Get your key from **Integrations** in your workspace settings.

Base URL: `https://docsbook.io`

Your workspace's API key, from **Integrations** in workspace settings.

The key reaches your MCP owner surface — orientation, delegating and watching a `docsbook_agent`
job, reading your own documentation and Docsbook's own docs — plus a narrow, separate list of
configuration settings (branding, navigation, the chatbot, translation mode, mention tracking) each
published at its own path below. It does **not** reach documentation writes, translations, webhooks
or the product's own memory: that catalog is reached by delegating a job to `docsbook_agent`, never
directly over REST. Treat the key as a server-side secret regardless: never ship it in a browser
bundle or a mobile app. Resetting a key revokes the old one immediately, everywhere.

Every page below is generated from the OpenAPI document, so it describes the API that is running right now.

26 more operations call MCP tools one by one; each is documented on its own tool page under **MCP Tools**, together with the MCP call it mirrors.

<!-- widget:cards cols=2 -->

- [Chat](./chat/README.md) — Ask your documentation a question and get one grounded answer.
- [Tools](./tools/README.md) — Dispatch any MCP tool by name.

<!-- /widget -->
