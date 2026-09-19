Everything your workspace API key can reach, your backend can call directly — one key,
plain REST, no MCP client.

## Get your key

Open **Settings ▸ Profile** in the admin panel, beside the GitHub account this project
commits through. View the key, copy it, or reset it there.

One live key per project. Resetting revokes the old one immediately, everywhere, and
there is no key history — so update your callers before you reset.

## What the key reaches, and what it does not

Since 2026-09-18 this key meets the same owner surface your own connected MCP agent
does: orientation, reading your own documentation and Docsbook's own docs, and giving a
job to `docsbook_agent` (then watching, answering, or stopping it) — plus a narrow,
separate list of pure configuration settings (branding, navigation, the chatbot,
translation mode, mention tracking), each published below at its own `GET` or `POST`
path.

**It does not reach documentation writes, translations or webhooks directly.** That
catalog — everything tagged below with a tool page rather than its own REST path — is
reached only by delegating a job to `docsbook_agent`; there is no `write_docs` endpoint
to call from your backend. This is a narrower key than it used to be, on purpose: see the
MCP Tools section's intro for why.

Treat the key as a server-side secret regardless of what it can reach: never ship it in a
browser bundle or a mobile app.

## Read vs write, as real HTTP verbs

Every tool below that is safe to call from a script now has its own path and its own
verb — `GET /api/v1/get_analytics?period=30d` reads, `POST /api/v1/update_branding`
writes a setting. Nothing here 404s on the first call: what you see below is what runs.
For a tool that has neither — no individual path — the dispatch-by-name form,
`POST /api/v1/tools/{tool}`, still reaches the handful of owner-surface tools that are
not settings-shaped (`create_workspace`, and giving/watching/answering/stopping a
`docsbook_agent` job).

## What a call costs

`POST /api/v1/chat` spends from your project's AI budget — the same wallet the Ask AI
widget on your published site spends from. There is no separate API quota.

Every other call is a tool call, charged the same flat per-call price it would cost over
MCP and written to the same event feed, marked `api` so your call history can tell the
two apart. Each tool's page names its price.
