---
title: "Link work"
description: "CONNECT TWO PIECES OF WORK — an issue, a pull request, a hypothesis or a memory line (a goal or an open question)."
---

# Link work

<!-- widget:mcp access=write price-millicents=2000 -->

## link_work

CONNECT TWO PIECES OF WORK — an issue, a pull request, a hypothesis or a memory line (a goal or an open question). Free on every plan. 🔴 THE LINK IS WHAT MAKES THE WORK MEASURABLE. A merged pull request with nothing linked to it appears on get_work_board as `unmeasured`, which is the honest word for a change nobody can say anything about afterwards. Link the hypothesis it tests (with a `check_at` date on it) and the goal it argues for — two calls, and the board then answers "did this work" by itself. Undirected: linking A to B is the same fact as linking B to A, and writing it twice is one row, not two. Refs: an issue or a pull request by its GitHub NUMBER; a hypothesis or memory line by its KEY. The usual set, in the order they are written: hypothesis ↔ issue (what the work is for), issue ↔ pull request (how it arrived — write_docs does this for you when you pass `closes_issues`), issue ↔ memory (the goal it argues for, the question it waits on). This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `from_kind` | string | yes | What sort of record this end is. issue: A GitHub issue on this project's repository — the unit of work. Ref is its number. pull_request: A GitHub pull request — the change that tests something. Ref is its number. hypothesis: A row of list_hypotheses — the claim a change is meant to prove. Ref is its key. memory: A row of list_memory — a goal the work argues for, a question it waits on, a fact or rule it rests on. Ref is its key. One of: `issue`, `pull_request`, `hypothesis`, `memory`. |
| `from_ref` | string | yes | The GitHub number ('12' or '#12') or the row's key. |
| `to_kind` | string | yes | What sort of record this end is. issue: A GitHub issue on this project's repository — the unit of work. Ref is its number. pull_request: A GitHub pull request — the change that tests something. Ref is its number. hypothesis: A row of list_hypotheses — the claim a change is meant to prove. Ref is its key. memory: A row of list_memory — a goal the work argues for, a question it waits on, a fact or rule it rests on. Ref is its key. One of: `issue`, `pull_request`, `hypothesis`, `memory`. |
| `to_ref` | string | yes | The GitHub number or the row's key. |

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
    "name": "link_work",
    "arguments": {
      "from_kind": "issue",
      "from_ref": "<from_ref>",
      "to_kind": "issue",
      "to_ref": "<to_ref>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"link_work","arguments":{"from_kind":"issue","from_ref":"<from_ref>","to_kind":"issue","to_ref":"<to_ref>"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/link_work

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/link_work' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"from_kind":"issue","from_ref":"<from_ref>","to_kind":"issue","to_ref":"<to_ref>"}}'
```

<!-- /widget -->
