---
title: "Read x profile"
description: "Follower count, bio and verification status for up to 5 X/Twitter profiles — a profile that does not exist returns no row at all, never a zeroed placeholder."
---

# Read x profile

<!-- widget:mcp access=read price-millicents=2400 -->

## read_x_profile

Follower count, bio and verification status for up to 5 X/Twitter profiles — a profile that does not exist returns no row at all, never a zeroed placeholder. Audience size for a lead's own account is not a field GitHub's API exposes at any price; a solo maintainer and a 200-person company both show up as `owner_class: User` without it. Routes from questions like: how big is this account's audience on x · check their twitter follower count · «какая аудитория у этого аккаунта в x» · «проверь число подписчиков в твиттере». Not: It reads a public profile's own stated numbers. Posting, following or DMing an account is not something this tool, or Docsbook, does. Example: Look up follower count and bio for https://x.com/vercel and https://x.com/supabase. Pass `workspace_id` whenever the answer will be quoted later: it is what files the reading in that project's history with a `call_id`, and only a `call_id` (or a URL) is accepted as the source of a figure on an audit finding — the tool's own name is not a source. One call fetches at most 5 results and costs $0.0240.

| Field | Type | Required | Description |
|---|---|---|---|
| `profile_urls` | string[] | yes | Full X/Twitter profile URLs, e.g. ["https://x.com/vercel"] — not bare handles. |
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
    "name": "read_x_profile",
    "arguments": {
      "profile_urls": []
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"read_x_profile","arguments":{"profile_urls":[]}}}'
```

<!-- /widget -->
