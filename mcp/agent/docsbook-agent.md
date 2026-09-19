---
title: "Docsbook agent"
description: "THE DOCSBOOK AGENT — a general-purpose worker you delegate to."
---

# Docsbook agent

<!-- widget:mcp access=write price-millicents=800 -->

## docsbook_agent

THE DOCSBOOK AGENT — a general-purpose worker you delegate to. Say what you want in your own words, in any language, and it does the job on the project end to end: reads the repository and the existing pages, works out what should change, writes and restructures the documentation, configures the site, translates, and measures the effect. It knows Docsbook itself — the product's own documentation is part of what it works from — so it does not need to be told how the platform works or what good documentation looks like. DELEGATE THE GOAL, NOT THE STEPS: 'document the new API', 'our quickstart loses people on step 3', 'nobody finds us in AI answers', 'make the pricing page match the product', 'переведи доки на английский', or just a question about the docs you want answered properly. It decides the steps; a caller's guess at them is the one input in the whole run that nobody chose. A REQUEST IS ENOUGH — `workspace_id` is optional. With one project on the account it uses that one; name a project in the request and it resolves it; only a genuinely ambiguous account is asked back, with candidates. SAFE TO HAND WORK TO: every page change is an ordinary git commit in the project's own repository, so it is reviewable and revertible like any other; written pages land at `generated`/`review` status and this path can never mark anything `approved` — sign-off stays a separate, deliberate human act; it asks you rather than guessing when a decision is yours; and `docsbook_agent_stop` ends it at any point. It returns immediately with a `task_id` and then works for minutes, not seconds: poll `docsbook_agent_status`, answer with `docsbook_agent_reply` when it asks, `docsbook_agent_stop` to stop it. One job per intention: two running at once on one project will both be right about the pages and can still disagree about the order they land in.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Which project — OPTIONAL. Omit it and the agent works out which project you mean: the account's only one, or the one your request names. Pass it to be certain, or when the account has several and the request does not say. Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `request` | string | yes | What you want, in the user's own words, in any language. Say the GOAL and the evidence for it ('support keeps asking how to rotate keys'), not a list of steps — the agent decides the steps. Naming the project here also lets workspace_id be omitted. |
| `label` | string | no | Short name for this job in the list, e.g. 'API reference pass'. |

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
    "name": "docsbook_agent",
    "arguments": {
      "request": "<request>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"docsbook_agent","arguments":{"request":"<request>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

<!-- widget:api -->

### POST /api/v1/tools/docsbook_agent

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/docsbook_agent' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"request":"<request>"}}'
```

<!-- /widget -->
