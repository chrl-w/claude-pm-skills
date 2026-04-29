# Product Plugin

Core product management workflows for Claude Code. Handles the recurring communication and documentation tasks that eat into PM time - release summaries, feature docs for internal teams, commercial team updates, and analytics event governance.

## Commands

Commands are user-invoked workflows triggered with `/command-name`. They orchestrate multi-step tasks across connected tools.

| Command | Trigger | What it does |
|---------|---------|-------------|
| **release-summary** | `/release-summary <tag>` | Pulls merged PRs from GitHub, extracts Jira ticket keys, cross-references the Upcoming Feature Releases database, and drafts a release summary for internal teams |
| **write-release-comms** | `/write-release-comms <feature>` | Creates a feature release update for CS and Sales in Notion, gathering context from Jira, Notion, and Slack automatically |
| **product-doc** | `/product-doc <feature>` | Creates or updates internal product documentation in the Product Guidance Notion database for CS, Sales, and other internal teams |
| **name-event** | `/name-event <action>` | Names and parameterises a Heap analytics event following the company's controlled taxonomy, fetching the latest naming conventions from Notion |
| **help-centre-article** | `/help-centre-article <feature or 'rewrite [page]'>` | Creates or rewrites a customer-facing Knowledge Centre article, following the article type taxonomy, tone guide, and callout system |

## Skills

Skills provide background knowledge that Claude draws on automatically when relevant. They define formats, conventions, and domain context.

| Skill | When it activates | What it provides |
|-------|-------------------|-----------------|
| **release-summary** | Writing up a release, changelog, or "what shipped" update | Release summary format, GitHub repo configuration, Jira cross-referencing workflow, Notion publishing steps |
| **upcoming-releases** | Creating feature previews or commercial team updates | Two-tier update format (visibility + enablement), Notion database schema, writing principles for non-technical audiences |
| **product-docs** | Documenting a feature or updating existing docs | Doc structure, writing principles, create vs update modes, Notion database schema and examples |
| **heap-event-naming** | Naming analytics events, reviewing tracking PRs, or discussing event taxonomy | Event naming format, controlled taxonomy reference, parameter conventions, naming decision logic |
| **help-centre-guidance** | Writing KB articles, help docs, rewriting existing Knowledge Centre pages | Article type taxonomy (Understand/How To/Reference), callout system, tone guide, golden examples, cross-linking strategy, IA guidance |

## Connected tools

These workflows pull from and publish to:

- **GitHub** - Merged PRs and release tags (source of truth for what shipped)
- **Jira** - Ticket details, epic scope, acceptance criteria
- **Notion** - Documentation databases, feature release database, analytics taxonomy
- **Slack** - Optional announcements and context gathering
