---
title: "Register webhook traffic drop"
description: "Register a webhook for the 'traffic_drop' event (BUSINESS, advanced event) — the direct call for 'notify us when…', 'alert me if…', 'ping our channel when…' about this event."
---

# Register webhook traffic drop

<!-- widget:api -->

## POST /api/v1/register_webhook_traffic_drop

Register a webhook for the 'traffic_drop' event (BUSINESS, advanced event) — the direct call for 'notify us when…', 'alert me if…', 'ping our channel when…' about this event. Fires when traffic drops sharply vs baseline (advanced event). Delivery is an asynchronous HTTP POST. A Slack (hooks.slack.com) or Discord (discord.com/api/webhooks) incoming-webhook URL is recognised by its host and the message shaped for that platform — paste it as-is; any other URL receives the signed JSON envelope (HMAC-SHA256 in X-Docsbook-Signature-256, event type in X-Docsbook-Event). Below the BUSINESS plan the call returns PLAN_RESTRICTION naming the tier — no pre-check needed.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/register_webhook_traffic_drop`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `url` | string | no | HTTPS endpoint to receive POST callbacks |
| `secret` | string | no | Optional shared secret (>=16 chars). One is generated if omitted. |
| `auth_header` | string | no | Optional Authorization header value sent verbatim on delivery, e.g. 'Bearer sk-…' for endpoints that require auth (Claude Code routine fire URLs). |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/register_webhook_traffic_drop' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
