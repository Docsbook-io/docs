> Product context for AI agents — mission, positioning, ICP, user desires, and go-to-market funnel. Read this before any task involving marketing copy, audience targeting, or product decisions.

# Product Context

## Mission and Idea

Docsbook sells **the simplicity of monetizing a product through documentation**. We turn an existing GitHub repository into an SEO-optimized documentation site in 5 seconds — no CI/CD, no DevOps, no data migration.

**Core thesis:** good documentation = more sales. Bad documentation = more expensive support, lower trial conversion, international customers don't buy.

**Tagline (internal):** *"The intelligence layer between your product and the world."*

**What we do for the user:**
- Save **time** for the product owner / tech lead — zero configuration.
- Increase **sales** — SEO + AI chat + translations + analytics → more organic traffic, lower barrier to entry, higher trial conversion.
- Remove vendor lock-in dependency — data stays in GitHub.

---

## Positioning

| | Docsbook |
|---|---|
| **What it is** | AI documentation from a GitHub repository in 5 seconds |
| **Who it's for** | Developers, indie hackers, startups, B2B SaaS, OSS projects |
| **What sets it apart** | Instant setup, AI/SEO/translations out of the box, lifetime purchase instead of subscription, MCP management |
| **The key magic** | Connect GitHub → site is ready. Push to main → auto-update. |
| **Brand promise** | "Don't write docs — publish them. The site is already there." |

**Style frame:**
- Direct, technical language. No fluff, no "enterprise-blah".
- Numbers over adjectives: "5 seconds", "$150 lifetime", "15 languages", "200 AI requests/month".
- Don't apologize for AI — it's an optional bonus, not marketing noise.
- No emojis in product UI and copywriting unless explicitly requested.

---

## ICP and Audience

### Who Buys (in priority order)

| Segment | Pain | What we sell them |
|---|---|---|
| **Developers with docs on GitHub** | Want a site but don't want to deal with Docusaurus/CI | "A site in 5 seconds from your README" |
| **Library authors without documentation** | Don't know where to start | "Upload what you have — Docsbook turns it into a site" |
| **Indie hackers and freelancers** | Documentation looks unprofessional, losing trust | Branding, custom domain, "looks enterprise" |
| **Startups without a technical writer** | Developers write docs themselves — expensive and poorly indexed | SEO + AI + translations replace a technical writer |
| **B2B SaaS with onboarding problems** | Users don't figure it out → rising ticket count | AI chat reduces support by 40% |
| **API products / developer tools** | Docs = main acquisition channel | DX-first, MCP, llms.txt, growth loops |
| **Products with open-source SDK** | OSS part sells the main product | Visibility in Google + AI agents |
| **EdTech / course authors** | Learning materials as docs | Navigation, SEO, AI Q&A |
| **Products in international markets** | Need localization without translators | 15 languages with separate SEO indexing |
| **Telegram/Discord bot authors** | Commands are unclear, no doc page | Minimal effort, SEO, community-friendly |
| **Corporate internal tools** | New employees spend hours on onboarding | Internal docs from private repo |
| **Game mods / Minecraft / Roblox / Unity** | Documentation scattered across forums | Beautiful wiki from repo |
| **Chrome extension authors** | Need a site + docs in one | Free plan + custom domain |
| **No-code creators (Make/Zapier/n8n)** | Selling templates, need instructions | Ready-made format + AI questions |

### Three User Personas "Under the Hood"

1. **End users** — need docs to figure things out → AI chat, search, translations.
2. **Developers** — need architectural grounding → documentation graph, MCP, source-of-truth.
3. **Business** — need metrics and reduced support → analytics, feedback, trial conversion.

---

## User Desires

Keep in mind when making product decisions:
- Real-time co-editing
- Affordable pricing
- "Wow" UI
- Docs live in Git (source of truth)
- API SDK generation (TODO for later)

---

## Go-to-Market Funnel

**Context for agents:** do not suggest ideas that contradict this funnel.

1. **GitHub login** — main product entry point. A bot scrapes fresh projects with docs on GitHub and extracts contact links (including Twitter).
2. **Manual outreach** — individual messages to each author:
   - "Published your documentation as a site personally for you"
   - "Found your project"
   - "Your project is great"
   - Identify the pain + immediate solution
   - Ask "can I share the link"
3. **Outreach contractor** — own mailing runs into spam blocks (proxies, accounts). Looking for a contractor.
4. **Free plan as a viral channel** — "Powered by Docsbook" in the footer on free sites.
5. **MCP / llms.txt** — discovery through AI agents (Claude Code, Cursor) — priority channel in 2026.
6. **Skills catalog** — `/skills` SSG catalog + `find_skill` MCP tool as the entry point for agents.
