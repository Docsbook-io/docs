---
title: "Write context"
description: "PUT SOMETHING INTO THIS ORGANIZATION'S FOLDER — what you worked out, so no later run has to work it out again."
---

# Write context

<!-- widget:api -->

## POST /api/v1/write_context

PUT SOMETHING INTO THIS ORGANIZATION'S FOLDER — what you worked out, so no later run has to work it out again. Free. This is how the agent gets better at one customer over time, and it is the half of a run that outlives the run. WRITE WHEN: you learned something that stays true (where the real pricing page is, which words this product never uses, who actually buys it); you are about to make a change and want the claim on record BEFORE the reading that judges it (`hypotheses/`, with `review_in_days`); the owner settled something (`decisions/`); you could not work something out and only they can answer it (`questions/`, with `review_in_days`); a way of working held up here and would hold again (`playbooks/`). WHERE: product/ — What is this business, what does it charge, what does it never claim? audience/ — Who reads these docs, what job are they on, what do they arrive already knowing? conventions/ — How must a page read here — voice, terms this product uses and never uses, structure? memory/ — What would the next run otherwise work out again from scratch? decisions/ — What did the owner settle, when, and what does it close? hypotheses/ — What might be true, what reading decides it, and by when? questions/ — What could not be worked out here, and who can answer it? playbooks/ — How is this kind of work done well HERE — what was tried, what held? Organization-level by default; put it under `projects/<id>/…` only when it is true of that one project and not of the company. What a run DID goes in its report. "too thin to trust, re-run once traffic passes N" filed where nothing can close it is read at the top of every later run, for ever, as the reason to do nothing again. If it has a date, it is a hypothesis with `review_in_days`. ⚡ THREE FIELDS ARE THE WHOLE CALL — `path`, `title`, `body`. Everything else is optional and folder-specific: `review_in_days` is required in `hypotheses/` and `questions/` and welcome anywhere a fact expires; `verdict` belongs in `hypotheses/` alone and is dropped with a warning if it arrives anywhere else. A fact does not need a verdict to be written down. One file answers one thing; the body caps at 4000 characters. Writing to a path that exists REPLACES it, and the date this organization first learned it survives the rewrite.

**Price** — $0.00003 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/write_context`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `path` | string | no | `<folder>/<name>.md` for the organization, `projects/<project id>/<folder>/<name>.md` for one project. Lowercase, hyphens, named for what it holds — `pricing-is-per-seat.md`, not `note-3.md`. |
| `title` | string | no | The one line a later run reads when deciding whether to open this file at all. |
| `body` | string | no | The knowledge itself, in prose. One thing per file — a file holding three cannot be corrected later, only replaced. |
| `evidence` | string | no | What it rests on — the page, the URL, the id of the reading. No length limit: this is where dates, figures and call ids belong, so the body can stay the claim they support. Without it nothing can ever mark this stale. |
| `confidence` | string | no | `observed` you saw it, `inferred` you worked it out, `told` the owner said so. It decides whether a later run may state this to a customer as fact. |
| `review_in_days` | string | no | When this is worth reading again. OPTIONAL everywhere except `hypotheses/` and `questions/`, where it is REQUIRED — the date is what lets a claim be closed instead of read for ever. |
| `verdict` | string | no | OPTIONAL, and `hypotheses/` ONLY — the one folder a reading decides. Leave it out everywhere else: a fact, an audience, a house rule and a settled decision are not confirmed or rejected, and one sent to those folders is dropped with a warning rather than refused. 🔴 In `hypotheses/`, "nothing distinguishable" is `rejected`, not a missing answer — and a rejection is the expensive half of what this customer knows. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | string | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### Limitations

- 🔴 NOT A DIARY.
- "cycle 2026-09-14: nothing found" is true of an hour, not of a project, and it is refused at the door — measured on two live projects, a folder of run logs is read first by every later run and is followed by hours that ship nothing.
- 🔴 NOT A STANDING ORDER TO WAIT.

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/write_context' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

### Response

```json
{
  "ok": true,
  "result": "<result>",
  "duration_ms": 0
}
```

### Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |

<!-- /widget -->
