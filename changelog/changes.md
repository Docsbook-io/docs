---
title: "What shipped in the Docsbook Changes tab, and when"
description: "Every release that touched the Changes tab: the commit history of your docs, the traffic each change moved, and the before/after compare."
---

# What shipped in the Docsbook Changes tab, and when

Everything that shipped in **Changes**. This is the Changes slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG).

## NEW - 05.09.2026

### Changed

- A merged pull request now tells you on its own page whether it worked: a score out of 100, four bars for readers served, reach, cost to run and edit quality, and the movements behind them — page reads, dead ends, search rank and AI spend, each coloured by whether it moved the way that is good for it. Checking whether an agent's change actually helped no longer means remembering to go and look on a second screen. `Changes`
- A pull request still waiting for your decision shows the same block as a forecast read from the diff alone, and it stays grey until something measured stands behind it, so an unreviewed change can never be mistaken for a proven one. `Changes`
- The right-hand column of a pull request replaced its file-count line with a footprint bar: added against removed lines as a proportion, plus how many documentation pages, links and headings the change actually touched. `Changes`

### Removed

- The **Merged & impact** view and its commit picker. What shipped and what it then did are now read on the pull request that shipped it, so the diff you approved and the result it produced are one page instead of two joined by a commit hash. `Changes`

## NEW - 04.09.2026

### Added

- Pull Requests now opens with a short walkthrough on a first visit instead of landing straight on a live GitHub read, the same "Turn on" introduction Agents and Sources already carry. `Changes`

### Changed

- The **Pull Requests** walkthrough does the same: the queue behind it now shows example changes waiting for approval, each with the agent that opened it and the issues it came out of, plus the publish-automatically switch the walkthrough talks about. It used to introduce itself with "Nothing is waiting for you", which is exactly what it says on the day you have not armed anything yet. `Changes`

### Fixed

- The Pull Requests panel no longer reports "Nothing is waiting for you" while a real pull request sits open on GitHub. Listing pull requests reused the credential resolution built for committing, so a project without escalated GitHub write access read its queue from the wrong repository instead of its own. Reading the queue no longer needs write access at all. `Changes`

## NEW - 03.09.2026

### Fixed

- The generated changelog pages can be reached and read. All 21 were orphans with no inbound link and no way out, and three of their links resolved from the docs root while the page sits a level or two below it, so they 404'd. Each page now closes with links to the full changelog, the neighbouring cut and the product page it documents, and each cut has an index. `Changes`

## NEW - 02.09.2026

### Changed

- Admin settings now open as a page everywhere on a documentation site — the settings gear, the account menu's settings rows and the language picker's "Activate languages" all navigate to the dashboard instead of throwing a full-height panel over the docs. An anonymous draft keeps its own page, so its unsaved work survives the trip. `Changes`

## NEW - 31.08.2026

### Fixed

- Header navigation links on a docs site served at an apex path (like `docsbook.io/docs`) no longer 404 — they used to resolve against the site root instead of the site's own base path, so a link meant for that site could bounce through a subdomain that doesn't exist. `Changes`

## NEW - 30.08.2026

### Added

- An open commit in `Changes` now has **Analyze**, which measures the pages it touched against the pages it did not over the same days, and is allowed to answer that it is too early to tell. `Changes`
- A commit made through Docsbook now shows **what was asked for** — the request that produced it, in the author's own words, above the files it changed. A commit pushed to the repository by hand says so, rather than showing an empty field. `Changes`
- Where a scheduled prompt made the commit, the effect it was predicted to have now sits under the measured figures, in the same cards, beside what actually happened. `Changes`
- Those checks are allowed to answer that **they cannot tell**, which is not the same as the prediction failing: too few visits either side, nothing to compare against, or a claim about your own week that no figure on a docs site could settle. Each says which of the three it is. `Changes`
- Every prediction states where its number came from — typical for that kind of prompt, or fitted to your site's own data — so a rule of thumb is never shown with the authority of a measurement. `Changes`

## NEW - 28.08.2026

### Added

- A commit in `Changes` now reads as a commit and is then measured: its labels, title, description and byline above ten indicators — readers, time reading, dead rate, CTA rate and AI citations measured, then score, earned, revenue, spent and steps to the CTA estimated — over a gallery of the files it touched. Picking a file re-points every number at that file alone. `Changes`

### Fixed

- **Earned** on a commit in `Changes` now sums exactly the figures the Users table prints for the same readers — a goal's declared value first, then your average product price — instead of a second, shorter calculation that ignored declared values and disagreed with the table its own explanation points at. `Changes`

## NEW - 25.08.2026

### Changed

- The admin Changes tab now leads with revenue, readers and every analytics list for the pages a commit touched, with a before/after compare toggle, instead of a bare score split across four tabs. `Changes`

### Fixed

- The Changes tab no longer stalls on busy repos — a stale per-run cap could stop it recording new commits once a repo shipped docs faster than it drained them. `Changes`
- Expanding a commit's diff in the Changes tab no longer fails for signed-in readers without write access. `Changes`

## NEW - 23.08.2026

### Added

- Every commit in `Changes` now carries one 0-100 score, with the four areas behind it: readers served, reach, cost to run and edit quality. Each area shows its own number, how much of the total it counts for, and how much data stands behind it. `Changes`
- A commit is scored the day it lands, from the diff alone, instead of showing nothing until its window closes two weeks later. `Changes`
- `Changes` now puts the cash figures up front: what re-translating the edited pages cost, what readers asking the chat cost either side of the commit, and total AI spend. `Changes`

### Changed

- `Changes` opens on the answer instead of on the charts. The score, what moved and what it cost come first; every measurement behind them is one `The measurements behind this score` toggle away, with nothing removed. `Changes`
- A thin sample no longer refuses to judge. A handful of visits still moves the score, just far less, and the page states how confident it is. A score with little behind it is never coloured and never called a success. `Changes`

### Fixed

- Commits stopped showing up in `Changes`. The nightly collector walked only part of the projects it should have, so an active repository could go days without a single new entry while the run reported success. Every project is now collected on every run. `Changes`
- Commits stuck on `Maturing` long after their two weeks were up: the measurement queue drained newest-first, so once a backlog formed the oldest commits were never reached. `Changes`

## NEW - 22.08.2026

### Added

- A new `Changes` tab lists every commit that touched your docs, with the page traffic before and after each one — and an on-demand check of whether a specific edit actually beat the rest of the site. `Changes`
- Every commit in `Changes` now shows what it cost: AI spend for the week before and the week after in dollars and percent, the share readers' own questions account for, cost per visit, and what re-translating the edited pages cost — with the sections served free from cache priced out. `Changes`
- `Changes` now reports what Google did with the pages a commit touched: average position, impressions, clicks and click-through rate against the rest of the site, a daily chart with the commit marked on it, and a per-URL rank table. `Changes`
- `Changes` now breaks each commit's visits down by country, reader language and device — every slice beside the same slice's move on the pages the commit did not touch, so growth that happened everywhere is not read as growth this edit caused. `Changes`

### Changed

- The `Changes` tab drops its date-range picker, commit count and card frame — pick a commit from the scrolling list and its impact opens right beside it, as colored charts instead of a paragraph. `Changes`
- Everything on the `Changes` tab reads larger — bigger type, taller charts, roomier tiles and a wider commit list. `Changes`
- The commit list is reachable as `Changes` in the account menu, beside `Analytics`. `Changes`

## Related

- [Full Docsbook changelog](../CHANGELOG.md) — every release, across every section
- [Changelogs by panel section](./README.md) — the same releases, cut by where they landed
- [Changelogs by outcome](./outcomes/README.md) — the same releases, cut by the number they move

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: add the entry to the general changelog with its component tag and rerun the script. -->
