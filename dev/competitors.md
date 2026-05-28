> Competitive analysis for AI agents — comparative table, moat against each competitor, Mintlify tactics to adopt, and GitBook traffic channel breakdown.

# Competitor Analysis

## Comparative Table

| | **Docsbook** | **GitBook** | **Mintlify** | **Docusaurus** | **Notion** | **Readme.io / Archbee** |
|---|---|---|---|---|---|---|
| **Setup time** | 5 sec | hours | 10 min | 2–3 days | minutes | hours |
| **Source of truth** | GitHub | their DB | Git/MDX | Git | their DB | their DB |
| **AI chat** | ✅ out of the box | ✅ AI Search | ✅ AI Assistant | ❌ (plugins) | ❌ | partial |
| **AI translations** | ✅ 15 languages | ❌ | ❌ | ❌ | ❌ | ❌ |
| **MCP server** | ✅ ~40 tools | ❌ | partial | ❌ | ❌ | ❌ |
| **llms.txt** | ✅ auto | ❌ | ✅ auto | ❌ | ❌ | ❌ |
| **SEO** | ✅ full | moderate | ✅ | requires setup | poor | moderate |
| **Analytics** | ✅ Axiom | basic | ✅ ClickHouse | ❌ | ❌ | basic |
| **Price (Pro)** | **$150 lifetime** | per seat ($$$) | $250+/mo | free (self-host) | $8–15/user/mo | $$/mo |
| **Vendor lock-in** | none (data in GitHub) | yes | minimal (MDX/Git) | none | yes | yes |
| **Custom domain** | ✅ PRO+ | ✅ paid | ✅ paid | manual setup | ✅ paid | ✅ |
| **Best for** | developers, indie, startups | enterprise teams | dev/API docs | OSS, dev heroes | internal wiki | support/API |

---

## Our Moat Against Each Competitor

- **vs GitBook** — saves ~$200/mo, AI chat + translations included, no vendor lock-in. GitBook is strong for enterprise (Zoom, FedEx, Nvidia) but expensive and slow for individual creators.
- **vs Mintlify** — Mintlify leads on DX for API docs (growth loops, llms.txt, MCP, reverse trial — worth studying, [see their tactics](#mintlify-tactics-worth-adopting)). We're cheaper ($150 lifetime vs $250+/mo), instant setup without MDX configs, supports GitHub repos as-is.
- **vs Docusaurus** — free, but 2–3 days of setup + hosting + CI/CD. "Your time is worth more."
- **vs Notion** — Notion doesn't index properly in Google, no SEO, vendor lock-in. Documentation is not a wiki.
- **vs Readme.io / Mintlify / Archbee / Document360** — they are API-focused; we're a generalist for any product + AI/MCP-native.

---

## Mintlify Tactics Worth Adopting

- **Powered by [Brand]** as a viral channel (we already do this — Pro removes it).
- **Reverse Trial** (14 days Pro → fallback to Free) — psychology of ownership.
- **Manual outreach** — they found companies with poor docs, built an updated version **without their knowledge**, and sent the finished result. We already have a similar funnel (see go-to-market).
- **llms.txt + MCP** — AI agents as a traffic channel. At Mintlify, 45.3% of requests come from AI agents (Claude Code 25%, Cursor 18%). We've already built both MCP and llms.txt — now we need to push this in marketing.
- **Technical SEO automation** — sitemap, canonical, H1–H3, mobile-first. We have it, but it's not highlighted in copy.

---

## GitBook Traffic Channels (for reference)

GitBook relies on: direct/branded traffic (~60%), organic (~15%), referral (~8%), social (~5%). Their email newsletter reaches 130k+ people/month. We are weakest in organic search and email list size — these are our growth directions.
