---
title: "Register webhook search popular"
description: "Register a webhook for the 'search_popular' event (BUSINESS) — the direct call for 'notify us when…', 'alert me if…', 'ping our channel when…' about this event."
---

# Register webhook search popular

<!-- widget:mcp access=write price-millicents=2000 -->

## register_webhook_search_popular

Register a webhook for the 'search_popular' event (BUSINESS) — the direct call for 'notify us when…', 'alert me if…', 'ping our channel when…' about this event. Fires when a search query crosses a popularity threshold. Delivery is an asynchronous HTTP POST. A Discord (discord.com) or Slack (hooks.slack.com) incoming-webhook URL is recognised by its host and the message shaped for that platform — paste it as-is; any other URL receives the signed JSON envelope (HMAC-SHA256 in X-Docsbook-Signature-256, event type in X-Docsbook-Event). Below the BUSINESS plan the call returns PLAN_RESTRICTION naming the tier — no pre-check needed.

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
    "name": "register_webhook_search_popular",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"register_webhook_search_popular","arguments":{"url":"<url>"}}}'
```

<!-- /widget -->
