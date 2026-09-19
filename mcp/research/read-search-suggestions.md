---
title: "Read search suggestions"
description: "What Google autocompletes after a phrase — including the who/what/why/how question forms — for up to 10 seeds, with the rank each suggestion held and the seed it came from."
---

# Read search suggestions

<!-- widget:mcp access=read price-millicents=11000 -->

## read_search_suggestions

What Google autocompletes after a phrase — including the who/what/why/how question forms — for up to 10 seeds, with the rank each suggestion held and the seed it came from. This is the questions half of demand, in the reader's own spelling: a volume number says whether anyone is asking, and only this says in what words, which is what a page can actually be titled with. Routes from questions like: what do people actually type when they search for this · what questions does google suggest about this · give me long-tail phrasings for this topic · «что люди реально набирают по этой теме» · «какие вопросы подсказывает гугл» · «собери длинный хвост запросов». Not: It is what Google SUGGESTS as somebody types, not what Google returns — the results page is read_serp_snapshot, whose People Also Ask box is Google's own curated question set rather than this raw prefix stream. How many people are behind any one of these phrasings is read_keyword_demand. Example: Expand "acme webhooks" and "acme rate limits" into Google's own autocomplete suggestions, question forms included. Pass `workspace_id` whenever the answer will be quoted later: it is what files the reading in that project's history with a `call_id`, and only a `call_id` (or a URL) is accepted as the source of a figure on an audit finding — the tool's own name is not a source. One call fetches at most 110 events and costs $0.1100.

| Field | Type | Required | Description |
|---|---|---|---|
| `keywords` | string[] | yes | Seed phrases to expand, e.g. ["acme webhooks"] — each comes back with what Google autocompletes after it, plus the who/what/why/how question forms. |
| `country` | string | no | ISO 3166-1 alpha-2 country for localized suggestions ("us", "gb", "de"). Defaults to us. |
| `language` | string | no | ISO 639-1 language for the suggestions ("en", "es", "ja"). Defaults to en. |
| `workspace_id` | string | no | The project this reading is FOR. 🔴 Pass it whenever the answer will be QUOTED later: it is what files the call in that project's history with a `call_id`, and a `call_id` is the only thing an opportunity accepts as the source of a demand figure (`demand_source`). Nothing about the project is sent to the site being read. Omitted, the reading still comes back — it simply lands in no history, so nothing afterwards can point at it. Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |

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
    "name": "read_search_suggestions",
    "arguments": {
      "keywords": []
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"read_search_suggestions","arguments":{"keywords":[]}}}'
```

<!-- /widget -->
