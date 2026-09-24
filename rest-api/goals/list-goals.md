---
title: "List goals"
description: "The goals and funnels defined for this workspace, with what each one MATCHES."
---

# List goals

<!-- widget:api -->

## GET /api/v1/list_goals

The goals and funnels defined for this workspace, with what each one MATCHES. A goal is a named thing you want a reader to do; a funnel is an ordered list of goals. Call this before creating anything — a goal whose name already exists is refused, and a funnel step refers to a goal by name. Free on every plan: defining measurement is not the paid part. 🔴 AN EMPTY LIST IS NOT A MISSING GOAL. Every project has the standing goal — be found, on Google and in AI answers (`standing_goal` here, `be_found` as a `goal_key`) — without declaring anything; these are the owner's EXTRAS, reader actions on the site. Never ask the owner to declare a goal, and never create a page-view goal to stand in for being found: decompose the standing goal instead (list_opportunities, add_direction).

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/list_goals`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |

### Request

```bash
curl -X GET 'https://docsbook.io/api/v1/list_goals' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY'
```

<!-- /widget -->

## Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |
