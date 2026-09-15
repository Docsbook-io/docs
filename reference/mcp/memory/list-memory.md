---
title: "List memory"
description: "THE BRIEF FOR THIS PROJECT — the owner's own goals beside the standing one (`goal`), what nobody here has answered yet (`question`), and what is already known about it (`fact` /…"
---

# List memory

<!-- widget:mcp access=read -->

## list_memory

THE BRIEF FOR THIS PROJECT — the owner's own goals beside the standing one (`goal`), what nobody here has answered yet (`question`), and what is already known about it (`fact` / `rule` / `preference`). Free on every plan. 🔴 READ THIS BEFORE YOU DECIDE ANYTHING HERE, in the same breath as get_workspace. `standing_goal` is every project's — be found, on Google and in AI answers — and needs no declaring; a `goal` line here is what this owner wants ON TOP of it. The open questions are what a previous run could not work out; answer what you can this run rather than re-deriving it. The rest is where the answers you were about to re-derive live: which page is the real pricing page, which words this product never uses, which section nobody may restructure. Each line says WHO wrote it (`owner` typed it in the panel, `agent` wrote it through this tool) and what it rests on (`evidence` — a URL, a path, a call id; null when there is none, which is honest for a preference and a warning sign on a fact). An owner's rule outranks your own reading of the site. A `goal` or a `question` also carries `resolution` — the outcome, or the answer. `null` there means OPEN, and the open ones are the rows worth acting on. `gap` names the one thing missing from this brief, when something is; it is advice about the store itself, not about the docs. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `kind` | string | no | Only lines of this kind. Omit for all of them. One of: `fact`, `rule`, `preference`, `goal`, `question`. |
| `open_only` | boolean | no | Only lines still open — goals not yet met, questions not yet answered. Ignored for the kinds that cannot be closed (a fact is never 'open'). |

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
    "name": "list_memory",
    "arguments": {
      "kind": "fact"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_memory","arguments":{"kind":"fact"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/list_memory

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/list_memory' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"kind":"fact"}}'
```

<!-- /widget -->
