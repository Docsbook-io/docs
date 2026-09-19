---
title: "Configure agent job"
description: "TURN AN AGENT JOB ON OR OFF, OR CHANGE WHAT IT DOES — works on the project's built-in jobs (code sync, gaps, fix, translate, styleguide…) and on ones you created."
---

# Configure agent job

<!-- widget:mcp access=write price-millicents=800 -->

## configure_agent_job

TURN AN AGENT JOB ON OR OFF, OR CHANGE WHAT IT DOES — works on the project's built-in jobs (code sync, gaps, fix, translate, styleguide…) and on ones you created. Pass only what you are changing; anything omitted is left exactly as it is. Use this to arm a job the owner asked for ('watch our docs for dead links every morning'), to point an existing job's report at a new channel, or to add a standing instruction to one. `job_id` comes from `list_agent_jobs`. Safe and reversible: it writes an arming, it never runs anything.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `job_id` | string | yes | From `list_agent_jobs`.jobs[].job_id. |
| `armed` | boolean | no | On or paused. |
| `trigger` | object | no | Replaces what wakes it. Omitted leaves the arming alone. |
| `goal` | string | no | Replaces the instruction it runs on. For a built-in job this is the catalog's own text, which the owner may have edited — read it first rather than overwriting a paragraph you have not seen. |
| `custom_prompt` | string | no | The owner's standing extra instruction, appended to the goal at call time. Pass an empty string to clear it. This is the field to use when ADDING to a built-in job rather than rewriting its goal. |
| `report_to` | integer[] | no | Replaces the destination list. Pass [] to stop it reporting anywhere. |
| `name` | string | no | Rename — agents you created only. |
| `description` | string | no | Re-describe — agents you created only. |
| `icon` | string | no | Re-mark — agents you created only. |

<!-- /widget -->

## `trigger` fields

| Field | Type | Required | Description |
|---|---|---|---|
| `kind` | string | yes | One of: `schedule`, `event`, `feed`, `manual`. |
| `cron` | string | no | Five-field cron, UTC. For kind 'schedule'. Example: '0 9 * * 1'. |
| `event` | string | no | Event name, underscore form. For kind 'event'. See `list_agent_jobs`. |
| `list_id` | integer | no | A saved feed's id. For kind 'feed'. |

## Call it

<!-- widget:code-group -->

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "configure_agent_job",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"configure_agent_job","arguments":{"job_id":"<job_id>"}}}'
```

<!-- /widget -->
