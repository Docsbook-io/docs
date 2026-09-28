---
title: "Goals and funnels for documentation: track what readers do"
description: "Define goals for what a docs reader should do, chain them into funnels, and see where the route breaks, who converted and how long it took."
status: generated
version: "0.2"
---

# Goals and funnels

A **goal** is one thing you want a reader to do — reach a section, open a page, copy a snippet, leave for your app — and a **funnel** is goals in the order you expect them.

Both are counted from visits Docsbook already recorded, so a goal you add today shows the last 30 days at once, with nothing to add to your pages.

## What can a goal count?

| In the panel | `kind` | It matches | Example |
|---|---|---|---|
| **Reached a section** | `section` | A heading that scrolled into view | `#pricing` |
| **Viewed a page** | `page` | A page path | `/quickstart` |
| **Did something** | `event` | An event your docs emit | `docs.copy_code` |
| **Left for a site** | `outbound` | A host readers clicked out to | `app.example.com` |

A goal counts once per visit, however often it fires: a reader who scrolls past `#pricing` five times is one completion. An `event` goal can be limited to one page, so "copied the quickstart snippet" and "copied the auth snippet" are two goals.

## Set up your first goal

<!-- widget:stepper -->

### Open Goals & funnels

Go to **Analytics ▸ Insights** and scroll to the **Goals & funnels** card. Press **+**, or **Create your first goal** on an empty card.

### Name it for what the reader did

Type a name such as `reached_pricing`, in lowercase with underscores. The name is fixed once saved, because funnels and the agent refer to the goal by it.

### Choose what counts

Pick **Reached a section**, **Viewed a page**, **Did something** or **Left for a site**, then choose from the list: headings readers scrolled to, pages your docs served, every event your docs emit, or hosts readers left for.

### Add a worth, or leave it empty

**Worth (optional)** is what one completion is worth in dollars. Leave it empty unless you can defend the number: an empty worth keeps money figures off instead of showing a guess.

<!-- /widget -->

Rather not choose? **Generate with AI** on an empty card has the agent read your docs, create three to five goals — reaching pricing, copying the install snippet, clicking through to your app — and say why each is worth measuring.

## How do funnels work?

A funnel is two to eight goals in order, and a visit reaches step N only if it passed steps 1 to N in that order. Press **+** on the **Funnel** tab to build one: a name, the steps, and an optional conversion window in hours.

- **Start broad** — most readers arrive deep from search or an AI answer, so a single page as step 1 drops them before anything is measured
- **End on a real outcome** — a click out to your pricing or signup page, not a scroll
- **Keep it short** — more than 5 steps brings a warning, more than 8 is refused
- **Leave the window empty** — the visit itself is then the window, the honest default for docs

The **Funnel** tab labels the drop-off at every step and names the worst transition: "The route breaks going into …". Under 30 visits into a step, it shows counts instead of a rate.

## Where do the numbers show?

The **Goals & funnels** card on **Analytics ▸ Insights** reads your goals three ways:

- **Goal** — completions of all goals in the window as one line, with the change against the previous week; the list beside it ranks each goal by **Reached**, **Rate** and **Potential**, and hovering or clicking a goal charts it alone
- **Funnel** — the route as a narrowing flow; hover a step for its conversion, its value and its top sources and countries
- **Journey** — everyone who reached one goal, what they touched on the way and how long it took; the median and p90 appear once five readers have completed it

**Activity ▸ People ▸ Users** lists the readers behind the completions — one row each, sorted by **Potential**, with outcomes per reader — and feeds **Potential** back into the Goals & funnels card.

## What the agent does with goals

- **Sets them up** — **Generate with AI** creates goals from your docs; on the **Funnel** tab it maps how readers move, then declares the route
- **Works a weak goal** — **Improve** on a goal row traces the route readers took to it, compares readers who reached it with those who did not, and first checks that the goal can fire at all
- **Works a leaking step** — **Improve** on a funnel step, or on the "route breaks" note, asks why readers stop there and what would carry them on
- **Answers questions** — ask the [Docsbook agent](./README.md) "who reached pricing this week, and from where?" and it reads the goal reports for you

## Set goals from your own agent

Six goal tools are on the Docsbook MCP server your Claude Code, Cursor or Codex connects to ([Tell your agent, get discovered](../get-discovered.md)):

| Tool | What it does |
|---|---|
| `list_goals` | Lists your goals and funnels and what each matches — call it first |
| `create_goal` | Takes `key`, `kind`, `match`, and optional `match_path`, `label`, `value_usd` |
| `edit_goal` | Changes a goal's label, match or worth; the `key` stays |
| `delete_goal` | Archives a goal, so funnels that name it keep their steps |
| `create_funnel` | Takes `key`, two to eight goal names as `steps`, and optional `label`, `window_hours` |
| `mark_path_as_funnel_step` | Adds a page to a funnel as its next step, creating the goal and the funnel if needed |

The owner server declares goals; it does not read their numbers. Read them in the panel or ask `docsbook_agent`. Every tool is in the [MCP tools reference](../mcp-tools/README.md).

## FAQ

**Why was my goal refused?** Definitions that could never measure anything are refused: an `event` goal naming an event your docs never emit, a worth of `0` (leave it empty instead), a funnel step naming a goal that does not exist, or a funnel with fewer than 2 or more than 8 steps. Softer problems — a single page as step 1, a funnel ending on a scroll, more than 6 goals — come back as warnings you can save past.

**Do goals cost anything?** Defining goals and funnels works on every plan. Reading the **Goals & funnels** reports needs Pro, which the 14-day trial includes — see [Plans and pricing](../pricing/plans.md).

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [Docs analytics](./insights.md) — Traffic, AI visitors and revenue per page {chart-line}
- [You hear every reader](./README.md) — Feedback, failed searches, dead ends and the agent loops {message-square}
- [MCP tools reference](../mcp-tools/README.md) — Every tool your own agent can call {terminal}
- [Tell your agent, get discovered](../get-discovered.md) — Connect Claude Code, Cursor or Codex {plug}

<!-- /widget -->