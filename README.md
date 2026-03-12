# Claude PM Skills

A collection of Claude Code skills and commands that extend Claude into a product management co-pilot. Built by a Senior PM working in B2B SaaS to automate the repetitive parts of the job - release comms, internal docs, analytics naming, changelog generation - so more time goes to the thinking that actually matters.

## What's in here

Each folder is a **plugin** containing skills (background knowledge Claude can draw on) and commands (user-invoked workflows triggered with `/command-name`).

| Plugin | Description |
|--------|-------------|
| [**product/**](./product/) | Core PM workflows - release summaries, feature documentation, commercial team updates, and analytics event naming |

## How it works

These are built for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) using the skills and commands system. Skills give Claude persistent context about formats, conventions, and domain knowledge. Commands wire that knowledge into repeatable workflows that pull from tools like Jira, Notion, GitHub, and Slack via MCP.

### Quick start

1. Clone this repo
2. Copy the plugin folders you want into your Claude Code configuration
3. Connect the relevant MCP integrations (Jira, Notion, GitHub, etc.)
4. Use `/command-name` to trigger workflows or let skills activate automatically

## Design principles

- **Source of truth over memory** - Commands pull live data from connected tools rather than relying on stale context
- **Two-pass drafting** - Gather context first, draft second, iterate with the PM in the loop
- **Opinionated formats** - Each output follows a consistent structure so teams know what to expect
- **PM stays in control** - These automate the legwork, not the judgement calls

## Licence

MIT - see [LICENSE](./LICENSE).
