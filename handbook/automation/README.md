---
title: "Keeping it current: drift, monitors, events and CI checks"
description: "How documentation falls behind its source of truth, which monitors are worth installing and how to tune them, the events worth handling, the checks that belong in CI, and when to turn each site capability on."
tldr: "Documentation does not go stale on a schedule; it goes stale on a deploy. This section is about making the upkeep happen without a person remembering — and about the harder half, which is saying what a monitor will NOT catch before you install it."
---

# Keeping it current

Every documentation set is correct on the day it ships. What decides whether it is still correct in six months is not diligence — it is whether anything notices when the thing being documented changes.

<!-- widget:cards cols=2 -->

- [Setting it up](./setting-it-up.md) — the interview to run before proposing any automation at all. {compass}
- [Drift](./drift.md) — documentation falling behind its source of truth, and how to detect it. {history}
- [Monitors and alerts](./monitoring.md) — which are worth installing, and how to tune one that fires too often. {chart-line}
- [Events and handlers](./events.md) — what is worth reacting to, and what to do when it happens. {plug}
- [CI checks](./ci-checks.md) — the checks that belong in the repository, next to the code. {code}
- [Site capabilities](./site-capabilities.md) — what each capability gives you, and when it is worth turning on. {settings-2}

<!-- /widget -->

The rule that matters most here is the one people skip: **say what the monitor will not catch, before installing it.** An alert that fires for everyone, always, is an alert nobody reads by the third day — and by then it is also the alert that hid the real one.

The mechanics of each webhook Docsbook can send are in [the webhooks reference](../../reference/webhooks.md); these pages are about when a given monitor is worth having.
