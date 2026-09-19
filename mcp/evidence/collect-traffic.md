---
title: "Collect traffic"
description: "One call for the four traffic facts every analysis starts from: who arrived (pageviews, visitors, top pages, referrers, countries), how the visits ENDED (success / dead end /…"
---

# Collect traffic

<!-- widget:mcp access=read price-millicents=12000 -->

## collect_traffic

One call for the four traffic facts every analysis starts from: who arrived (pageviews, visitors, top pages, referrers, countries), how the visits ENDED (success / dead end / bounce / partial, with the denominator), which pages they ended on, and the 2–4 page sequences readers actually walk. Four tools' worth of warehouse in one probe, and kept as four separate tables rather than averaged into a health number — a pageview count answers 'is anyone here', the outcome mix answers 'did it work', and a report that merges them answers neither. Every rate here is an estimate over hashed IPs and says so; where the warehouse withheld a rate for too small a sample, this returns null WITH the reason rather than a zero, because a zero is the version an owner acts on. Returns an evidence record and the exact `get_analytics` / `get_visit_outcomes` / `get_dead_end_pages` / `get_route_patterns` calls behind every row. No ranking, no cause, no fix. Use it for 'give me the traffic numbers', 'how do visits end', 'which pages do people give up on', 'what routes do readers walk', «дай цифры по трафику», «чем заканчиваются визиты», «на каких страницах сдаются». WHY the numbers moved, and what to do about any one page, is not in here — ask `docsbook_expert` with the outcome you want: it names what to compare this window against (a control set, the same window last year) and the readings that separate a real move from the season. Returns a validated `collect_traffic.v1` payload: an `evidence` map, the normalised `rows` behind it, and a `reproduce` block naming the exact MCP calls and arguments that produced every row — run them yourself and you get the same answer. There is no model in the path, so there are no findings, no scores and nothing to disbelieve; interpretation is what the audits charge for. Changes nothing; safe on a read-only token.

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
    "name": "collect_traffic",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"collect_traffic","arguments":{}}}'
```

<!-- /widget -->
