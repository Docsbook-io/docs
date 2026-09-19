---
title: "Search brief"
description: "HAS THIS BEEN TRIED HERE?"
---

# Search brief

<!-- widget:mcp access=read price-millicents=800 -->

## search_brief

HAS THIS BEEN TRIED HERE? One query over everything this project has written down — its memory lines and its hypotheses, closed ones included. Free on every plan. 🔴 CALL THIS BEFORE YOU PROPOSE A CHANGE, in the same breath as search_prior_work. That one searches the repository's issues and pull requests; this one searches what was THOUGHT and MEASURED. Between them they answer the question that decides whether a recommendation is worth making: somebody already considered this — what did they conclude? The rows that matter most carry `closed_with`: a `rejected` hypothesis with its figures, a question with its answer. Each of those is this project deciding AGAINST something, and citing one as precedent FOR it is the one way to use this tool that is worse than not calling it. Search with the words the work would be described in — the page, the metric, the change — not with your conclusion. Any language. An empty result is evidence of absence FOR THOSE WORDS ONLY: try the vocabulary the work itself would use before concluding the idea is new.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `query` | string | yes | What to look for, in the words the work would be written in. 'quickstart dead end', 'translations German', «переводы на немецкий». |
| `limit` | number | no | How many rows. Default 20. |

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
    "name": "search_brief",
    "arguments": {
      "query": "<query>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"search_brief","arguments":{"query":"<query>"}}}'
```

<!-- /widget -->
