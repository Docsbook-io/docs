---
title: "Search prior work"
description: "Has this already been tried on this project?"
---

# Search prior work

<!-- widget:mcp access=read price-millicents=6000 -->

## search_prior_work

Has this already been tried on this project? Searches the repository's ISSUES AND PULL REQUESTS together for work like the one you are about to propose, and says what happened to each: still open (proposed, nobody acted), closed without merging (written and then REJECTED), or merged (it shipped, and its effect can be measured). CALL THIS AFTER YOU HAVE ESTABLISHED THE PROBLEM AND BEFORE YOU DECIDE WHAT TO DO ABOUT IT. A recommendation made without it is made blind: the same idea gets proposed every quarter and the reason it was dropped last time is sitting in a closed pull request nobody read. Search with the words the WORK would be described in ('quickstart rewrite', 'nav restructure', 'add llms.txt'), not with your conclusion. Rows come back ranked by relevance, each carrying `outcome` and `status` (the same fact in plain words), `days_ago`, the agent that filed it if a machine did, and the issues a pull request came out of. ALWAYS read a row's status before citing it — a closed pull request is this project deciding AGAINST the change, and quoting it as precedent for making that change is the one way to use this tool that is worse than not calling it. Then read the promising one in full: get_pull_request for what actually changed, get_issue for the hypothesis. An empty result means nothing matched those words — never invent a number.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `query` | string | yes | What to look for, in the words the work would be written in. Qualifiers that would move the search off this repository are removed. |
| `kind` | string | no | Default 'both', which is almost always right — you do not know in advance whether the attempt was written down or shipped. One of: `both`, `issue`, `pull_request`. |
| `state` | string | no | Default 'all'. Narrowing to 'open' hides exactly the rejected and shipped attempts you are looking for. One of: `all`, `open`, `closed`. |
| `limit` | integer | no | How many rows (default 20) |

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
    "name": "search_prior_work",
    "arguments": {
      "query": "<query>",
      "kind": "both",
      "state": "all"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"search_prior_work","arguments":{"query":"<query>","kind":"both","state":"all"}}}'
```

<!-- /widget -->
