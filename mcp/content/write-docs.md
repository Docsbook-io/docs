---
title: "Write docs"
description: "Write, delete, move and rename markdown documentation files — this is how a site gets its pages and how its structure is changed, including a site just created from scratch by…"
---

# Write docs

<!-- widget:mcp access=write price-millicents=30000 -->

## write_docs

Write, delete, move and rename markdown documentation files — this is how a site gets its pages and how its structure is changed, including a site just created from scratch by create_workspace. EVERYTHING in one call lands in ONE atomic git commit: batch a restructure (the moves, the deletions, and the pages whose links they change) into a single call rather than calling this repeatedly — a rename split across two commits leaves the published site with a broken link in between. `files` writes whole files. `operations` says what a content array cannot: {op:'delete', path, redirect_to?} removes a page, {op:'move', from, to, content?} renames or relocates one (its body carries over untouched unless you pass `content`; naming a directory moves every page under it). Operations are applied before `files`, so writing a page at a path you just moved away from leaves a stub behind rather than cancelling the move. Every move — and every delete that names `redirect_to` — is recorded in the site's redirect map in the same commit, so the old URL keeps working instead of 404-ing every external link to it. Publishes to the Docsbook-hosted repository using Docsbook's own GitHub credentials, so the user needs no GitHub access; the repository is created on the first write if it does not exist yet. A site served from a repository in the user's OWN GitHub account is refused (NO_GITHUB_ACCESS) rather than committed to hosting the site does not read — the refusal names the routes that can write it. The result carries `site_url` — report that link, do not construct one. It also carries `widget_review`: a read of the markdown you just wrote, naming any widget marker that will NOT render (unclosed, misspelled, nested, switched off) and any region that has the shape of a content widget and was left as plain markdown — a stacked set of snippets in three languages, a bare list of links closing the page, numbered step headings, a bolded `Note:`. Act on the ones that fit the page with a follow-up call; `list_content_widgets` has each widget's full contract. Every written page carries a LIFECYCLE — a `status` and a `version` in its own frontmatter — and this call maintains it: a new page opens at `generated` 0.1, an edit bumps the version, and an edit to an `approved` page sends it back to `review`, because the sign-off was of the text that just changed. The result's `lifecycle` says where each page landed; report a demotion rather than describing the docs as settled. A page at `locked` or `archived` REFUSES the whole call (DOC_FROZEN, naming the pages) — nothing is written, because everything here is one commit. Thaw it with `set_doc_status` first. This call can never produce `approved` or `locked`, whatever the frontmatter you send says: approving your own output in the same breath as writing it is the one thing the lifecycle exists to prevent. `set_doc_status` is the separate, deliberate act. REQUIRES a read-write MCP token — a read-only token gets a READ_ONLY_TOKEN error.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `files` | object[] | no | Files to write in full. Committed together with `operations` as a single commit. Optional only when `operations` is given. |
| `operations` | string[] | no | Structural changes — deletes, moves and renames — applied in the same commit as `files`, in the order given. |
| `message` | string | no | Commit message (default: 'docs: update via Docsbook MCP'). |
| `intent` | string | no | What the person asked for, in their own words — the goal behind this edit, not a summary of the diff. Shown on the change in the Changes panel so the owner can later see what the edit was for and judge whether it worked. Pass the user's original request verbatim when you have it. |
| `closes_issues` | integer[] | no | The issue numbers this change finishes. Written into the pull request body as `Closes #N`, so merging it closes the work — on GitHub as well as here — and the board folds the change into that issue's card instead of drawing it as unattached work. Pass them even when the review mode merges immediately: the record is what makes the change readable in six weeks. |
| `hypothesis` | string | no | The key of the hypothesis this change TESTS, from list_hypotheses. 🔴 Without it a merged change has nothing to be judged against and shows on get_work_board as `unmeasured` — which is the honest word, and the debt somebody pays later by reconstructing what you already knew. Write the claim first with add_hypothesis; this call attaches it. |
| `impact_metric` | string | no | Which of the thirteen outcomes this change moves. Give it together with impact_unit, impact_baseline, impact_target and impact_check_at, and the pull request carries a claim that code can score later — the share of the move you predicted that actually happened. Leave the whole set off for a change that is not making a claim (a typo, a reword); do NOT guess figures to fill it. One of: `support_load`, `upkeep_time`, `manual_checks`, `ai_spend`, `broken_pages`, `time_to_answer`, `ai_citations`, `new_markets`, `organic_traffic`, `conversion`, `first_visit_bounce`, `repeat_readers`, `hands_on_time`. |
| `impact_unit` | string | no | What the two figures count, stated once: 'visits/30d', '%', 'questions/week', 'seconds'. |
| `impact_baseline` | number | no | What that number says TODAY. Read it — an invented baseline is the one error here that cannot be corrected later, because the whole comparison hangs off it. |
| `impact_target` | number | no | What it should say after this lands, in the same unit. A target equal to the baseline, or a move smaller than the reading's own noise, is refused. |
| `impact_check_at` | string | no | YYYY-MM-DD — the day the reading gets taken. REQUIRED once impact_metric is given: a change with no day to judge it on is never judged. |
| `impact_source` | string | no | Where you read the baseline — a tool name, a URL, a query. |

<!-- /widget -->

## Call it

<!-- widget:code-group -->

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "write_docs",
    "arguments": {
      "impact_metric": "support_load"
    }
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"write_docs","arguments":{"impact_metric":"support_load"}}}'
```

<!-- /widget -->
