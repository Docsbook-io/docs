---
title: "Edit memory"
description: "CORRECT a line in this project's brief, or CLOSE it."
---

# Edit memory

<!-- widget:mcp access=write -->

## edit_memory

CORRECT a line in this project's brief, or CLOSE it. Free on every plan. 🔴 ANSWERING A QUESTION IS THIS TOOL: pass `resolution` with the answer, and the question stays on the record with the answer beside it — which is what stops the next run asking it again. The same field marks a `goal` met, with the reading that showed it. Corrections happen in place, rather than removing a line and adding it back, and the difference is not cosmetic: `created_at` is when this project first learnt the thing, and a re-create resets it so every line reads as learnt today. A memory whose age is a lie is one the owner cannot audit. Pass only the fields that change. This is also how a line gets DOWNGRADED honestly — a fact that turns out to be an assumption becomes a rule or a preference rather than being quietly deleted. This answers WHAT, not what to do about it. If you have not already got the method from `docsbook_expert`, get it first: it names which readings answer this question, what to compare them against, and what would make the conclusion wrong. One call, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `key` | string | yes | The line's handle, from list_memory. |
| `kind` | string | no | What sort of line this is, and it decides how a later run WEIGHS it. goal: What these docs are FOR, in the owner's words — the outcome every recommendation here is argued against. NOT an analytics goal (create_goal): that one is a thing a reader does that counts as a conversion and is measured in visits; this one is the aim a run steers toward, and nothing counts it. question: Something nobody here has answered yet. Write one down instead of guessing mid-run; close it with edit_memory's `resolution` once somebody — a later run, or the owner, who often just knows — answers it. fact: True of this project and checkable — where a page lives, what the product charges, which generator builds the reference. rule: What to do or never do here. Not checkable against the site; it is an instruction, and it outranks an agent's own preference. preference: Taste — wording, tone, structure. Arguable by design, and the first thing to drop when it collides with a rule. One of: `fact`, `rule`, `preference`, `goal`, `question`. |
| `text` | string | no | Replacement text. Omit to keep it. Same hard limit as add_memory (600 characters, refused rather than truncated) — move dates, numbers, call_ids and secondary observations into `evidence` instead, which has none. |
| `evidence` | string | no | Replacement evidence. Pass an empty string to clear it. No length limit — this is where the supporting detail belongs. |
| `resolution` | string | no | Close this line: the answer to a question, or what showed a goal was met. Pass an empty string to REOPEN one — an answer that turns out to be wrong has to be retractable. goal and question lines only. |
| `waiting_on` | string | no | Change who this question waits on — `owner` when you have established that only they can answer it, `agent` when you have worked out that it is findable and the next run should go and find it. Cleared automatically when the question is answered. One of: `owner`, `agent`, `owner_blocking`. |

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
    "name": "edit_memory",
    "arguments": {
      "key": "<key>",
      "kind": "fact",
      "waiting_on": "owner"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"edit_memory","arguments":{"key":"<key>","kind":"fact","waiting_on":"owner"}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/edit_memory

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | yes | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/edit_memory' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{"key":"<key>","kind":"fact","waiting_on":"owner"}}'
```

<!-- /widget -->
