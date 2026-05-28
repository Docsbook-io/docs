# Webhooks — event and architecture reference

Docsbook dispatches workspace events to registered HTTPS endpoints. Delivery uses HMAC signatures, exponential retry, and history stored in the database.

## Events

| Event | When it fires | Where `dispatchEvent` is called |
|---|---|---|
| `content.indexed` | After repository reindexing | `api/workspaces`, `api/mcp/workspaces/[id]/reindex` |
| `content.outdated` | Cron finds pages not updated for > N days | `api/cron/stale-check` |
| `translation.completed` | After auto-translation | `api/translate` |
| `translation.outdated` | Source hash changed, translation is stale | `api/translate` (upsertTranslationDraft) |
| `translation.needed` | A new language was enabled — translations are needed | (on user request) |
| `chat.question_asked` | After any AI chat response | `api/ai-chat` |
| `chat.no_answer` | AI responded with "I don't know" / empty response | `api/ai-chat` |
| `chat.negative_feedback` | User gave 👎 to an AI response | `api/analytics/feedback` |
| `feedback.received` | Any feedback (👍/👎/comment) | `api/analytics/feedback` |
| `search.no_results` | Search returned an empty result | `api/search-index/[user]/[repo]` |
| `search.popular` | A query exceeded the popularity threshold | (cron) |
| `plan.upgraded` | Subscription activated / upgraded | `utils/paddle/handleWebhook` |
| `plan.downgraded` | Subscription cancelled / past_due | `utils/paddle/handleWebhook` |
| `usage.limit_approaching` | ≥80% of monthly limit reached (AI / translation / reindex) | `api/ai-chat` |
| `traffic.spike` / `traffic.drop` | Sudden traffic change (via Axiom) | (cron, optional) |
| `mcp.tool_called` | Any MCP tool call | `api/mcp/server` |

## Architecture

- **Wrapper:** `src/lib/dispatch-event.ts` — type-safe `dispatchEvent(workspaceId, eventType, payload)` with Zod schemas for each event. Fire-and-forget: `void dispatchEvent(...).catch(logDispatchError)`.
- **Dispatcher:** `src/lib/webhook-dispatcher.ts` — puts the delivery in the queue, computes HMAC, retries.
- **Worker / cron:** delivery with exponential backoff.
- **Schema version:** all payloads contain `schema_version: 1`.
- **Full Zod schemas and payload examples:** `docs/webhooks.md`.

## Registration (MCP)

```typescript
register_webhook_chat_negative_feedback({
  workspace_id: 42,
  url: "https://your-handler.com/docsbook",
  secret: "whsec_..."   // HMAC secret for signature verification
})
```

Signature in the header `X-Docsbook-Signature: t=<ts>,v1=<hex>` — standard Stripe-style HMAC SHA256.
