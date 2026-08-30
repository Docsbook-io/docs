---
title: "API Reference"
description: "Call Docsbook from your own backend — authenticate with your workspace API key and export your AI docs-chat as a REST endpoint."
---

# API

Every workspace has one public API key, used to authenticate calls to Docsbook's
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

```
Authorization: Bearer dbk_<your_api_key>
```

Keep your key secret — it grants full access to your workspace's AI chat, billed
against your account's AI budget (the same budget the docs-chat widget uses;
there is no separate API-only quota).

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
  -H "Authorization: Bearer dbk_<your_api_key>" \
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
| `429` | The account's AI budget is exhausted |

<!-- /widget -->
