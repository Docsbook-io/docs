# docs/ structure — project documentation

The `docs/` folder contains the built-in documentation (indexed by Docsbook itself). All 47 files have YAML frontmatter (title + description) and are connected via index pages:

```
docs/
├── README.md                  # TOC for all documentation
├── quick-start.md             # Quick Start — publish in 30 seconds
├── basics.md                  # Core concepts
├── faq.md                     # FAQ
├── webhooks.md                # Webhook events and Zod payload schemas
├── CHANGELOG.md               # Versions and releases
│
├── ai/                        # Docsbook AI features (new section)
│   ├── README.md              #   Index
│   ├── chat.md                #   AI chatbot: RAG flow, providers, limits
│   ├── translations.md        #   AI translations into 15 languages with SEO
│   ├── llms-txt.md            #   llms.txt standard for AI agents
│   ├── source-of-truth.md     #   Documentation graph (PRO+)
│   ├── mcp.md                 #   MCP server: connection and tools
│   ├── chat-hooks.md          #   Pre/post-LLM hooks (PRO)
│   └── skills.md              #   docs-skills catalog
│
├── guides/                    # Step-by-step tutorials
│   ├── README.md
│   ├── getting-started/       #   Creating and managing a workspace
│   └── advanced/              #   Custom domain, translation, PRO features
│
├── analytics/                 # Analytics
│   ├── README.md
│   ├── tracking/              #   Overview, events
│   └── reports/               #   Read time, countries
│
├── design/                    # Branding and layout
│   ├── README.md
│   ├── style/                 #   Branding, themes
│   └── layout/                #   Sidebar, header
│
├── content/                   # Content and setup
│   ├── README.md
│   ├── setup/                 #   GitHub integration, options
│   └── features/              #   Search, copy, feedback, SEO
│
├── translation/               # AI translations (settings)
│   ├── README.md
│   ├── settings.md
│   └── ai-translations.md
│
└── blog/                      # Articles: comparisons, AI search, SEO guides
    ├── README.md
    ├── docusaurus-vs-docsbook.md
    ├── mintlify-vs-docsbook.md
    ├── why-documentation-matters.md
    ├── ai-search-documentation.md
    └── documentation-seo-guide.md
```

**Local documentation audit:** 11 [docs-skills](https://github.com/Docsbook-io/docs-skills) are installed in `.claude/skills/` (`docs-analyze`, `docs-seo`, `docs-accessibility`, `docs-i18n`, `docs-style-tone`, `docs-structure-templates`, `docs-content-types`, `docs-audience`, `docs-navigation-linking`, `docs-media`, `docs-maintenance`). Run with `/docs-analyze` in Claude Code or install in another repo via `npx docs-skills install`.
