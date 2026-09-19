---
title: "Send inbox message"
description: "WRITE A LETTER INTO THIS PROJECT'S INBOX — the owner's mailbox in their panel, with its unread count on the row."
---

# Send inbox message

<!-- widget:mcp access=read price-millicents=800 -->

## send_inbox_message

WRITE A LETTER INTO THIS PROJECT'S INBOX — the owner's mailbox in their panel, with its unread count on the row. Free on every plan. Use it for a REPORT worth a human read (a run finished and found something) or a QUESTION you cannot decide without the owner's own words. 🔴 THIS IS NOT A LOG LINE. The Inbox exists because a station runs unwatched — call this once per RUN, for what the run is worth reading, never once per tool call inside it. A letter for every step is exactly the failure this call exists to prevent: a mailbox nobody reads any more, which is worse than no mailbox at all. ⚡ IT IS ALSO THE ONLY WAY GOOD NEWS REACHES THE OWNER. A run that finishes well writes nothing by itself any more, so if this one is worth a person's minute, say it here in your own sentences; if it is not, say nothing and let the Agent section carry the fact that the run happened. 🔴 NAME THE SUBJECT SPECIFICALLY. "Questions about the pricing page rewrite" lets a later run of yours recognise this letter at a glance and check whether it was answered; "Question" or "Update" does not, and by the time the owner has opened ten of those the mailbox is unreadable. `body` is Markdown, rendered as the owner reads it — headings, lists, links and code all work. Keep it to what a person needs, not everything the run collected. 🔴 ASK IN THE BODY, IN YOUR OWN SENTENCES. Every letter carries ONE reply box, and the owner's answer starts a run that reads this whole thread — so a question is just a letter that ends in one. Ask what you actually need decided, and ask it plainly enough to be answered in a sentence: three vague questions get one shrug, and you will have spent the owner's attention for nothing. list_inbox_messages FIRST, to see what you already asked and whether it was answered — asking the same thing twice because a status was never checked is the other way this becomes noise.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `kind` | string | yes | `report` — something finished that is worth a human read. `question` — something you cannot decide without the owner; ask it in `body`, and the owner's reply comes back through list_inbox_messages as a turn in this letter's thread. One of: `report`, `question`. |
| `subject` | string | yes | The mailbox's subject line — name the SPECIFIC topic ('Questions about the pricing page rewrite'), never a generic 'Report' or 'Question'. One line, no trailing period. |
| `body` | string | yes | The letter, in Markdown — what actually happened, or what you need decided, written for the owner to read cold. No call ids or tool names unless they are themselves what the owner asked about. |
| `tone` | string | no | Default `neutral`. `ok` — finished well. `error` — finished badly, printed in red. `due` — a deadline or something owed. Never `error` for a question the owner merely needs to answer; that paints asking for input as a failure. One of: `ok`, `error`, `due`, `neutral`. |

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
    "name": "send_inbox_message",
    "arguments": {
      "kind": "report",
      "subject": "<subject>",
      "body": "<body>",
      "tone": "ok"
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"send_inbox_message","arguments":{"kind":"report","subject":"<subject>","body":"<body>","tone":"ok"}}}'
```

<!-- /widget -->
