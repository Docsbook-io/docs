---
title: "Register webhook traffic spike"
description: "Register a webhook for the 'traffic_spike' event (BUSINESS, advanced event) — the direct call for 'notify us when…', 'alert me if…', 'ping our channel when…' about this event."
---

# Register webhook traffic spike

<!-- widget:mcp access=write price-millicents=2000 -->

## register_webhook_traffic_spike

Register a webhook for the 'traffic_spike' event (BUSINESS, advanced event) — the direct call for 'notify us when…', 'alert me if…', 'ping our channel when…' about this event. Fires when traffic exceeds typical baseline (advanced event). Delivery is an asynchronous HTTP POST. A Discord (discord.com) or Slack (hooks.slack.com) incoming-webhook URL is recognised by its host and the message shaped for that platform — paste it as-is; any other URL receives the signed JSON envelope (HMAC-SHA256 in X-Docsbook-Signature-256, event type in X-Docsbook-Event). Below the BUSINESS plan the call returns PLAN_RESTRICTION naming the tier — no pre-check needed. BEFORE ARMING THIS, call `docsbook_expert` with what you are trying to catch: it names what is worth watching and at what threshold. An alert that fires on noise is muted within a week, which is worse than no alert. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `url` | string | yes | HTTPS endpoint to receive POST callbacks |
| `secret` | string | no | Optional shared secret (>=16 chars). One is generated if omitted. |
| `auth_header` | string | no | Optional Authorization header value sent verbatim on delivery, e.g. 'Bearer sk-…' for endpoints that require auth (Claude Code routine fire URLs). |

<!-- /widget -->

## Call it

<!-- widget:code-group -->

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "register_webhook_traffic_spike",
    "arguments": {
      "url": "<url>"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"register_webhook_traffic_spike","arguments":{"url":"<url>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/register_webhook_traffic_spike

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/register_webhook_traffic_spike' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"url":"<url>"}}'
```

<!-- /widget -->
