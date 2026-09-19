---
title: "List agent jobs"
description: "THE WHOLE AGENT SECTION OF A PROJECT, IN ONE ANSWER — every job the agent does without being asked (armed or not), every SAVED FEED the event log can be filtered by, every…"
---

# List agent jobs

<!-- widget:mcp access=read price-millicents=800 -->

## list_agent_jobs

THE WHOLE AGENT SECTION OF A PROJECT, IN ONE ANSWER — every job the agent does without being asked (armed or not), every SAVED FEED the event log can be filtered by, every destination a result can be sent to, and every connected app with the occasions it could wake a job on. Call this FIRST for any request about automating, scheduling, watching, notifying, alerting or 'do X when Y happens'. Every id it returns — `job_id`, `feed_id`, `destination_id`, `occasion_id`, `account_id` — is an id the write tools take, so nothing downstream has to be guessed. Reads only; changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |

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
    "name": "list_agent_jobs",
    "arguments": {}
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_agent_jobs","arguments":{}}}'
```

<!-- /widget -->
