---
title: "What shipped in the Docsbook issue tracker, and when"
description: "Every release that touched Issues: the GitHub tracker inside the panel, the impact each issue and pull request claims, and the score that says whether it worked. The section was retired on 12.09.2026 and came back on 18.09.2026 as one tabless list of every issue and pull request, which is why this page has a gap in the middle."
---

# What shipped in the Docsbook issue tracker, and when

Everything that shipped in **Issues**. This is the Issues slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG).

## NEW - 19.09.2026

### Improved

- **The figure on a merged change is now read by Docsbook rather than typed onto it.** Where we measure the outcome ourselves — organic traffic today, and questions reaching your assistant — the number is taken the moment you open the list, so a reading stops going stale as soon as anything moves and nobody has to monitor a date and copy the result onto the record by hand. Each row says which figures are ours and which were reported, and we only stand in for a figure when it is the same measurement over the same window. `Issues`

### Changed

- **Issues is one list — the Open, Measuring and Closed tabs are gone.** They were the same records asked a slightly different question, so a project with six open records drew three "nothing here" pages beside the one list that had everything. The counts above the list are the same doors: each one writes a filter you can read in the box, combine (`is:pr is:due`) and paste to somebody. `Issues`
- **Every pull request now shows how far it actually got** — opened, reviewed, merged, measured, as four marks worked out from the record itself instead of from a sentence somebody wrote on it. A merged change that never got its reading is a gap you see at a glance, rather than something to monitor by reading the tracker. Issues carry none on purpose: an issue ships nothing, so there is nothing for it to be three quarters of the way through. `Issues`

### Removed

- **Opportunities is gone from the panel.** It showed what an audit had found beside the list of work, where research reads as a backlog of things nobody has agreed to do. What an audit finds is still kept and still readable by an agent over MCP; what went is the screen. `Issues`

## NEW - 18.09.2026

### Added

- **Issues now shows the whole tracker on one screen — every issue and every pull request together**, filtered the way you already filter GitHub (`is:issue state:open`, `label:bug`, a number typed from memory). They are two stages of one piece of work, so checking what is open on a project stops being two tabs and two mental lists, and nobody has to keep a browser tab on GitHub open beside the panel to see what is actually happening. `Issues`
- **Every issue and pull request now says what number it is supposed to move**, in figures: which outcome, the unit, what the number says today, what it should say afterwards, and the day we look. The claim is written into the record itself, so it is readable on GitHub as well as here, and it survives the project moving. `Issues`
- **A bar on each row says how much of that promise actually arrived**, worked out from the figures rather than asserted by the assistant — so "did that change do anything" is answered by looking instead of by somebody re-running the numbers by hand a month later. A change that claimed nothing says so plainly rather than looking finished. `Issues`
- **Sort by "Impact at risk"** to put the readings nobody has taken at the top, and filter to the work that claimed nothing at all — the backlog can now be read by outcome rather than only by date. `Issues`
- **Comment on an issue or a pull request without leaving the panel**, with the same Write and Preview tabs you are used to. The comment lands on the record on GitHub, where the next person will find it. `Issues`
- **A comment left here also puts the assistant to work**: it reads the conversation, the record and the change, then answers on the thread or does what was asked. Replying to a question on your own tracker stops being something you have to sit down and do. `Issues`

## NEW - 13.09.2026

### Improved

- The Issues tab keeps the same move: no more open/filed-this-week figures, just its own icon and the list, sharing the card with Pull Requests. `Issues`

### Fixed

- Filing an issue on a Docsbook-hosted site works again where the tracker had been switched off: Docsbook switches its own repository's tracker back on and files the issue, rather than sending you to a settings page on a repository you have no account on. Every new hosted repository is created with issues on so it cannot happen again, and a repository Docsbook does not own is never changed. `Issues`

## NEW - 04.09.2026

### Added

- Every station of an agent's run files what it found as a GitHub issue on your own tracker, so nobody has to read a transcript to learn what needs doing. The finding outlives the run that produced it: a person can pick it up, the diff that fixes it can reference it, and merging that diff closes it. `Issues`
- An issue an agent filed names that agent in its sidebar and opens its card from there, so "what wakes this thing, and what route is this station part of" is one click rather than a walk back through the panel. Beside it sit the run behind the finding, the other stations of the same route, the other issues that reference this one, and the pull request that closes it. `Issues`
- An open issue can be closed straight from its page — as completed, not planned, or duplicate, the same three reasons GitHub's own page offers — without leaving the panel to do it. `Issues`
- Issues gets that same first-visit walkthrough instead of opening straight onto a live GitHub read. `Issues`

### Changed

- Reading an issue now tells you what came of it, not only what it says: the comments, the agent and the run that filed it, and the pull requests written against it. A hypothesis somebody wrote down and a hypothesis somebody actually tested read very differently, and the tracker was only showing you the first. `Issues`
- An agent's issue now opens on what it FOUND. Why the run happened, what earlier steps handed it, what happens to anything it writes and the raw call all moved into one collapsed block at the bottom, so deciding what to do about a finding no longer means scrolling past four headings about the machinery to reach it. `Issues`
- The **Issues** walkthrough now runs over example issues instead of an empty tracker. A first visit shows what a filed finding looks like — the badge that marks one an agent opened on its own, the labels that say which kind of reader raised it, an open one beside a closed one — so the introduction argues for the section rather than reporting that there is nothing in it. The examples say they are examples and disappear the moment a real issue exists. `Issues`

### Fixed

- Issues an agent files carry their labels on GitHub again, and any label your repository does not have yet is created first. Without them the panel could not tell an agent's finding from something a person typed, so twenty findings opened with no run, no route and no sibling stations beside them. `Issues`

### Removed

- The **Generate Issues** button is gone from the Issues list. Asking for issues along a stage still works exactly as before — say it to the assistant, or arm the matching agent — the button was one way to compose that request, not a separate capability. `Issues`

## NEW - 02.09.2026

### Added

- An **Issues** section in the admin panel — the GitHub issues on the repository your documentation is built from, sitting under Changes. Changes is what was already done to the project and what it moved; Issues is what has yet to be. Hover a row for a card with the issue's body, labels and author; open one for the whole thing. `Issues`
- Each issue carries three buttons that hand it to your assistant. **Start** does the work it asks for. **Audit** judges the issue before anybody acts on it — is the problem real for this project, are its numbers true, is it already done or already open somewhere else. The third is **Verify** on a closed issue (prove the result it claims, against a baseline and the pages nobody touched) and **Discover** on an open one, because an issue with nothing finished has no result to verify yet. `Issues`
- **Generate Issues** asks your assistant to look at the project and file what it finds, after two questions: which stage of work you want to be in — observe, understand, discover, decide, plan, execute, measure, verify, learn, coordinate — and which number you want moved. Asking is the point. With no stage named an assistant returns things to *build* every time, and a backlog with no Measure or Verify in it belongs to a team that never finds out whether the last thing it built worked; the pair you pick also selects the agents that already cover it, so the issues come from this project's own evidence rather than from general advice. `Issues`
- **New issue** files one yourself without leaving the panel. `Issues`

## Related

- [Full Docsbook changelog](../CHANGELOG.md) — every release, across every section
- [Changelogs by panel section](./README.md) — the same releases, cut by where they landed
- [Changelogs by outcome](./outcomes/README.md) — the same releases, cut by the number they move

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: add the entry to the general changelog with its component tag and rerun the script. -->
