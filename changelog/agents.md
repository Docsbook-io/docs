---
title: "What changed in Docsbook Agents, and when it shipped"
description: "Every release that touched Agents: the goals your project pursues on its own, the route of MCP calls each one walks, what wakes them, and the history of every run."
---

# What changed in Docsbook Agents, and when it shipped

Everything that shipped in **Agents**. This is the Agents slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG).

## NEW - 05.09.2026

### Added

- Agents now leads with a **Last Runs** shelf — the six most recently invoked agents, including ones you started by hand without arming them — so "what just ran" is answered before you go looking through the list. `Agents`

## NEW - 04.09.2026

### Added

- An **Agents** section in the admin panel: forty goals your project can pursue on its own, each one an ordered route of subagents rather than a single call, with what it is for, the number it is bought to move, and what a run costs before you arm it. Recurring documentation work you were doing by hand every week can now be handed to a schedule. `Agents`
- Arm one on a schedule you read as a sentence in your own clock: how often, which days, at what time, with the next run printed underneath in the same clock. The six presets it replaced were labelled in UTC, so checking one meant converting in your head, and "Tuesday and Thursday at nine" could not be asked for at all. `Agents`
- A **Runs** tab beside the catalog answers "did anything run last night, and did it hold up" of the whole project. That history used to be reachable only from inside one agent's settings, so the question could only be asked forty times. `Agents`
- Agents can now be armed to run every hour, not just once a day at the fastest. The schedule sentence gained an **Hourly** option that asks which minute past the hour rather than a time of day, for work that should not wait for tomorrow's run. `Agents`

### Changed

- A run's transcript opens as its own table of contents, every station closed. Which stations ran, which held up and how long each took now fits on one screen instead of being spread over forty screens of prose. `Agents`
- Which sources an agent may read is one picker that says what an empty pick means, instead of a wall of toggles as tall as the number of sources you are not choosing. `Agents`
- **Start agent** now sits at the top of an agent's panel, beside Close, reachable from Overview as well as Runs, instead of only appearing once you switched to the Runs tab. `Agents`
- The trigger's "On a schedule / On an event / ..." control is now sized to match the detail underneath it, with the dividing line between them removed, so the two read as one card rather than two stacked controls. `Agents`
- Pressing **Improve** or **Analyze** anywhere in the panel — a reader row, a goal, a funnel step, a commit — now starts the agent that fits what you were looking at, carrying what was already on screen as that run's own instruction, and opens the run to watch live: a clock that keeps ticking while it works, and the instruction it started from shown apart from what it did. The button used to just copy that text to your clipboard, from when it opened a chat that no longer exists. `Agents`
- The price shown for an agent's route, and for one subagent call in it, now reads **up to** instead of a bare figure. It is still exact for the metered calls themselves, but a run also spends from your AI balance on the model turns it makes, which is billed separately and can push the real cost above the number shown. `Agents`
- The **Runs** tab reads as a feed of what your agents actually did. Each run is a card carrying its own route: one line per station saying what that station established, the pull requests and issues it opened at the foot of it, and a divider each time you scroll back into an earlier day. Catching up on a week of agent work is a minute of scrolling now, instead of opening every run in turn to find the one that shipped something. `Agents`
- Each card in the **Runs** feed now reads like a post rather than a table row: a bigger mark and name for the agent as its author, the run's own finding promoted into a lead line under it, and its route redrawn as a connecting timeline instead of a column of touching marks — so what an agent did is legible without opening the transcript. `Agents`

### Fixed

- A station with nothing to report no longer fails the whole run. On a project with no Search Console history and no in-doc searches, a station that correctly answered "there is no intent mismatch to explain here, and here is each check I could not make and why" was refused three times over and stopped the route, so an agent could not finish on exactly the projects it had least to invent about. `Agents`
- A run whose hand-off went missing no longer spins for ever. The route is driven inside its own request, and anything still open is picked up within five minutes or reported as failed with the reason, so nobody has to watch a run to find out it stopped. `Agents`
- Clicking the schedule's time no longer leaves it unclear what you are about to change. It is now the browser's own time control, in place of an invisible layer that gave no sign of which part a click had landed on. `Agents`

## NEW - 24.08.2026

### Fixed

- The MCP install commands, raw config and example questions are usable without an account, matching the public MCP page they mirror. `Agents`
- Opening an MCP tool or a skill no longer hides its catalog for the rest of the session — the breadcrumb goes back, and a failed catalog load retries when you reopen the page. `Agents`

## NEW - 22.08.2026

### Added

- The `Agents` tab has a new `MCP` page listing every tool this project's MCP server serves — read live from the server, so it is never a stale copy — with each tool's description, its arguments, and the sentences to say to a connected agent to make it fire. `Agents`
- The `MCP` page marks the four tools a client can reach with no token at all, so you can see what a reader of your docs could call, not just what you can. `Agents`
- The `Agents` tab has a `Skills` page: every docs skill from the published catalog with its plan gate, install line, the sentences that trigger it, the MCP tools it calls, and its full instructions. `Agents`

### Changed

- The `Agents` tab now drills into a catalogue of every docs-subagents agent grouped by pipeline; picking one lists its ready-to-run prompts instead of a single shared MCP-connection card. `Agents`
- Tool, agent and skill names across the `Agents` tab read as names (`Docs Planner`, not `docs-planner`), with the machine id kept verbatim under each title. `Agents`

## Related

- [Full Docsbook changelog](../CHANGELOG.md) — every release, across every section
- [MCP server](../ai/mcp.md) — the calls an agent's route is made of
- [Changelogs by panel section](./README.md) — the same releases, cut by where they landed
- [Changelogs by outcome](./outcomes/README.md) — the same releases, cut by the number they move

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: add the entry to the general changelog with its component tag and rerun the script. -->
