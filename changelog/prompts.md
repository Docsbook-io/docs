---
title: "Prompts changelog"
description: "What shipped in the Docsbook prompt library — the catalog of prompts your agent can run, the wording your workspace overrode, and what runs on a schedule."
---

# Prompts changelog

Everything that shipped in **Prompts**. This is the Prompts slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG).

## NEW - 03.09.2026

### Added

- The prompts listed under a tool can be searched once that tool has more than a handful of them, so finding the right example is reading one line instead of scrolling the list. `Prompts`

## NEW - 02.09.2026

### Added

- Copying a prompt from the Prompts table now appends what the receiving assistant cannot know: which project it is about, the project's docs URL and repository, the Docsbook MCP endpoint, the tools that prompt calls, and an instruction not to invent what only those tools could have answered. The same sentence pasted into Claude, ChatGPT, Cursor or Codex used to read as a request about no particular site. The note is composed at the clipboard only — it is never stored and never sent on a scheduled run. `Prompts`

## NEW - 01.09.2026

### Added

- A **Sources** column on the Prompts table, and the same chips under an MCP tool's description, showing which of your sources that particular run can actually read — lit where it fetches them, unlit where it only knows they exist, and blank where the run reaches no source at all. `Prompts`

## NEW - 31.08.2026

### Added

- A prompt can now be armed on one of your saved feeds instead of a single event, so it runs whenever anything lands in that feed — the same set of events the feed already shows you, chosen once on the page where you watched them arrive. The **On event** picker lists your feeds above the individual events, each with what it covers. `Prompts`

## NEW - 30.08.2026

### Added

- Every prompt in `Prompts` now suggests what to arm it with. The suggestion is read from your own prompt — its wording, its tools, its tags — and says which part it read, so it is a shortcut you can check rather than one you have to undo later. Both pickers open with it, because "run this when the docs change" and "run this every Monday" are answers to the same question. `Prompts`
- The event picker now offers every event your workspace can actually react to, in plain words with the machine name under them, grouped the way `Feeds` groups the same events, with a filter box pinned above a list that is now past forty. `Prompts`
- Every prompt in `Prompts` now shows what one run is worth, in a **Cost** column: the MCP calls it makes plus the model turns around them, so a prompt costing a fraction of a cent is told apart from one costing a quarter of a dollar before you put it on an hourly schedule. `Prompts`
- Beside it, an **Impact** column says what running it typically moves and which way — support load, upkeep hours, manual watching, time to an answer, citations, markets, traffic, conversion — green for up and red for down, where down is the good one on anything that costs you. `Prompts`
- Both are estimates of what prompts of that kind do, and both say so when you hover them: neither is a reading off your own workspace, and the cost hover breaks the figure into the calls and the turns it is made of. `Prompts`
- `Prompts` gained an **Impact** menu of its own beside **Filters**, for the prompts that move one particular thing — support load, upkeep hours, manual checks, time to an answer, citations, markets, traffic, conversion. It asks what you are trying to move rather than what a prompt is about, so a support inbox on fire collects the prompts that help with it whatever they are tagged and whether or not you have ever touched one. Picking two means either would help, not both at once, and every family carries the count it would leave. `Prompts`
- The Impact chip on a row is the same narrowing, so pressing one is the shortcut to the menu. It narrows by the kind of payoff, never by the size of it. `Prompts`

### Changed

- `Prompts`' Run, schedule and trigger controls are now named buttons in the toolbar (**Run now** / **Schedule** / **On event**) that ask which prompt first, instead of three small icons that only appeared while hovering a row. The four state filters (Automated, Edited, Mine, Has run) moved into **Filters** alongside everything else that narrows the table. `Prompts`
- Hovering a prompt in `Prompts` now opens a card that carries every action the row has, each with its name beside the icon: Copy, Edit, Trigger, Schedule, Transcript and Run. The row's icons only exist while the pointer is on the row, so reading the full wording used to take them all away and leave copying as the only thing you could do with what you had just read. It is also the first place the panel says in words what the pencil, the bell and the clock do. `Prompts`
- A prompt that already runs on a schedule or fires on an event now shows that on those two buttons in blue, in the card and on the row. The colour was there in the code and had never actually rendered, so a prompt already working by itself looked the same as one that had never been set up. `Prompts`
- The `Tags` column in `Prompts` is now off by default, one click away in the **Columns** menu. The prompt itself already says what it is about in the widest column on screen, and the **Filters** menu keeps every label — including the ones a truncated cell never showed — so narrowing by one is unchanged. `Prompts`
- The `Tools` column in `Prompts` is now off by default too, alongside `Tags`. The chips named which endpoints the agent would reach for, and both questions you actually decide on — the price and the payoff — are computed from that same list, with the cost hover naming the dearest thing the prompt touches. Every tool is still listed in the row's card, and the column is one click away in **Columns**. `Prompts`
- The figures in the Impact column are smaller and more careful than they shipped this morning: single digits and low teens rather than numbers in the thirties and forties. They are what a documentation change plausibly moves, not what a landing page would claim. `Prompts`

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: add the entry to the general changelog with its component tag and rerun the script. -->
