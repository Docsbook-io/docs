---
title: "Write docs"
description: "Write, delete, move and rename markdown documentation files — this is how a site gets its pages and how its structure is changed, including a site just created from scratch by…"
---

# Write docs

<!-- widget:api -->

## POST /api/v1/write_docs

Write, delete, move and rename markdown documentation files — this is how a site gets its pages and how its structure is changed, including a site just created from scratch by create_workspace. EVERYTHING in one call lands in ONE atomic git commit: batch a restructure (the moves, the deletions, and the pages whose links they change) into a single call rather than calling this repeatedly — a rename split across two commits leaves the published site with a broken link in between. `files` writes whole files. `operations` says what a content array cannot: {op:'delete', path, redirect_to?} removes a page, {op:'move', from, to, content?} renames or relocates one (its body carries over untouched unless you pass `content`; naming a directory moves every page under it). Operations are applied before `files`, so writing a page at a path you just moved away from leaves a stub behind rather than cancelling the move. Every move — and every delete that names `redirect_to` — is recorded in the site's redirect map in the same commit, so the old URL keeps working instead of 404-ing every external link to it. Publishes to the Docsbook-hosted repository using Docsbook's own GitHub credentials, so the user needs no GitHub access; the repository is created on the first write if it does not exist yet. The result carries `site_url` — report that link, do not construct one. It also carries `widget_review`: a read of the markdown you just wrote, naming any widget marker that will NOT render (unclosed, misspelled, nested, switched off) and any region that has the shape of a content widget and was left as plain markdown — a stacked set of snippets in three languages, a bare list of links closing the page, numbered step headings, a bolded `Note:`. Act on the ones that fit the page with a follow-up call; `list_content_widgets` has each widget's full contract. And `style_review`: where the prose departs from the house style — a paragraph past four lines, four paragraphs with nothing between them, identifiers (`--flag`, `API_KEY`, `fooBar`, `file.json`) written outside inline code, a long page with no links. `list_content_widgets` → `writing_style` is the style itself; read it before your first page. Every written page carries a LIFECYCLE — a `status` and a `version` in its own frontmatter — and this call maintains it: a new page opens at `generated` 0.1, an edit bumps the version, and an edit to an `approved` page sends it back to `review`, because the sign-off was of the text that just changed. The result's `lifecycle` says where each page landed; report a demotion rather than describing the docs as settled. Thaw it with `set_doc_status` first. `set_doc_status` is the separate, deliberate act.

**Price** — $0.00009 per call (twice what serving it costs us), charged to the workspace balance, the same as over MCP.

Also reachable by name at `POST /api/v1/tools/write_docs`.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `files` | object[] | no | Files to write in full. Committed together with `operations` as a single commit. Optional only when `operations` is given. |
| `operations` | string[] | no | Structural changes — deletes, moves and renames — applied in the same commit as `files`, in the order given. |
| `message` | string | no | Commit message (default: 'docs: update via Docsbook MCP'). |
| `intent` | string | no | What the person asked for, in their own words — the goal behind this edit, not a summary of the diff. Shown on the change in the Changes panel so the owner can later see what the edit was for and judge whether it worked. Pass the user's original request verbatim when you have it. |
| `closes_issues` | integer[] | no | The issue numbers this change finishes. Written into the pull request body as `Closes #N`, so merging it closes the work — on GitHub as well as here — and the board folds the change into that issue's card instead of drawing it as unattached work. Pass them even when the review mode merges immediately: the record is what makes the change readable in six weeks. |
| `hypothesis` | string | no | The key of the hypothesis this change TESTS, from list_hypotheses. 🔴 Without it a merged change has nothing to be judged against and shows on get_work_board as `unmeasured` — which is the honest word, and the debt somebody pays later by reconstructing what you already knew. Write the claim first with add_hypothesis; this call attaches it. |
| `impact_metric` | string | no | Which of the thirteen outcomes this change moves. Give it together with impact_unit, impact_baseline, impact_target and impact_check_at, and the pull request carries a claim that code can score later — the share of the move you predicted that actually happened. OMIT ALL SIX impact_* fields unless you have READ a baseline with a tool: a typo, a reword, and every page of a new or demonstration site have no number to move, and a claim invented to fill this in is refused by the same check it was invented for. One of: `support_load`, `upkeep_time`, `manual_checks`, `ai_spend`, `broken_pages`, `time_to_answer`, `ai_citations`, `new_markets`, `organic_traffic`, `conversion`, `first_visit_bounce`, `repeat_readers`, `hands_on_time`. |
| `impact_unit` | string | no | What the two figures count, stated once: 'visits/30d', '%', 'questions/week', 'seconds'. |
| `impact_baseline` | number | no | What that number says TODAY. Read it — an invented baseline is the one error here that cannot be corrected later, because the whole comparison hangs off it. |
| `impact_target` | number | no | What it should say after this lands, in the same unit. A target equal to the baseline, or a move smaller than the reading's own noise, is refused. |
| `impact_check_at` | string | no | YYYY-MM-DD — the day the reading gets taken. REQUIRED once impact_metric is given: a change with no day to judge it on is never judged. |
| `impact_source` | string | no | Where you read the baseline — a tool name, a URL, a query. |
| `expectations` | object[] | no | What this change will do, PAGE BY PAGE: which catalog rule it applies to which page, and the two figures an instrument should read before and after. Merging the pull request records those rules as applied to those pages — this is how a verdict is EARNED rather than asserted, and there is no other way to record one. On the check date, call the instrument's own tool again: the comparison and the verdict are computed by code from the two recorded calls, and nothing ever asks you for the answer. |

### Returns

| Field | Type | Description |
|---|---|---|
| `ok` | boolean | Whether the tool itself succeeded. A tool that ran and refused — an exhausted balance, a plan restriction, a bad argument — answers `200` with `ok: false`: the call was made and billed, and that refusal is its answer. |
| `result` | object | The tool's own JSON answer, already parsed — not a string to parse a second time. |
| `duration_ms` | integer | Server-side wall time for the call. |

### `result` fields

| Field | Type | Description |
|---|---|---|
| `committed` | boolean | — |
| `published` | boolean | false when the change is awaiting review — committed to a branch, live nowhere yet. |
| `pull_request` | object | { number, url, branch, review_mode, merged } — present when review opened one. |
| `site_url` | string | — |
| `note` | string | — |
| `widget_review` | object | { note, files[] } — a read of the markdown just written. Present only when there is something to say: `problems` are markers that will not render (unclosed, misspelled, nested, switched off), `suggestions` are regions shaped like a content widget and left as plain markdown, each with the exact marker to wrap it in. |

### Limitations

- A site served from a repository in the user's OWN GitHub account is refused (NO_GITHUB_ACCESS) rather than committed to hosting the site does not read — the refusal names the routes that can write it.
- A page at `locked` or `archived` REFUSES the whole call (DOC_FROZEN, naming the pages) — nothing is written, because everything here is one commit.
- This call can never produce `approved` or `locked`, whatever the frontmatter you send says: approving your own output in the same breath as writing it is the one thing the lifecycle exists to prevent.
- REQUIRES a read-write MCP token — a read-only token gets a READ_ONLY_TOKEN error.

### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/write_docs' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"impact_metric":"support_load"}'
```

### Response

```json
{
  "ok": true,
  "result": {
    "committed": true,
    "published": true,
    "pull_request": {},
    "site_url": "<site_url>",
    "note": "<note>",
    "widget_review": {}
  },
  "duration_ms": 0
}
```

### Responses

| Status | Meaning |
|---|---|
| `200` | The tool ran. Read `ok` to see whether it succeeded. |
| `401` | Missing or invalid API key. |

<!-- /widget -->
