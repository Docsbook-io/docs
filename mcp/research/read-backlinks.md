---
title: "Read backlinks"
description: "How many distinct domains currently link to a site, and the actual referring pages — a real number where our own tools have always had to leave this field null."
---

# Read backlinks

<!-- widget:mcp access=read price-millicents=1500 -->

## read_backlinks

How many distinct domains currently link to a site, and the actual referring pages — a real number where our own tools have always had to leave this field null. "Referring domains" is a metric this product has never been able to populate; this is the first source for it, cheap enough to run per lead. Routes from questions like: who links to our docs · check backlinks for this domain · «кто ссылается на наш сайт» · «проверь бэклинки этого домена». Not: It counts referring domains and pages for up to three domains. It does not return anchor text or dofollow/nofollow status at all — a claim that needs either belongs to a link-graph product this catalog does not carry, and must be stated as a limitation, not rounded up to "full backlink audit". Example: Check backlinks for ourdocs.com and rivaldocs.com — referring domain counts and the pages themselves. Pass `workspace_id` whenever the answer will be quoted later: it is what files the reading in that project's history with a `call_id`, and only a `call_id` (or a URL) is accepted as the source of a figure on an audit finding — the tool's own name is not a source. One call fetches at most 3 events and costs $0.0150.

| Field | Type | Required | Description |
|---|---|---|---|
| `domains` | string[] | yes | One to three bare domains to check, e.g. ["ourdocs.com", "rivaldocs.com"] — no scheme, no path. |
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
    "name": "read_backlinks",
    "arguments": {
      "domains": []
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"read_backlinks","arguments":{"domains":[]}}}'
```

<!-- /widget -->
