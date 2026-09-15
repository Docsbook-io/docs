---
title: "Get pull request"
description: "Read ONE pull request on this project's repository in full — and, crucially, WHO made it and WHAT CAME OF IT."
---

# Get pull request

<!-- widget:mcp access=read price-millicents=6000 -->

## get_pull_request

Read ONE pull request on this project's repository in full — and, crucially, WHO made it and WHAT CAME OF IT. Returns its status in plain words (merged / closed without merging / still open), the files it touched with their line counts, the agent and run that opened it when a machine did (`opened_by`), the issues it came out of (`linked_issues`), the reviews and comments on it, and — once merged — the commit sha to measure its actual effect with (`measure_impact_with`, for get_page_diff_impact). This is how you find out what a change was FOR. The body carries what the author was trying to achieve, the issues it closes carry the hypothesis being tested, and the review comments carry why it was cut down or thrown out. Use it on a row from search_prior_work before repeating, extending or arguing against that change — reading the title alone is how a rejected change gets proposed a second time. The diff itself is omitted unless you ask for it: the file list answers 'what did this touch' at a fraction of the size. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `number` | integer | yes | The pull request number, e.g. 128. Find candidates with search_prior_work. |
| `include_patch` | boolean | no | Include each file's diff. Off by default; ask for it only when the answer depends on HOW the change was written. |

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
    "name": "get_pull_request",
    "arguments": {
      "number": 0
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_pull_request","arguments":{"number":0}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/get_pull_request

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/get_pull_request' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"number":0}}'
```

<!-- /widget -->
