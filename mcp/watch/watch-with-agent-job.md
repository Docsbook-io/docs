---
title: "Watch with agent job"
description: "WAKE A JOB FROM A CONNECTED APP — 'when commits land on main', 'when a pull request merges', 'when a support ticket is solved'."
---

# Watch with agent job

<!-- widget:mcp access=read price-millicents=800 -->

## watch_with_agent_job

WAKE A JOB FROM A CONNECTED APP — 'when commits land on main', 'when a pull request merges', 'when a support ticket is solved'. This is the arming behind 'do X when I push'. Pass the `job_id` of the agent that should run (create one first with `create_agent_job` if the owner asked for something specific) and the `occasion_id` from `list_agent_jobs`.integrations. 🔴 An occasion whose runner this deployment does not have is REFUSED rather than stored: an arming that can never fire is indistinguishable from a quiet week, and the owner would find out months later.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `job_id` | string | yes | Which agent runs when it happens. |
| `occasion_id` | string | yes | From `list_agent_jobs`.integrations[].occasions[].occasion_id. |
| `account_id` | integer | no | Which attached account to watch, when the project has more than one. Omitted watches any. |
| `settings` | object | no | The occasion's own answers — a branch name, a channel. Required ones are named in `list_agent_jobs`. |

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
    "name": "watch_with_agent_job",
    "arguments": {
      "job_id": "<job_id>",
      "occasion_id": "<occasion_id>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"watch_with_agent_job","arguments":{"job_id":"<job_id>","occasion_id":"<occasion_id>"}}}'
```

<!-- /widget -->
