---
title: "Chat hooks: block, enrich and record every AI answer"
description: "Intercept Docsbook AI Chat with a pre-LLM hook that blocks or injects context, plus post and streaming hooks that mirror every answer to your systems."
---

# AI Chat Hooks

Docsbook chat hooks are HTTPS endpoints of yours that Docsbook AI Chat calls around each answer. There are three: a **pre-hook** that runs before the model is called and can change or stop the request, and **post** and **streaming** hooks that receive the finished answer after the reader already has it.

Use them to enforce a compliance rule, to hand the model context only your systems know, or to mirror every question and answer into your own analytics — without forking the chat.

## What can a chat hook actually change?

Only the pre-hook changes anything. Docsbook AI Chat calls it and waits for the reply, so its answer shapes the request. The post and streaming hooks are fire-and-forget: Docsbook does not wait for them and does not re-read the response, so they cannot redact, rewrite or reformat what the reader sees.

| Hook | When it runs | Can it change the answer? | What it is for |
|---|---|---|---|
| Pre-hook | Before the model is called, blocking | Yes — block the request or inject context | Refuse a question, add plan or locale context |
| Post-hook | After the answer is complete | No | Log the question/answer pair to your own store |
| Streaming hook | Alongside the post-hook | No | Feed a live dashboard or an alerting channel |

Each hook has its own URL, set independently. All three time out after **5 seconds**; a hook that does not answer in time is skipped, and the reader's answer is not delayed further.

## How do I block or enrich a question before the model sees it?

Set a pre-hook URL. Docsbook AI Chat POSTs the reader's question to it as JSON and waits for a reply, then acts on two optional fields.

The request Docsbook sends:

```json
{
  "question": "What's the price for team@acme.com?",
  "session_id": "sess_YOUR_SESSION_ID",
  "workspace_id": 42
}
```

The reply Docsbook understands:

```json
{
  "block": true,
  "reason": "Ask your account manager for account-specific pricing",
  "inject_context": "The reader is on the Acme account, locale en-GB."
}
```

- Return `block: true` and the reader sees your `reason` instead of an answer. Nothing is sent to the model.
- Return `inject_context` and that string is added to the prompt for this one question. This is where live facts belong — the reader's plan, their region, a feature flag.
- Return anything else, a non-2xx status, or nothing at all, and the chat continues as if no hook were set. A broken hook degrades the chat; it does not break it.

## What does the post-hook receive?

The post-hook receives the finished exchange as JSON, once, after the reader has already seen the answer:

```json
{
  "question": "How do I rotate an API key?",
  "answer": "Rotate an API key in Workspace settings…",
  "tool_calls": [{ "tool": "read_page", "path": "guides/keys.md" }],
  "latency_ms": 2840,
  "workspace_id": 42,
  "session_id": "sess_YOUR_SESSION_ID"
}
```

The streaming hook receives the same fields plus `event: "message"` and the `refs` the answer cited. Both are one-way. If your compliance rule is "this text must never reach a reader", it belongs in the pre-hook or in the system prompt, not here.

## Use cases

| Scenario | Hook | Why that one |
|---|---|---|
| Refuse questions about another customer's account | Pre-hook | Only the pre-hook can stop the request |
| Give the model the reader's plan and locale | Pre-hook (`inject_context`) | The model needs it before it answers |
| Mirror every Q&A into your own analytics store | Post-hook | Needs the finished answer, changes nothing |
| Alert a channel when an answer takes too long | Streaming hook | Carries `latency_ms` per message |
| A/B two prompt phrasings | Pre-hook | Mutates the prompt, one question at a time |

## Are chat hooks signed?

Docsbook chat hooks are **not** signed. Docsbook sends a plain `POST` with `Content-Type: application/json` and no HMAC header, so your endpoint must not treat the payload as proof of origin. Keep the URL secret, put it behind an allowlist or a token in the path or query string, and treat the body as untrusted input.

Docsbook [webhooks](../webhooks.md) are different: those are signed with HMAC-SHA256 in `X-Docsbook-Signature-256`. Do not carry a webhook's verification code over to a chat hook and assume it verifies anything.

## Managing hooks from an MCP client

Three MCP tools configure hooks from Claude Code, Cursor, or any MCP client:

```bash
set_chat_hooks          # register pre / post / streaming hook URLs
test_chat_hook          # dry-run one hook against sample data
get_chat_system_prompt  # inspect the current system prompt
```

Pass an empty string to `set_chat_hooks` to clear an individual hook. The same fields are editable in the workspace admin panel.

## Related

- [AI Chat](./chat.md) — the pipeline the hooks plug into.
- [Sources](./sources.md) — the other way to give the assistant facts it does not have.
- [Webhooks](../webhooks.md) — signed, event-driven deliveries, and how to verify them.
- [MCP Server](./mcp.md) — configure hooks remotely from your editor.
