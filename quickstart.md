---
title: "Quickstart: publish your docs with Docsbook"
description: "Go from a GitHub repo, a website or a short product description to a live documentation site in minutes, then hand the writing to the Docsbook agent."
status: generated
version: "0.2"
---

# Quickstart

Open [docsbook.io/create](https://docsbook.io/create), pick where your pages come from, and your documentation site is live the moment you sign in — ready to hand to the Docsbook agent.

Nothing to install and no card. A GitHub account is optional, and every new account starts with a 14-day Pro trial that includes $5 of AI credit ([pricing](./pricing/plans.md)).

## Create your site

The **New project** screen walks through three steps — **Start**, **Your project**, **Your agent** — and only the first one needs an answer. Already signed in, you get the same steps from **Create new project** in the panel's project switcher.

<!-- widget:stepper -->

### Pick a starting point

The first tile imports a repository: **Connect GitHub**, or **Select repository** once GitHub is connected. Every other tile is a template — 38 of them in 9 categories, from **Docs shell** to **REST API** — pictured with the pages it will create.

### Tell Docsbook about your project

Every field on **Tell us about your project** is optional:

- **Project name** — the site's title, and its address when Docsbook hosts it
- **Main site** — read for your colours, logo and fonts, and the site the agent checks facts against
- **Add website** — up to four more sites, connected as [sources](./brain/sources.md)
- **Attachments** — PDF, DOCX and Markdown files become pages; pictures become images any page can use
- **What does your product do?** — a paragraph only your agent reads, never published

### Onboard your agent

Copy the one-line prompt for the agent you already use, pick **Channels** where the Docsbook agent posts what it finds (Slack, Telegram and more), and add **Instructions** or a **Model** if you want to. All of it can wait for the panel.

### Create and sign in

Press **Create Agent and Project**. Signed out, you choose **Continue with GitHub** (recommended — it lets agents commit to your repo), **Continue with Google** or **Continue with Email** with a 6-digit code. Your answers survive the sign-in, and the project exists as soon as you're in.

### Let the first run finish

You land in the project's panel with the site already live. A new project built from a template, with a site, a description or files to work from, starts the one-time trigger **Generate docs from your site** — or **Generate docs from your brief** without a site — and the agent's report arrives in **Inbox**.

<!-- /widget -->

The run replaces the template's placeholder wording with your product's real names, features and steps. It is told never to invent a price, a limit or an integration: what it can't confirm comes back as questions in the report.

## Which starting point fits?

<!-- widget:tabs -->

Only importing a repository needs GitHub. A template runs on a repository Docsbook creates and hosts for you.

### Your repo {git-branch}

Choose **Connect GitHub**, then your repository. Its Markdown becomes the site as it stands: Docsbook reads it, writes nothing back, and the one-time run doesn't start. Nothing rewrites your pages until you ask the agent or arm a trigger.

### Your website {globe}

Pick a template — **Docs shell** is the blank one — and put your site in **Main site**. **Generate docs from your site** reads about ten of its pages, pricing, features and existing docs first, and rewrites the template pages about your product.

### A description {file-text}

No site yet? Pick a template, fill in **What does your product do?** and attach any files or screenshots. **Generate docs from your prompt** drafts the docs from that material alone and removes the template pages it says nothing about.

<!-- /widget -->

## Where does your site live?

Every site gets a `docsbook.io` address the moment it's created:

| You started from | Your site's address |
|---|---|
| A template (Docsbook hosts the repo) | `https://<project-name>.docsbook.io` |
| Your GitHub repository | `https://<owner>.docsbook.io/<repo>` |
| Either, on your own domain | `https://docs.example.com` — see [custom domain](./site/custom-domain.md) |

Change the name in the address on **Settings ▸ General ▸ Site source**; nothing on GitHub moves. For a repository site, `docsbook.io/<owner>/<repo>` redirects to its address too.

## Hand the rest to your agent

From here the Docsbook agent does the work. Paste one sentence into Claude Code, Cursor, Codex or ChatGPT and it connects itself:

```text
Set up Docsbook for me. Fetch https://docsbook.io/get-started.md and follow it.
```

Then ask for outcomes in your own words — "document our API from the repo", "get us cited in AI answers" — as [Tell your agent, get discovered](./get-discovered.md) shows. To keep work coming without asking, arm ready-made [triggers](./agent/triggers.md) such as **Organic search audit** or **Answer what the chat could not**.

## FAQ

**Does Docsbook change my repository?** Not when you import it. Later, each change the agent makes arrives as a pull request that merges itself or waits for you, set on **Settings ▸ General ▸ When a change goes live** ([reviewing changes](./agent/review.md)).

**Why didn't the first run start?** It runs once, only for a new project built from a template with something to work from, and only when your balance covers a run. Otherwise your attached files are published as pages as they are, and you can ask the agent at any time.

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [Tell your agent, get discovered](./get-discovered.md) — Connect your agent over MCP and ask for outcomes {bot}
- [Find wins fast](./find-wins-fast.md) — How the agents pick the change that moves a number {target}
- [Edit and publish](./site/editing.md) — The editor, GitHub sync and your hosted repo {file-text}
- [Custom domain](./site/custom-domain.md) — Serve the docs from your own domain {globe}

<!-- /widget -->
