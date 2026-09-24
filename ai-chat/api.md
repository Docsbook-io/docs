---
title: "Docs chat API and chat hooks"
description: "Ask your documentation from your own backend with POST /api/v1/chat, and run your own HTTPS endpoints before and after every AI chat answer with chat hooks."
---

# Docs chat API and chat hooks

Ask your documentation from your own code with `POST /api/v1/chat` — the same [AI chat](./README.md) your readers use — and put your own HTTPS endpoints in front of and behind every answer with chat hooks.

## Authenticate with the project API key

Every call sends the project's API key as a bearer token.

1. Open **Settings ▸ Domain & API** and find the **API Key** card.
2. Copy the key. It starts with `dbk_`.
3. Send it on each request as `Authorization: Bearer dbk_…`.

**Reset key** on the same card issues a new key and revokes the old one at once.

<!-- widget:callout type=warning -->

Keep the key on your server. It can change your project's settings and spend your balance, so it must never ship in a browser bundle or a mobile app.

<!-- /widget -->

## Ask a question

One call returns one finished answer as JSON; the endpoint does not stream.

<!-- widget:api -->

## POST /api/v1/chat

Ask the project's documentation a question and get back the answer, its sources and three follow-up questions — the same retrieval and model call as the chat on your site.

| Field | Type | Required | Description |
|---|---|---|---|
| `question` | string | yes | What to ask the documentation. |
| `lang` | string | no | Answer in this language. Defaults to the project's default language. |
| `sessionId` | string | no | Groups several calls under one conversation id. Each call is still answered on its own. |
| `mentionedPages` | string[] | no | Page paths to read regardless of what search finds. |
| `currentPath` | string | no | The page the reader is on. That page is left out of what the answer reads, so omit it when it may hold the answer. |

### Response

```json
{
  "answer": "Rotate a key from the API keys page … [ref:guides/api-keys|API keys||Rotate a key]",
  "refs": [
    {
      "pagePath": "guides/api-keys",
      "pageTitle": "API keys",
      "headingText": "Rotate a key",
      "headingId": "rotate-a-key"
    }
  ],
  "follow_up_questions": [
    "Do old keys stop working right away?",
    "Can I have two keys at once?",
    "Where do I see when a key was created?"
  ]
}
```

### Errors

| Status | `error` | Meaning |
|---|---|---|
| `400` | `Missing question` | `question` is empty. |
| `401` | `Missing Bearer token`, `Invalid API key` | No key, or a key that belongs to no project. |
| `403` | `plan_restricted` | The project is on Free; the chat is part of Pro. |
| `429` | `token_limit_reached`, `ai_reserve_reached`, `source_limit_reached`, `daily_limit_reached` | The balance, or a spend limit, can't cover the answer. |
| `502` | `blocked_by_hook`, `model_call_failed`, `answer_not_parseable` | No answer was produced; `reason` says why. |

<!-- /widget -->

`answer` is markdown. With **Semantic Search** on, it carries an inline `[ref:…]` marker after each cited sentence and `refs` lists those pages, `headingId` being the anchor on the rendered page. With it off, `refs` comes back empty.

## Call it from your server

<!-- widget:code-group -->

### curl

```bash
curl -X POST https://docsbook.io/api/v1/chat \
  -H "Authorization: Bearer $DOCSBOOK_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"question": "How do I rotate an API key?"}'
```

### JavaScript

```javascript
const res = await fetch("https://docsbook.io/api/v1/chat", {
  method: "POST",
  headers: {
    Authorization: `Bearer ${process.env.DOCSBOOK_API_KEY}`,
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ question: "How do I rotate an API key?" }),
})
const { answer, refs, follow_up_questions } = await res.json()
```

<!-- /widget -->

An API call is billed like a reader's question.

- **Balance** — it draws on your balance by the tokens it used, at the price shown on **AI Visitors Chat Model**; there is no separate API quota.
- **Your own key** — answers made with **Your own AI API Key** are billed by your provider.
- **Events** — each call fires `chat_question_asked`, plus `chat_no_answer` when the chat didn't know, so [alerts](../analytics/alerts.md) and trigger cards see API questions too.

## Chat hooks: your code around every answer

Chat hooks are three HTTPS URLs of yours that Docsbook calls around every answer — on your site, over this API and through `ask_project_docs`.

| Hook | When Docsbook calls it | What it sends | Can it change the answer? |
|---|---|---|---|
| Pre-hook | First, before search and the model; waits up to 5 seconds | `question`, `session_id`, `workspace_id` | Yes — block the question or add context |
| Post-hook | After the answer; does not wait | `question`, `answer`, `tool_calls`, `latency_ms`, `workspace_id`, `session_id` | No |
| Streaming hook | With the post-hook; does not wait | `event` (`message`), `question`, `answer`, `refs`, `workspace_id`, `session_id`, `latency_ms` | No |

`tool_calls` lists the pages the answer read, one `{ "tool": "read_page", "path": … }` each. Every hook request is a `POST` with a JSON body and a 5-second timeout.

## What the pre-hook can return

The pre-hook can stop a question or add to it. Reply with one of these, or with nothing.

<!-- widget:code-group -->

### Block

```json
{ "block": true, "reason": "Contract pricing comes from your account manager." }
```

### Add context

```json
{ "inject_context": "This reader is on the Enterprise plan, region EU." }
```

<!-- /widget -->

- **`block: true`** — stops before search and the model, so nothing is billed. The chat on your site shows "Sorry, I could not answer that."; the API returns `502` with `blocked_by_hook` and your `reason`.
- **`inject_context`** — added to the chat's instructions for this one question.
- **Anything else** — a non-2xx status, a body that isn't JSON, or no reply within 5 seconds, and the chat answers as if no hook were set.

## Set and test hooks

Set hooks from your agent with `set_chat_hooks`; there is no form for them in the panel. URLs must be `https://`, and an empty string clears one.

```json
{
  "workspace_id": "acme/docs",
  "pre_url": "https://api.example.com/docsbook/pre?token=YOUR_SECRET",
  "post_url": "https://api.example.com/docsbook/post?token=YOUR_SECRET"
}
```

- **Test** — `test_chat_hook` with `hook_type` set to `pre`, `post` or `streaming` posts `{ "test": true, … }` to that hook and returns its status code, latency and the first 500 characters of its reply.
- **Over REST** — `POST /api/v1/set_chat_hooks` takes the same `pre_url`, `post_url` and `streaming_url` with your API key.
- **Not a hook** — the chat's other URL, the [Call To Action URL](./configure.md#tell-it-where-to-send-readers), is a link the chat offers readers.

<!-- widget:callout type=warning -->

Hook requests carry no signature, unlike [webhooks](../analytics/alerts.md). Put a secret token in the hook URL, check it on every request, and treat the body as untrusted input.

<!-- /widget -->

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [Configure the chat](./configure.md) — Prompt, questions, model and where readers open it {sliders-horizontal}
- [Alerts and webhooks](../analytics/alerts.md) — Signed events for every question, vote and search {bell}
- [REST API reference](../rest-api/README.md) — Every endpoint your API key reaches {braces}
- [MCP tools](../mcp-tools/README.md) — `set_chat_hooks`, `test_chat_hook` and the rest {plug}

<!-- /widget -->
