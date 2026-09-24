---
title: "Agent memory: what the docs agent knows about your product"
description: "The Docsbook agent keeps a folder per organization of what it learned about your product. See what's in it, tell it facts in chat, and read it from your editor."
---

# Agent memory

The Docsbook agent keeps a folder of what it has learned about your product — one per organization — reads it before every run, adds to it as it works, and answers you out of it.

## What's in the folder?

Eight fixed folders, each answering one question:

| Folder | On the card | What it holds |
|---|---|---|
| `product/` | Product | What this business is, what it charges, what it never claims |
| `audience/` | Audience | Who reads the docs, what job they are on, what they already know |
| `conventions/` | House style | How a page must read here — voice, words used and never used, structure |
| `memory/` | Memory | What the next run would otherwise work out again from scratch |
| `decisions/` | Decisions | What you settled, when, and what it closes |
| `hypotheses/` | Under test | What might be true, which reading decides it, and by when |
| `questions/` | Open questions | What could not be worked out here, and who can answer it |
| `playbooks/` | Playbooks | How this kind of work is done well here — what was tried, what held |

Each entry is a short Markdown file: a title, the claim itself, the evidence it rests on, and how it is known — `observed`, `inferred`, or `told` by you.

## Whose folder is it?

A project shares its folder with every project of the same owner:

- **A project in a Docsbook organization** uses the organization's folder.
- **Any other project** uses the folder of its repository's GitHub owner, kept separately for each Docsbook account.
- **A project Docsbook hosts for you**, with no GitHub account, uses your personal folder.

Inside, `product/pricing.md` is true of the whole organization, and `projects/41/product/pricing.md` is true of project 41 alone and overrides it. One agent working on six projects of one company learns what they share once.

## Tell it something

Say it in the admin chat. The agent files it, marked as told by you, and says back in one line what it kept and where:

```text
Remember: our Starter plan includes 3 seats.
Remember for this project only: the v1 endpoints are deprecated.
We decided to drop the Windows installer — note that down.
The spring sale runs until Friday; check that note again next week.
What do you know about our audience?
Forget the note about the old pricing page, it's gone.
```

A plain fact lands in `memory/` or `product/`, a settled choice in `decisions/`, a rule about writing in `conventions/`. Anything that expires gets a date and comes back for a second look instead of being read as true for ever; "forget" retires an entry rather than deleting it.

## What the agent writes on its own

Every run starts from the folder and ends by adding to it:

1. **Lists the folder first** — titles and dates only — and opens the few entries that bear on the job.
2. **Searches it before proposing anything**, so an idea you already settled or already tested is not brought back.
3. **Writes what stays true**: where the real pricing page is, which words your product never uses, what you decided.
4. **Files a claim before testing it**, in `hypotheses/` with a date to re-check, and closes it later as `confirmed` or `rejected`.
5. **Checks its own log before it stops** that it wrote down what it learned.

Two rules keep the folder useful. An entry named after an hour — `run-2026-09-14`, `cycle-3` — is refused, because a diary of runs teaches the next run nothing. And every open claim in `hypotheses/`, like every entry in `questions/`, carries a date to look again, between 1 and 365 days out.

<!-- widget:callout type=tip -->

**Overview ▸ Docsbook agent** counts the entries in each folder, says when the agent last learned something, and shows how many are due a second look — entries whose date to look again has passed.

<!-- /widget -->

## Read it from your editor

On [your MCP connection](../get-discovered.md), the five folder tools are reached through `call_tool` — `find_tool` names them:

- **`list_context`** — every entry's path, title and date, no contents.
- **`search_context`** — entries matching your words, with a short extract each.
- **`read_context`** — one entry, whole.
- **`write_context`** — add or replace an entry; pass `confidence: "told"` for something you are telling it.
- **`retire_context`** — take an entry out of what later runs read; it stays findable.

A `call_tool` request that records one of your decisions:

```json
{
  "name": "write_context",
  "arguments": {
    "workspace_id": "acme/docs",
    "path": "decisions/no-windows-installer.md",
    "title": "The Windows installer is discontinued",
    "body": "We stopped shipping the Windows installer. Point Windows users to WSL instead.",
    "confidence": "told"
  }
}
```

The call writes an organization-wide decision; a path under `projects/<id>/` would make it true of one project only.

## Limits

- **No export.** No tool returns the folder whole, and a listing carries titles and dates, never contents.
- **An hourly reading ceiling** per account or agent run: 40 entries and 120,000 characters, of which at most 6 from `playbooks/`.
- **Entry size** — 200 characters for a title, 4,000 for the body. A folder holds up to 600 entries and warns from 240.

## When a project changes hands

Give a project away with a claim link and its own entries — everything under `projects/<id>/` — move to the new owner's folder, with its audit verdicts. Organization-wide entries and your [skills](./skills.md) stay with you.

## FAQ

**Is the folder the same as the AI chat's knowledge?** No. The [AI chat](../ai-chat/README.md) on your site answers readers from your published pages; the folder is for your agent and for you.

**Can I change what the agent wrote?** Yes. Tell it in the admin chat — a newer fact replaces the old entry and keeps the date it was first learned — or call `write_context` or `retire_context` from your editor.

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [Skills](./skills.md) — Turn a house rule into a way of working the agent follows {sparkles}
- [Sources](./sources.md) — Give the agent the code and sites to learn from {plug}
- [Tell your agent, get discovered](../get-discovered.md) — Connect Claude Code, Cursor or Codex {terminal}
- [A second brain for your product](./README.md) — How memory fits with pages, sources and skills {network}

<!-- /widget -->
