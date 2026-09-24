---
title: "Docsbook API"
description: "Call Docsbook from your own backend with one API key and plain HTTPS."
---

# Docsbook API

Call Docsbook from your own backend with one API key and plain HTTPS. Everything your MCP connection can do has its own endpoint here: projects, your pages, site settings, languages and translations, goals, webhook alerts, the agent's memory, `docsbook_agent` — and the AI chat that answers from your docs.

## Get your key

Open **Settings ▸ Domain & API** in the panel to view, copy or reset the project's API key. Send it as `Authorization: Bearer dbk_…`.

There is one live key per project. Resetting it revokes the old key everywhere at once, so update your callers first — and keep the key on your server, never in a browser or mobile app: it can change your site.

## How the endpoints are shaped

- **Reads** — `GET /api/v1/{tool}`, arguments in the query string: `GET /api/v1/search_project_docs?query=custom%20domain`.
- **Changes** — `POST /api/v1/{tool}`, arguments as the JSON body: `POST /api/v1/update_branding` with `{"accent_color": "#0f766e"}`.
- **Ask your docs** — `POST /api/v1/chat`, a grounded answer with sources: the same engine as the [AI chat](../ai-chat/README.md).
- **By name** — `POST /api/v1/tools/{tool}` with `{"args": {…}}`, for a caller that holds the tool name in a variable.

The project is taken from the key, so there is no workspace to name. Every endpoint answers `{ "ok": true, "result": … }`; a tool that ran and refused (a bad argument, an empty balance) answers `200` with `ok: false` and its reason.

## What a call costs

Each call is charged to your balance at **twice what serving it costs us** — the price is on every endpoint's page, and it is the same price as the MCP tool it runs. For most endpoints that is a few cents per thousand calls; discovery calls are free. Model tokens are billed at twice the provider's price, and an endpoint that calls a paid data vendor adds twice the vendor's price. `POST /api/v1/chat` is billed by its tokens only. See [pricing](../plans-and-pricing.md).

Base URL: `https://docsbook.io`

Every page below is generated from the OpenAPI document, so it describes the API that is running right now.

<!-- widget:cards cols=2 -->

- [Chat](./chat/README.md) — Ask your documentation a question and get one grounded answer.
- [Tools](./tools/README.md) — Dispatch any MCP tool by name.
- [Settings](./settings/README.md) — Change one thing about the site to a value the user stated.
- [Content](./content/README.md) — Read and write the documentation itself.
- [Handoff](./handoff/README.md) — Give a finished site to the business it was built for — a claim link that moves the project onto their…
- [Goals](./goals/README.md) — Declare what a reader was supposed to do, and count who did.
- [Create](./create/README.md) — Bring a documentation site into existence.
- [Agent](./agent/README.md) — The Docsbook agent — one worker you delegate to, and the whole of "manage the documentation" on a customer's…
- [Orientation](./orientation/README.md) — Find out what this server is, which project the user means, and — on an owner's token — what else this…
- [Context](./context/README.md) — THIS ORGANIZATION'S FOLDER — what previous runs worked out about this customer, as files the agent reads and…
- [Product Help](./product-help/README.md) — The craft corpus — `docsbook_assistant` — how the work is done well, from Docsbook's published pages, with…
- [Alerts](./alerts/README.md) — Outbound notifications when something happens on the site.

<!-- /widget -->
