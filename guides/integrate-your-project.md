---
title: "Integrate a project into Docsbook: specs, stories and internal docs"
description: "Move the specs, user stories, decision records, runbooks and docs in your codebase into private GitHub repositories, and serve each as a Docsbook project in one organization."
---

# Integrate your project into Docsbook

Give every folder of knowledge in your codebase its own private GitHub repository, put it back at the same path as a git submodule, and serve each repository as a Docsbook project in one organization. The checkout looks exactly as before, and one MCP connection can answer questions from all of it.

## What you end up with

For a product called Acme with four knowledge folders in `acme/acme-app`:

| Folder | Private repository | Submodule | Docsbook project | Site |
|---|---|---|---|---|
| `specs/` | `acme/acme-app-specs` | `specs/` | Acme — Specs | private |
| `stories/` | `acme/acme-app-stories` | `stories/` | Acme — Stories | private |
| `docs/internal/` | `acme/acme-app-docs-internal` | `docs/internal/` | Acme — Internal | private |
| `docs/public/` | `acme/acme-app-docs-public` | `docs/public/` | Acme — Docs | public |

Four rules hold the whole way through:

- **Everything stays in GitHub**, in repositories you own, and every repository is created private. Whether a site is public is a separate setting.
- **Private until proven public.** A folder gets a public site only when it was written for outsiders, a secret scan is clean, and you said yes.
- **Nothing irreversible before you confirm the plan.** The code repository changes on a branch, as a draft pull request.
- **The content does not change in the move**, and a git tree hash proves it.

## Who does which part

The move and the Docsbook setup run in two different places:

- **In your checkout**, with `git` and `gh`: finding the folders, creating the repositories, the submodules and the pull request. You run it, or your coding agent does — Claude Code, Codex or Cursor.
- **In Docsbook**, through [your MCP connection](../get-discovered.md) or the panel: the projects, the organization, privacy and sources.

The [Docsbook agent](../agent/README.md) has no shell, so it cannot move folders. It can plan the move with you and do the Docsbook half once the repositories exist.

<!-- widget:callout type=info -->

### Before you start

- A clean working tree with a GitHub remote. Commit first; nothing here stashes or discards your changes.
- `gh auth status` succeeds, as an account that can create repositories under the target owner.
- `git subtree` is installed. Without it, you can still move the files, but not their history.
- Docsbook connected read-write as the account that will **own** every project — only needed from step 4.

<!-- /widget -->

## 1. Find the folders that are knowledge

Count the markdown per directory, over tracked files only:

```bash
git ls-files -- '*.md' '*.mdx' \
  | awk -F/ 'NF>1{print $1} NF>2{print $1"/"$2} NF>3{print $1"/"$2"/"$3}' \
  | sort | uniq -c | sort -rn | head -40
```

A directory is worth moving when all of these hold:

- **At least 3 markdown files**, and markdown is at least 60% of its files, not counting images, diagrams and PDFs.
- **Not generated or vendored** — `node_modules`, `vendor`, `dist`, `build`, `site/`, `coverage`.
- **Not the repository root.** The root `README.md`, `CHANGELOG.md` and `CONTRIBUTING.md` stay where they are.

Three look-alikes to rule out:

- **Storybook stories.** `*.stories.tsx` and a `.storybook/` directory are component code, not user stories.
- **Mixed folders.** `src/` with a few READMEs stays put; the build imports it.
- **Nested folders.** If `docs/public/` and `docs/internal/` have different readers, move the two leaves. If everything under `docs/` has one reader, move `docs/` whole — never both.

A folder that is already a submodule is skipped here and only connected to Docsbook in step 4.

## 2. Decide who each folder is for

Private is the default. Propose a folder as public only when it has a public signal **and** no internal one:

| Public signal | Internal signal — overrides any public one |
|---|---|
| A docs-site config: `mkdocs.yml`, `docusaurus.config.*`, `docs.json`, `book.toml` | Internal hostnames: `*.internal`, `*.corp`, private IP ranges |
| A folder named `public`, or described as customer-facing | Links into Jira, Linear, Slack or Notion workspaces |
| Pages for an outside reader: install, quickstart, API reference | People, salaries, customer names, roadmap dates, `confidential` |

Scan every folder you propose as public before it gets a site:

```bash
git grep -nIE \
  -e 'sk-[A-Za-z0-9]{20,}' -e 'ghp_[A-Za-z0-9]{36}' -e 'AKIA[0-9A-Z]{16}' \
  -e '-----BEGIN [A-Z ]*PRIVATE KEY-----' \
  -e '(password|secret|api[_-]?key|token)[[:space:]]*[:=][[:space:]]*[^[:space:]]{8,}' \
  -- docs/public | cut -d: -f1,2
```

Each hit keeps that folder private until you resolve it. Deleting a secret from the files does not delete it from history, so rotate it.

Then settle the plan in one go: the GitHub owner, the repository names (`<repo>-<folder>` by default), the Docsbook organization's name, the audience of each folder, and whether to keep history.

## 3. Move each folder into its own repository

Work on a branch of the code repository. For each folder, run this from the repository root:

```bash
git switch -c docs-integrate/submodules          # once, before the first folder
gh auth setup-git                                # once: lets git push over HTTPS with gh's credential

F=specs; OWNER=acme; NAME=acme-app-specs
BEFORE=$(git rev-parse "HEAD:$F")                # the folder's tree hash

git subtree split --prefix="$F" -b "integrate/$NAME"
[ "$(git rev-parse "integrate/$NAME^{tree}")" = "$BEFORE" ] || { echo "split differs"; exit 1; }

gh repo view "$OWNER/$NAME" >/dev/null 2>&1 || gh repo create "$OWNER/$NAME" --private
URL="$(gh repo view "$OWNER/$NAME" --json url -q .url).git"
git push "$URL" "integrate/${NAME}:refs/heads/main"
[ "$(gh repo view "$OWNER/$NAME" --json defaultBranchRef -q .defaultBranchRef.name)" = main ] \
  || gh repo edit "$OWNER/$NAME" --default-branch main

git rm -r -q "$F"
git submodule add "../$NAME.git" "$F"            # relative URL: same owner as the code repository
[ "$(git -C "$F" rev-parse 'HEAD^{tree}')" = "$BEFORE" ] || { echo "content differs"; exit 1; }

git commit -m "Move $F/ into $OWNER/$NAME (submodule at the same path)"
git branch -D "integrate/$NAME"
```

Git names a directory by the hash of its contents, so an equal hash before and after means the same files, byte for byte. Any mismatch stops the run.

<!-- widget:callout type=warning -->

Check that the new repository's default branch is `main`, the branch you pushed. A default branch that was never pushed makes the submodule check out empty, and the folder vanishes from the checkout. If the repository already exists with different history, stop for that folder — never force-push over it.

<!-- /widget -->

A few cases change the commands:

- **A different owner** than the code repository: use the absolute URL in `git submodule add` instead of `../$NAME.git`.
- **No history wanted**, or no `git subtree`: copy the folder into a fresh repository with `cp -a`, commit and push; the tree-hash check still applies.
- **Git LFS files**: run `git lfs push --all "$URL"` after the push.

After the last folder, push the branch and open a **draft** pull request. Its description tells your team three things:

- **How to update a checkout**: `git pull && git submodule update --init --recursive`; new clones use `git clone --recurse-submodules`.
- **Which CI jobs read a moved path** (`git grep -n specs -- .github/`). They need `submodules: recursive` on checkout, and a token that can read the new private repositories.
- **Where editing happens now**: inside the submodule — commit and push there, then commit the new pointer in the code repository.

## 4. Create the Docsbook projects

Install the **Docsbook GitHub App** on the owner of the new repositories first, at `https://github.com/apps/docsbook/installations/new`, and pick **Only select repositories**. Docsbook reads a private repository only through that installation.

Then make one project per repository. How depends on who owns the repository on GitHub:

<!-- widget:tabs -->

### Your GitHub account

Ask your agent to create each one with `create_workspace`, passing the repository, a display name and the organization:

```json
{
  "repo_full_name": "acme/acme-app-specs",
  "custom_name": "Acme — Specs",
  "organization": "Acme"
}
```

`organization` files the project into your Docsbook organization of that name, and creates the organization first if you have none. Repeat it for every project, and they all land in one team.

### A GitHub organization

Import these in the panel, because an MCP connection holds no GitHub credential and cannot prove the repository is yours:

1. Switch the panel to your Docsbook organization from the account menu at the bottom left. If you have none yet, create it there.
2. Open **Select repository** at the top of the sidebar and click the repository.
3. Repeat for each one. Each click makes a project inside that organization and starts nothing else.

Then ask your agent to call `create_workspace` with the same `repo_full_name`: it returns the project with `already_existed: true` and its id.

<!-- /widget -->

<!-- widget:callout type=warning -->

**Check every answer.** `create_workspace` must come back with `hosting: "github"` and the `repo_full_name` you asked for. `hosting: "docsbook"` or a `note` means Docsbook could not claim your repository and made a hosted site instead. Do not write to it; delete it in **Settings ▸ Danger Zone** and use the panel import. Do not use **Generate** on the connect page for these repositories either: it starts a paid run that writes new pages into the repository.

<!-- /widget -->

## 5. Make the internal sites private — at once

A new project is public until you change it, so switch each internal one right after it exists. In the panel, open **Settings ▸ Access ▸ Privacy & Access** and turn off **Public — anyone with the link**; from your agent, call `update_access` with `visibility: "private"` through `find_tool` and `call_tool`.

A private site with no password and no SSO is read only by you, your collaborators and members of the organization it is filed in, signed in to Docsbook. Add a password or SSO only when people outside the team need it — see [Private docs](../site/private-docs.md).

## 6. Connect the code as a source

Connect the code repository to each project with `connect_source`, and say in `note` what it is to that project — "the application code these specs describe". The Docsbook agent can then check a spec against the code instead of recalling it. See [Sources](../brain/sources.md).

## 7. Mark what the team has settled

Docsbook reads a page with no `status:` in its frontmatter as `generated` — written by a machine, read by nobody — and tells every agent not to build work from it. For specs your team argued over, that label is wrong. Ask folder by folder:

| The team says | Frontmatter | What agents do |
|---|---|---|
| Settled, we stand behind it | `status: approved` | Build from it; an edit through Docsbook sends the page back to `review` |
| Frozen on purpose — a decision record | `status: locked` | Build from it; Docsbook refuses to rewrite it |
| Still being written | `status: draft` | Quote it as a draft |
| Not sure | nothing | Treat it as `generated` |

Stamp a whole folder in one commit inside its repository. This adds only the `status:` line, creates a frontmatter block where there is none, and leaves an existing status alone:

```bash
F=specs; STATUS=approved
git -C "$F" switch main
git -C "$F" ls-files -- '*.md' '*.mdx' | while read -r f; do
  p="$F/$f"
  awk -v st="$STATUS" '
    NR==1 && /^---[ \t]*$/ { infm=1; print; next }
    NR==1 { print "---"; print "status: " st; print "---"; print; next }
    infm && /^status:/ { hasst=1 }
    infm && /^---[ \t]*$/ { if (!hasst) print "status: " st; infm=0; print; next }
    { print }' "$p" > "$p.tmp" && mv "$p.tmp" "$p"
done
git -C "$F" commit -am "Mark $F as $STATUS" && git -C "$F" push
git add "$F" && git commit -m "Bump $F to the status-stamped commit"
```

After that, one page at a time goes through `set_doc_status`, which commits the change to the repository.

## No public docs yet?

If none of your folders is written for customers, Docsbook can write the first public docs:

1. **Create an empty private repository** with `gh repo create acme/acme-app-docs --private --add-readme`, and add it as a submodule, at `docs/` if that path is free.
2. **Create its project** as in step 4 and make it private, so the first draft is not the first thing a search engine caches under your name.
3. **Let Docsbook write to it.** Call `grant_repo_access` for the repository; `works_unattended: true` means the agent can publish there with nobody signed in.
4. **Connect the code** as a source. Connect a private folder only if you want it used as background, with a note that nothing from it may be quoted.
5. **Ask the agent for the goal**, not the steps: who reads, in which language, and what they must be able to do afterwards.

The agent never approves its own pages. Read the first pass, approve what holds, then make the site public.

## Check the result

- **`git submodule status`** lists every moved folder, and a fresh `git clone --recurse-submodules` of the branch has the same files.
- **Every project answers** a `search_project_docs` question about a heading from its own folder.
- **Every private site** shows the sign-in page in a private browser window, never the page text.

## Tell your agent

Paste this into Claude Code, Codex or Cursor, in the code repository:

```text
Integrate this project into Docsbook the way docsbook.io/guides/integrate-your-project describes.
Start by listing the folders that hold our specs, stories and docs, who each is for, and why.
Change nothing until I confirm the plan.
```

## FAQ

<!-- widget:accordion -->

### Why submodules instead of leaving the folders where they are?

A Docsbook project serves one repository. A folder of specs inside the code repository cannot be its own private site, and an agent working anywhere else cannot see it. As a submodule it is both: its own repository and site, and still at the same path in your checkout.

### Can my teammates' agents ask these projects?

Private projects answer the MCP connection of the account that owns them. Teammates in the organization read the private sites in the browser, but their own connections reach only projects they own. Public projects also answer anyone's agent through each site's [public MCP server](../brain/mcp-server.md).

### What happens to links between the folders?

In your checkout they keep working, because the paths did not move. On Docsbook each repository is its own site, so a relative link from `specs/` into `docs/` breaks there. Count them before the move with `git grep -nE '\]\(\.\./' -- specs`.

### Does anything in the files change?

Not during the move — the tree-hash check fails the run if a single byte differs. The only edit is the optional `status:` line in step 7, and only in folders you named.

<!-- /widget -->

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [Teach your agent where knowledge lives](./teach-your-agent.md) — One block for CLAUDE.md or AGENTS.md that routes each question to the right project {brain}
- [Private docs](../site/private-docs.md) — Who can read a private site, and how to add a password or SSO {lock}
- [Sources](../brain/sources.md) — Give the agent the code your specs describe {plug}
- [Tell your agent, get discovered](../get-discovered.md) — Connect Claude Code, Cursor or Codex to Docsbook {terminal}

<!-- /widget -->
