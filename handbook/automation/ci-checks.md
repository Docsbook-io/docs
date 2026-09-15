---
title: "CI checks and repository hooks: catching a docs problem before a reader does"
description: "What a pull-request check should test, why a pre-push hook warns instead of blocking, and the rules for generating a workflow that the team will not disable in a week."
tldr: "There are two places a documentation check can run before a problem reaches a reader: on the developer's machine before a push, and in CI on a pull request. Three checks earn their place in CI — code changed without docs, frontmatter validity, internal link integrity — all scoped to the changed files in the diff, and blocking is a parameter rather than a default."
---

# CI checks and repository hooks

Two places a check can run before a problem reaches a reader: on the developer's machine before a push, and in CI on a pull request. They catch different things and they fail in different ways.

| | Pre-push hook | Pull-request check |
|---|---|---|
| Catches | Drift, before it leaves the machine | Everything, including what came from a branch nobody ran the hook on |
| Speed | Must be seconds, or it gets bypassed | Can afford a minute |
| Failure | Warns by default; blocking is opt-in and set in the repository's own config | A red check, in the place review already happens |
| Blind spot | Anyone who has not installed it, and `--no-verify` | Changes that never go through a pull request |

Most teams want the pull-request check first and the hook second.

## What should the pull-request check actually test?

Three checks earn their place, and they are cheap:

1. **Code changed without docs changing.** Not a hard rule — plenty of changes need no documentation — so this is a warning that prompts a sentence in the pull request, never a block.
2. **Frontmatter validity on changed Markdown.** Required fields present and within size limits. **Never fail on a missing optional field**, or the check becomes something people learn to skip. [Writing rules](../writing/writing-rules.md) owns what those fields are.
3. **Internal link integrity.** Broken links and dead anchors in the changed files. Anchors are the half that breaks without anything else noticing — see [drift](./drift.md) for how quietly.

### Rules for generating it

- **Trigger on pull requests only**, and run against the **changed files in the diff** — never the base branch, and never the whole tree. A first run that drowns in pre-existing findings is a check that gets disabled the same afternoon.
- **Blocking is a parameter, not a default.** Where the owner has not asked for blocking, the link job continues on error and reports. Make it fail the build only when that was asked for explicitly.
- **Write one file, and touch no other workflow.** Overwriting the file this automation owns is fine; editing a workflow somebody else wrote is not, and the file's name should make its ownership obvious.
- **Report the path, the effective settings, and the reminder that it activates on merge.** A workflow file sitting unmerged on a branch does nothing, and that is a surprisingly common ending.

## When is a pre-push hook worth it?

When the drift you are catching is expensive to discover later — a renamed symbol whose page still says the old name — and the team pushes more often than it opens pull requests.

- **Offer it once**, on the first drift run, and never nag again.
- **Exit fast and silent when nothing relevant changed.** A hook that pauses on every push gets removed within a week.
- **Warn by default.** Blocking a colleague's push at a bad moment costs more trust than the drift costs, and the repository's own configuration is where blocking gets turned on.
- **Never fail silently.** If the dependency the hook needs is unreachable, print one line and let the push through. A hook that goes quiet when its search index is down is indistinguishable from a repository with no drift.

## Workflows driven by an event rather than by a commit

A workflow triggered by an external dispatch — the shape behind [events and handlers](./events.md) when the action belongs in the repository rather than in a chat channel.

- Trigger on the repository-dispatch event type the handler sends.
- For each item in the payload, take one action: file an issue linking to the source file, post a message, open a pull request.
- **One action per distinct thing**, never one per event, or a busy day produces forty issues about the same page.
- Reference every credential as a stored secret; never inline.
- Where the platform's event does not exist yet, wire the workflow against the closest native repository event as a documented fallback, and say clearly which one it is running on.

## What makes a generated workflow wrong

- **Never hardcode a credential.** Repository secrets, by name, with the names listed in the report so the owner knows what to store.
- **Never generate a command, URL or version you did not read** from the repository or the diff.
- **Overwrite only the file this automation owns.**
- **Create the directory if it does not exist**, and say where the file landed.
- **List what the owner must still do by hand** — store the secret, connect the channel, merge the branch. The automation is not live until those are done, and saying so is the difference between a working setup and a believed one.

## Related

- [Drift](./drift.md) — what the diff-triggered checks are looking for, and the pipeline behind them.
- [Events and handlers](./events.md) — the platform side of a dispatch-driven workflow.
- [Setting up automation](./setting-it-up.md) — why blocking is almost never what was actually wanted.
- [Monitors and alerts](./monitoring.md) — the standing watches that catch what never goes through a pull request.
