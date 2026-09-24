---
title: "Docsbook agent"
description: "THE DOCSBOOK AGENT — a general-purpose worker you delegate to."
---

# Docsbook agent

<!-- widget:api -->

## POST /api/v1/docsbook_agent

THE DOCSBOOK AGENT — a general-purpose worker you delegate to. Say what you want in your own words, in any language, and it does the job on the project end to end: reads the repository and the existing pages, works out what should change, writes and restructures the documentation, configures the site, translates, and measures the effect. It knows Docsbook itself — the product's own documentation is part of what it works from — so it does not need to be told how the platform works or what good documentation looks like. DELEGATE THE GOAL, NOT THE STEPS: 'document the new API', 'our quickstart loses people on step 3', 'nobody finds us in AI answers', 'make the pricing page match the product', 'переведи доки на английский', or just a question about the docs you want answered properly. It decides the steps; a caller's guess at them is the one input in the whole run that nobody chose. A REQUEST IS ENOUGH — `workspace_id` is optional. With one project on the account it uses that one; name a project in the request and it resolves it; only a genuinely ambiguous account is asked back, with candidates. It returns immediately with a `task_id` and then works for minutes, not seconds — that is not a reason to sit and wait: call `docsbook_agent_activity` any time to watch it work step by step, live, and `docsbook_agent_reply` to ask it something about the job while it runs, not only when it asks first. `docsbook_agent_status` gives the current state and result, `docsbook_agent_stop` ends it. One job per intention: two running at once on one project will both be right about the pages and can still disagree about the order they land in.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/docsbook_agent`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `request` | string | no | What you want, in the user's own words, in any language. Say the GOAL and the evidence for it ('support keeps asking how to rotate keys'), not a list of steps — the agent decides the steps. Naming the project here also lets workspace_id be omitted. |
| `label` | string | no | Short name for this job in the list, e.g. 'API reference pass'. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | string | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### Limitations

- SAFE TO HAND WORK TO: every page change is an ordinary git commit in the project's own repository, so it is reviewable and revertible like any other; written pages land at `generated`/`review` status and this path can never mark anything `approved` — sign-off stays a separate, deliberate human act; it asks you rather than guessing when a decision is yours; and `docsbook_agent_stop` ends it at any point.

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/docsbook_agent' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

### Response

```json
{
  "ok": true,
  "result": "<result>",
  "duration_ms": 0
}
```

### Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |

<!-- /widget -->
