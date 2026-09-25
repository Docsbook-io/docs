---
title: "Register webhook usage overage limit reached"
description: "Register a webhook for the 'usage_overage_limit_reached' event (BUSINESS) — the direct call for 'notify us when…', 'alert me if…', 'ping our channel when…' about this event."
---

# Register webhook usage overage limit reached

<!-- widget:api -->

## POST /api/v1/register_webhook_usage_overage_limit_reached

Register a webhook for the 'usage_overage_limit_reached' event (BUSINESS) — the direct call for 'notify us when…', 'alert me if…', 'ping our channel when…' about this event. Fires when a workspace's monthly overage spend cap is reached. Overage is switched off in favour of opt-in auto-recharge, so this event does not fire today. Delivery is an asynchronous HTTP POST. A Slack (hooks.slack.com) or Discord (discord.com/api/webhooks) incoming-webhook URL is recognised by its host and the message shaped for that platform — paste it as-is; any other URL receives the signed JSON envelope (HMAC-SHA256 in X-Docsbook-Signature-256, event type in X-Docsbook-Event). Below the BUSINESS plan the call returns PLAN_RESTRICTION naming the tier — no pre-check needed.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/register_webhook_usage_overage_limit_reached`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `url` | string | no | HTTPS endpoint to receive POST callbacks |
| `secret` | string | no | Optional shared secret (>=16 chars). One is generated if omitted. |
| `auth_header` | string | no | Optional Authorization header value sent verbatim on delivery, e.g. 'Bearer sk-…' for endpoints that require auth (Claude Code routine fire URLs). |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | — |
| `webhook_id` | number | — |
| `workspace_id` | number | — |
| `event_type` | string | — |
| `url` | string | — |
| `channel` | string | slack \| claude \| api — read off the URL's host. |
| `secret` | string | The HMAC signing secret — generated if one was not given. |
| `enabled` | boolean | — |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/register_webhook_usage_overage_limit_reached' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

### Response

```json
{
  "ok": true,
  "result": {
    "ok": true,
    "webhook_id": 0,
    "workspace_id": 0,
    "event_type": "<event_type>",
    "url": "<url>",
    "channel": "<channel>",
    "secret": "<secret>",
    "enabled": true
  },
  "duration_ms": 0
}
```

### Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |

<!-- /widget -->
