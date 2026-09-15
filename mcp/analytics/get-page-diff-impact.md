---
title: "Get page diff impact"
description: "Did a documentation edit actually work?"
---

# Get page diff impact

<!-- widget:mcp access=read price-millicents=4000 -->

## get_page_diff_impact

Did a documentation edit actually work? (BUSINESS) Give it a commit and it compares the pages that commit TOUCHED against the pages it did NOT, in the week before and the week after — dead-end rate, self-serve resolution, time to first value, visit outcomes. The untouched pages are the control group, and they are the point: docs traffic moves for reasons that have nothing to do with you, so 'dead ends fell after my edit' is only evidence if they fell FURTHER on the edited pages than everywhere else. A change that merely matched the site trend is reported as no effect, not as a win. Call it with NO sha to list the commits that can be measured here — this tool carries its own index of them, so there is no separate history tool to call first. Use it after making a change you were told to make, and before making the same kind of change again. It measures a change that arrived as a COMMIT. For a change that did not — a setting, a language, a nav, a prompt — take a reading before and after with any read tool and compare the two with `compare_tool_calls`, which needs no commit at all. Also breaks the visits down by country, reader language and device, each beside the same slice's move on the untouched pages — which is how 'traffic went up' becomes a decision ('the growth is German readers on the English page') instead of a headline. Returns an explicit 'cannot measure' for commits too recent to have an after-window, or too old for visit data to still cover their before-window — never zeroes that look like a collapse. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `sha` | string | no | The commit to measure, full or short SHA. Omit to get the list of commits that CAN be measured here, newest first. |
| `window_days` | integer | no | Days compared on each side (default 7) |

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
    "name": "get_page_diff_impact",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_page_diff_impact","arguments":{}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/get_page_diff_impact

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/get_page_diff_impact' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{}}'
```

<!-- /widget -->
