---
title: "Call your documentation's AI chat from your own backend"
description: "Authenticate with your workspace API key and POST a question to the Docsbook REST endpoint to get an answer grounded in your own documentation pages."
---

# API

The Docsbook REST API answers a question against your own documentation. Every workspace has one public API key, used to authenticate calls to Docsbook's
REST API from your own backend. Today the API exposes one capability: exporting
your workspace's AI docs-chat as a plain REST endpoint — the same grounded-answer
engine that powers the AI chat widget on your published docs site, so you can
build your own support bot, Slack integration, or CLI on top of it.

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

Keep your key secret — it grants full access to your workspace's AI chat. Every
answer is billed against the same project balance the docs-chat widget spends;
there is no separate API-only allowance.

<!-- widget:api -->

## POST /api/v1/chat

Ask a question against your workspace's documentation and get back an answer
grounded in your own pages.

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
| `401` | Missing or invalid API key |
| `403` | AI chat is not enabled for this workspace |
| `429` | The project's balance is exhausted |

<!-- /widget -->

## Related

- [MCP tools reference](./mcp-tools.md) — the tool surface an agent uses instead of this endpoint
- [AI chat](../ai/chat.md) — the assistant this endpoint exposes, and how it is configured
- [Webhooks](./webhooks.md) — being told when a question goes unanswered, rather than polling for it
- [AI usage & cost statistics](../analytics/tracking/ai-usage.md) — what these calls cost and what readers asked
