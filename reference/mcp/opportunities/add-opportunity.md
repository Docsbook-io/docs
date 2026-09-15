---
title: "Add opportunity"
description: "ADD ONE OPPORTUNITY to a direction — one search, question or job people actually make, how many of them there are, where these docs stand for it, who wins it today, and what…"
---

# Add opportunity

<!-- widget:mcp access=write -->

## add_opportunity

ADD ONE OPPORTUNITY to a direction — one search, question or job people actually make, how many of them there are, where these docs stand for it, who wins it today, and what winning it is worth. Free on every plan. 🔴 WRITTEN FOR THE OWNER, AND REFUSED WHEN IT IS NOT. `intent`, `current`, `competitor`, `potential`, `demand_note` and `drop_reason` are the row on their screen: no call ids, tool names, file paths, metric dumps or jargon they would have to look up. Say what the customer looks for, what they see today, who they are sent to instead and what beats them, what winning brings. Example — intent: 'virtual card for paying foreign subscriptions'; current: 'our card page never uses those words, so Google does not show it'; competitor: 'Yello Card and three others — Google's AI answer recommends them with a price table'; potential: '110 people a month who today see four competitors priced 19–200% above us'. The trace — call ids, URLs, the figures as measured — goes in `evidence` and `demand_source`. 🔴 `demand_value` IS NULLABLE AND NULL IS NOT ZERO. Leave it out when nobody measured it and say what you tried in `demand_note`, plainly. A zero written where nothing was measured reads as "nobody searches for this", travels into the decision to skip the row, and is never revisited — this repository has paid for that mistake twice. 🔴 A FIGURE REQUIRES A `demand_source`, and for an agent this is REFUSED rather than warned about. It has to be something a reader can open: a `call_id` from this project's own ledger (re-readable with get_tool_call) or an absolute URL. Where the figures come from: read_keyword_demand (absolute monthly searches), read_search_trends (relative interest — never a count), read_search_suggestions (the exact phrasings people type), read_serp_snapshot (what Google shows, AI Overview included), get_failed_searches / get_popular_searches (what readers asked once already here), collect_ai_citability (whether an assistant can quote this project), crawl_competitor_docs (what the competitor holding the slot has). `action` is from a closed list — create / rewrite / expand / structure / authority / none — because free text here becomes a promise the product cannot keep. `none` is a real answer: a recorded "measured and deliberately not worth doing" is what stops the next run re-finding it. Nothing here says whether the opportunity was WON: that is the verdict on the hypotheses pointing at this row. After adding the top opportunities, configure_mentions with their `intent`s so the direction is measured by whether the docs actually show up. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `direction_key` | string | yes | The direction this belongs to, from list_opportunities. |
| `key` | string | yes | Short machine handle for this row, e.g. 'virtual_card_subscriptions'. A hypothesis names it in `opportunity_key`. |
| `intent` | string | yes | The search, question or job — in the words somebody actually types or asks, not in ours. Printed on the owner's screen. |
| `demand_value` | number | no | How many are looking. OMIT when nobody measured it — never pass 0 for that. |
| `demand_unit` | string | no | What the figure counts: `searches/mo`, `impressions/mo`, `threads`, `%`. Without it the direction's total adds monthly searches to forum threads. |
| `demand_source` | string | no | REQUIRED beside a figure: the `call_id` it came from, or an absolute URL. A description is not a source and is refused. Technical — not shown to the owner. |
| `demand_note` | string | no | Why the figure is unknown, when it is — in the owner's words: 'too niche for Google's keyword tool to report a number; three competitors sell to exactly this search'. An honest null still needs a sentence, or the next run re-measures it from scratch. |
| `current` | string | no | Where these docs stand for that search TODAY, as the owner would see it: 'nothing at all', 'a page about something else', 'on the second page of results', 'present but the AI answer never quotes it'. The `potential` is a delta from this. Refused when technical. |
| `competitor` | string | no | Who wins it today — and what gives them the slot: a price table, a comparison, a one-paragraph definition the AI answer lifts whole. Written for the owner. |
| `competitor_url` | string | no | The page of theirs that holds it. |
| `action` | string | no | create (write the page): No page answers this at all. Write one. rewrite (rewrite the page): A page exists and answers something else — it is about us, or about a different job than the one people search for. expand (complete the answer): A page answers part of it. The rest of the answer is missing, not wrong. structure (make it quotable): The answer is on the page and nobody can lift it out — buried under a heading nobody searches for, split across three pages, or locked in a screenshot or a table with no sentence around it. Search engines and assistants quote sentences. authority (earn the trust): The answer is there, correct, and not believed: nothing links to it, no assistant cites it, and the competitor holding the slot says the same thing with more proof around it. none (not worth it): Measured and deliberately not worth doing — the audience is real and the fit is not. Recorded so the next run does not find it again. One of: `create`, `rewrite`, `expand`, `structure`, `authority`, `none`. |
| `potential` | string | no | What winning it is worth, for the owner: the people it brings in a month, the price comparison it wins, the support question it retires — sized from the demand figure and a stated assumption, not from a number you liked. Refused when technical. |
| `potential_value_cents` | number | no | What that gain is worth, in cents. Omit when unpriced. |
| `evidence` | string | no | Technical, not shown to the owner: the `call_id`s and URLs behind `current` and `competitor`, and the figures as measured. |
| `disposition` | string | no | `open` by default. `dropped` = measured and deliberately not being worked; say why in `drop_reason`, in plain words, or the next run re-proposes it. One of: `open`, `dropped`. |
| `drop_reason` | string | no | Written for the owner. |
| `position` | number | no | Where it sits in the table. Default: appended. |

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
    "name": "add_opportunity",
    "arguments": {
      "direction_key": "<direction_key>",
      "key": "<key>",
      "intent": "<intent>",
      "action": "create",
      "disposition": "open"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"add_opportunity","arguments":{"direction_key":"<direction_key>","key":"<key>","intent":"<intent>","action":"create","disposition":"open"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/add_opportunity

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/add_opportunity' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"direction_key":"<direction_key>","key":"<key>","intent":"<intent>","action":"create","disposition":"open"}}'
```

<!-- /widget -->
