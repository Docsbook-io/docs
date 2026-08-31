---
title: "Feeds changelog"
description: "What shipped in Docsbook Feeds — the live event stream from your docs site and the webhooks that carry it somewhere else."
---

# Feeds changelog

Everything that shipped in **Feeds**. This is the Feeds slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG).

## NEW - 31.08.2026

### Added

- **Set up Prompt** sits beside Set up alert on the feed's toolbar, with a count of what is already running on this feed. An alert forwards the feed to a person; a prompt hands it to your assistant to act on, and now both are one glance apart instead of two screens. `Feeds`
- Each prompt watching a feed gets a chip on that toolbar — filled while it runs, hollow while it is paused, its last run in the tooltip — and clicking one opens the conversation the prompt has been having on its own, so you can see what it actually did rather than only that it is switched on. `Feeds`

### Removed

- The **Usage** button has left the feed's toolbar. The breakdown itself has not moved: **See usage** on the sidebar balance card still opens it. It is about the whole project over a window, while every other control on that row acts on the feed in front of you. `Feeds`

## NEW - 30.08.2026

### Added

- `Feeds` gained a **Usage** button that swaps the live stream for the sum: what this project's money went on over a window, dearest first, as three tables — every AI answer, translation and indexing run by model, every MCP tool call by tool, and every event by type. A price on one row at a time was never a column anybody could add up. `Feeds`
- The two figures above those tables are kept apart on purpose. AI answers and MCP calls are **charged** — that money came off your balance — while events are **priced** so the traffic is not invisible and nothing is deducted for them, and every section says which it is. One total covering both would be a bill for money nobody took. `Feeds`
- Pick a window of **24 hours**, **7 days** or **30 days**, and export what you are looking at: the breakdown itself as a spreadsheet, with each line's cost as a number you can sum and a column saying whether it was charged, or the raw events behind it bounded by the same window. `Feeds`

### Changed

- `Feeds` now lists feeds as rows in the sidebar with a one-line toolbar of icon filters and an always-visible search box, instead of a separate picker page. `Feeds`
- A pinned reader's goal chips in `Feeds` now say WHEN each goal was reached, so a conversion on the card points at the row in the stream underneath it. `Feeds`
- The `Feeds` toolbar no longer carries a running "1,204 of 7,279" count or a second, icon-only button for creating a notifier — `Set up alert` is the one way to make one, and it now also lists the destinations you already have, including any attached to nothing. `Feeds`
- `Feeds` rows are tighter, fitting noticeably more of the stream on a screen without changing what a row says. `Feeds`
- `Feeds` now filters events with three separate chips — Workspace, MCP and Analytics — each opening only its own catalog, instead of one menu you scrolled past two stores to use. `Feeds`
- MCP traffic in `Feeds` is now filterable per tool as well as per price class, so one filter can mean the expensive half of a single tool's calls. The narrowing rides the export and saved lists too, so a downloaded file matches what was on screen. `Feeds`
- The second built-in feed in `Feeds` is now **Reader events**, everything the people reading your docs did: pages read, searches run, questions asked of the AI and feedback left. It replaces **Unanswered questions**, which only filled up where an answer came up empty; those two event types are still one click away in the Workspace filter. `Feeds`
- `Feeds` opens on a page of cards again — one per built-in feed plus your own saved lists, each with a line saying what it holds — instead of straight onto the unfiltered stream. The sidebar list from earlier today is still there for switching feeds without leaving one, but now starts closed behind a chevron on the `Feeds` row, remembering whether you left it open. `Feeds`
- Three feeds joined the built-in roster: **Translations** (every language generated, outdated or still needed), **Language events** (which languages readers switch the docs into) and **Chat events** (questions the AI assistant was asked, where it came up empty, which answers got a thumbs-down). `Feeds`

## NEW - 28.08.2026

### Added

- Narrowing a feed to one reader now puts a card above it saying who that reader is: their country, device, system and browser, the language they actually read in, the page they keep coming back to, how long they have spent reading your docs in total, the goals they have reached, and what they are worth today as well as what they might still be. A stream of pageviews under a pseudonym could not answer "who is this". `Feeds`

### Changed

- `Feeds` now opens on **Select a feed**: a card for each feed with a line saying what it holds. Four are built in — All events, Unanswered questions, Reader feedback and Delivery trouble — so there is something to open before you have saved anything of your own. `Feeds`
- Saved feeds now live on that page instead of the sidebar, where each one had room for its name and nothing else. Every card says what its feed narrows to, shows a dot when a destination already fires on it, and carries its own delete. `Feeds`
- The event feed is now one line per event instead of a card, so a day of events fits on a screen and can be scanned rather than scrolled. Clicking a line still expands the full payload and every delivery attempt underneath it. `Feeds`
- Event times in the feed are now clock times, since the day is already named by the section above them. `Feeds`
- Filtering the feed now offers each facet by name — **Add event**, **Add visitor**, **Add goal**, **Add status**, **Add destination**, **Search payload** — instead of one **Add filter** button that kept the choices a click out of sight. `Feeds`
- Webhooks are no longer counted against a per-plan cap: a paid plan registers as many feed notifiers as it needs, and Free has none. `Feeds`

### Improved

- Event rows in the feed now carry their own icon instead of sharing one per category — reading time, a page view and a heading view no longer draw the identical glyph, and neither do leaving the site and clicking an outbound link. `Feeds`

### Fixed

- Filtering `Feeds` by a visitor now finds that reader's events. It searched only the events your docs dispatched — nearly all of which belong to the project rather than to any one reader — and answered "Nothing matches this filter" about readers who had been active all along. It now searches what that reader did on the site as well, across the whole window rather than the most recent few hundred events. `Feeds`
- Goal events in `Feeds` now carry their goal's colour. The tint only appeared for goals with a colour set by hand, which almost none have, so for most projects it silently never showed at all. `Feeds`

## NEW - 26.08.2026

### Added

- `Feeds` can now filter the docs site's own analytics stream — page views, searches, chat questions and more — as an opt-in category alongside webhook events. `Feeds`

## NEW - 25.08.2026

### Changed

- Feeds cards now lead with the reader's avatar when one caused the event — click it to filter by them — collapse status/type/destination into tappable glyphs, and expand in place instead of opening a separate view. `Feeds`

## NEW - 23.08.2026

### Added

- `Feeds` can now filter by a single visitor or by whoever completed a goal — open a reader in `Analytics` and jump straight to everything they did in `Feeds`, or paste in an id by hand. `Feeds`

### Changed

- `Feeds` puts `Export` and `Set up alert` in one row beside the list's name, as identical buttons. `Feeds`
- Each row of the `Add notifier` menu now has an edit control, so a destination attached to another list — or to none yet — can be opened without hunting for it. `Feeds`
- `New list from current filter` in the `Feeds` sidebar is now just `New List`. `Feeds`
- `Feeds` is live now: the panel refreshes itself every few seconds while it's open, instead of showing a fixed window you had to pick. `Feeds`

### Removed

- The three summary tiles above the `Feeds` feed (all activity, needs attention, failed deliveries) — `failed` moved into `Add filter` under `Delivery status`. `Feeds`
- The `Notifiers` group in the `Feeds` sidebar, and with one group left, the `Events` heading above the lists. Destinations are reached from the chips beside the filters, from `Set up alert`, and from the `Add notifier` menu. `Feeds`
- The time range picker in `Feeds` — `Export` and `Set up alert` are the two buttons left; exports now cover every event ever logged, filtered but never time-bound. `Feeds`
- The chip row above the `Feeds` list — filter by event type from `Add filter` like every other facet. `Feeds`

## NEW - 22.08.2026

### Added

- The `Feeds` page now shows every event your workspace produces, including the ones no alert was watching, marked `not sent`. You no longer need a subscription set up to find out what your docs actually emit. `Feeds`
- Each event in `Feeds` lists the destinations it was handed to and what each one answered, under one status folded from them, so a fan-out that half succeeded reads as a failure worth opening. `Feeds`
- `not sent` is a filter of its own in `Feeds`, next to delivered, pending, retrying and failed. `Feeds`
- Test pings and replays appear in `Feeds` like any other event, so the panel can answer whether a test worked. `Feeds`
- A notifier is now its own thing in `Feeds`: create the Slack channel, Discord channel or endpoint once, then tick it onto as many saved event lists as it should serve. Pausing, testing or deleting it applies everywhere it fires at once. `Feeds`
- `Add notifier` sits beside the filter chips — attach a destination you already have to the list on screen, or create one, without retyping its URL and secret. `Feeds`
- The `Feeds` sidebar splits into `Events` and `Notifiers`, each with its own create action, so a destination can be added before there is a list for it and a list before there is anywhere to send it. `Feeds`
- The `Feeds` page opens on a digest of the range: all activity, events that need attention, and failed deliveries as three counters, plus a chip per event group with its count — every number is a one-click filter on the feed, and clicking it again clears it. `Feeds`
- `Needs attention` in the `Feeds` digest counts the events where a reader hit a wall — unanswered chat questions, dead-end searches, stale content and translations, usage limits — separately from routine activity. `Feeds`
- The feed reads in day sections (`Today`, `Yesterday`, dates), and `Show more` grows the page in place instead of paginating. `Feeds`
- Every event type in `Feeds` carries its own coloured tile and glyph, and destination labels show the real Slack and Discord marks, so a mixed stream is scannable without reading it. `Feeds`
- Opening a feed card shows the full event: every delivery attempt with its response, replay, and the raw payload — the card itself stays a three-line summary. `Feeds`
- Export the feed you are looking at — filters and range applied — as CSV, JSON or NDJSON from the button beside the view's title. `Feeds`
- The notifiers firing on the list you are looking at now show as chips beside the filters — each with its channel's real mark, its name, and `paused` when it is off — and clicking one opens it. `Feeds`

### Changed

- The `Feeds` page dropped its wrapping card and the `Feed`/`Subscriptions` tabs: each saved list now shows its alert status right in the switcher, the sidebar drills into your lists the same way `Settings` drills into its categories, and setting up or managing an alert happens in one panel. `Feeds`
- Saved lists in `Feeds` are now created and deleted from the sidebar, and the list dropdown is gone from the panel, so one control owns which list you are looking at. `Feeds`
- The `Feeds` filter menu is a quarter of its old width and picks one facet at a time — events, delivery status, destination or a payload search — with the event list flat and searchable instead of split across nine headings. Each active filter now reads as its facet and count, and clicking it reopens that facet. `Feeds`
- `Set up alert` is gone from the `Feeds` toolbar: an alert is a notifier attached to an event list, so it is made where both of those live. `Feeds`
- The `Only failed` toggle left the `Feeds` toolbar: the failed-deliveries counter in the digest is the same switch with its number on it. `Feeds`

### Fixed

- Alerts that stopped being delivered are firing again — every event was being dropped before it reached its destinations. `Feeds`
- Deleting an event list, or detaching a notifier from one, can no longer leave an alert firing on every event in the workspace. `Feeds`

## NEW - 08.08.2026

### Fixed

- Webhooks now actually fire. Registered subscriptions never matched the events the product dispatched, so no real event had ever reached a subscriber's endpoint. `Webhooks`
- Registering a webhook accepts the event names exactly as this documentation writes them, with a dot. `Webhooks`

## NEW - 24.07.2026

### Changed

- Webhook registration now requires the Business plan consistently, whether registered via the dashboard or an MCP agent. `Webhooks`

## NEW - 06.07.2026

### Added

- Optional `auth_header` field when registering a webhook, sent verbatim as the `Authorization` header on every delivery — for receivers that require their own bearer token. `Webhooks`

## NEW - 05.07.2026

### Added

- Webhook count limits per plan, shown in workspace `Limits` settings. `Webhooks`

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: add the entry to the general changelog with its component tag and rerun the script. -->
