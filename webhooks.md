---
title: "Webhook Events Reference"
description: "Subscribe to Docsbook workspace events — content indexed, translations, AI chat, feedback, plan changes — with HMAC-signed retries and typed payloads."
---

# Webhooks

Docsbook can notify your systems about events that happen inside a workspace —
new content indexed, translations needed, chat questions asked, traffic anomalies
and more. Each webhook is **typed**: you subscribe to one specific event, and
Docsbook only POSTs to your URL when that exact event fires.

## How it works

1. You register a webhook with `event_type`, `url`, and an optional `secret`.
2. When the event occurs, Docsbook enqueues a delivery (outbox pattern).
3. The worker (Vercel cron, every minute) POSTs the JSON body to your URL.
4. We retry **up to 3 attempts** with exponential backoff (1s, 10s, 60s).

### Request format

```
POST https://your-url.example.com
Content-Type: application/json
User-Agent: Docsbook-Webhooks/1.0
X-Docsbook-Event: content.indexed
X-Docsbook-Signature-256: sha256=<hex hmac of body>
X-Docsbook-Delivery: 12345
X-Docsbook-Attempt: 1
```

```json
{
  "event": "content.indexed",
  "workspace_id": 42,
  "occurred_at": "2026-05-23T12:34:56.000Z",
  "data": { /* event-specific payload */ }
}
```

### Verifying signatures

```ts
import crypto from "node:crypto"
const expected = "sha256=" + crypto.createHmac("sha256", SECRET).update(rawBody).digest("hex")
if (expected !== req.headers["x-docsbook-signature-256"]) reject()
```

A 2xx response = delivered. Anything else triggers retry until the attempt budget is exhausted.

## Event catalog

| Event | Min plan | Payload fields |
|---|---|---|
| `content.indexed` | PRO | `pages_count`, `relations_count`, `indexed_at` |
| `content.outdated` | PRO | `last_indexed_at`, `repo_head_sha` |
| `translation.needed` | PRO | `source_path`, `language` |
| `translation.completed` | PRO | `source_path`, `language`, `origin` |
| `translation.outdated` | PRO | `source_path`, `language`, `source_hash_changed` |
| `chat.question_asked` | PRO | `question`, `answered`, `chat_id` |
| `chat.no_answer` | PRO | `question`, `chat_id` |
| `chat.negative_feedback` | PRO | `chat_id`, `question`, `answer` |
| `search.no_results` | PRO | `query` |
| `search.popular` | PRO | `query`, `count_24h` |
| `traffic.spike` | PRO+ | `path`, `views`, `baseline` |
| `traffic.drop` | PRO+ | `path`, `views`, `baseline` |
| `feedback.received` | PRO | `path`, `rating`, `comment` |
| `plan.upgraded` | Free | `from`, `to` |
| `plan.downgraded` | Free | `from`, `to` |
| `usage.limit_approaching` | PRO | `metric` (`ai`\|`translation`), `used`, `limit` |
| `mcp.tool_called` | PRO+ | `tool_name`, `args` |

## Registering a webhook

### Via REST

```bash
curl -X POST https://docsbook.io/api/webhooks \
  -H "Content-Type: application/json" \
  -d '{"workspace_id": 42, "event_type": "content.indexed", "url": "https://you.example.com/hook"}'
```

The response includes the `secret` exactly once — store it.

### Via MCP

Each event has a dedicated MCP tool, so an AI agent can subscribe to a specific
notification stream without picking strings:

```
register_webhook_content_indexed(workspace_id: 42, url: "https://...")
register_webhook_translation_needed(repo: "owner/repo", url: "https://...")
register_webhook_traffic_spike(workspace_id: 42, url: "https://...")
```

Other MCP tools:

- `list_webhooks(workspace_id)` — Free
- `unregister_webhook(webhook_id)` — Free
- `test_webhook(webhook_id)` — Free (enqueues a synthetic ping)
- `list_webhook_deliveries(webhook_id)` — PRO
- `replay_webhook_delivery(delivery_id)` — PRO

### REST endpoints

- `GET  /api/webhooks?workspace_id=X` — list
- `POST /api/webhooks` — create
- `DELETE /api/webhooks/:id` — delete
- `POST /api/webhooks/:id/test` — test ping
- `GET  /api/webhooks/:id/deliveries` — recent deliveries
- `POST /api/webhook-deliveries/:id/replay` — re-enqueue an existing delivery

## Retry & failure semantics

- Worker runs every minute via Vercel cron.
- A delivery is attempted up to 3 times.
- Backoff is enforced from `created_at` of the row: 1s, 10s, 60s.
- After the 3rd failure → `status = "failed"`. Use `replay_webhook_delivery` to re-attempt.
- Response code and (truncated) body are stored on every delivery row.
