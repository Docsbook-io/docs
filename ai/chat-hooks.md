---
title: "AI Chat Hooks — Customize the LLM Pipeline"
description: "Intercept the LLM pipeline with pre and post hooks (PRO+). Filter PII, inject context, enforce brand voice, and shape every response."
---

# AI Chat Hooks

Chat hooks let you intercept the LLM pipeline at two points: before the prompt reaches the model and after the model returns a response. Use them to enforce compliance, brand voice, or analytics requirements without forking the chat infrastructure.

## Pre-hook

The pre-hook runs after the reader's question is captured and before the LLM is called. It can:

- Strip PII (emails, account IDs, tokens) from the user's text.
- Inject extra context — current plan, account tier, locale.
- Rephrase the question to match canonical terminology.
- Block the request entirely with a structured error.

```typescript
// Example pre-hook payload
{
  question: "What's the price for team@acme.com?",
  context: { plan: "pro_plus", locale: "en" }
}
```

## Post-hook

The post-hook runs after the LLM produces an answer and before it streams to the reader. It can:

- Redact sensitive information that leaked into the response.
- Append a disclaimer or a CTA.
- Reformat code blocks, links, or headings.
- Log the final pair to your own analytics store.

## Use cases

| Scenario | Hook |
|---|---|
| Compliance (GDPR, HIPAA) | Pre + post redaction |
| Brand voice enforcement | Post-hook style rewrite |
| Internal analytics | Post-hook mirror to your DB |
| A/B prompt testing | Pre-hook prompt mutation |

## MCP tools

Manage hooks from Claude Code or any MCP client:

```bash
set_chat_hooks          # register pre/post-hook URLs and secrets
test_chat_hook          # dry-run a hook against sample data
get_chat_system_prompt  # inspect the current system prompt
```

Hooks are HTTPS endpoints. Docsbook signs every call with an HMAC SHA-256 signature in the `X-Docsbook-Signature` header, the same scheme used by webhooks.

## Pricing

Chat hooks are a **PRO+** feature ($59/month).

## Related

- [AI Chat](./chat.md) — The pipeline the hooks plug into.
- [MCP Server](./mcp.md) — Configure hooks remotely from your editor.
