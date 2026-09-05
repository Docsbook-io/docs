---
title: "What Docsbook has shipped that removes manual checks"
description: "Every release that removes a watch somebody kept by remembering to look: webhooks, alerts, delivery logs and the usage limits that fire before you do."
---

# What Docsbook has shipped that removes manual checks

Everything Docsbook shipped that moves one number: **Manual checks** — fewer things somebody has to check by hand. On this axis, down is better.

A watch someone keeps by remembering to look, kept by a webhook instead. This is the Manual checks slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG); an entry appears here whenever what it shipped moves this number, whichever part of the panel it landed in.

## NEW - 05.09.2026

### Added

- Overage now warns you five times before it stops anything — at 75%, 85%, 90%, 95% and finally at the cap — each one saying how much room is left, what pauses when it is gone, and the two ways to keep it running. Register a webhook on `usage.limit_approaching` or `usage.overage_limit_reached` and the same five moments reach your channel, so nobody has to watch a balance to find out. `Webhooks`

## NEW - 31.08.2026

### Added

- **Set up Prompt** sits beside Set up alert on the feed's toolbar, with a count of what is already running on this feed. An alert forwards the feed to a person; a prompt hands it to your assistant to act on, and now both are one glance apart instead of two screens. `Feeds`

## NEW - 30.08.2026

### Added

- And ten more: what should keep happening without anybody remembering, and whether each check belongs in a hook or in CI (`plan_automation_workflows`); which of these tools your workspace can answer with at all, and the cheapest thing to connect (`assess_setup_readiness`); the material you already have that could be docs, support answers and community threads included (`map_content_sources`); whether this kind of change has ever worked here before you repeat it (`assess_fix_precedent`); which two to four tools your question actually calls for (`plan_audit_route`); what each number is worth to the business (`map_business_value`); whether the corpus reads as an authority or as a site that mentions a topic (`map_topic_authority`); the region readers can only reach from the sidebar (`audit_internal_links`); which languages are read and which translations are behind their source (`audit_translation_coverage`); and what shape of answer a query wanted against what the ranking page delivers (`diagnose_intent_mismatch`). `MCP`

### Changed

- The `Feeds` toolbar no longer carries a running "1,204 of 7,279" count or a second, icon-only button for creating a notifier — `Set up alert` is the one way to make one, and it now also lists the destinations you already have, including any attached to nothing. `Feeds`

## NEW - 28.08.2026

### Added

- The setup checklist now also appears on the Overview as **Recommendations**, open by default with each step carrying the reason to do it and the button that walks you through it; closing it is remembered so it stays out of the way afterward. Once everything is done it collapses to **Guides**, so any walkthrough can be replayed. `Dashboard`

### Changed

- `Feeds` now opens on **Select a feed**: a card for each feed with a line saying what it holds. Four are built in — All events, Unanswered questions, Reader feedback and Delivery trouble — so there is something to open before you have saved anything of your own. `Feeds`
- The event feed is now one line per event instead of a card, so a day of events fits on a screen and can be scanned rather than scrolled. Clicking a line still expands the full payload and every delivery attempt underneath it. `Feeds`
- Webhooks are no longer counted against a per-plan cap: a paid plan registers as many feed notifiers as it needs, and Free has none. `Feeds`

### Removed

- The **Webhooks** card is gone from Usage. It counted your webhooks against a limit that no longer exists. `Limits`

## NEW - 26.08.2026

### Added

- `Feeds` can now filter the docs site's own analytics stream — page views, searches, chat questions and more — as an opt-in category alongside webhook events. `Feeds`

## NEW - 24.08.2026

### Fixed

- A social link to LinkedIn, YouTube or Slack now shows the site header, which previously appeared only for GitHub, Discord or X. `Branding`

## NEW - 23.08.2026

### Changed

- `Feeds` puts `Export` and `Set up alert` in one row beside the list's name, as identical buttons. `Feeds`
- Each row of the `Add notifier` menu now has an edit control, so a destination attached to another list — or to none yet — can be opened without hunting for it. `Feeds`

### Removed

- The three summary tiles above the `Feeds` feed (all activity, needs attention, failed deliveries) — `failed` moved into `Add filter` under `Delivery status`. `Feeds`
- The `Notifiers` group in the `Feeds` sidebar, and with one group left, the `Events` heading above the lists. Destinations are reached from the chips beside the filters, from `Set up alert`, and from the `Add notifier` menu. `Feeds`
- The time range picker in `Feeds` — `Export` and `Set up alert` are the two buttons left; exports now cover every event ever logged, filtered but never time-bound. `Feeds`

## NEW - 22.08.2026

### Added

- The `Feeds` page now shows every event your workspace produces, including the ones no alert was watching, marked `not sent`. You no longer need a subscription set up to find out what your docs actually emit. `Feeds`
- `not sent` is a filter of its own in `Feeds`, next to delivered, pending, retrying and failed. `Feeds`
- Test pings and replays appear in `Feeds` like any other event, so the panel can answer whether a test worked. `Feeds`
- A notifier is now its own thing in `Feeds`: create the Slack channel, Discord channel or endpoint once, then tick it onto as many saved event lists as it should serve. Pausing, testing or deleting it applies everywhere it fires at once. `Feeds`
- `Add notifier` sits beside the filter chips — attach a destination you already have to the list on screen, or create one, without retyping its URL and secret. `Feeds`
- The `Feeds` sidebar splits into `Events` and `Notifiers`, each with its own create action, so a destination can be added before there is a list for it and a list before there is anywhere to send it. `Feeds`
- The `Feeds` page opens on a digest of the range: all activity, events that need attention, and failed deliveries as three counters, plus a chip per event group with its count — every number is a one-click filter on the feed, and clicking it again clears it. `Feeds`
- Every event type in `Feeds` carries its own coloured tile and glyph, and destination labels show the real Slack and Discord marks, so a mixed stream is scannable without reading it. `Feeds`
- Opening a feed card shows the full event: every delivery attempt with its response, replay, and the raw payload — the card itself stays a three-line summary. `Feeds`
- The notifiers firing on the list you are looking at now show as chips beside the filters — each with its channel's real mark, its name, and `paused` when it is off — and clicking one opens it. `Feeds`

### Changed

- The `Feeds` page dropped its wrapping card and the `Feed`/`Subscriptions` tabs: each saved list now shows its alert status right in the switcher, the sidebar drills into your lists the same way `Settings` drills into its categories, and setting up or managing an alert happens in one panel. `Feeds`
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

## NEW - 28.07.2026

### Added

- Growth and Scale can now work in the AI chat together: see who from your team is in the chat, invite a teammate by email, and watch the same answer stream in for both of you instead of relaying it through Slack. `AI Chat`

### Changed

- Growth and Scale now include every Business capability — custom domain, white-label, webhooks, your own AI and translation keys, UTM analytics and API reference — which the higher-priced tiers were previously denied. `Pricing`

## NEW - 24.07.2026

### Changed

- Webhook registration now requires the Business plan consistently, whether registered via the dashboard or an MCP agent. `Webhooks`

## NEW - 06.07.2026

### Added

- Optional `auth_header` field when registering a webhook, sent verbatim as the `Authorization` header on every delivery — for receivers that require their own bearer token. `Webhooks`

## NEW - 05.07.2026

### Added

- New `Business` plan — everything included in `Pro`, with higher AI chat, translation, and webhook limits. `Billing`
- Webhook count limits per plan, shown in workspace `Limits` settings. `Webhooks`

## 0.22.3 - 30.05.2026

### Fixed

- Fix scroll shadow in Webhooks (Events) tab — shadow now appears only when content is scrollable

## 0.16.0 - 22.05.2026

### Added

- Paddle `SubscriptionPaymentFailed` webhook handler — downgrades workspace to Free and sends Resend email to the owner with payment-update link

## 0.15.0 - 22.05.2026

### Added

- Events webhook endpoint in `API` for receiving real-time workspace events

## Related

- [Full Docsbook changelog](../../CHANGELOG.md) — every release, on every axis
- [Changelogs by outcome](./README.md) — the other eleven numbers a release can move
- [Changelogs by panel section](../README.md) — the same releases, cut by where they landed

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: the entry goes in the general changelog, and the axis is read from its wording via src/lib/outcomes/axes.json. -->
