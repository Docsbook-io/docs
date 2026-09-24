---
title: "Edit goal"
description: "CORRECT a goal that already exists — its label, what one completion is worth, or what it matches — without breaking it."
---

# Edit goal

<!-- widget:api -->

## POST /api/v1/edit_goal

CORRECT a goal that already exists — its label, what one completion is worth, or what it matches — without breaking it. 🔴 Not the same as deleting it and creating it again, which was the only route until 2026-09-12 and silently cost two things every time. A funnel step refers to a goal BY KEY, so archiving the goal breaks every funnel naming it, and a funnel that loses a step reports a BETTER conversion rate than the real one. And `created_at` is when this project started measuring the thing: a re-create resets it, so four months of history reads as a goal created today. The KEY cannot be changed here, deliberately — funnels, MCP callers and the owner's own notes all point at it, and a rename leaves all of them pointing at nothing. A different name is a different goal. Pass only what changes. Warnings come back in `issues` and are worth relaying verbatim.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/edit_goal`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `key` | string | no | The goal's name, from list_goals. Not editable — see the description. |
| `kind` | string | no | page = a pageview of a path. event = one of the events the docs emit (see get_analytics event names). section = a heading/anchor came into view — THIS is how a 'scrolled as far as pricing' goal works, and it needs no new tracking. outbound = a click leaving for a host (matched by host, so query strings do not matter). One of: `page`, `event`, `section`, `outbound`. |
| `match` | string | no | New matcher: a path for 'page', an event name for 'event', an anchor for 'section', a host for 'outbound'. |
| `match_path` | string | no | New scope. Pass an empty string to clear it and count the goal everywhere. |
| `label` | string | no | New human label. |
| `value_usd` | number | no | What ONE completion is worth, in dollars. Pass 0 to clear it — which switches money figures OFF for this goal rather than reporting it as worthless. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/edit_goal' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"kind":"page"}'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
