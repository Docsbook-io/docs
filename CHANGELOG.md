---
title: "Docsbook Changelog"
description: "Release notes for Docsbook — new features, fixes, and improvements to the AI-powered documentation platform shipped across every version."
---

# Releases

## NEW - 23.08.2026

### Added

- A `Lang` tab on the `Conversations` card in `Chat` shows which languages readers write in, each row with its flag, so a workspace serving several languages can see the split at a glance. `AI Chat`
- Every conversation in `Chat` — the dialog list, the sidebar, and the open conversation — now shows the flag of the language it was written in. `AI Chat`
- Every commit in `Changes` now carries one 0-100 score, with the four areas behind it: readers served, reach, cost to run and edit quality. Each area shows its own number, how much of the total it counts for, and how much data stands behind it. `Changes`
- A commit is scored the day it lands, from the diff alone, instead of showing nothing until its window closes two weeks later. `Changes`
- `Changes` now puts the cash figures up front: what re-translating the edited pages cost, what readers asking the chat cost either side of the commit, and total AI spend. `Changes`
- A `Widgets` gallery in settings shows every content widget your pages can render, each with a preview of the block it produces and a page describing the markdown it expects. `Settings`
- Any content widget can now be switched off for a project. Its comments stay in your files and every word between them still publishes; only the rich block is withheld. Switch it back on and every page that used it returns, with nothing to re-write. `Content Widgets`
- `Apply to a page` on a widget closes settings and turns on editing over your docs, offering that widget first on whichever block you pick. `Settings`
- `Analytics` now leads with six figures instead of four counts: visitors, revenue, conversion rate, revenue per visitor, bounce rate and session time, each showing how it moved against the period before it. `Analytics`
- An `Average Product Price` setting under `Branding`. Together with your `Call To Action URL` it turns readers who click through to your sales page into a revenue figure. Set only one of the two and the revenue tiles stay switched off saying which half is missing, rather than reporting a confident `$0`. `Settings`
- The visitors chart now splits new readers from returning ones, and its tooltip carries pageviews, pages per visitor and the returning rate for the hour or day under the cursor. `Analytics`
- `Bounce rate` and `Session time` are now reported per visit, so you can see how many readers arrive and leave without reading, and how long the rest stay. `Analytics`
- The average product price can also be set from the assistant and over MCP, through `update_branding`. `MCP`
- Every row of the analytics cards now carries revenue beside visitors, so you can see which pages, referrers, channels, countries, browsers and languages brought the readers who *bought* — not only the readers who came. One click switches all four cards between ranking by `Visitors` and by `Revenue`. `Analytics`
- Hovering a row shows its visitors, revenue, revenue per visitor and conversion rate, with buttons to filter by it or open it. `Details` on each card opens the same numbers as a full table. `Analytics`
- Filtering by a row narrows the whole dashboard — the other cards and the six figures above the chart — so a country, device or referrer can be read end to end. Filters stack, and each is a chip you can remove. `Analytics`
- New breakdowns: `Entry` and `Exit` pages, traffic `Channels` (organic search, social, referral, AI assistant, direct), `Countries` and `Languages`. `Analytics`
- `Pages` and `Headings` can now be ranked by `Views` and `Reading time` as well as visitors and revenue, and each figure counts only what happened on that page — a busy visit no longer makes every page it touched look busy. `Analytics`
- `Headings` is now a full breakdown: which section readers reached, how long they stayed on its page, and what those readers were worth. `Analytics`
- A `Keyword` tab in `Sources` shows the Google queries you rank for, with position, impressions, clicks and click-through rate, from your connected Search Console. `Analytics`
- Hovering a `Channels` row names the three sites the channel actually consists of, with their shares. `Analytics`
- `Languages` rows carry a flag, and `Referrers` rows show the subdomain in grey so the list reads by domain. `Analytics`
- Your workspace's background glow and accent color now carry into the AI chat panel too — full-screen and side-by-side — instead of stopping at the docs page's edge. `Theme Settings`
- Your docs now follow your commits: on the `Auto` translation mode, a push that changes a page re-translates it in every enabled language without being asked, within your existing budget and provider limits. `Translations`
- Every language page opens on whether that language is keeping up — coverage split into current, fallen behind and never translated, when it was last written to, and which commit your docs stand at. `Translations`
- A translation in progress now says what started it: you, someone else on the dashboard, switching the language on, or a commit Docsbook followed. `Translations`
- A language's last dozen runs are shown as a strip coloured by how each one ended, so a single failed run reads differently from a language that has not finished cleanly in weeks. `Translations`
- Each language can be switched on and off from its own page, with the same cost confirmation you get in settings. `Translations`

### Changed

- The `Top searches` tab on the `Conversations` card is now called `Searches`. `AI Chat`
- The `Limits` tab is now called `Usage`. `Usage`
- `Changes` opens on the answer instead of on the charts. The score, what moved and what it cost come first; every measurement behind them is one `The measurements behind this score` toggle away, with nothing removed. `Changes`
- A thin sample no longer refuses to judge. A handful of visits still moves the score, just far less, and the page states how confident it is. A score with little behind it is never coloured and never called a success. `Changes`
- `Feeds` puts everything that acts on the whole view in one row beside the list's name: `Export`, the time range and `Set up alert`, as three identical buttons. The range used to be a bare dropdown that read as a caption rather than a control. `Feeds`
- Each row of the `Add notifier` menu now has an edit control, so a destination attached to another list — or to none yet — can be opened without hunting for it. `Feeds`
- `New list from current filter` in the `Feeds` sidebar is now just `New List`. `Feeds`
- The live editor and the assistant now offer only the widgets a project has switched on, so neither can write markers that would not render. `Content Widgets`
- The settings gear on your docs site opens the panel on its main page instead of jumping into `Branding`. `Docs`
- The standalone `Support` button beside the gear is gone. Support is reachable from the settings panel's own sidebar. `Docs`
- `Online` is no longer one of the metrics above the analytics chart. It counts readers right now rather than over the period you picked, so it sits as its own live chip beside the panel title. `Analytics`
- The AI crawler chart moved from the metrics row into the `AI` tab of the `Referrers` card, above the per-bot totals it explains. `Analytics`
- The analytics cards are now grouped as `Pages`, `Sources`, `Audience` and `Conversions`. Nothing was dropped — every existing tab moved into one of the four. `Analytics`
- Visitors with no referrer are now a row of their own, `Direct / None`, instead of being left out of the referrer list. On most documentation sites they are the largest single source. `Analytics`
- Each analytics card picks its tab from a dropdown instead of a row of tabs that scrolled sideways inside the card. Every tab is one click away at any window width. `Analytics`
- `AI Views` moved to its own full-width card under the others, so the crawl chart is wide enough to show the shape of a crawl rather than just its total. `Analytics`
- `Read Time` is no longer a separate tab — it is a `Reading time` ranking on `Pages` and `Headings`, still on `Pro`. `Analytics`
- A period with very few visits now says so under the figures, instead of presenting percentages that move by whole points per visit as measurements. `Analytics`
- Project cards in the project picker show the connected repository's real GitHub avatar instead of a generic folder icon, and list your most recently used projects first. `AI Chat`
- `More` in the project picker now reveals two more rows at a time instead of the whole list at once, and relabels to `Load more` after the first press. `AI Chat`
- The project and conversation pickers in the chat header lost their border and background, with a bolder project name and tighter spacing. `AI Chat`

### Fixed

- The analytics `Details` view opened behind the settings panel that launched it. `Analytics`
- Long project names and site paths no longer overflow their card in the project picker. `AI Chat`

- Commits stopped showing up in `Changes`. The nightly collector walked only part of the projects it should have, so an active repository could go days without a single new entry while the run reported success. Every project is now collected on every run. `Changes`
- Commits stuck on `Maturing` long after their two weeks were up: the measurement queue drained newest-first, so once a backlog formed the oldest commits were never reached. `Changes`

### Removed

- The three summary tiles above the `Feeds` feed (all activity, needs attention, failed deliveries). The chips per event group stay and still filter in one click; `failed` moved into `Add filter` under `Delivery status`. `Feeds`
- The `Notifiers` group in the `Feeds` sidebar, and with one group left, the `Events` heading above the lists. Destinations are reached from the chips beside the filters, from `Set up alert`, and from the `Add notifier` menu. `Feeds`
- Overage billing. AI usage now simply pauses once the plan's monthly budget is used up — never billed above your plan price. `Usage`
- The repository browsing list under `Connect a repository` in the project picker. `Start a new project` connects a new repo instead. `AI Chat`
- The `Try Docsbook` prompt grid that used to follow a finished setup checklist. `AI Chat`

## NEW - 22.08.2026

### Added

- A new `Changes` tab lists every commit that touched your docs, with the page traffic before and after each one — and an on-demand check of whether a specific edit actually beat the rest of the site. `Changes`
- Every commit in `Changes` now shows what it cost: AI spend for the week before and the week after in dollars and percent, the share readers' own questions account for, cost per visit, and what re-translating the edited pages cost — with the sections served free from cache priced out. `Changes`
- `Changes` now reports what Google did with the pages a commit touched: average position, impressions, clicks and click-through rate against the rest of the site, a daily chart with the commit marked on it, and a per-URL rank table. `Changes`
- `Changes` now breaks each commit's visits down by country, reader language and device — every slice beside the same slice's move on the pages the commit did not touch, so growth that happened everywhere is not read as growth this edit caused. `Changes`
- `get_page_diff_impact` returns that same country, language and device breakdown, so an agent can tell a translation-shaped audience from a general rise in traffic. `MCP`
- A new `Dialogs` card lists every AI chat conversation individually — topic, funnel stage, answered/dead-end status, and estimated savings — open one to read the full exchange, its real cost, and how it compares to the topic's usual answer rate. `AI Chat`
- The `Conversations` card gets an `Outcome` tab — answered, dead-end, and unrated conversations at a glance, each opening straight into `Dialogs` pre-filtered. `AI Chat`
- Each conversation in `Dialogs` now shows what it actually cost to run, right next to its estimated savings. `AI Chat`
- Every language you translate into now has a page of its own under `Translations` — pick it from the sidebar to see how many readers arrive from that language's countries in the first place, how many of them actually read in it, where it landed and where it missed, what they read, and what the language has cost against a human translator. `Translation`
- A language you switch off keeps its page, so its stored pages and past readers stay readable next to the audience that is still arriving — which is what tells you whether to turn it back on. `Translation`
- `Select Chat` in the account menu lists every conversation in this project behind a search field, so a thread from last week is one query away instead of a scroll. `AI Chat`
- The `Agents` tab has a new `MCP` page listing every tool this project's MCP server serves — read live from the server, so it is never a stale copy — with each tool's description, its arguments, and the sentences to say to a connected agent to make it fire. `Agents`
- The `MCP` page marks the four tools a client can reach with no token at all, so you can see what a reader of your docs could call, not just what you can. `Agents`
- `Select Mode` in the account menu picks how the chat and your documentation share the screen: `Fullscreen`, `Sidescreen`, or `Preview` for the docs on their own. It sits on the doc toolbar's avatar too, so a chat you put away is always one click from coming back. `AI Chat`
- A `Changes` button sits beside the account control at the top of the chat, so the list of what was published to your docs is one click away from the conversation that wrote it. `AI Chat`
- The `Feeds` page now shows every event your workspace produces, including the ones no alert was watching, marked `not sent`. You no longer need a subscription set up to find out what your docs actually emit. `Feeds`
- Each event in `Feeds` lists the destinations it was handed to and what each one answered, under one status folded from them, so a fan-out that half succeeded reads as a failure worth opening. `Feeds`
- `not sent` is a filter of its own in `Feeds`, next to delivered, pending, retrying and failed. `Feeds`
- Test pings and replays appear in `Feeds` like any other event, so the panel can answer whether a test worked. `Feeds`
- The `Translations` tab has a reader map that plots every country your readers come from as its own flag, ringed in a colour saying whether a translation is actually reaching it — green where they read the docs in their language, amber where the translation exists and most still read the original, red where readers arrive and none of them do. It never counts your own language as a missing translation. `Translation`
- `Interactive mode` sits next to `+` in the composer: turn it on and the docs open beside the chat with click-to-edit armed. Turning it off stops click-to-edit and leaves the docs where they are, so the page you were editing does not disappear behind the chat. `AI Chat`
- The reader map opens framed on the countries you have readers in, and you can drag it to pan and zoom in on a crowded region — the flags keep their size as you zoom, so neighbours spread apart instead of overlapping harder. `Translation`
- Every country in the `Countries` breakdown now carries the share of its readers who landed on a translated page, coloured by the same verdict as its marker; point at a row to read what the colour means and light that country on the map. `Translation`
- `Search rankings` now opens with a one-click activation prompt when SEO, GEO and AEO are all off — showing what your rankings will look like and turning any of them on, free on every plan, instead of an empty tab. `SEO`
- An `Invite` button now sits next to `Visit` in the chat toolbar, and split view gets a fullscreen toggle beside it. `AI Chat`
- A notifier is now its own thing in `Feeds`: create the Slack channel, Discord channel or endpoint once, then tick it onto as many saved event lists as it should serve. Pausing, testing or deleting it applies everywhere it fires at once. `Feeds`
- `Add notifier` sits beside the filter chips — attach a destination you already have to the list on screen, or create one, without retyping its URL and secret. `Feeds`
- The `Feeds` sidebar splits into `Events` and `Notifiers`, each with its own create action, so a destination can be added before there is a list for it and a list before there is anywhere to send it. `Feeds`
- `Get Support` now has a message form built in — the reply address is prefilled from your account and stays editable, and the message goes straight to us without opening a mail client. `Settings`
- The `Feeds` page opens on a digest of the range: all activity, events that need attention, and failed deliveries as three counters, plus a chip per event group with its count — every number is a one-click filter on the feed, and clicking it again clears it. `Feeds`
- `Needs attention` in the `Feeds` digest counts the events where a reader hit a wall — unanswered chat questions, dead-end searches, stale content and translations, usage limits — separately from routine activity. `Feeds`
- The feed reads in day sections (`Today`, `Yesterday`, dates), and `Show more` grows the page in place instead of paginating. `Feeds`
- Every event type in `Feeds` carries its own coloured tile and glyph, and destination labels show the real Slack and Discord marks, so a mixed stream is scannable without reading it. `Feeds`
- Opening a feed card shows the full event: every delivery attempt with its response, replay, and the raw payload — the card itself stays a three-line summary. `Feeds`
- Export the feed you are looking at — filters and range applied — as CSV, JSON or NDJSON from the button beside the view's title. `Feeds`
- The notifiers firing on the list you are looking at now show as chips beside the filters — each with its channel's real mark, its name, and `paused` when it is off — and clicking one opens it. `Feeds`
- The `Agents` tab has a `Skills` page: every docs skill from the published catalog with its plan gate, install line, the sentences that trigger it, the MCP tools it calls, and its full instructions. `Agents`

### Changed

- The admin panel's sidebar now opens `Get Support` directly, replacing the old `Book a demo` link — booking a demo lives inside that tab now, alongside `Contact Us`. `Settings`
- The chat toolbar's site-link button now reads `Visit` with a leading external-link icon, instead of `Open website` as plain text. `AI Chat`
- The chat's top-left button shows the Docsbook mark instead of your avatar. It opens the same account menu, which names the account you are signed in as in its first row. `AI Chat`
- `Invite` in the chat toolbar is now a button with its label on it rather than a bare icon, so it is clear before you click that it adds someone to the workspace. `AI Chat`
- The `+` for a new conversation left the chat's top-left corner; `New chat` is the first row of `Select Chat` in the account menu, where it always was. `AI Chat`
- Every row in the `Conversations` card (topics, buying stage, coverage gaps, feedback) now opens straight into `Dialogs`, pre-filtered to that group. `AI Chat`
- The `Feeds` page dropped its wrapping card and the `Feed`/`Subscriptions` tabs: each saved list now shows its alert status right in the switcher, the sidebar drills into your lists the same way `Settings` drills into its categories, and setting up or managing an alert happens in one panel. `Feeds`
- `Chat` now opens into its own page from the sidebar, the same way `Settings` and `Feeds` do — `Dialogs` no longer sits beside `Conversations` as a separate card: it drops its own time range and filters (`Conversations` already covers the whole page) and loads older conversations automatically as you scroll. `AI Chat`
- The `Changes` tab drops its date-range picker, commit count and card frame — pick a commit from the scrolling list and its impact opens right beside it, as colored charts instead of a paragraph. `Changes`
- Everything on the `Changes` tab reads larger — bigger type, taller charts, roomier tiles and a wider commit list. `Changes`
- The `Agents` tab now drills into a catalogue of every docs-subagents agent grouped by pipeline; picking one lists its ready-to-run prompts instead of a single shared MCP-connection card. `Agents`
- The `Translations` tab is one page instead of three stacked cards: a single interval control now governs the impact figures, the reader map and both country breakdowns, which could previously each report a different period. `Translation`
- `Visitor Countries` and `Language Countries` are one card with `Countries` and `Languages` tabs, sitting beside the reader map instead of under it — the same Countries/Languages split used to appear twice on the tab, once as map tabs and once as two separate tables. `Translation`
- The preview pane's address strip is now a compact pill: a page picker that names the page instead of showing the URL, with open-in-new-tab, mobile width and reload beside it, and `Copy link` moved into the picker's menu. `AI Chat`
- The reader map dropped its colour legend: the breakdown rows beside it carry the colours now, on figures that say what they measure. `Translation`
- Mobile width in the preview now clamps the page to a real 430px card rather than emulating a phone, so what you check is the live page at that width. `AI Chat`
- The account avatar moved to the top-left of the chat, into the corner the conversation switcher, layout toggle and change-history buttons used to occupy: all three are named rows of its menu now, so nothing in the chat's chrome has to be recognised by its icon. `AI Chat`
- The commit list is reachable as `Changes` in the account menu, beside `Analytics`. `Changes`
- The `api` widget's playground now takes your workspace's colours instead of a fixed blue: the accent, buttons, focus rings and path parameters follow your brand, and the method chips stay readable on a dark or tinted page. `Widgets`
- Saved lists in `Feeds` are now created and deleted from the sidebar, and the list dropdown is gone from the panel, so one control owns which list you are looking at. `Feeds`
- The sidebar's plan usage meter is now clickable anywhere on the card, not just the `Manage` link, and highlights on hover to show it. `Billing`
- Standalone chat pages show the Docsbook mark and your project's name in the top-left corner instead of your avatar — the same account menu opens either way. `AI Chat`
- The `Powered by Docsbook` badge now shows in a footer strip under your docs on every plan, replacing the old sidebar toggle. `Branding`
- The `Feeds` filter menu is a quarter of its old width and picks one facet at a time — events, delivery status, destination or a payload search — with the event list flat and searchable instead of split across nine headings. Each active filter now reads as its facet and count, and clicking it reopens that facet. `Feeds`
- `Set up alert` is gone from the `Feeds` toolbar: an alert is a notifier attached to an event list, so it is made where both of those live. `Feeds`
- Every tag on a `Dialogs` row and on an open conversation's header — buying stage, outcome, docs gap — now carries its own colour instead of some falling back to plain grey. `AI Chat`
- The `Only failed` toggle left the `Feeds` toolbar: the failed-deliveries counter in the digest is the same switch with its number on it. `Feeds`
- Tool, agent and skill names across the `Agents` tab read as names (`Docs Planner`, not `docs-planner`), with the machine id kept verbatim under each title. `Agents`

### Fixed

- The translation savings, visitor and conversion figures no longer render blurred on a paid plan. `Translation`
- Alerts that stopped being delivered are firing again — every event was being dropped before it reached its destinations. `Feeds`
- Reader-language traffic is now measured against the language your docs are actually written in, so a workspace whose original is not English no longer counts its own pages as translated ones. `Translation`
- Hovering the reader map now opens the country you are pointing at. `Translation`
- Reader-map markers are now sized against the map's real width instead of always falling back to their smallest size. `Translation`
- An `api` widget endpoint with no example no longer renders its form at half width, and a `### Response` block now sits beside the example it should be compared with instead of under the form. `Widgets`
- Documenting `Authorization` in an `api` widget's parameter table no longer renders it a second time as a required query field, which would have put the reader's key in the URL. `Widgets`
- Deleting an event list, or detaching a notifier from one, can no longer leave an alert firing on every event in the workspace. `Feeds`
- `www.docsbook.io` now redirects to the apex domain instead of showing a 404. `Marketing`

### Removed

- The `AI Usage` and `Chats Analysis` cards — the numbers now live inside `Conversations` and the new `Dialogs` card. `AI Chat`
- The separate button for hiding the chat: `Visit` already hands the page back to your documentation with the conversation still running, and `Select Mode` names that same state as `Preview`. `AI Chat`
- `Remove Branding` — hiding the `Powered by Docsbook` badge is no longer possible on any plan. `Branding`
- The project-switcher pill in the chat composer — pick a project from the new top-left menu instead. `AI Chat`

## NEW - 21.08.2026

### Added

- Keep a single page out of search with `noindex: true` in its frontmatter. Until now the only control was the site-wide `SEO` toggle, so a changelog or a page of internal notes could not be hidden without hiding everything. `SEO`
- The pricing page now lists multiplayer chat under Growth and Scale, so the one capability a team is buying is visible before you subscribe. `Pricing`
- The startups page now answers its common questions instead of linking to a section that was not there: what happens to the price as the team grows, whether you need a tech writer or a CI/CD setup, and how you leave. `Landing`

### Fixed

- `docsbook.io/<owner>/<repo>/api/mcp/server` now answers MCP clients that follow redirects. The redirect to your project dropped the request body, so a tool call arrived empty and the endpoint replied "Invalid JSON" instead of listing your tools. `MCP`
- A link copied straight from GitHub's file view now opens on your docs domain instead of 404ing, so pasting `.../blob/main/README` works without hand-editing the path. `Docs`
- The example-prompt arrows in chat are now labelled "Previous / More example prompts", so they are no longer mistaken for a way back to earlier conversations. `AI Chat`
- A momentary limit on the AI provider is now retried, and falls back to a second key when one is configured; if it still fails you get a plain explanation instead of a raw provider error. `AI Chat`
- A page you have translated now shows its title in that language. Translated pages could fall back to the original-language title, so the line a reader sees in a search result was in a different language from the page itself. `Translation`
- Your sitemap now lists a language's URL only for pages actually translated into it. Enabling a language does not translate anything, so those URLs served your original text and asked search engines to crawl a page that points back to the original. `SEO`
- Translated pages of a site with several languages are now grouped correctly for search engines. One URL in the group that served untranslated content was enough for the whole group to be discarded, including the languages that were translated. `SEO`

### Changed

- An empty chat with no project selected now opens with your projects to pick from, and the connectable repositories under them. It used to open with the setup checklist, whose every step configures one specific site, so it asked you to brand, translate and publish a project you had not chosen yet. `AI Chat`
- The lists under the chat composer are set at a readable size and scroll with the page instead of inside their own box, so a long list is no longer cropped at an edge that looks like its end. The composer itself stays in the middle of the screen however long that list is. `AI Chat`
- The documented behaviour on renaming a page has been corrected: Docsbook does not create a redirect from the old URL. `SEO`

## NEW - 15.08.2026

### Changed

- The landing page's feature section now answers the four questions buyers actually ask, in the order they ask them: what the bill can do, what the docs return, whether you can act on that, and what it costs to leave. `Landing`
- Each of those cards leads with the numbers that decide the answer instead of a replica of the full dashboard behind it. `Landing`
- The landing page's call-to-action band is now a single input instead of three separate `Create from …` buttons. `Landing`
- AI chat answers now reveal word by word as they stream in, instead of a blinking caret. `AI Chat`

### Fixed

- Widgets on a generated draft site no longer link to pages that were never created. `Draft`
- Admin card deltas no longer blur when the card's icon node is mistaken for a leaf. `Settings`

## NEW - 14.08.2026

### Added

- Ask the assistant what to improve and the answer is now a list you tick, not prose you re-type. Each row is one concrete change to one of your real pages, or the settings card that applies it; tick several and press `Apply` once, and they are all done in a single pass. Nothing is ticked for you, and what you leave unticked is never written. The list is drawn from the documentation skill that covers what you asked, what can be measured about your site, and the cards that exist — not from what the model already believed about the topic. `AI Chat`
- The same picker works on a draft before you have an account, and applying picks that span several pages updates all of them in one go. `Draft`
- A correction that redefines what your business is now offers to regenerate the whole site instead of quietly fixing only the page you had open, and says up front that regenerating discards edits you have already made. `Draft`
- A freshly generated draft opens with a summary of what was read and written, plus one-click follow-ups. `Draft`
- The first-day `Try Docsbook` cards now lead with filling in your docs and saving them to GitHub. `AI Chat`

### Changed

- The onboarding wizard builds the docs inside itself and lands you on the finished site, without asking the same question twice. `Onboarding`
- The settings panel no longer opens itself over a preview or a freshly generated draft — it interrupted the first look at the site. `Draft`
- AI chat answers are set in a tighter line-height. `AI Chat`
- The landing page's first screen states what Docsbook is and what it costs. `Landing`
- The landing page now opens on what you get, a branded site from your GitHub docs in 15 seconds, and its main button reads `Get started`. `Landing`
- Disabled `SEO`, `GEO` and `AEO` toggles now sort to the top of the SEO panel so you see what to turn on first; a toggle you just enabled stays put until you reopen the panel. `Settings`
- The button that hands a draft or preview site to you is labelled `Publish Free`, or `Claim ownership` when you arrived through a mailed claim link. `Draft`
- Opening the language switcher on your own site before any language is enabled now offers to activate them and takes you to the translation settings, instead of reporting that none are added. Readers of your published docs still see the plain notice. `Translations`

### Fixed

- A question asked on a draft is answered as a question instead of quietly rewriting the page you had open. `Draft`
- A visitor reading a preview of a repository that has no workspace yet gets their question answered instead of `Sign in to make changes`. `Draft`
- The draft chat showed the platform's own spending cap as if it were the visitor's. `Draft`
- A draft edit that mixed in another page's content is rejected rather than written over the page you were on. `Draft`
- The AI no longer offers a preview visitor the full 36-card owner library, or a working Account/Invite pair next to the locked one. `Draft`
- Typing on `/chat` with projects but none selected no longer sends you into the create flow. `AI Chat`
- Asking for a change on the project you already have open no longer tries to create it again. `AI Chat`
- `Start new project` from a workspace subdomain no longer 404s, and the project switcher no longer doubles the organisation in its path. `AI Chat`
- Country flags in the translation language picker now render the same on every platform instead of depending on the operating system's emoji font. `Translations`
- A new workspace can use its free AI budget straight away instead of hitting an empty-balance notice before its first question. `Billing`
- Opening the settings panel no longer blanks the documentation page for a signed-in owner. `Settings`
- Documentation pages with non-Latin paths load instead of failing with a server error. `Docs`
- A site whose homepage the repository listing missed now falls back to reading `README.md` directly. `Docs`
- Switching or resetting the sidebar language now lands on the right URL. `Docs`
- Images that ship several sizes (`srcset`) resolve their relative paths like ordinary images. `Docs`
- The default side chat no longer opens an empty rail. `Docs`
- The change history panel asks you to sign in instead of showing a raw `Unauthorized`. `Docs`
- The toolbar's `Claim` button no longer reopens the sign-up modal for someone already signed in. `Draft`
- Analytics tab strips on a phone use the full width and scroll instead of clipping. `Analytics`
- The Limits panel no longer reports a brand-new wallet as out of budget. `Billing`
- The `Compare all plans` table no longer overflows the Upgrade Plan modal, and that panel no longer mentions per-seat pricing. `Pricing`
- On a phone, the preview's Design settings had no route to pricing. `Settings`
- Numbers next to icons stay blurred in an anonymous preview. `Analytics`
- A `GET` to the MCP server routes is rejected outright instead of hanging until the request is killed. `MCP`

## NEW - 10.08.2026

### Added

- The empty chat now offers four ways to start — from a GitHub repo, from your website, from an idea, or from files and screenshots — and each one opens the create flow with that source already chosen, so you go straight to the one question it needs. `AI Chat`
- `Start a new project` is now always in the project menu, not only when a project is already open. `AI Chat`
- Opening a preview or a draft now puts the site and the chat side by side, so you can see a change as you ask for it. `Draft`

### Changed

- Custom domain and white-label now start on `Pro` instead of `Business`. Your own domain and your own brand are the first two things a site owner wants, so they no longer wait for the $159 tier. `Pricing`
- The preview tour introduces branding second-to-last, closer to the point where you would use it. `Onboarding`

### Fixed

- `Start from an idea` and the other build shortcuts used to start generating without ever asking what to build from, and named the result on their own. They now ask first. `AI Chat`
- `Upgrade plan` did nothing when clicked on a chat with no project selected. `Billing`
- Plans on `/pricing` could not be bought: the upgrade CTAs dropped the plan you picked, and the two top tiers were sold with the wrong AI budget. `Pricing`
- The wizard's `See the magic` step failed with an error instead of building your site. `Onboarding`
- A repository preview opened on a workspace subdomain returned a 404 when you sent a message. `Draft`
- Signed-out visitors editing a preview saw a raw `HTTP 401` instead of an invitation to sign in — and the sign-in button that replaced it was invisible against its own background. `Draft`
- Switching tabs in the settings widget kept the previous tab's scroll position. `Settings`
- `Claim website` no longer overflows its row on a phone. `Draft`
- Showcase sites had a canonical URL that pointed in a loop and no sitemap of their own. `SEO`

## NEW - 08.08.2026

### Added

- Enabling a language now asks you to confirm, showing how many pages will be translated, the estimated cost and your remaining budget. When the run does not fit, it says what share of your docs the budget covers and offers the upgrade. `Translations`
- Each enabled language shows what its translation run is doing: a progress counter while it works, and a `Stopped` marker you can hover for the reason when a run ended early. `Translations`
- Long translation runs resume on their own until every page is done, and the pages a commit changed are translated first. `Translations`
- A draft's toolbar now offers `Share`, which copies a link to the page you are on so you can send the site to whoever decides. `Draft`

### Changed

- The draft's blue button now says what a click does: `Claim website` while the generated site stands as built, `Save changes` once you have customised it. It was called `Publish`, which named an outcome a visitor without an account could not reach. `Draft`
- In the full-screen chat, `Preview` is now `Open website` — it leaves the chat for the site, rather than naming a state you were already in. `AI Chat`
- The project switcher offers visitors without an account `Claim website` instead of `Sign up to connect a repo`. `AI Chat`

### Fixed

- Webhooks now actually fire. Registered subscriptions never matched the events the product dispatched, so no real event had ever reached a subscriber's endpoint. `Webhooks`
- Registering a webhook accepts the event names exactly as this documentation writes them, with a dot. `Webhooks`
- A translation run that is interrupted no longer blocks that language for hours. Stalled runs are detected and picked up automatically. `Translations`
- Re-translating a page you barely touched no longer pays to translate the parts that did not change. `Translations`
- Readers no longer see a banner claiming they are looking at the original when a translation is on screen. `Docs`
- The sidebar no longer shows translated labels on a page whose body is still in the original language. `Docs`
- Turning a language off explains that nothing is deleted and that turning it back on does not pay again for unchanged pages. `Translations`
- Answers about paid features keep the plan requirement instead of describing the steps as if the feature were available on any plan. `AI Chat`
- The docs chat no longer invents integrations that do not exist, and admits when a topic is not covered. `AI Chat`
- Search finds the right page for questions asked in ordinary language, instead of failing on filler words and word endings. `Search`
- AI spend is billed at the rate your plan states. A rounding floor inflated the cost of small requests. `Billing`

## NEW - 07.08.2026

### Added

- `CTA Clicks` shows how many readers left your docs through a link you placed there, with a trend chart and a ranked list of the destinations they clicked. `Analytics`
- Per-source spend limits let you cap what one source may spend each cycle, so AI translations or the semantic index can never eat the whole budget. Each bar under `Spend by source` now shows your limit next to the plan's own. `Limits`
- `Semantic Search` turns meaning-based answers on or off for your readers, shows when the index last updated, and keeps the rebuild controls in one place. `AI Chat`
- Ask the chat what to fix in your docs and the answer arrives as ranked recommendation cards, each opening a fresh chat that already knows the page and the problem. `AI Chat`
- A `recommendations` widget renders a marked list of findings as cards, ranked by how much each one is costing you. `Docs`
- A `Feedback` tab next to `CTA Clicks` ranks your pages by the thumbs readers gave them, most-disliked first, counting both the page rating and the votes on AI answers given there. `Analytics`
- A `Feedback` tab in the chat card shows which topics readers approve of and which they vote down. `AI Chat`
- `Search rankings` leads with four figures — impressions, clicks, average position and the queries you rank for — each with its own trend, and every query row carries the action to take on it. `SEO`

### Changed

- `Analytics Explorer` opens on an overview instead of a report picker: headline figures across the top, then every report as a row showing what it found, its key number and its trend. Click a row to expand the full report, filters and export in place. `Analytics`
- Each report in `Analytics Explorer` now renders in the shape its data means, so there is no chart-type menu to get wrong, and every row carries an icon you can scan for. `Analytics`
- `AI Views` moved in as a tab of the Referrers card, and the `UTM Parameters` tab is now simply `UTM`. `Analytics`

### Removed

- The `Pages` tab is gone. Its semantic graph now lives on as `Semantic Search` in `AI Chat`, its recommendations moved into the chat itself, and change history stays available where you already track it. `Dashboard`

### Fixed

- Switching the doc language from inside a subfolder no longer leads to a 404 page. `Docs`
- The semantic index now builds when you ask for it and keeps itself up to date as your docs change, instead of staying empty and leaving meaning-based answers falling back to keyword search. `AI Chat`
- Long URLs in `Search rankings` are shortened to fit the card instead of pushing the table sideways. `SEO`
- Clicking a search result now jumps straight to the matching section instead of the top of the page. `Search`

## NEW - 03.08.2026

### Fixed

- Pricing pages across the docs (blog comparisons, MCP reference, AI features overview, quick-start, branding guide) no longer show AI chat, SEO/GEO/AEO, or the MCP server as paid-tier features — they are free on every plan, including Free. Custom domain and white-label are now correctly attributed to Business (not Pro), and the Source-of-Truth content graph to Business (not Pro). `Docs`

## NEW - 02.08.2026

### Added

- Any change the assistant publishes can be undone from the chat: an undo button on the card that announced it, and a clock icon in the chat header listing recent changes with an undo beside each one. Undoing writes a new commit rather than rewriting history, so it shows up in the list itself and never discards a teammate's work. `AI Chat`

### Changed

- Ask AI on a draft is no longer capped at 3 messages before signing in: it now runs on a free daily AI credit, so short questions barely count while rewriting a long page uses more of it. `AI Chat`

### Fixed

- Asking a question on a docs site that has no AI chat connected now explains that in plain language instead of showing `HTTP 400`. `AI Chat`
- A draft message sent after the free AI credit runs out no longer disappears: it stays in the conversation with the explanation beneath it, instead of the chat looking as though nothing was sent. `AI Chat`
- The `Sign in` prompt on a draft now opens the sign-in window over your site, with GitHub, Google and email, instead of sending you straight out to GitHub. `AI Chat`

## NEW - 01.08.2026

### Added

- A blue `Upgrade` badge appears next to the account controls in the docs toolbar for free-plan workspaces. `AI Chat`
- The chat header's `GitHub` icon now shows a green dot when your GitHub account is linked, and clicking it opens a switcher listing your account and every organization you belong to — hover one to see its repositories and connect one as a new project. `AI Chat`
- Editing a page can now add content, not just change it: hovering the seam between two blocks reveals a plus button that inserts a paragraph, heading, list, code block, quote, callout, table or content widget right there. `Block Editor`
- An `Add a page` button in the sidebar creates a new documentation page from a title, a folder and an optional brief. `Block Editor`
- Your AI agent can now read a public web page and get it back as clean Markdown, so it can check your docs against a competitor's pricing, your own marketing site, or a link that may have gone dead. `MCP`
- Signing up now starts by asking what you do — founder, developer, technical writer, marketing, support — so the product can speak to your job rather than treat everyone the same. `Onboarding`
- A `Call To Action URL` field sets the one page your docs should drive readers to. Your AI chat points evaluating readers there, content generation writes pages towards it and can add it to your header as a button, and analytics counts conversations ending on that domain as reaching the goal. `Branding`
- The welcome questions now end by asking where your docs should send readers, so your first pages are written towards a real destination. The step is optional and can be skipped. `Onboarding`
- Your AI agent can read and set the call-to-action page through `update_branding`, and sees it on every workspace it reads. `MCP`

### Changed

- The chat's target page setting moved from `AI Chat` to `Branding` and is now called `Call To Action URL`, since it is your project's goal rather than a chat option. Anything you already set is unchanged. `Branding`
- A site built before signing up now keeps the call to action found on your own website, so the published project starts with a goal instead of a blank field. `Onboarding`
- If you built a site before signing up, the welcome questions no longer ask what you are documenting: your site publishes while you answer, and finishing takes you straight to it instead of an empty chat. `Onboarding`
- A conversation you started before signing up carries over to your new project and reopens beside your documentation, so you can pick it up where you left off. `Onboarding`
- The docs toolbar's `Ask AI` button is now two icon buttons next to your avatar: `Chat` opens the full AI chat directly with the composer focused, `Editor` arms block-level editing with no chat needed. Pressing the active one returns the page to its normal state. `AI Chat`
- The conversation switcher left the docs toolbar — past chats are switched from the chat's own header, where a conversation is on screen to switch away from. `AI Chat`
- The `Invite` button in the chat header is now a plus-icon next to your account avatar, matching the header's other icon-only controls. `AI Chat`
- The account menu (theme, Integrations, sign out) and the `Workspace settings` gear moved from the chat input's footer to the header, next to your avatar. `AI Chat`
- The admin/reader mode toggle inside an open chat is gone — the mode now follows how you opened the chat (the admin toolbar starts the builder, a site chat widget starts reader mode). `AI Chat`
- The Docsbook mark in the docs toolbar is now the project switcher, so you can move between projects from any documentation page. `AI Chat`
- `Preview` in a chat opened from your documentation now puts the chat away and hands the page back to the doc underneath, instead of navigating and losing the conversation. `AI Chat`
- The full-screen/side-dock toggle appears once a conversation has something in it, since an empty thread has nothing to watch beside the page. `AI Chat`
- Bringing a hidden conversation back restores the shape you hid it from, full screen or side dock, rather than always reopening as a side dock. `AI Chat`

### Fixed

- A workspace's forced light or dark theme no longer loses to the system theme in the AI chat and other admin surfaces. `Branding`
- Reopening a past conversation no longer restores it as a chat you cannot see, and the docs toolbar no longer shows `Chat` as active while a plain documentation page is on screen. `AI Chat`
- Dropdowns inside a full-screen chat stay clickable after arming the block editor — the editing affordances now stand down while the page they edit is covered. `Block Editor`
- The side-by-side view no longer opens with a strip of empty space above the page header and subheader. `AI Chat`
- The sitemap now lists each marketing page's real publication date instead of the time it was last crawled, so Google can trust which pages actually changed. `SEO`
- A step the assistant never finished no longer spins forever when you reopen the conversation: it is marked as interrupted and tells you to send the message again. `AI Chat`
- A conversation cut short by a dropped connection stays usable, where before every following message failed. `AI Chat`
- Expanding a step in the assistant's trail now always shows what it ran on and what came back, instead of opening onto an empty panel. `AI Chat`
- Steps in the assistant's trail now name what they did and what they found, such as the traffic numbers they read, rather than repeating the name of the operation. `AI Chat`

## NEW - 31.07.2026

### Added

- A new `Stepper` content widget renders headed sections as a numbered, connected sequence — for installation guides and multi-stage tutorials where order matters. `Content Widgets`
- Two new call-to-action content widgets close a page with the next step the reader should take: `cta` renders a heading and one or two buttons, and `cta-form` turns the primary action into a single field whose value is carried into the target URL. Both stay compact so a documentation page still reads as documentation. `Content Widgets`
- A [Content Widgets](./content/features/widgets.md) page documents all six widgets, their markdown contract, and how to insert one from the block editor. `Documentation`
- Generated draft sites now close their selling pages with a call-to-action block, chosen from the widget catalog rather than a fixed list, so a newly shipped widget reaches generated sites automatically. `Site Generation`
- A Docsbook-hosted project can now be moved into a GitHub repository you own, straight from the chat header: Docsbook creates the repository and copies every page across in one commit. Note that the public URL changes and the move is one-way. `AI Chat`
- A GitHub button in the chat header shows where a project's source lives, and connects an account when there is none. `AI Chat`

### Changed

- The chat header now shows the Invite panel on every plan, with sending gated to Growth, so you can see collaboration before buying it. Inviting by email and creating an invite link sit in one place. `AI Chat`
- The chat's close icon is now a labelled `Preview` button that leads to your documentation site. `AI Chat`

### Fixed

- The auto-generated TL;DR block now replaces the opening paragraph it was taken from, instead of repeating the same sentence directly below itself. `GEO`
- Cards, tables, and the accordion/stepper surface now match a custom-branded workspace's background instead of staying stark white. `Branding`
- Documentation edits made through a connected AI tool no longer report success while writing to an abandoned repository, on projects that were moved to their own GitHub. `MCP`
- Editing on the live page is now documented as its own method alongside GitHub and Claude Code — the guide promised three ways to edit and listed two. `Documentation`
- The FAQ links in the documentation-management guide pointed one folder too high and led nowhere. `Documentation`
- The sidebar now opens with your introduction and quick start instead of whatever page happens to come first alphabetically, and leaves reference pages, changelogs and FAQs at the end. Previous/next links follow the same order. `Navigation`
- The drag handle no longer disappears as you move the pointer toward it, so blocks can actually be dragged. On a narrow preview it sits over the block's first line rather than being pushed onto the text. `Live Editing`
- Dragging a heading now moves its whole section on the page, matching what the edit is described as doing — previously the heading moved alone and left its content behind. `Live Editing`

## NEW - 30.07.2026

### Added

- Add a [lucide](https://lucide.dev/icons) icon next to any page or folder in the left sidebar, and to any tab in the subheader folder navigation. `Sidebar`

## NEW - 29.07.2026

### Added

- Ask AI now works on a draft before you sign in — 3 free messages, then a sign-in prompt to keep chatting and save your site. `AI Chat`

### Improved

- Every paid feature in the plan comparison now carries a question-mark tooltip explaining what it buys your business, in plain language rather than capability names. `Billing`
- The semantic doc index is now described by what it actually does for you: it is the biggest single improvement to AI chat answer quality, the chat answers from the exact section with the page cited instead of inventing one, and replies come back faster. `AI Chat`

### Changed

- The guided tour of a preview now walks you through the real settings panel filled with sample numbers, instead of standing in for it with a picture. `Preview`
- Prices are no longer hidden from visitors who have not signed up: the full plan comparison is visible in a preview, and picking a plan opens the signup form. `Billing`
- Every sign-up prompt in a preview now opens the signup form where you are, rather than sending you to a page that asks you to sign in again and loses the preview you were exploring. `Preview`
- Generating your first draft no longer pops the settings panel open over your new site — it stays open, with a "Customize your site here" hint pointing at the gear instead. `Preview`

### Fixed

- The guided tour no longer crashes on the Translations step. `Preview`
- The Search rankings card in a preview no longer claims Search Console is not connected. `SEO`
- The project picker no longer offers a visitor without an account a "Connect GitHub" action that could not apply to them. `AI Chat`
- The Semantic Graph card on a plan below Business now opens a page explaining the feature before sending you to the price table. `AI Chat`
- Long feature explanations in the plan comparison no longer get cut off at the edge of the Business column. `Billing`
- Clicking a page link inside an anonymous draft at `docsbook.io/draft` no longer redirects to a broken `draft.docsbook.io` subdomain. `Preview`
- The feature unlock cards no longer advertise plans and features that do not exist: there is no "Starter" tier, DeepSearch was removed long ago, and Custom Questions is free on every plan rather than Pro. `Billing`
- Unlock cards now quote the real numbers instead of stale ones: your monthly AI budget in dollars rather than a query count, 15 supported languages rather than "50+", and the actual chat model and MCP tool counts. `Billing`
- Extra usage is now described the way it is actually billed, in dollars against your monthly spend limit, instead of a per-query price that was never charged. `Billing`
- Paywall messages now name the tier you can actually buy, "Pro", instead of a "Pro+" plan that is not on the price list. `Billing`
- The chat feature is now called `AI Chat` everywhere in the admin panel, instead of switching between "AI Agent" and "AI Chat" between screens. `AI Chat`

## NEW - 28.07.2026

### Added

- Growth and Scale can now work in the AI chat together: see who from your team is in the chat, invite a teammate by email, and watch the same answer stream in for both of you instead of relaying it through Slack. `AI Chat`
- You can now see whether each visit actually succeeded — visits, outcomes, dead-end pages and exit pages are reconstructed from your existing events, with crawler traffic and inflated read time filtered out. `Analytics`
- The new Explorer replaces the raw event feed with charts, click-to-filter facets that show counts, drill-down from chart to table to individual visits, and CSV export. `Analytics`
- Seven new analyses answer real business questions: the routes readers walk, where they leak out of a funnel you declare, reverse funnels from successful visits, W1/W4 retention, searches that got results but no clicks, rage signals, and any headline metric plotted over time. `Analytics`
- Filters are now a searchable multi-select dropdown per dimension, offered only where the current view supports them, and language is filterable for the first time. `Analytics`
- Every number now ships with what it means for your business, what can make it misleading, and which metric to read it alongside. `Analytics`
- Chat is now a unit of analytics: questions from one reader group into a conversation, clicks on links the AI cites are tracked, and new conversation and intent views show what readers ask and why. `AI Chat`
- The SEO/GEO tab now shows your real Google Search Console positions, including which queries are worth improving, with no OAuth or domain verification needed on a `*.docsbook.io` subdomain. `SEO`
- Search rankings gained a Search Health Score, period-over-period comparison, rising and falling queries, and pages Google shows but nobody clicks. `SEO`
- Business plans can now build a semantic index over their docs, so readers' chat questions find the right page by meaning even when it shares no keywords, plus a relationship graph of how pages connect. `AI Chat`
- Content health merges the relationship graph, semantic index and findings into one card that names orphan pages, meaning-duplicates, broken links, unread pages and key hubs, each with a concrete next step. `Analytics`
- Your custom questions now appear as clickable suggestion chips when a reader focuses the chat input, and adding a skill swaps them for that skill's own example questions. `AI Chat`
- A new `/showcase` page browses live Docsbook sites by category, including five real customer sites. `Landing`
- A new **Search + Ask AI** header preset puts a wide search bar in the middle of the header with the Ask AI button right beside it, so both primary actions sit together instead of being split across the right edge. `Design`
- Headings and body text can now use different fonts, so you can pair a display face with a readable content face. `Design`
- The language of your docs is now detected automatically, so there is no Auto-detect button to press. `Translation`
- Translation Activity is now a searchable table of your pages: each row shows whether a page changed in git and whether its translations followed, per language, with a retranslate button on the row. `Translation`
- Opening a page from that table shows every language's state side by side, your source text next to the translation, and lets you correct a translation by hand without it being overwritten by later automatic runs. `Translation`
- Analytics can now chart AI Visits as one line per crawler, so you can see which AI assistants read your docs and how that changes over time. `Analytics`

### Changed

- Growth and Scale now include every Business capability — custom domain, white-label, webhooks, your own AI and translation keys, UTM analytics and API reference — which the higher-priced tiers were previously denied. `Pricing`
- Source of Truth and white-label are now Business features, and the pricing page, plan modals and AI upgrade prompts no longer advertise them at the Pro price. `Pricing`
- The homepage now leads with what your docs do for your revenue rather than the underlying tech, and the FAQ accordion is replaced by a gallery of live customer docs. `Landing`
- The **Split** header preset is replaced by **Search + Ask AI**; if you were using Split, your header keeps its current arrangement and you can rebuild it from the nav-link position field. `Design`
- A draft generated before signing in now opens as a real documentation site — header, sidebar tree, outline, breadcrumbs and prev/next — so you can browse every generated page and tune branding, layout and SEO before deciding to publish. `Design`

### Removed

- The separate AI Spend card is gone from the AI Chat tab. What the assistant cost you now sits as an expandable line at the bottom of `Conversations`, so the tab leads with what the chat did for your business rather than what it billed. `AI Chat`

### Fixed

- Answers in the docs chat now cite the pages they came from. Citations were previously empty on every answer, so readers had no way to jump to the source. `AI Chat`
- Free workspaces no longer see a "credit almost gone" warning on their very first visit, before spending anything. `AI Chat`
- Visitors, page views, top pages, referrers and events now exclude crawler traffic, which was up to 93% of pageviews on some sites. AI Visits remains the one card that reports bot volume. `Analytics`
- Search rankings now report your full search volume instead of only the fraction Google exposes per query, and time windows are anchored to the date Google's data actually covers. `SEO`

## NEW - 27.07.2026

### Added

- Paid plans no longer hard-stop when the monthly AI budget runs out — usage continues as metered overage billed on top of the subscription, up to a monthly cap you set yourself (default $20/month) from the Limits tab in workspace settings. `Billing`
- Annual billing (20% off) is now wired end-to-end through checkout for Pro, Business, Growth, and Scale — the toggle appears in the pricing tab once Paddle annual prices are configured. `Billing`
- Per-model AI spend view showing what each call cost at the provider's real price. `AI Chat`
- Translation activity and spend breakdown. `Translations`
- Re-translate a single page or a whole language on demand, straight from the Translation Activity panel. `Translations`
- Translation Activity now reports how many pages have fallen behind your source content, and how many point at files that were renamed or deleted. `Translations`
- Per-language coverage shows, for every page in your docs, how many are translated and current, how many are behind, and how many have no translation at all — so you can tell at a glance whether a language is genuinely complete. `Translations`
- Filling in a language translates only the missing and outdated pages; pages already up to date are skipped and cost nothing. `Translations`
- Live progress while a translation run is going, including why a run stopped early when it hits your budget or the provider's quota. `Translations`
- Translation spend is now shown next to how many page sections were reused from cache instead of re-translated. `Translations`
- Correct a machine translation by editing its text directly, instead of re-uploading the whole page. `Translations`
- Choose which AI model answers your readers, from Pro upwards. `AI Chat`

### Changed

- One subscription now covers several projects through project seats instead of being bought per workspace. `Billing`
- AI usage is measured in money rather than tokens, so your plan's monthly allowance and every charge are shown in dollars. `Billing`
- Every paid plan now includes an AI budget equal to its price: Pro gives $59 of AI usage a month, Business $159, Growth $349, and Scale $899. `Billing`
- AI usage is now charged at the provider's real model price plus 150%, replacing the previous 20% markup. A Pro budget covers roughly 15,000 answers a month on the default model, and switching to a cheaper model makes it go further. `Billing`
- Analytics history now follows your plan: 24 hours on Free, 7 days on Pro, and 30 days on Business, Growth, and Scale. `Analytics`

### Fixed

- Subscribing now funds the AI budget on your account. Activation credited an unused balance, so a new subscriber could pay and still see an empty budget. `Billing`
- The `MCP Server` card in the `Integrations` tab now renders with its plan badge and upgrade footer instead of a bare blurred panel. `Integrations`
- Documentation corrected across pricing, plans, AI chat, API, and analytics pages, which still described token budgets, per-workspace billing, and analytics windows that no longer match the product. `Docs`
- Translation freshness is now measured against your actual source content. The previous check never flagged anything, so sites could serve translations of long-changed pages while reporting everything as current. `Translations`
- The per-language "Last update" time was off by your timezone offset, making fresh translations look hours old. `Translations`
- Translation docs no longer claim that pushing to GitHub re-translates changed pages on its own — it does not, and the new Translation Activity panel is how you catch pages up. `Docs`

## NEW - 24.07.2026

### Added

- You can now generate a documentation site without an account — pick a website URL to scan, a GitHub repo to link, or just describe an idea in text at `docsbook.io/create`, then preview and AI-chat-edit the draft before signing in. `Onboarding`
- Anonymous drafts get a live split-screen chat + preview (or a full-screen preview at `/draft`), with a short trial of AI edits before you're asked to sign in. `Onboarding`
- Signing in after building an anonymous draft automatically publishes it as a live workspace — no re-work needed. `Onboarding`
- Workspaces can now be made private, requiring a password and/or your own SSO/OIDC identity provider (Google Workspace, Microsoft Entra ID, or Okta) before anonymous readers can view them. `Privacy & Access`
- Two new plans: Growth ($349/month) and Scale ($899/month), for teams that want deeper analytics, conversion tracking, and workflow features on top of the existing plans; annual billing on any paid plan now gets a 20% discount. `Pricing`
- A public Security & Privacy page explains how visitor analytics avoid PII, don't use tracking cookies, and can never link the same visitor across two different workspaces. `Security`
- Two new pages for API-first SaaS teams and AI/LLM companies show how Docsbook fits their specific documentation needs. `Marketing`
- A case studies page, including a real look at how Docsbook documents itself, plus an ROI calculator that estimates support-ticket savings from self-serve docs and AI chat. `Marketing`

### Changed

- Business plan price corrected to $159/month everywhere — pricing page, FAQ, and machine-readable `/pricing.md` and `/llms.txt` now agree with the actual checkout price. `Pricing`
- Webhook registration now requires the Business plan consistently, whether registered via the dashboard or an MCP agent. `Webhooks`
- MCP tool count claims corrected to the real number across the site and `/llms.txt`. `MCP`
- Landing page copy reworded to lead with outcomes (traffic loss, AI vs Google attribution) instead of pricing gimmicks or raw tech specs. `Landing`
- `/llms.txt` and the shared preview image now describe Docsbook's current positioning instead of an outdated tagline. `SEO`
- Homepage copy and structured data now frame Docsbook around growth and conversion outcomes, not just docs hosting. `Landing`

### Removed

- The discontinued one-time lifetime plan is no longer offered anywhere, including in AI chat upgrade prompts. `Billing`

### Fixed

- Failed documentation searches (zero results) are now tracked and queryable via the MCP analytics tools, closing a gap where this data silently went missing. `Analytics`
- `/llms-full.txt` no longer silently serves a "Failed to generate" stub when the docs source is unavailable — it now falls back to the same content as `/llms.txt`. `SEO`

## NEW - 18.07.2026

### Added

- Guided setup after sign-up: a short questionnaire asks whether you have a site, a GitHub repo, or just an idea, then takes you straight to your docs or starts generating them. `Onboarding`
- A live demo gallery on the homepage lets you page through real generated docs before signing up. `Marketing`

### Changed

- AI chat is now available on every plan, including Free — plans differ by the monthly AI token budget, not by a feature switch. `AI Chat`
- SEO, GEO, and AEO optimization now apply to docs on every plan, no longer Pro-only. `SEO`
- The chat now shows an upgrade prompt in place of the plan badge when you approach your limit. `AI Chat`

### Fixed

- Monthly AI token budgets now reset correctly at the start of each billing period. `Billing`

## NEW - 17.07.2026

### Added

- `GitBook` and `Mintlify` comparison pages with a feature-by-feature table and FAQ. `Marketing`
- `/pricing.md` — a plain-markdown pricing page for AI agents to read directly. `Pricing`
- Plan badge in the chat input footer shows your current plan and remaining free credits. `AI Chat`

### Improved

- Doc page titles are now derived from the page's own H1 heading instead of its filename. `SEO`
- Sitemap no longer collapses nested `README` pages onto the repo-root URL. `SEO`

### Fixed

- Internal links that pointed at a blocked documentation path now resolve to the canonical `/docs/*` URL. `SEO`
- A doc URL with different letter casing than the source file now redirects to the canonical URL instead of 404ing. `SEO`
- Section breadcrumbs now link to that section's own landing page instead of an arbitrary first page. `Navigation`
- Decorative background animation on the homepage no longer leaves placeholder text in the page source. `SEO`
- Sign-in link now shows the correct "Welcome back" or "Sign up" heading based on intent. `Auth`

## NEW - 14.07.2026

### Added

- Hosted demo sites now reachable directly on `docsbook.io/<name>` (e.g. `docsbook.io/host4-ai-demo`), no subdomain needed. `Routing`
- Partner demo workspaces — a temporary Pro trial can be granted and handed off to the client via a one-click claim link that transfers ownership. `Workspace`
- `MCP Server` card in the `Integrations` tab — copy your workspace's MCP endpoint alongside the API key. `Integrations`
- `Header Layout` card — pick a preset arrangement (Classic, Search-centric, Split, Centered, Minimal) for the header's theme toggle, search, Ask AI, and nav links; independent of which blocks are shown. `Header`
- `Copy page menu` card — independent toggles for each item in the `Copy page` dropdown (Skills.md URL, view as Markdown, and shortcuts for ChatGPT, Claude, Cursor, Windsurf, VS Code MCP). `Content`

### Improved

- Redesigned social-media preview cards for doc pages — cleaner editorial layout with your logo, accent color, and page title. `Social Preview`
- "Create docs from a website" now generates a foldered 8-page site (features, guides, use-cases, FAQ) instead of 5 flat pages — a stronger starting point and a real FAQ page for AI-answer citability. `AI Chat`

### Fixed

- Per-page social preview images on client doc sites, previously broken (404) on every page except the repo root. `Social Preview`
- Workspace subdomain `sitemap.xml` crashing instead of listing pages. `SEO`
- Favicon not loading on some subdomains (`docs.*`, alias subdomains). `Branding`
- Account switcher dropdown in settings sidebar was too narrow, squeezing org names and links. `Navigation`
- "Ask AI" bubble on text selection now flips below the selection instead of overlapping it when there's no room above. `AI Chat`

## NEW - 12.07.2026

### Fixed

- Navigation link button color picker restored in workspace settings — links with a saved color could no longer be recolored or reset to a plain text link. `Navigation`

## NEW - 06.07.2026

### Added

- Public REST API — call your workspace's AI docs-chat from your own backend with a Bearer API key, exported as `POST /api/v1/chat`. `API`
- `Integrations` panel — view, copy, and reset your workspace's API key from the `/chat` avatar menu or admin profile menu. `Integrations`
- Optional `auth_header` field when registering a webhook, sent verbatim as the `Authorization` header on every delivery — for receivers that require their own bearer token. `Webhooks`
- "Heading views" tracked event, showing which sections of a page readers actually scroll to. `Analytics`

## NEW - 05.07.2026

### Added

- New `Business` plan — everything included in `Pro`, with higher AI chat, translation, and webhook limits. `Billing`
- Webhook count limits per plan, shown in workspace `Limits` settings. `Webhooks`

### Changed

- `Pro+` renamed to `Pro`; the one-time `Lifetime` plan is no longer sold (existing lifetime customers are unaffected). `Billing`
- Upgrade page no longer shows specific AI-queries-per-month numbers that had drifted out of sync with actual limits. `Billing`

## 0.26.5 - 29.06.2026

### Fixed

- Free-text questions in the onboarding AI chat now render a text field so you can type your answer — previously a question with no preset options left nowhere to respond. `AI Chat`
- Single-option prompts like "Type your website URL here" now open a real input instead of submitting a placeholder value, so sources (website or repo URL) are captured correctly. `AI Chat`
- Creating docs from just an idea no longer stalls with a "process did not complete" error — the underlying request was being rejected; the onboarding chat now runs through to a published site. `AI Chat`
- New documentation projects are named from your product or brand instead of your full request sentence (e.g. "Coffee Shop" rather than "Create New Docs For A Coffee Shop"). `Workspace`

### Added

- Released `@docsbook/specify` — open-source CLI for spec-driven development. Validate markdown spec trees, verify spec↔code conformance bidirectionally, and generate specs from existing code. Available via `npx @docsbook/specify`. `OSS`

### Improved

- The "Go to website" link after publishing now waits until your site is actually live, showing a brief "deploying" state instead of opening a page that 404s for the first few minutes. `Publishing`
- The chat now shows honest progress while creating your docs (reading your site, writing docs, publishing) instead of sitting silent during generation. `AI Chat`
- Updated landing page feature names for clarity: "AI Agents", "Live Sync", "Auto Translations", "Auto Distribution". `Landing`

## 0.26.4 - 12.06.2026

### Added

- Separate credit cards for AI Chat, AI Translations, and Visitor AI Chat usage in admin dashboard — granular view of token spend by feature.

### Fixed

- Zero credits shown for newly created workspaces in `Token Budget` — `ensureWorkspace` now seeds the initial monthly token balance on creation.

### Improved

- **Buddy mode:** Converted `/buddy` from command to dedicated skill with isolated context — improves modularity and reduces main session token usage.
- **Agent daemon:** Enhanced reliability with revised `auto-commit.sh` lock handling and improved logging for task transitions.
- Progress bar in credit cards now shows remaining credits instead of usage percentage — better visibility of available budget in `AI Chat Credits` and `Visitors AI Chat Credits`

## 0.26.3 - 11.06.2026

### Fixed

- **Limits card:** "Usage by source" bars now show each category's share of *actual spend* instead of a tiny fraction of the full budget ceiling — so you can see at a glance where your tokens go (AI Chat readers vs. Admin vs. AI Translations) and what to optimize.
- **Usage attribution:** When a workspace owner uses the docs-chat widget, their token spend is now correctly charged to the "Admin & AI Agent" category instead of inflating the "Readers (AI Chat)" bar — giving an accurate picture of how much visitors actually cost.

## 0.26.2 - 11.06.2026

### Improved

- **Agent daemon:** Token diet for `spawn_session()` — now selects model by priority (P1 → Sonnet, P2/P3 → Haiku instead of fixed Sonnet) and adds bash pre-checks in merger role (skip if PR already merged or base=main). Selective directory copy by role (merger copies only `routines/` + `agents/branch-merger.md` instead of full context).

## 0.26.1 - 11.06.2026

### Fixed

- **Daemon:** Unreleased `agent:working` labels no longer hang forever — added reconcile sweep in `sweep_locks()` to auto-remove labels without live lock files; also fixed repo context (added `-R Docsbook-io/docsbook` to all gh-calls) and network hangs (wrapped git/gh in 20/30s timeouts)
- **Merger:** Now closes issues explicitly after merge instead of relying on GitHub's unreliable `Closes #N` auto-close for feature branches; added fallback search for already-merged PRs (`--state merged`) to prevent zombie cycles when PR is merged manually
- **Labels:** New `awaiting-release` label (blue, `#0075CA`) for base=main PRs awaiting manual `/merge` — separates "blocked and needs human intervention" (`needs-human`) from "queued for release" (`awaiting-release`)
- **Hooks:** `auto-commit-hook.sh` now removes stale lock files (>10 min) instead of skipping forever after crash

## 0.26.0 - 11.06.2026

### Added
- New `/chat` page with full AI agent for docs: search, edit settings, publish changes, and get answers — all in one conversation interface.
- `DocsAskInput` floating panel on every docs page — readers can ask questions without leaving the page.
- `AuthModal` with Google, Apple, and email-OTP sign-in alongside existing GitHub OAuth.
- `LimitsCard` in admin dashboard — unified token budget view with per-workspace usage breakdown.
- `AdminCard` manifest system — all FloatWidget settings tabs now driven by a single `ADMIN_CARDS` registry, making tabs easier to add and test.
- `applyWorkspacePatch` shared layer — workspace PATCH API consolidated from 400 lines of inline conditionals into one validated, plan-gated function.
- Workspace list sorted by most-recently-used first (`last_used_at DESC NULLS LAST`).
- New-chat `+` button in `/chat` header to reset conversation without page reload.
- Interactive upsell card when Pro/Pro+ features are mentioned in chat.
- Demo login button for Vercel preview deployments.
- `watch-issues.sh` script and local agent daemon for automated pipeline tasks.
- `code-scout` subagent — investigates code by problem description and creates GitHub Issues with technical context, so Buddy stays in orchestration mode without reading code directly.
- `qa-agent` now accepts a `FOCUS` parameter when called directly via Agent tool, enabling targeted testing without a full `/qa-plan` sweep.

### Fixed
- Agent pipeline `agent:working` lock now released automatically on any session exit (trap on EXIT in nohup subprocess) — no more manual lock cleanup after agent crashes.
- `merger` now finds PRs by branch name `claude/issue-N` as fallback when `Closes #N` body search returns empty — eliminates false NEEDS_HUMAN blocks.
- `task-builder` now verifies `Closes #N` is present in every PR body and auto-adds it if missing — prevents merger from losing the PR link.
- Auth `CSRF` error on Vercel preview deploys — `AUTH_URL` now overridden to preview origin.
- Redirect loop on preview deploys — `vercel.app` added to `isDev` proxy check.
- Cold-start Neon timeout on preview auth — DB lookup skipped in `preview-bypass` authorize.
- `ask_user` deduplication in LLM transcript — prevents 400 errors on Idea path.
- `MenuGroupRootContext` crash in ProjectSelector dropdown — owner groups wrapped in `DropdownMenuGroup`.
- Chat close button used hardcoded `docsbook.io` URL — switched to relative path.
- `/api/auth/signin` now redirects to `AuthModal` via `pages.signIn` instead of blank form.

## 0.25.1 - 08.06.2026

### Fixed

- **Accessibility**: Added `aria-label` to 4 icon-only buttons in the AI Chat mock on the landing page — screen readers and WCAG 2.1 AA compliance restored
- **Docs**: Removed internal operational files (`TWITTER_SETUP`, `outreach/`) from the public documentation sidebar — visitors no longer see private tooling pages
- **Skills**: Corrected the `npx install` link on the `/skills` page — now points to the correct `Docsbook-io/docs-skills` package

## 0.25.0 - 04.06.2026

### Added

- **Onboarding**: Interactive 7-step onboarding guide on first login to Docsbook — guided tour highlights key features in FloatWidget toolbar, adapts to user's plan (Free/PRO/PRO+/Enterprise), and remembers when dismissed with `hasSeenOnboarding` flag in `workspaces`
- **Onboarding**: New `about/feature-access.md` — private single source of truth matrix (Preview Anonymous × Free × PRO × PRO+ × Enterprise) documenting 80+ features, their availability per tier, limits, and onboarding rules for what to highlight to each user persona
- **Admin**: Fix FloatWidget (toolbar) not appearing for authenticated repo owners after "Start for free" — added direct GitHub repo ownership check in `ensureWorkspaceIfMember()` so owners see the admin interface immediately
- **Skills**: SKILL.md schema preview on detail pages (`/skills/[name]`) — developers now see required/optional frontmatter fields, YAML example from the current skill, and copy-paste instructions before installing with `npx docs-skills install`

## 0.24.0 - 04.06.2026

### Added

- **Landing**: New `PricingSection` — 3-column plan comparison block (Free / PRO $150 / PRO+ $59/mo) placed on homepage between CtaBand and FAQ so founders can compare plans at a glance without reading paragraphs
- **Enterprise**: Add WorkOS SSO/SAML integration scaffold — `@workos-inc/authkit-nextjs` package, `enterprise` plan enum added to `users` and `workspaces` tables, new `workosUserId`, `ssoOrganizationId`, `ssoDomain` columns

### Fixed

- **Landing**: Reframe CI/CD copy in `Features.tsx` to be positive trust signal for devs; add Mintlify to migration sources list alongside Confluence, GitBook, Docusaurus
- **Landing**: Fix `/skills` install command showing hardcoded "25 skills" — now uses dynamic `index.skills.length` (currently 36)
- **Admin**: Fix branding Save not updating sidebar/header name live in preview mode — `DocsContentArea` now resolves `previewSettings` fields with workspace fallback for `customName`, `iconUrl`, `logoUrl`, `fontFamily`

## 0.23.0 - 03.06.2026

### Added

- **Analytics**: Exclude internal (founder/admin) traffic from Axiom with `INTERNAL_IPS` env allowlist — single source of truth in `src/utils/analytics/internal.ts` with consistent IP extraction across all six ingest points (`/api/axiom`, server pageview logger, `/api/vitals`, `/api/_axiom/web-vitals`, `/api/analytics/{cta,feedback}`)
- **Growth**: New `/enrich-audience` command for the first growth-reasoning team — reasons over `about/` + Axiom analytics and appends insights back into the product business-layer. Adds cross-artifact drift contract in `CLAUDE.md` + `AGENTS.md` (MCP ↔ docs-skills ↔ docs-subagents ↔ docs-claude-plugins dependency graph)

## 0.22.3 - 30.05.2026

### Fixed

- Fix `/pricing` route returning 404 — now redirects to `/` instead of broken `pricing.docsbook.io` subdomain
- Fix `/blog` and `/blog/:path*` returning 500 — now redirects to `docsbook.io/docs/blog` for marketer SEO entry-points
- Fix SEO/GEO/AEO toggles showing "Active" in anonymous mode — toggle now rolls back and shows an inline error when unauthenticated
- Fix 503 errors on sidebar RSC prefetch in preview mode — prefetch disabled so navigation still works on click
- Fix copy button position in multiline code blocks — now anchored to top-left so it's always accessible in long snippets
- Fix scroll shadow in Webhooks (Events) tab — shadow now appears only when content is scrollable

### Improved

- Resized folder visibility and subheader folder toggles to match the standard Search Bar checkbox size for visual consistency

## 0.22.2 - 28.05.2026

### Changed
- Official documentation now served at `docsbook.io/docs` — middleware rewrites `/docs/*` internally instead of redirecting to `docsbook-io.docsbook.io`; canonical URLs, sitemap, JSON-LD, and all links updated across landing, admin, and MCP pages
- `docs.docsbook.io` and `docsbook-io.docsbook.io` now return `Disallow: /` in robots.txt so search engines index only the canonical `docsbook.io/docs` path

## 0.22.1 - 28.05.2026

### Fixed
- Fixed broken navigation on `docs.docsbook.io` alias — clicking any sidebar/inline link returned 404 because cached HTML carried the `/docs/` repo prefix while middleware rewrote it again. Added `x-docs-alias` header in `src/proxy.ts` and routed `basePath` to empty in `src/app/[user]/[repo]/[[...path]]/page.tsx` so links render as `/ai/mcp` instead of `/docs/ai/mcp`. Existing `docsbook-io.docsbook.io/docs/*` paths keep working unchanged

## 0.22.0 - 28.05.2026

### Removed
- Removed server-side Source of Truth indexing — `get_doc_graph`, `read_doc_sections`, `reindex_doc_graph` and the 17 `doc_*` LSP-style MCP tools are gone. Graph search now runs locally via the [docs-claude-plugins](https://github.com/Docsbook-io/docs-claude-plugins) package (`/plugin install docs-sync@docs-claude-plugins`). Deleted `src/lib/source-of-truth.ts`, `src/lib/mcp/lsp-tools.ts`, the reindex REST route, the daily `stale-check` cron and the two smoke scripts

### Changed
- Replaced the admin Source of Truth card in `src/components/mcp/SourceOfTruthControls.tsx` — the reindex usage counter (`/100`) and Reindex button are gone, replaced by a promo card with the install command and a link to the docs-claude-plugins repository
- Updated `src/components/SourceOfTruthUpgradeModal.tsx` bullet from "100 reindexes/month" to "Local indexing via Claude Code"
- Cleaned `src/app/mcp/page.tsx`, `src/app/mcp/_data/prompts.ts` (239 lines dropped) and `src/lib/generate-llms-txt.ts` of references to the removed tools

## 0.21.7 - 27.05.2026

### Fixed
- Mobile sidebar overlay no longer covers sticky subheader in `src/components/docs/Sidebar.tsx` and `src/components/docs/Subheader.tsx` — overlay `top` now adds the subheader's `2.25rem` when present, and subheader `z-index` raised from `z-30` to `z-40` so it stays above the overlay just like the main header

## 0.21.6 - 27.05.2026

### Fixed
- Fixed mobile sidebar backdrop overlay no longer covering the header in `src/components/docs/Sidebar.tsx` — overlay now starts below the header (h-12 + preview banner offset) and z-index lowered from 40 to 30 so the header stays interactive while the sidebar is open
- Fixed mobile outline (right table-of-contents panel) backdrop overlay no longer covering the header in `src/components/docs/Outline.tsx` — same treatment as the sidebar overlay so the header stays clickable when the outline drawer is open on mobile

## 0.21.5 - 27.05.2026

### Changed
- Restyled TL;DR block in docs to Vercel-style neutral border in `src/app/globals.css` — removed blue accent border-left and background fill, replaced with thin 1px border all around, transparent background, and muted-gray uppercase label for a cleaner minimal look in both light and dark modes

## 0.21.4 - 26.05.2026

### Fixed
- Ask AI on selection bubble: no longer interrupts text selection — bubble appears only after `mouseup`/`touchend` so selecting words and lines works normally
- Copy button on single-line code blocks: now vertically centered (`top: 50%`) so it appears on hover for all code block heights

### Chore
- Optimized Claude Code token usage with `claude-token-optimizer`: added Session Start Protocol, filled `.claude/QUICK_START.md`, `.claude/COMMON_MISTAKES.md`, `.claude/ARCHITECTURE_MAP.md` with project-specific content — auto-loaded tokens reduced from ~137k to ~121k

## 0.21.3 - 25.05.2026

### Fixed
- Mobile `/skills` and `/mcp` pages: added hamburger mobile menu to `Header` with full nav links, "Start for free" and "Log in" CTAs
- Mobile `/skills` top padding: reduced from `pt-28` to `pt-20` on mobile (consistent with `/mcp`)
- `SkillsInstallSelector`: install/use columns no longer stack on tablets — now `lg:grid-cols-2`
- `SkillInstallGuide`: install/use columns now split at `sm:` breakpoint for earlier two-column layout
- `PromptsFilters`: tags hidden on mobile (`hidden sm:inline-flex`), tool hover-state hidden on mobile to prevent overflow

## 0.21.2 - 25.05.2026

### Fixed
- Mobile header: removed the second nav-links row on small screens — header now shows only logo + CTA button
- Hero badge animation on Safari/iOS: `@property` conic-gradient is not supported in Safari; added CSS fallback via `border-beam-rotate` keyframe + `@supports` guard so the animated border renders correctly on all browsers
- Footer layout on mobile: removed `max-w-4xl mx-auto` from the `<footer>` tag, added `w-full` + horizontal padding on the inner container — background and `border-t` now stretch full-width on all screen sizes
- Hero top padding reduced from `pt-40` to `pt-28` on mobile (was over-compensating for the now-removed second header row)

## 0.21.1 - 25.05.2026

### Added
- Short marketing alias `docs.docsbook.io` for the product documentation — opens the same content as `docsbook-io.docsbook.io/docs/*` without redirect (URL stays clean in the browser). New `DOCS_ALIAS_SUBDOMAINS` map in `src/proxy.ts` rewrites `docs.docsbook.io/{path}` → `/docsbook-io/docs/{path}`; `/api/*` is passed through untouched, original subdomain URLs keep working.

## 0.21.0 - 25.05.2026

### Added
- SEO / GEO / AEO admin cards with real functionality — admin tab renamed from "SEO" to "SEO / GEO" (key `seo-geo`) and split into three toggleable cards, each with a `Learn more about …` footer link. GEO toggle injects a TL;DR `<aside class="tldr">` at the top of every page (from `tldr:` frontmatter or auto-extracted first paragraph), shows a visible `Updated DD MMM YYYY` `<time>` at the article end, and switches author in JSON-LD `TechArticle` to a full `Person` schema (frontmatter `author`/`authorUrl` or fallback to last git commit author). AEO toggle gates the existing `FAQPage` JSON-LD, auto-detects `HowTo` JSON-LD from `## How to …` / `## Как …` headings followed by numbered lists (`src/utils/seo/extractHowTo.ts`), and adds a `speakable` `SpeakableSpecification` to `TechArticle` for voice assistants. New MCP tools `update_geo` and `update_aeo` (PRO-gated) mirror `update_seo`. Markdown pipeline migrated from regex-strip to `gray-matter` for typed frontmatter (new `src/utils/markdown/parseFrontmatter.ts`); 4 call-sites refactored. New `docs/content/features/geo.md` and `aeo.md` document the behavior and authoring patterns; `seo.md` updated with cross-links. DB columns `workspaces.geo_enabled` and `aeo_enabled` (migration `0028_public_marvex.sql`)

## 0.20.2 - 25.05.2026

### Added
- UTM parameters on all internal CTAs leading from `/skills`, `/mcp`, `/docs` (Preview banner), and the blog to the landing page — every `/start` and `/connect` link now carries `utm_source` (`skills` / `mcp` / `preview` / `blog`), `utm_medium` (`nav` / `cta` / `banner`), and `utm_campaign` (e.g. `header_signup`, `mcp_start_free_top`, `preview_connect`, post slug for blog). New `src/utils/utm.ts` helper (`withUtm()`) wires the landing `Header`/`Footer` via an optional `utmSource` prop, the two inline CTAs on `/mcp`, and the `PreviewConnectBanner` on workspace pages. Blog post CTAs (`docusaurus_vs_docsbook`, `mintlify_vs_docsbook`, `gitbook_vs_docsbook`, `ai_search_documentation`, `documentation_seo_guide`, `how_to_host_docs_from_github`, `why_documentation_matters`) now tag their conversions per post. The landing page itself stays UTM-free so internal scroll-to-CTAs aren't mis-attributed

## 0.20.1 - 25.05.2026

### Changed
- Landing page positioning rewritten for AI crawlers — ChatGPT and Perplexity were describing Docsbook as a plain GitBook/Mintlify/Docusaurus alternative, missing the entire AI-Native layer. Hero H1 changed from "The AI Knowledge Platform" to "Docs from GitHub. For humans and AI agents." with concrete subtitle naming MCP, llms.txt, and 15 languages. New full-width "Built for AI agents" bento card with terminal mock (`claude mcp add`), MCP tool grid (`doc_outline`, `doc_search_text`, `read_doc_sections`, …) and client logos (Claude Code, Cursor, ChatGPT, Perplexity, Cline). New "AI Agents" social-proof tab with CTA to `/mcp`. `metadata.title`, `metadata.description`, JSON-LD `SoftwareApplication.featureList`, and FAQPage rewritten to surface MCP server, llms.txt, Source of Truth graph, Skills catalog, and updated pricing ($150 lifetime PRO / $59/mo PRO+) so AI search engines cite the current product correctly

## 0.20.0 - 25.05.2026

### Added
- SEO content hub — 20 new long-tail GEO/AEO blog posts in `docs/blog/` targeting AI search citation (ChatGPT, Perplexity, Claude, Gemini) and high-intent developer queries. Covers comparisons (Docusaurus vs Docsbook 2026, AI docs platform comparison, free hosting comparison, docs as code vs managed), AI infrastructure (`llms.txt` complete guide, JSON-LD for documentation, MCP server for documentation, docs-skills for AI agents, how to get docs cited by ChatGPT, Perplexity citations for docs, multi-language documentation SEO, AI chat build vs buy), migrations (GitBook → Docsbook, Docusaurus → Docsbook), and practical guides (custom domain how-to, API documentation best practices 2026, documentation analytics, README → docs site, why README-only projects need a docs site, best docs platforms for startups 2026). `docs/blog/README.md` restructured into five sections: Foundations, SEO & AI search (GEO/AEO), AI features, Comparisons & migration, Practical guides

## 0.19.0 - 25.05.2026

### Added
- MCP visitor activity drill-down — two new tools on PRO+ (`get_top_visitors` and `get_visitor_activity`) let AI agents investigate what one specific anonymous visitor actually did end-to-end. `get_top_visitors` returns the most active anonymous visitors with a stable hashed `visitor_id`, pageview count, country, and first/last seen; pass that `visitor_id` to `get_visitor_activity` to get the full chronological event timeline (pageviews, page feedback, CTA clicks) with paths and event-specific details (vote, query, href, heading, …). `get_page_journeys` also returns the same `visitor_id` so journeys can be drilled into immediately. `visitor_id` is `sha256(VISITOR_ID_SALT + repoFullName + ip).slice(0,16)` — stable across sessions for the same person within one workspace, but raw IPs never leave Axiom

## 0.18.1 - 25.05.2026

### Changed
- Bento feature cards on the landing page now link to their corresponding documentation pages instead of `/connect` — `AI Chat` → `/docs/ai/chat`, `SEO Optimization` → `/docs/content/features/seo`, `Web Analytics` → `/docs/analytics/tracking/overview`, `AI Translations` → `/docs/translation/ai-translations`, `User Feedback` → `/docs/content/features/feedback`. Smoother funnel (visitor reads about the feature first) and internal-linking SEO boost

## 0.18.0 - 24.05.2026

### Added
- Devices, Browsers and AI Visits analytics — new row of cards under Pages/Referrers in the Analytics tab. First card has tabs for `Devices` (Mobile/Desktop/Tablet) and `Browsers` (Chrome, Safari, Firefox, Edge, Brave, Arc, Vivaldi, Yandex…) with favicon icons. Second card lists AI crawler visits (GPTBot, ClaudeBot, PerplexityBot, Google-Extended, Bingbot, Applebot-Extended, Meta-ExternalAgent, CCBot, Bytespider, MistralAI-User and 12+ more) grouped by provider so you can see exactly which AI agents read your docs
- Ask AI on text selection — when readers highlight a snippet inside the docs, a floating `Ask AI` bubble appears above the selection; one click sends the selected text to AI Chat as a ready prompt. Tooglable per-workspace (Content tab in admin and `show_ask_ai_on_selection` in MCP `update_ui_settings`). On by default. Reduces friction for "explain this paragraph" / "rephrase this" use cases and pushes AI engagement
- Mobile Outline drawer — on screens <1280px the right-hand "On this page" panel is now reachable via a floating button in the bottom-left corner that opens a slide-up sheet with the same heading list and actions (scroll to top, ask AI, copy markdown, edit on GitHub, page feedback); desktop layout unchanged
- Signup attribution tracking — capture UTM parameters and referrer on landing pages, persist as first-touch cookie (`ds_attr`, 90 days), and write `signup_source` / `signup_medium` / `signup_campaign` / `signup_referrer` / `signup_landing_path` to `users` on GitHub OAuth signup so we can measure which channel (Twitter, HN, Product Hunt, dev.to, blog, organic, AI assistants) actually converts
- New FAQ sections covering subscription model, cancel behaviour, GitBook migration (3-step guide), annual vs monthly trade-offs, and grandfathered lifetime users
- Updated refund Q&A — 30-day money-back on first payment, prorated refunds for annual after the window
- Sitelinks-friendly structured data on the landing — added `SiteNavigationElement` JSON-LD for 8 key sections (Quick Start, AI Features, MCP Server, Agent Skills, Documentation, FAQ, Blog, Changelog), an `ItemList` with top destinations, and `WebSite.hasPart` linking the main pages so Google has explicit signals for generating sitelinks under the docsbook.io result
- New sitemap entries — `/mcp` and `/skills` with priority `0.9`, plus `/connect` with `0.5`, so Google can discover and weigh these promo pages
- FAQ reply notebook for community comments at `docs/blog/faq-replies.md` — 32 ready-to-paste answers (TL;DR + Long versions) across 8 sections (General, Pricing, Competitors, AI, SEO, Tech, Security, Objections) for Reddit, X, IndieHackers, and HackerNews distribution
- Simplified install/use guide on each skill page `/skills/[name]` — tabs for 7 AI clients (Claude Code, Cursor, Codex CLI, Windsurf, Cline, Gemini CLI, Copilot), two steps (Install + Use) with the command pre-filled for this specific skill, plus a runtime-discovery block via Docsbook MCP
- Install snippets for 8 AI clients on `/mcp` — interactive selector with tabs for Claude Code, Cursor, Codex CLI, Windsurf, Cline, Gemini CLI, GitHub Copilot (VS Code), and ChatGPT; each one shows its own command or config (bash/JSON/TOML) with filename and optional install steps
- Expanded the `Install in your AI client` section in [docs/ai/mcp](./ai/mcp.md) from a single Claude snippet to 8 subsections — one per client
- New blog tutorial `/blog/how-to-host-docs-from-github` — walks through three ways to turn a GitHub repo into a live docs site (GitHub Pages + Jekyll, Docusaurus, Docsbook) with step-by-step setup, tradeoffs, and a decision matrix; targets the "how to host documentation from github" high-intent SEO query
- New opinion blog post `/blog/notion-for-docs-engineering-lessons` — first-person engineering essay on why Notion stops working as a docs system once docs leave the building (SEO surface vs internal wiki, version control drift, multilingual coupling, AI crawler discoverability, performance budget, export lock-in, wiki-vs-docs permission split) with a soft Docsbook pitch in the closing section; written for SEO ("notion for documentation") + outreach + objection handling
- Month-1 transparency Twitter thread draft at `marketing/twitter-threads/2026-05-month-1-transparency.md` — 11-tweet build-in-public post (genre reference: @levelsio / @marc_louvion) covering hook with revenue, three things that worked (lifetime PRO, MCP server, llms.txt auto-generation), three that didn't (cold email, paid ads, feature bloat), AI chat numbers, and what changes in month 2; placeholders for MRR/lifetime revenue/conversion, character counts inline, posting checklist included
- Twitter teaser thread for Product Hunt launch at `marketing/twitter/ph-teaser-thread.md` — 9-tweet building-in-public thread (D-10 hook + 7 building-in-public tweets covering Anonymous MCP, llms.txt auto-discovery, TOON format, Docusaurus alternatives guide, attribution tracking, sitelinks JSON-LD, skills install UX + CTA), each tweet ≤280 chars, character counts inline, posting notes with UTM campaign `ph-teaser-twitter`
- New blog comparison post `/blog/gitbook-vs-docsbook` — honest 2026 head-to-head against GitBook (~1900 words) covering TL;DR matrix, four reasons teams leave GitBook (per-editor pricing, vendor lock-in, migration cost, AI as commodity), side-by-side feature table, pricing math for three team sizes (solo / 5-person / 20-editor mid-market), 7-step migration path, an honest "when GitBook is the better choice" section, and a 6-question FAQ — targets the "GitBook alternative", "GitBook vs Docsbook", and "GitBook pricing 2026" SEO queries
- Rewrote `/blog/docusaurus-vs-docsbook` into a full "Docusaurus Alternatives in 2026" guide (2.7k words) — TL;DR decision matrix, four reasons teams leave Docusaurus, 9 alternatives compared (Docsbook, Mintlify, GitBook, ReadMe, Archbee, VitePress, Nextra, Starlight, MkDocs Material) with pros/cons/pricing/migration, a "how to choose" section with three decision questions, a step-by-step migration guide, and a 7-question FAQ — targets the "docusaurus alternatives" SEO query instead of the narrower 1:1 comparison

### Changed
- Pivoted pricing FAQ from one-time lifetime to subscription model — PRO now $19/month or $190/year, PRO+ stays $59/month or $590/year (annual saves 2 months)
- Replaced legacy "Will the price increase?" answer with a price-lock guarantee for active subscriptions
- Moved "Get Support" out of the admin sidebar — replaced the bulky "Help & Support" section with a subtle "Need help? Contact support" footer link pinned to the bottom of the settings modal sidebar, freeing vertical space
- Reordered and trimmed the floating admin toolbar — now 5 quick-access buttons (Analytics, AI Chat, AI Translations, Design, SEO) instead of 6; removed setup-once entries (Custom Domain, MCP Server) and surfaced SEO, which was previously only reachable via the settings modal

### Fixed
- AI Skills cards in the admin no longer 404 on workspace subdomains — clicking a card now opens an in-place modal with the full `SKILL.md` (description, install snippets for 7 AI clients, keywords, MCP tools, GitHub link) instead of routing to `/skills/<name>` which only exists on `docsbook.io`. Landing-page behavior is unchanged
- Mobile adaptation for `/mcp` promo page — Hero `pt-28` reduced to `pt-20` on mobile, H1 base set to `text-3xl`, endpoint URL no longer overflows the screen
- `CopyCommand` on mobile — reduced padding/height, font-size scaled down, long install command no longer breaks the layout
- `AiClientsRow` — `gap-x-5` on mobile (was 9) so client icons line up more evenly at 375px
- `PromptsFilters` — category/plan selects use `grid-cols-2` on mobile instead of a single row; prompt row padding reduced, prompt text set to `13px` on mobile

### Removed
- Broken `SearchAction` from the landing JSON-LD — it pointed at `/search?q=`, a page that does not exist, sending a negative signal to Google instead of unlocking the Sitelinks Search Box

## 0.17.4 - 23.05.2026

### Fixed
- Replaced broken `(#)` CTA links across 5 blog posts (`mintlify-vs-docsbook`, `docusaurus-vs-docsbook`, `why-documentation-matters`, `documentation-seo-guide`, `ai-search-documentation`) — all now point to `https://docsbook.io/start`
- Removed misleading "free for 14 days" copy in `mintlify-vs-docsbook` — Free plan is free forever; added note that the 14-day trial applies only to PRO+ ($59/month)

## 0.17.3 - 23.05.2026

### Changed
- Reworked landing header navigation — replaced old category dropdowns (AI, Analytics, Branding, Widgets, Translation) with 3 direct links (`AI`, `MCP`, `Skills`) plus 2 curated dropdowns: `Documentation` (Quick Start, Basics, Creating Docs, Custom Domain, AI Translations, FAQ) and `Blog` (all 5 posts)

### Added
- Anonymous MCP access: any AI model can now connect to `https://docsbook.io/{owner}/{repo}/api/mcp/server` without authentication and use `get_info`, `get_doc_graph`, and `read_doc_sections` for PRO+ workspaces
- Scoped MCP endpoint `/{owner}/{repo}/api/mcp/server` — connecting to this URL auto-scopes the server to the specified repository
- Scoped `/{owner}/{repo}/.well-known/oauth-protected-resource` for OAuth discovery per workspace
- Every documentation page now includes `<link rel="mcp-server">` meta tag so AI models can auto-discover the MCP server from any docs URL
- `llms.txt` now includes a full MCP Server section with connect instructions, tool list, and discovery notes

## 0.17.2 - 23.05.2026

### Added
- `get_doc_graph` now supports `format` parameter: `"toon"` (default) returns a compact text tree ~10x smaller than JSON with `@canonical/ref` syntax that LLMs parse natively; `"json"` preserves the previous full structured response for programmatic clients

### Fixed
- Paginate MCP `get_doc_graph` to avoid hitting the MCP response token limit on large repos (previously a single 110k+ character JSON line blew past the limit and made the tool unusable in Claude). Added `page`/`page_size` (default 50), `path_prefix`, `include_headings`, `include_relations`, and `include_github_urls` flags; relations are only emitted on `page=1` to save bytes

## 0.17.1 - 23.05.2026

### Fixed
- Prevent race conditions in monthly usage limits for `AI Chat`, `Translations`, and `Reindex` — concurrent requests could each pass a stale pre-check and push counters past the plan limit (visible as `78/50` pages translated on Pro). Replaced check-then-act with atomic conditional `UPDATE ... RETURNING` in `batchTranslate`, `/api/ai-chat`, and the MCP `reindex` endpoint
- Roll back the reserved reindex slot when `fetchAndIndexRepo` fails so transient errors no longer eat the monthly quota

## 0.17.0 - 23.05.2026

### Changed
- Remove live preview modal from landing — `GitHub to DocsBook` input now navigates directly to `/<owner>/<repo>?preview=true` instead of opening an overlay
- Replace dark-background OG/Twitter image with a landing-style preview — light gradient, "The AI Knowledge Platform" headline, feature badges, and a docs UI mockup — improves appearance when sharing links on X/Twitter

### Fixed
- Wrap long project names in sidebar to prevent overflow outside the sidebar boundary

### Changed
- Enable `Ask AI` button near the page title by default for new workspaces — previously off by default
- Fix system theme not applying correctly due to shared `localStorage` key across workspaces
- Fix `docs-proxy` route ignoring saved `defaultTheme` and always falling back to `light`

### Changed (previous)
- Rename `MCP Server` to `MCP Source of Truth` in Pro+ pricing rows and add a hover `?` tooltip explaining the AI-coupled indexing graph
- Enable Source of Truth by default for Pro+ workspaces — removed the manual toggle from the admin MCP tab
- Add a Pro+ badge next to `Reindex Usage` that opens the Source of Truth promo modal on click

### Added
- 10 new MCP Example Questions in admin (copy brandbook from a URL, change logo, custom domain, translations, social links, AI key, analytics, reindex, read sections); moved the `authentication module` example to the bottom of the list

## 0.16.3 - 23.05.2026

### Fixed
- Neutralize green styling on "Get Support" button in workspace settings sidebar — now matches the muted look of other navigation items
- Remove duplicate `opengraph-image.tsx` inside `[[...path]]` catch-all route that broke the Next.js build (parent route already handles all path scenarios)

## 0.16.2 - 23.05.2026

### Changed
- Open docs in `?preview=true` mode after submitting GitHub URL on `/start` — newly published documentation now lands directly in Preview Mode

## 0.16.1 - 22.05.2026

### Added
- New `/start` page replaces the `LivePreviewExpanded` modal on "Start for free" — logo, GitHub URL input, Sign in with GitHub, email/Discord support links, social icons, hero-style shards background, cascade animations

## 0.16.0 - 22.05.2026

### Changed
- Rework billing model — Pro is now $150 lifetime one-time payment, Pro+ replaces Enterprise as $29/mo subscription with white-label and Source of Truth
- New AI query limits — `Free` 0/mo, `Pro` 200/mo, `Pro+` 2000/mo (was 20/1000/unlimited)
- New translation limits — `Free` 0/mo, `Pro` 50/mo, `Pro+` 500/mo (was 30/300/unlimited)
- Existing `pro` workspaces (legacy $29 one-time) grandfathered as lifetime Pro at no extra cost
- Existing `enterprise` workspaces auto-migrated to `pro_plus` keeping all features

### Fixed
- Auth redirect loop after GitHub OAuth — stale `callbackUrl` cookie pointing at a subdomain `/connect` caused an infinite redirect cycle; NextAuth `redirect` callback now normalises any subdomain `/connect` → `docsbook.io/connect`
- `/connect` on a workspace subdomain now redirects to `docsbook.io/connect` instead of 404
- `ConnectPage` now redirects to sign-in when the session cookie is present but invalid/expired, preventing a broken `ConnectPicker` state
- Workspace redirect after sign-in always uses `APP_DOMAIN` instead of the request `host` header, preventing wrong subdomain redirects
- Infinite redirect loop for workspaces whose repo is named `connect` — subdomain middleware no longer intercepts `user.docsbook.io/connect` as a `/connect` auth route

### Added
- Paddle `SubscriptionPaymentFailed` webhook handler — downgrades workspace to Free and sends Resend email to the owner with payment-update link
- Subscription management UI in `FloatWidget` pricing tab — shows current plan, subscription status, next billing date, and Manage subscription button linking to Paddle Customer Portal (Pro+ only)
- `pricing-spec.md` in `docs/content/setup` — source of truth for the new billing model
- Two-option upgrade layout in `AiUpgradeModal` and `ProUpgradeModal` — side-by-side Pro lifetime vs Pro+ monthly cards
- Subscription metadata columns on `workspaces` — `paddle_subscription_id`, `paddle_customer_id`, `subscription_next_billed_at`, `subscription_status`

## 0.15.2 - 22.05.2026

### Fixed
- Show "AI not enabled" message with owner contact link in `AiPanel` instead of generic error when AI is disabled for a workspace — users now see a helpful message with a link to the project owner's GitHub profile to request enabling the feature

## 0.15.1 - 22.05.2026

### Added
- Animated growth counters in `CtaBand` — 4 stats (workspaces, pages indexed, countries, AI queries) count up over 6 seconds on scroll-into-view
- Before→After traffic animation in `BentoFeatures` analytics cell — visitors climb from 11 to 1,240 and page views from 34 to 8,900 in a 9-second loop
- Ticket deflection counter above AI chat mock — shows 0→847 tickets saved this month, growing over 6 seconds
- Concrete numbers in `SocialProof` tabs — `2,400+ workspaces`, `3× more signups`, `40% fewer tickets`, `15 languages`

## 0.15.0 - 22.05.2026

### Added
- `Get Support` tab in admin panel with email, Discord, and Twitter contacts
- Email support link in landing `Footer` for quick access to `support@docsbook.io`
- `SoftwareApplication` structured data schema on `Landing Page` for AI search visibility
- `llms-full.txt` endpoint with complete product brief for AI crawlers
- Explicit allow rules for GPTBot, ClaudeBot, PerplexityBot, Google-Extended in `robots.txt`
- Events webhook endpoint in `API` for receiving real-time workspace events
- Blog section in `docs` with 5 SEO-optimized posts for distribution — competitor comparisons (Mintlify, Docusaurus), AI search, documentation SEO guide
- New `SEO Optimization` page in `docs` explaining automatic meta tags, JSON-LD, static pages, sitemap, canonical URLs, hreflang, and llms.txt — with compounding ROI timeline
- Expanded `AI Translations` page in `docs` with sections on why Claude outperforms generic translation tools and how each language version is indexed separately for multilingual SEO

### Fixed
- Image-only paragraphs (e.g. GitHub release badges) in `prose` content now center-align instead of left-align
- `Preview mode` Connect GitHub button now redirects to main domain `/connect` instead of subdomain path
- Replaced PNG logo with inline SVG in `opengraph-image` for correct social preview branding
- `Copy Page` dropdown now uses fixed positioning to stay within viewport on mobile instead of overflowing off the left edge

### Added
- Confetti animation on `/success` page after successful payment via `canvas-confetti`

### Improved
- Search widget UX with breadcrumb paths and "Ask AI assistant" option in `Search Bar`
- `AI Panel` input field now receives focus automatically when the panel opens
- `Organization` schema expanded with founder, email, foundingDate, and social sameAs links
- `FAQPage` schema expanded to 9 Q&A pairs with detailed AI-citable answers
- `WebSite` schema now includes SearchAction for Google Sitelinks Search Box
- `llms.txt` now serves full product brief — pricing, features, audience, competitors
- FAQ answers server-rendered in HTML for Googlebot (no JS required to read)
- Page title, og:title, and twitter:title unified to single consistent value
- `llms.txt` fallback content replaced with full product brief

### Fixed
- GitHub icon removed from primary CTA button on `Landing Page`
- Missing top padding in `Content` area when breadcrumbs are disabled
- Left `Sidebar` collapsible folders not opening when navigating via subheader links without full page reload
- `Copy Markdown` button no longer shown on pages without a workspace
- Translation toggle now enabled for preview admins on pages without a workspace
- `MCP Server` tab in admin panel now shows sign-in overlay in preview mode instead of raw content

### Security
- Added `X-Frame-Options`, `X-Content-Type-Options`, `Referrer-Policy`, `Permissions-Policy` headers
- HSTS upgraded with `includeSubDomains` and `preload` directives

## 0.14.0 - 20.05.2026

### Improved
- Follow-up question suggestions after each AI response in `AI Chat`
- Animated "Thinking…" indicator while AI is generating a response in `AI Chat`
- Share and Copy as Markdown buttons, plus a Report Issue option in `AI Chat`
- Smoother entrance animations on the `AI Chat` welcome screen
- Source of Truth automatically enabled for Enterprise workspaces in `AI Chat`

### Removed
- DeepSearch and References toggles from `AI Chat` — simplified to core Q&A

## 0.13.0 - 18.05.2026

### Added
- Documentation graph indexing for AI agents in `Source of Truth` (Enterprise)
- Manual reindex button with 100 uses/month in `Source of Truth` (Enterprise)
- Source of Truth settings panel in `FloatWidget` (Enterprise)

### Fixed
- Reindex button now works correctly for logged-in users in `Source of Truth`

## 0.12.0 - 17.05.2026

### Added
- `/llms.txt` endpoint so AI crawlers can discover and understand your docs

### Fixed
- Special characters (e.g. `&`) now display correctly in the page outline
- Sidebar folder collapse/expand now works correctly

## 0.11.1 - 17.05.2026

### Improved
- Documentation content and sidebar now render on the server for faster load and better SEO

## 0.11.0 - 16.05.2026

### Added
- Header navigation links now translate to the active language

### Improved
- Interface language auto-detected from workspace settings — no URL prefix needed
- Enabling multiple languages at once is now significantly faster
- A loading banner appears while fresh translations are being prepared in the background

### Fixed
- Default theme now always applies when theme-switching widgets are disabled
- Sidebar labels translate instantly without requiring a page refresh
- English sidebar labels now work when switching back to English
- Previous/Next navigation buttons now show translated page names

## 0.10.0 - 15.05.2026

### Added
- Bring-your-own API key for OpenAI, Gemini, Anthropic, OpenRouter in `AI Agent` (Pro/Enterprise)
- Folder visibility toggles — hide specific folders from the sidebar in `Admin Panel`
- Per-theme accent, muted, and base color customization in `Branding`
- Live font preview — font names in the picker display in their actual typeface
- Accent color tinting on inline code, code blocks, and sidebar hover states
- MCP server for AI-assisted workspace administration via natural language

### Improved
- Subheader dropdown loads instantly — no more network requests on hover
- Ask AI, Search, and Language header buttons now have a unified consistent style
- Theme and Branding settings reorganized for clarity in `Admin Panel`
- Page feedback ratings moved into the Events section in `Analytics`

### Fixed
- Ask AI button styling now matches other header buttons
- Browser tab no longer shows duplicate workspace name on root page
- Favicon correctly shows custom workspace icon and uses accent color as background
- Images with relative paths now load correctly in documentation
- Subheader links navigate to correct translated pages when translations are active
- AI chat responses now appear in `Chats Analysis` analytics
- AI Agent settings always shows 3 question input fields
- Globe icon size and color now consistent in language picker
- Paddle checkout modal now opens correctly

## 0.8.2 - 13.05.2026

### Fixed
- Language code now inserts at the correct position in sidebar links
- Custom AI panel questions now load correctly from workspace settings
- Sidebar footer border no longer shows when all footer controls are hidden

## 0.8.1 - 12.05.2026

### Added
- FAQPage structured data for Google rich snippets on landing page

### Improved
- Language switching now instant — translation happens in the background with a loading indicator
- Hero image now uses Next.js optimized loading for faster page speed

### Fixed
- Sidebar dividers now only appear when there is content to separate
- Multi-line folder names in sidebar now left-align correctly
- Paddle script no longer blocks page render
- Landing page HTML structure and heading hierarchy corrected

## 0.8.0 - 11.05.2026

### Improved
- Live Preview replaced modal with a smooth inline animation experience

## 0.7.0 - 11.05.2026

### Added
- Custom background color support for individual header navigation links

## 0.6.0 - 10.05.2026

### Added
- Subheader navigation with folder tabs and hover dropdowns
- Heading anchor now copies full link URL to clipboard with a success toast

## 0.5.0 - 10.05.2026

### Added
- Open in Cursor IDE option in `Copy Page` dropdown
- Open in Windsurf IDE option in `Copy Page` dropdown

### Improved
- `Copy Page` button redesigned with modern styling and check icon feedback on copy

## 0.4.1 - 10.05.2026

### Improved
- Auto-detect button in Translation panel detects documentation language from README and updates language picker with native name and flag

## 0.4.0 - 10.05.2026

### Added
- Country flag icons in language switcher with native language names
- Background glow effect using accent color in `Theme Settings`
- Empty state page for users with no repositories after sign-in
- Getting started guide, GitHub editing instructions, Claude Code and VS Code guides in documentation

### Fixed
- Landing page mobile layout and hero section scaling
- Header and sidebar horizontal alignment on desktop

## 0.3.1 - 09.05.2026

### Added
- Double-clicking inline `code` now selects all content inside the backticks

### Improved
- Sidebar folders auto-expand and scroll to active page on nested pages

### Fixed
- Hamburger menu now toggles closed on second click
- Keyboard shortcut display shows `⌘ K` on Mac and `Ctrl K` on Windows/Linux
- Heading anchors now appear to the right on mobile to prevent text wrapping

## 0.2.3 - 09.05.2026

### Improved
- Syntax highlighting switched to native GitHub themes (light and dark)
- SEO Optimization upsell card now shows as a centered overlay with pricing details
- Translation tab layout — usage card moved above country stats
- Features cards on landing page now always show icon and description

### Fixed
- Sidebar stays fixed during scroll — no more jumping
- Mobile burger menu positioning and z-index corrected
- Page titles no longer include "| Docsbook" suffix
- Web Vitals analytics no longer produce CORS errors

## 0.2.0 - 08.05.2026

### Added
- System theme option — respects OS-level dark/light preference
- Theme dropdown picker in sidebar and header (Light / Dark / System)
- Per-plan monthly translation quotas with usage tracking and progress bar
- SEO panel — control search engine indexing, canonical URLs, and structured data
- Subdomain root page listing all user's documentation projects
- GitHub URL paste detection with a helpful redirect banner

### Improved
- Upgrade plan button styled with blue background for better visibility

### Fixed
- DeepSearch and References toggles now persist correctly
- AI panel no longer returns 403 when toggling DeepSearch/References
- GitHub rate limit errors eliminated — content now fetched from raw.githubusercontent.com
- `?preview=true` query string preserved on subdomain redirects
- AI Agent tab now loads with a single request instead of three

## 0.1.1 - 07.05.2026

### Added
- Scroll shadow on document outline to indicate scrollable content

### Improved
- Sidebar Language and Theme toggle button padding and visual style

### Fixed
- Pro plan features now accessible when workspace has an active Pro subscription
- Language switcher now visible to all visitors when enabled, even before languages are added

## 0.1.0 - 06.05.2026

### Added
- Mini analytics dashboard preview on landing page

### Fixed
- Custom workspace favicons now display correctly in browser tabs
- Inline badge images no longer break to new lines in documentation
- Subdomain authentication no longer blocks authorized users with 403 errors
