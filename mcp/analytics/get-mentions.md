---
title: "Get mentions"
description: "Read the mention checks for the docs: for each query the owner watches, whether Google's AI Overview names them (surface 'ai_overview'), and where they sit on Google's or Bing's…"
---

# Get mentions

<!-- widget:mcp access=read price-millicents=800 -->

## get_mentions

Read the mention checks for the docs: for each query the owner watches, whether Google's AI Overview names them (surface 'ai_overview'), and where they sit on Google's or Bing's results page ('google' / 'bing') — plus which OTHER sites on that page name the product. Answers the half Search Console cannot: a query the docs do not rank for returns nothing there, and Bing is not in it at all. 🔴 EVERY QUERY COMES BACK WITH ITS OWN EARLIER READINGS in `history`, newest first — this is the before-and-after on a search position, and the only one this product has. It is what makes a claim about ranking judgeable: take the reading before the change, name it as the hypothesis's `baseline`, and on the check date read the same query here again. A verdict written without looking at `history` is a verdict on one number with nothing behind it. Cached; pass refresh=true to run the check now (a metered fetch, rate-limited to once every few minutes per surface). Use configure_mentions to choose the queries first — with none saved this returns an empty, switched-off surface rather than an error. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped to a workspace). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `surface` | string | no | Which engine to read. Omit for all of them. One of: `ai_overview`, `google`, `bing`. |
| `refresh` | boolean | no | Run the check now before answering. Requires `surface`, costs one metered fetch, and is refused inside the cooldown (the cached answer comes back with a note). |

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
    "name": "get_mentions",
    "arguments": {
      "surface": "ai_overview"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_mentions","arguments":{"surface":"ai_overview"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/get_mentions

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/get_mentions' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"surface":"ai_overview"}}'
```

<!-- /widget -->
