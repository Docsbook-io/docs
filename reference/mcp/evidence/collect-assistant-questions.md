---
title: "Collect assistant questions"
description: "Return what readers asked your docs assistant, verbatim, with which of it produced no answer — plus the answer rate with its denominator and the languages the questions arrived in."
---

# Collect assistant questions

<!-- widget:mcp access=read -->

## collect_assistant_questions

Return what readers asked your docs assistant, verbatim, with which of it produced no answer — plus the answer rate with its denominator and the languages the questions arrived in. This is the only source on the server where a reader speaks in full sentences. A failed search is three words; an assistant question is the whole job, stated by somebody who wanted it done — which is why it is the raw material under every question about MOTIVE rather than behaviour. Quotes are carried through unparaphrased, because 'how do I rotate a key' and 'where do I regenerate my token' summarise to one bullet and are two different pages. Says plainly what the answer rate is NOT: it counts questions the assistant produced something for, and knows nothing about whether that something was right. Returns an evidence record and the `get_ai_questions` / `get_ai_unanswered` calls that produced it — no ranking, no themes, no recommendation. Use it for 'what are people asking the bot', 'show me the unanswered questions', 'what did readers ask last week', «что спрашивают у бота», «на что бот не смог ответить», «покажи вопросы читателей». Grouping those questions into jobs, and deciding which of them is a missing page rather than a missing sentence, is the judgement: ask `docsbook_expert` with what you are trying to achieve and it gives the method, the reads it runs on, and what would make it wrong. Returns a validated `collect_assistant_questions.v1` payload: an `evidence` map, the normalised `rows` behind it, and a `reproduce` block naming the exact MCP calls and arguments that produced every row — run them yourself and you get the same answer. There is no model in the path, so there are no findings, no scores and nothing to disbelieve; interpretation is what the audits charge for. Changes nothing; safe on a read-only token. Evidence, not a verdict — nothing here says what the gap MEANS. If you have not already asked `docsbook_expert` how to read it, ask: it says what this evidence is worth against, and what to do with it. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `window_days` | integer | no | Days of history to read (default 28). One window is used for every signal in the run and stated in the payload — mixing windows silently invents trends. |

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
    "name": "collect_assistant_questions",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"collect_assistant_questions","arguments":{}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/collect_assistant_questions

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/collect_assistant_questions' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{}}'
```

<!-- /widget -->
