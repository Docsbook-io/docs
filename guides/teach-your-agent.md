---
title: "Turn your team's knowledge into your AI agent's memory"
description: "Write one block for CLAUDE.md, AGENTS.md, Cursor rules or a ChatGPT or Claude project that tells your agent which Docsbook project answers which question."
---

# Teach your agent where your knowledge lives

Paste one block into your agent's memory — `CLAUDE.md`, `AGENTS.md`, a Cursor rule or a ChatGPT or Claude project — and it asks the right Docsbook project on the first try, instead of grepping the code, answering from memory or asking you which project to use.

Connecting the [Docsbook MCP server](../get-discovered.md) gives your agent a list of tools, not a map. Nothing in it says that "what does the refunds spec say" is a question for your Specs project and not for the code. The block is that map.

<!-- widget:callout type=note -->

This is the memory of **your own** agent. What the Docsbook agent keeps about your product is a different thing, its [memory folder](../brain/memory.md), and you fill that one by telling it facts in chat.

<!-- /widget -->

## What goes in the block

Six things, each in your team's own words:

- **Projects** — which Docsbook project holds what, by numeric id, with two or more real example questions each.
- **When to look unprompted** — before implementing a ticket, before changing something customers see, and when not to bother.
- **How to search** — one project at a time, what "the latest" means here, and what to do when nothing is found.
- **How to answer** — a link for every claim, how to treat unapproved pages, which source wins when two disagree.
- **Vocabulary** — codenames and abbreviations, mapped to a project and section.
- **Never** — what must not leave a private project, and whether the agent may change docs.

## Before you start

- **The projects exist.** If your specs and docs are still folders in a codebase, [integrate the project](./integrate-your-project.md) first; its final table of projects is this guide's input.
- **Your agent is connected** to Docsbook as the account that **owns** those projects. A connection reaches only its own account's projects, so a block pointing at a teammate's project fails on the first question.

## 1. See what can be searched

Ask your agent "What can you search in our Docsbook projects?" and have it build a topic map: for each project, its id, visibility, page count, how many pages are approved, and three to seven topics named the way its own titles name them.

> **Acme — Specs (512)**, private, 84 pages, 12 approved: billing, authentication, notifications, onboarding, rate limits.

It gets there with `list_workspaces` and one `get_project_doc_outline` per project. The outline reads every page, so it is slow — once per project is enough.

## 2. Settle what only your team knows

The block is only as good as these answers, so take them from the team, not from a guess. Have your agent propose an answer to each and let you confirm or correct it:

<!-- widget:accordion -->

### Which projects, and what each is for

The confirmed list, one sentence of purpose each, in your words — and which projects the agent should not know about.

### What people actually ask each project

Three to five phrasings per project, plus two or three questions somebody really asked last week. Those become both the block's examples and its test in step 4.

### When to look without being asked

For example: before estimating or implementing a feature → Specs and Stories for it; before changing an API, a limit or UI copy → the public docs, to see what was promised; on "how do we…", "what did we decide…", "where is it described…". And when not to: general programming, what the code in front of the agent already answers.

### Which source wins, and what "latest" means

The order when two disagree — for instance an approved spec over a story, a story over the public docs, the code as what actually runs. How your files mark freshness: a date prefix like `2026-09-12-refunds.md`, an ADR number, a `version:` in frontmatter. Whether unapproved pages count, labelled as drafts, or are ignored.

### Your vocabulary

Every codename, product name and abbreviation the agent will not know, mapped to a project and section: "Atlas" → Internal, `architecture/`.

### Boundaries and answer form

Whether the agent may change docs (the usual answer: no, only through the Docsbook agent when asked). What never leaves a private project. The answer language, the citation style, and the sentence to say when nothing is found.

<!-- /widget -->

## 3. Write the block

Here is a finished block for Acme's four projects. Keep its structure and fixed heading; replace everything Acme-specific with your answers:

````markdown
## Docsbook — where Acme's knowledge lives

Acme's knowledge lives in Docsbook, organization "Acme", one project per kind of document. The Docsbook MCP server is connected as `docsbook`. Before saying what we decided, described or promised, look there. Do not answer from memory, and do not infer it from the code.

### Projects

| What | Project (workspace_id) | Visibility | Holds | Send it questions like |
|---|---|---|---|---|
| Specs | Acme — Specs (512) | private | What we decided to build and why: behaviour, limits, edge cases | "what does the spec say about refunds after 14 days", "latest specs on notifications" |
| Stories | Acme — Stories (513) | private | User stories and acceptance criteria per feature | "acceptance criteria for CSV export", "what can an admin do in roles" |
| Docs | Acme — Docs (514) | public | What customers read: setup, API, pricing | "what do we promise about API rate limits", "how is the payment webhook documented" |
| Internal | Acme — Internal (515) | private | How it is built and run: architecture, runbooks | "how does the billing worker work", "what to do if the mail queue stalls" |

### Look without being asked

- Before estimating or implementing a feature → Specs and Stories for it.
- Before changing anything customers see (API, copy, limits, prices) → Docs: what did we promise?
- On "how do we…", "what did we decide…", "where is it described…" → the project from the table.
- Code contradicts a page → say so and quote the page.

Do not look for: general programming questions, what the code in front of you answers, small talk.

### How to search

1. Pick the project from the table and the vocabulary. A question about two projects is searched in each, separately; say which part came from where. There is no single call across projects.
2. Call `search_project_docs` with the project's `workspace_id` and the whole question, as the person asked it. For an exact string — an error code, a flag — use `search_docs`.
3. The result carries an `answer` and the pages it used. Use it with the pages' `url`s. Open a page in full with `read_project_doc` only to quote it or when the answer is thin.
4. "The latest…": the `YYYY-MM-DD` prefix in the file name decides; ADRs go by number. For what changed, run `git -C specs log -10 --date=short --format='%ad %s' --name-only` in the checkout.
5. Nothing in the first project → try the next the table suggests. Nothing anywhere → say "not in Docsbook" and name the project where it belongs. Never fill the gap from memory.
6. "What is in <project>?" → `get_project_doc_outline`. It is slow; use it only for an inventory.

### How to answer

- Every claim links to its page.
- `read_project_doc` returns `lifecycle`. `agent_may_build_from: false` means nobody signed the page off: use it and say "not approved". Build code, estimates and tickets only on `approved` or `locked` pages.
- Sources disagree → an approved spec beats a story, a story beats the public docs, the code shows what runs. Name the conflict with both links; never pick one silently.
- Answer in English.

### Vocabulary

- "Atlas" → Internal / `architecture/atlas-*` (the API gateway)
- "portal", "B2B portal" → Specs / `b2b/`
- "billing", "refunds" → Specs / `billing/`; the public side → Docs / `pricing/`

### Never

- Nothing from Specs, Stories or Internal goes anywhere public: public docs, issues and pull requests in public repositories, public commit messages, answers to customers.
- Do not change docs unless asked. Changes go through `docsbook_agent`, and a person approves them.
- Never quote a page the search did not return, and never describe a spec you did not read.
- Docsbook tools missing or failing → say Docsbook is not connected or not answering, and stop rather than guess.

Each search is answered by the Docsbook docs agent and spends the project's balance: one well-formed question beats five fragments.
````

What makes a block work:

- **Numeric ids** in the table. A renamed project breaks a name, never an id.
- **Real example questions**, at least two per project, in the team's words and language. The next session matches against them.
- **Short.** It loads into every session: aim for 60–90 lines and about 6,000 characters. Cut explanation before examples.
- **No secrets** — no MCP token, site password or API key. It is text every session reads.
- **The private line** whenever any project is private.
- **The fixed heading**, so running this again replaces the block instead of adding a second one.

If your agent does not work inside a checkout with the folders as submodules, replace the `git log` line with `read_source`, `source_id: "workspace_repo"`, `commits: true` — the last 10 commits of the repository the project is built from.

## 4. Test it on real questions

Take three to five of the questions people actually asked in step 2. For each, route it with the block's own table and vocabulary, exactly as a new session would, run one search in the chosen project, and write down what came back:

| Question | Routed to | Top page | Answered? |
|---|---|---|---|
| "what does the spec say about refunds after 14 days?" | Specs (512) | Refunds — `billing/2026-08-12-refunds.md` | yes |
| "what do we promise about API rate limits?" | Docs (514) | Rate limits — `api/rate-limits.md` | yes — and the spec says 50 rps where the docs say 100, so the conflict is named |
| "latest specs on notifications" | Specs (512) | a 2025 page ranked first | fixed: added the date-prefix rule, asked again |

A question that routes nowhere, routes to two projects with no rule, or finds nothing where you expected an answer means the block is wrong. Fix the row or the vocabulary and ask that question again.

## 5. Paste it

Append the block to the file your agent loads; never overwrite the file. If an older block with the same heading is there, replace it.

| Agent | Where |
|---|---|
| Claude Code | `./CLAUDE.md` for this repository, or `~/.claude/CLAUDE.md` for every one |
| Codex | `./AGENTS.md`, or `~/.codex/AGENTS.md` |
| Cursor | `.cursor/rules/docsbook.mdc`, with `alwaysApply: true` in its frontmatter |
| A Claude or ChatGPT project | The project's instructions |

## Tell your agent

Paste this into the agent that will use the block:

```text
Read docsbook.io/guides/teach-your-agent and set up your memory for our Docsbook projects.
Show me what you can search first, then ask me the questions one topic at a time,
test the block on questions I give you, and hand it to me. Do not write the file yourself.
```

## FAQ

<!-- widget:accordion -->

### Can the agent search all our projects in one call?

No. Each search runs in one project, which is why the block routes a question to a project first and says what to do when it spans two.

### Does each search cost anything?

Yes, a little. On your own connection, `search_project_docs` is answered by the Docsbook docs agent — it reads the pages and writes an answer — and that spends the project's balance.

### Can teammates use the same block?

The private projects answer only the owning account's connection, so a teammate's agent on their own account gets nothing from them. Public projects work for anyone through each site's [public MCP server](../brain/mcp-server.md), whose tools are named after the project's repository (`search_<slug>_docs`).

### When do I redo it?

When a project is added, renamed or made private. After a week of use, ask which questions went to the wrong project: each one is a missing example or vocabulary line, not a reason to rewrite the block.

<!-- /widget -->

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [Integrate your project](./integrate-your-project.md) — Turn the folders of specs and docs in your codebase into Docsbook projects {git-branch}
- [Tell your agent, get discovered](../get-discovered.md) — Connect Claude Code, Cursor or Codex to Docsbook {terminal}
- [Agent memory](../brain/memory.md) — What the Docsbook agent itself remembers about your product {brain}
- [MCP server for your docs](../brain/mcp-server.md) — What anyone's agent can read from a public site {plug}

<!-- /widget -->
