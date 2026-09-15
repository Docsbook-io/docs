---
title: "Call Docsbook's AI chat and any MCP tool from your own backend"
description: "Authenticate with your workspace API key and call the Docsbook REST endpoints: ask your documentation a question, or call any MCP tool — analytics, content, translations, webhooks — over plain REST."
---

# API

Every workspace has one public API key, used to authenticate calls to Docsbook's REST
API from your own backend. The API exposes two things: exporting your workspace's AI
docs-chat as a plain REST endpoint — the same grounded-answer engine that powers the AI
chat widget on your published docs site — and, since 15.09.2026, every tool the Docsbook
MCP server exposes, callable the same way. Build your own support bot, Slack integration,
or CLI on top of either.

## Getting your API key

Open **Integrations** — reachable from your avatar dropdown in the assistant's
input, or your profile dropdown in the admin panel. From there you can view
(masked or revealed), copy, or reset your key.

There is one live key per workspace. Resetting immediately revokes the old one —
there is no key history, so update any callers before you reset.

## Authentication

Every request is authenticated with a Bearer token — your workspace's API key.

```http
Authorization: Bearer dbk_YOUR_API_KEY
```

Keep your key secret — it grants the same full access an owner has from the admin
panel: your AI chat, and every tool below, including ones that write to your docs.

<!-- widget:api -->

## POST /api/v1/tools/{tool}

Call any tool the Docsbook MCP server exposes — analytics, content search and
writing, translations, webhooks, workspace settings — as a plain REST call instead
of an MCP client. It dispatches into the exact same server an MCP-connected agent
talks to, so it is billed and logged exactly like an MCP call: the same flat
per-call price off your workspace's balance, published on the [MCP tools
reference](./mcp-tools.md), and the same row in your event feed. Your workspace is
resolved from the API key, so there is no `workspace_id` to pass.

| Field | Type | Required | Description |
|---|---|---|---|
| `args` | object | no | The tool's own arguments, exactly as an MCP client would send them |

### Example

```bash
curl -X POST https://docsbook.io/api/v1/tools/get_analytics \
  -H "Authorization: Bearer dbk_YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"args": {"period": "30d"}}'
```

### Response

```json
{
  "ok": true,
  "result": { "visitors": 1284, "pageviews": 5310 },
  "duration_ms": 214
}
```

### Errors

| Status | Meaning |
|---|---|
| `401` | Missing or invalid API key |
| `404` | `TOOL_NOT_FOUND` — this server has no tool by that name. Never billed: the call never reached a tool. |

`result` is that tool's own answer, already parsed from JSON. A tool that ran and
answered with its own error — an insufficient balance, a plan restriction, a bad
argument — still returns `200`, with `ok: false` and the tool's structured error
under `result`: the call was made and billed, and that error is its answer.

## POST /api/v1/chat

Ask a question against your workspace's documentation and get back an answer
grounded in your own pages. Billed against the same project balance the docs-chat
widget spends; there is no separate API-only allowance.

| Field | Type | Required | Description |
|---|---|---|---|
| `question` | string | yes | The question to ask |
| `currentPath` | string | no | The doc page slug the question is asked from, to exclude it from its own citations |
| `lang` | string | no | Answer language code; defaults to the workspace's default language |
| `sessionId` | string | no | Groups related questions for analytics and webhooks |
| `mentionedPages` | string[] | no | Page slugs to force into context |

### Example

```bash
curl -X POST https://docsbook.io/api/v1/chat \
  -H "Authorization: Bearer dbk_YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"question": "How do I set a custom domain?"}'
```

### Response

```json
{
  "answer": "You can set a custom domain from the Branding tab...",
  "refs": [{ "pagePath": "design/domains", "title": "Custom Domains", "heading": "Setup" }],
  "follow_up_questions": ["What SSL certificate is used?", "Can I use a subdomain?"]
}
```

### Errors

| Status | Meaning |
|---|---|
| `400` | The request body is missing `question` |
| `401` | Missing or invalid API key |
| `502` | The chat engine failed to produce an answer |

⚠️ **A refused question can also come back as a normal-looking `200`.** When AI
chat isn't enabled for the workspace's plan, its AI balance is exhausted, or the
request is flagged as automated, the endpoint currently answers with `200` and
an **empty** `answer` (`refs` and `follow_up_questions` empty too) rather than a
distinct error status. Treat an empty `answer` as a failure case in addition to
the statuses above — do not assume `200` means the question was actually
answered.

<!-- /widget -->

## Related

- [MCP tools reference](./mcp-tools.md) — the full tool catalog `/api/v1/tools/{tool}` dispatches into, with argument schemas and prices
- [AI chat](../ai-chat/chat.md) — the assistant this endpoint exposes, and how it is configured
- [Webhooks](./webhooks.md) — being told when a question goes unanswered, rather than polling for it
- [AI usage & cost statistics](../analytics/tracking/ai-usage.md) — what these calls cost and what readers asked
