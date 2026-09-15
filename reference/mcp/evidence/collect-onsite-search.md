---
title: "Collect onsite search"
description: "What readers typed into YOUR search box, in three tables that must never be merged: what they looked for, what returned nothing, and what returned results and got no click."
---

# Collect onsite search

<!-- widget:mcp access=read -->

## collect_onsite_search

What readers typed into YOUR search box, in three tables that must never be merged: what they looked for, what returned nothing, and what returned results and got no click. Those three are different failures with different fixes and wildly different prices. Zero results is a missing page or a missing synonym; shown-and-rejected is a title losing an argument against its own siblings, an order of magnitude cheaper to fix and invisible in every zero-result report. Merged into 'search is bad', they send the owner to rewrite bodies when the fix was a heading. The cheapest source of your readers' own vocabulary that exists: every row is somebody who was already on the site, wanted something, and told you what they call it. Returns an evidence record and the `get_popular_searches` / `get_failed_searches` / `get_search_zero_click` calls behind every row, with the zero-result SHARE computed only when both its numerator and its denominator were actually read. Use it for 'what are people searching for', 'what returns no results', 'which searches get no click', «что ищут на сайте», «какие запросы ничего не находят», «ищут и не кликают». Deciding which of those is a renaming and which is a missing page is the judgement, and the two cost an order of magnitude apart: ask `docsbook_expert` before you act on any of these rows. Returns a validated `collect_onsite_search.v1` payload: an `evidence` map, the normalised `rows` behind it, and a `reproduce` block naming the exact MCP calls and arguments that produced every row — run them yourself and you get the same answer. There is no model in the path, so there are no findings, no scores and nothing to disbelieve; interpretation is what the audits charge for. Changes nothing; safe on a read-only token. Evidence, not a verdict — nothing here says what the gap MEANS. If you have not already asked `docsbook_expert` how to read it, ask: it says what this evidence is worth against, and what to do with it. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `window_days` | integer | no | Days of history to read (default 28). One window is used for every signal in the run and stated in the payload — mixing windows silently invents trends. |

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
    "name": "collect_onsite_search",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"collect_onsite_search","arguments":{}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/collect_onsite_search

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/collect_onsite_search' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{}}'
```

<!-- /widget -->
