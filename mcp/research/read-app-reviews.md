---
title: "Read app reviews"
description: "Up to 50 recent reviews for one app, with star rating, the review text, the app version reviewed, and any developer reply already given."
---

# Read app reviews

<!-- widget:mcp access=read price-millicents=2500 -->

## read_app_reviews

Up to 50 recent reviews for one app, with star rating, the review text, the app version reviewed, and any developer reply already given. A one-star review naming a confusing setup step is a documentation-gap complaint that never touches the website our analytics watches at all — for an app-shipping ICP this is often the loudest unanswered-question channel there is. Routes from questions like: what do app store reviews say about onboarding · check google play reviews for setup complaints · «что пишут в отзывах про сложную настройку» · «проверь отзывы в google play про онбординг». Not: It reads reviews already posted about one named app. It is not a review-monitoring subscription and does not run on a schedule by itself. Example: Read the 50 most recent Google Play reviews for com.example.app, looking for onboarding complaints. Pass `workspace_id` whenever the answer will be quoted later: it is what files the reading in that project's history with a `call_id`, and only a `call_id` (or a URL) is accepted as the source of a figure on an audit finding — the tool's own name is not a source. One call fetches at most 50 results and costs $0.0250.

| Field | Type | Required | Description |
|---|---|---|---|
| `app_id` | string | yes | Google Play package name (e.g. com.example.app) or numeric App Store id (e.g. 310633997). |
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
    "name": "read_app_reviews",
    "arguments": {
      "app_id": "<app_id>"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"read_app_reviews","arguments":{"app_id":"<app_id>"}}}'
```

<!-- /widget -->
