---
title: "Add memory"
description: "WRITE ONE LINE INTO THIS PROJECT'S BRIEF — an aim, an open question, or something learnt — for every later run and for the owner to see."
---

# Add memory

<!-- widget:mcp access=write price-millicents=2000 -->

## add_memory

WRITE ONE LINE INTO THIS PROJECT'S BRIEF — an aim, an open question, or something learnt — for every later run and for the owner to see. Free on every plan. Write a `goal` ONLY when the owner tells you what these docs are for beyond the standing goal every project already has (be found, on Google and in AI answers — never ask for that one, never write it down again). Write a `question` the moment you would otherwise GUESS something about THE PRODUCT that nobody can read off it — 'is 2 490 ₽ a month still the price?', 'who buys this: solo developers or companies with a support team?', 'is the v1 API still supported?'. It costs one call, it stops the guess from being laundered into a fact, and the owner reading the panel can often answer it in one line. Close it later with edit_memory's `resolution`. 🔴 A QUESTION IS WRITTEN FOR THE OWNER AND IS ABOUT THEIR PRODUCT, and this call REFUSES an agent's question that is not: no call ids, tool names, file paths, environment names or jargon in it, and nothing about the machinery — access, tokens, plans, grants, the loop's own cadence. Those are setup problems: say them in your run report (the harness reads blockers off the ledger, and the setup checklist shows the owner what to connect) and go on with the work that does not depend on them. Measured 2026-09-14: four of the six open questions filed to owners were about a token, a plan's expiry or a GitHub grant, in the loop's own words, and none of them was a question the owner could answer on a phone. Write a `fact`, `rule` or `preference` when you learn something the NEXT run would otherwise work out again — where a thing lives, what the product actually charges, which generator builds the reference, what an experiment already showed. Do NOT write findings that expire: 'the quickstart is slow this week' is a measurement (take a reading instead, they are recorded automatically), while 'measure the quickstart against the week before a change, not against last month' is a rule that stays true. 🔴 Never file a standing order to WAIT as a `fact` or `rule` — neither one takes a `resolution`, so 'too thin to trust yet, re-run once traffic passes N' has no way to close, and it is the first line every later run reads, forever, as the reason to do nothing again. Measured live 2026-09-14: one project's own such line sat in front of sixteen consecutive empty cycles before it was rewritten. A sample-size observation belongs on a hypothesis instead — `check_in_days` gives it a date this project is worth reading again, and that date is the thing a fact cannot hold. One claim per line. A paragraph holding three cannot be corrected later, only replaced. `evidence` is what the line rests on — the page, the URL, the `call_id` of the reading it came from — and it has NO length limit, unlike `text` (hard 600). Put the dates, numbers, call_ids and secondary observations there; keep `text` to the one sentence they support. A fact without evidence can never be re-checked, so nothing will ever mark it stale; you will get a warning saying so, and the line is still written. Relay the warnings: they are the part the owner needs.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `key` | string | yes | Short machine handle, e.g. 'pricing_page_path'. Lowercase and underscores; it is what edit_memory and remove_memory name this line by. |
| `kind` | string | yes | What sort of line this is, and it decides how a later run WEIGHS it. goal: What these docs are FOR, in the owner's words — the outcome every recommendation here is argued against. NOT an analytics goal (create_goal): that one is a thing a reader does that counts as a conversion and is measured in visits; this one is the aim a run steers toward, and nothing counts it. question: Something nobody here has answered yet. Write one down instead of guessing mid-run; close it with edit_memory's `resolution` once somebody — a later run, or the owner, who often just knows — answers it. fact: True of this project and checkable — where a page lives, what the product charges, which generator builds the reference. rule: What to do or never do here. Not checkable against the site; it is an instruction, and it outranks an agent's own preference. preference: Taste — wording, tone, structure. Arguable by design, and the first thing to drop when it collides with a rule. One of: `fact`, `rule`, `preference`, `goal`, `question`. |
| `text` | string | yes | The line itself, one claim, at most a couple of sentences — hard limit 600 characters, and a longer one is refused rather than truncated. For a `question`, the question as you would put it to the owner. A run log ("cycle 2026-09-14: nothing found") is not a line for this store: it is not true of the project, it is true of one hour, and the next run reads it as if it were the former. |
| `evidence` | string | no | What it rests on: a page path, a URL, or the call_id of the reading that showed it. |
| `resolution` | string | no | File it already closed — the answer to a question you worked out this run, or a goal recorded as already met. goal and question lines only; anything else is refused, because a fact does not get answered, it stops being true (remove_memory). |
| `waiting_on` | string | no | Who answers this question — `question` lines only. `owner` when only the person who owns the project can (leave it open and SAY so; do not guess), `agent` when the answer is findable and the next run should go and find it. Omitted reads as `owner`, which is the safe default: the cost of guessing at something only the owner knows is the reason this kind exists. One of: `owner`, `agent`, `owner_blocking`. |

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
    "name": "add_memory",
    "arguments": {
      "key": "<key>",
      "kind": "fact",
      "text": "<text>",
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
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"add_memory","arguments":{"key":"<key>","kind":"fact","text":"<text>","waiting_on":"owner"}}}'
```

<!-- /widget -->
