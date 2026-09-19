---
title: "Create event feed"
description: "SAVE A FILTER OVER THIS PROJECT'S EVENT LOG, so a job can be armed on a CLASS of log lines rather than on one event name — 'anything a reader did', 'every failed delivery',…"
---

# Create event feed

<!-- widget:mcp access=write price-millicents=2000 -->

## create_event_feed

SAVE A FILTER OVER THIS PROJECT'S EVENT LOG, so a job can be armed on a CLASS of log lines rather than on one event name — 'anything a reader did', 'every failed delivery', 'every chat question with no answer'. Returns a `feed_id` to pass as trigger {kind:'feed', list_id:…}. The feed is stored on the server and shows up in the owner's Logs tab strip like one they saved themselves. 🔴 An EMPTY `events` list means EVERY event, not none — say the names unless you mean everything.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `name` | string | yes | What the owner will see in their Logs tabs. |
| `events` | string[] | yes | Event names from `list_agent_jobs`.available_events. An empty array means every event. |

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
    "name": "create_event_feed",
    "arguments": {
      "name": "<name>",
      "events": []
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"create_event_feed","arguments":{"name":"<name>","events":[]}}}'
```

<!-- /widget -->
