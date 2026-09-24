---
title: "Create goal"
description: "Define a goal — one thing you want a reader to do."
---

# Create goal

<!-- widget:api -->

## POST /api/v1/create_goal

Define a goal — one thing you want a reader to do. Matched RETROACTIVELY against the history already recorded, so the numbers appear immediately rather than starting from today. Refused when it cannot ever fire (an event these docs do not emit) or when the value is 0 — a goal that never fires looks EXACTLY like a goal with 100% drop-off, and $0 reads as a measurement instead of an absent declaration. Warnings come back in `issues` and are worth relaying to the owner verbatim. Set `value_usd` only if you can defend the number; leaving it empty keeps money figures switched off rather than showing an invented one.

**Price** — $0.00001 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/create_goal`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `key` | string | no | Machine name, e.g. 'reached_pricing'. Lowercase and underscores; it is the handle funnels and these tools refer to the goal by. Never put a path, id or email in it. |
| `kind` | string | no | page = a pageview of a path. event = one of the events the docs emit (see get_analytics event names). section = a heading/anchor came into view — THIS is how a 'scrolled as far as pricing' goal works, and it needs no new tracking. outbound = a click leaving for a host (matched by host, so query strings do not matter). One of: `page`, `event`, `section`, `outbound`. |
| `match` | string | no | What to match: a path for 'page', an event name for 'event', a heading anchor for 'section' (with or without the '#'), a host for 'outbound'. |
| `match_path` | string | no | Optional scope — only count the goal on this page. Lets one event be two goals ('copied the quickstart snippet' vs 'copied the auth snippet'). |
| `label` | string | no | Human label for the dashboard. Defaults to the key. |
| `value_usd` | number | no | What ONE completion is worth, in dollars. Omit unless defensible. |

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/create_goal' \
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
