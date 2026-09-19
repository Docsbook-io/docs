---
title: "Delete agent job"
description: "FORGET A JOB'S ARMING."
---

# Delete agent job

<!-- widget:mcp access=write price-millicents=2000 -->

## delete_agent_job

FORGET A JOB'S ARMING. For an agent you created, the card goes away entirely. For one of the project's built-in jobs, only the arming is removed — the card stays on the owner's grid, switched off, which is what 'this project does not do that' looks like there. Prefer `configure_agent_job` with armed:false when the owner may want it back: pausing keeps the goal they wrote.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `job_id` | string | yes | — |

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
    "name": "delete_agent_job",
    "arguments": {
      "job_id": "<job_id>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"delete_agent_job","arguments":{"job_id":"<job_id>"}}}'
```

<!-- /widget -->
