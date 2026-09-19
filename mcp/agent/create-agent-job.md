---
title: "Create agent job"
description: "CREATE A NEW AGENT OF YOUR OWN on this project — a named, described card in the owner's Agent panel with ITS OWN PROMPT, its own trigger, and its own report destinations."
---

# Create agent job

<!-- widget:mcp access=write price-millicents=2000 -->

## create_agent_job

CREATE A NEW AGENT OF YOUR OWN on this project — a named, described card in the owner's Agent panel with ITS OWN PROMPT, its own trigger, and its own report destinations. This is how a request like 'run a drift check on every push and post the changelog to Discord' becomes something the project does by itself. The `prompt` is the whole of what it does, so write it as a GOAL with what to measure and what a good result looks like — it is handed to a fresh documentation agent that has no memory of this conversation, so anything it needs to know (which channel, which tone, which repository) must be IN it. Safe: this stores an arming, it does not run anything, and the owner can see, edit, pause or delete the card in their panel the moment it exists. Returns the `job_id` to configure it with later.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `name` | string | yes | The card's heading. Two or three words read best. |
| `prompt` | string | yes | What this agent is told to do, every time it runs. State the goal, what to measure and what a good result looks like — never a list of steps; the agent chooses those. If the job is to notify somebody, say WHERE and in what shape, because a later run has only this text. |
| `description` | string | no | One line on the card about what the OWNER gets from it. Not what it runs. |
| `icon` | string | no | The card's mark. One of the names in `list_agent_jobs`.available_icons; defaults to Bot. |
| `trigger` | object | no | What wakes it. Omit for 'manual' — a card the owner runs by hand. |
| `report_to` | integer[] | no | Destination ids from `list_agent_jobs`.destinations. The finished run's report is delivered to each, through the same queue and per-channel formatting as every other alert. |
| `armed` | boolean | no | Start it on (default true). False stores it paused. |

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
    "name": "create_agent_job",
    "arguments": {
      "name": "<name>",
      "prompt": "<prompt>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"create_agent_job","arguments":{"name":"<name>","prompt":"<prompt>"}}}'
```

<!-- /widget -->
