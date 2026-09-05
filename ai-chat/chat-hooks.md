---
title: "Chat hooks: block, enrich and mirror every AI answer"
description: "Three HTTPS endpoints of yours around Docsbook AI chat — one that can stop or enrich a question before the model sees it, and two that receive the finished answer."
tldr: "The pre-hook runs before the model, blocks or injects context, and Docsbook waits up to 5 seconds for it. The post and streaming hooks are fire-and-forget and cannot change what the reader sees. None of the three is signed — authenticate them yourself."
---

# Chat hooks

Docsbook chat hooks are HTTPS endpoints of yours that [AI chat](./chat.md) calls around each answer. Use them to enforce a rule your compliance team wrote, to hand the model a fact only your systems know, or to mirror every question and answer into your own store — without forking the chat.

## What you get

Three hooks, each with its own URL, each set independently:

| Hook | When it runs | Can it change the answer? | What it is for |
|---|---|---|---|
| **Pre-hook** | Before the model is called, blocking | **Yes** — block the request, or inject context into the prompt | Refuse a question; add the reader's plan, region or feature flags |
| **Post-hook** | After the answer is complete | No | Log the question/answer pair to your own store |
| **Streaming hook** | Alongside the post-hook | No | Feed a live dashboard or an alerting channel |

Only the pre-hook changes anything, because it is the only one Docsbook waits for. The other two are dispatched after the reader already has the answer and their responses are never read — they cannot redact, rewrite or reformat what was shown.

Hooks are available on **every plan**, and calling them draws nothing from your balance. URLs must be `https://`; an `http://` URL is rejected when you save it.

## How is a question blocked or enriched?

Set a pre-hook URL. Docsbook POSTs the reader's question to it as JSON and waits, then acts on two optional fields of your reply.

What Docsbook sends:

```json
{
  "question": "What's the price for team@acme.com?",
  "session_id": "sess_YOUR_SESSION_ID",
  "workspace_id": 42
}
```

What Docsbook understands back:

```json
{
  "block": true,
  "reason": "Ask your account manager for account-specific pricing",
  "inject_context": "The reader is on the Acme account, locale en-GB."
}
```

- **`block: true`** stops the request. No model is called and no tokens are spent. The stream carries an error of `blocked_by_hook` with your `reason` — but see the limit below on what the reader actually sees.
- **`inject_context`** is added to the prompt as an extra system message for this one question, after your own system prompt and before the question itself. This is where live facts belong: the reader's plan, their region, a feature flag.
- **Anything else** — a non-2xx status, unparseable JSON, an empty body, or no reply within the timeout — and the chat continues exactly as if no hook were set. A broken hook degrades the chat; it does not break it.

All three hooks share a **5-second timeout**, enforced by aborting the request. The pre-hook's timeout costs the reader those seconds once; the other two cost them nothing, because the answer has already streamed.

## What the post-hook receives

One POST, after the reader has already seen the answer:

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

`tool_calls` is one entry per page the server actually fetched for this question, in the order it read them — the same list the reader saw as `Reading <page>` lines. It is a record of retrieval, not of the model's own tool use.

The streaming hook receives `event: "message"`, `question`, `answer`, `refs` (the citations that survived filtering), `workspace_id`, `session_id` and `latency_ms`. It does **not** carry `tool_calls`; the post-hook is the one that does.

## Which hook for which job

| Scenario | Hook | Why that one |
|---|---|---|
| Refuse questions about another customer's account | Pre-hook | Only the pre-hook can stop the request |
| Give the model the reader's plan and locale | Pre-hook (`inject_context`) | The model needs it before it answers |
| Mirror every exchange into your own analytics store | Post-hook | Needs the finished answer, changes nothing |
| Alert a channel when an answer takes too long | Streaming or post-hook | Both carry `latency_ms` |
| A/B two prompt phrasings | Pre-hook | Mutates the prompt, one question at a time |
| Guarantee a string never reaches a reader | Pre-hook or the system prompt | The post-hook runs after the reader has it |

## Are chat hooks signed?

**No.** Docsbook sends a plain `POST` with `Content-Type: application/json` and no HMAC header, so your endpoint must not treat the payload as proof of origin. Keep the URL secret, put a token in its path or query string, restrict it to Docsbook's egress, and treat the body as untrusted input.

Docsbook [webhooks](../reference/webhooks.md) are a different mechanism and *are* signed: HMAC-SHA256 over the raw body in `X-Docsbook-Signature-256`, as `sha256=<hex>`. Do not carry a webhook's verification code over to a chat hook and assume it verifies anything — it will pass on a body anyone could have sent.

## Managing hooks from an MCP client

Three tools configure hooks from Claude Code, Cursor or any MCP client:

```bash
set_chat_hooks          # register pre / post / streaming hook URLs
test_chat_hook          # send a test ping to one hook and report its status
get_chat_system_prompt  # inspect the current system prompt
```

Pass an empty string to `set_chat_hooks` to clear an individual hook. `test_chat_hook` posts `{ test: true, hook_type, workspace_id, timestamp, message }` and reports the status code and round-trip time, using the same 5-second timeout the live path uses. The same fields are editable in the admin panel.

## Why this is the right way (evidence)

| Rule | Why it works | Source |
|---|---|---|
| Inject live facts through the pre-hook rather than letting the model recall them | Retrieval-augmented generation produces "more specific, diverse and factual language than a state-of-the-art parametric-only" baseline — a fact placed in the prompt is grounded; a fact recalled is not | Lewis et al., 2020 — [RAG](https://arxiv.org/abs/2005.11401) |
| Block at the pre-hook, not by post-processing | Instruction alone does not reliably stop a model answering: ordinary tuning "force[s] the model to complete a sentence no matter whether the model knows the knowledge or not". A refusal you can guarantee is one that never reaches the model | Zhang et al., 2023 — [R-Tuning](https://arxiv.org/abs/2311.09677) |
| Treat an unsigned hook payload as untrusted | A signature is what proves origin: "to ensure that your server only processes webhook deliveries that were sent by GitHub and to ensure that the delivery was not tampered with, you should validate the webhook signature". Chat hooks carry none, so authenticate them yourself | GitHub — [Validating webhook deliveries](https://docs.github.com/en/webhooks/using-webhooks/validating-webhook-deliveries) |
| Compare Docsbook's webhook signature in constant time | "Never use a plain `==` operator. Instead consider using a method like `secure_compare` or `crypto.timingSafeEqual`" | GitHub — [Validating webhook deliveries](https://docs.github.com/en/webhooks/using-webhooks/validating-webhook-deliveries) |

## Limits

- **The reader does not see your block reason.** The `reason` string is delivered in the response stream, but the shipped docs-site widget replaces it with its generic "Something went wrong. Please try again." Under question: the value is on the wire and a custom front-end can read it, but the widget you get out of the box does not display it. Treat `reason` as a value for your logs, and put anything the reader must read into your system prompt instead.
- **Hooks do not run on the anonymous preview path.** A repository previewed before it has a project row answers questions without a workspace, and the pre-hook is skipped along with every other per-project branch.
- **No retries and no delivery log.** Post and streaming hooks are dispatched once and their outcome is not recorded. If you need at-least-once delivery with retries and a visible delivery history, use [webhooks](../reference/webhooks.md), which have both.
- **No signature, and no plan to add one before webhooks' scheme is reused.** See above.
- **`set_chat_hooks` and `test_chat_hook` still describe themselves as requiring Pro.** The capability they check is open on every plan, so the tool descriptions are stale rather than the behaviour. Under question until those strings are corrected.
- **A slow pre-hook is paid for by the reader.** Five seconds is the ceiling, and it lands before the first token. Keep the endpoint fast, or return nothing and let the chat continue.

## Related

- [AI chat](./chat.md) — the contract the hooks plug into.
- [Answer quality](./answer-quality.md) — where in the pipeline each hook sits.
- [Sources](./sources.md) — the other way to give the assistant facts it does not have.
- [Webhooks](../reference/webhooks.md) — signed, retried, event-driven deliveries.
- [MCP server](../agent-ready/mcp.md) — configure hooks remotely from your editor.
