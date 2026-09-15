---
title: "Collect page text"
description: "Fetch your live pages and report what actually arrives on the wire — status, title, meta description, how many words of prose survive with no JavaScript engine, headings, code…"
---

# Collect page text

<!-- widget:mcp access=read price-millicents=12000 -->

## collect_page_text

Fetch your live pages and report what actually arrives on the wire — status, title, meta description, how many words of prose survive with no JavaScript engine, headings, code blocks, links — beside the character count of the source we store for the same path. The row worth the call is the GAP between those two: a page that is 8 000 characters of markdown in the repository and 40 words on the wire renders client-side, which makes it perfect to every check that reads the source and unquotable to every assistant that reads the page. Nothing else on this server holds both ends of that comparison at once. Returns an evidence record and the exact `fetch_url` calls that produced every row, so you can re-run it by hand and get the same answer. No scores, no findings, no opinion — it is the raw material the audits are built on, at a sixtieth of the price. Use it for 'what does our page actually serve', 'is this page rendering server-side', 'check these three URLs', 'do our titles and descriptions exist', «что реально отдаёт страница», «рендерится ли она без JS», «проверь эти адреса». It does not say what the gap MEANS — for that, ask `docsbook_expert` with what you are trying to achieve and it names what to compare these rows against. `collect_ai_citability` is the neighbouring probe, scoring whether an answer engine can fetch and quote the same pages. Returns a validated `collect_page_text.v1` payload: an `evidence` map, the normalised `rows` behind it, and a `reproduce` block naming the exact MCP calls and arguments that produced every row — run them yourself and you get the same answer. There is no model in the path, so there are no findings, no scores and nothing to disbelieve; interpretation is what the audits charge for. Changes nothing; safe on a read-only token. Evidence, not a verdict — nothing here says what the gap MEANS. If you have not already asked `docsbook_expert` how to read it, ask: it says what this evidence is worth against, and what to do with it. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `pages` | string[] | no | Page paths to probe, e.g. ["/", "/docs/quickstart"]. Defaults to the site root and two common docs paths. Each page costs two fetches. |

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
    "name": "collect_page_text",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"collect_page_text","arguments":{}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/collect_page_text

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/collect_page_text' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{}}'
```

<!-- /widget -->
