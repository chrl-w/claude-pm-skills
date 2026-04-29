# claude-pm-skills

Product management plugins for [Claude Code](https://docs.claude.com/en/docs/claude-code/overview) and [Cowork](https://www.anthropic.com/news/claude-cowork). Skills, commands, and workflows used by [Charlie Watkinson](https://github.com/chrl-w) at Spotted Zebra.

This repo is structured as a Claude plugin marketplace. Each plugin lives in its own subfolder and can be installed independently.

## Plugins

| Plugin | What it does |
|---|---|
| [`product`](./product) | Core PM workflows - release summaries, feature documentation, commercial team updates, analytics event naming, and customer-facing Knowledge Centre articles. |

## Install

### Cowork (desktop app)

1. Open Cowork settings -> Plugins -> Add marketplace
2. Paste `https://github.com/chrl-w/claude-pm-skills.git`
3. Install the `product` plugin from the marketplace listing

### Claude Code (CLI)

```bash
claude plugin marketplace add https://github.com/chrl-w/claude-pm-skills.git
claude plugin install product
```

## Develop

Clone this repo somewhere persistent on your machine:

```bash
git clone https://github.com/chrl-w/claude-pm-skills.git
cd claude-pm-skills
```

Edit skills, commands, and the plugin manifest in `product/`. Bump the version in `product/.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json` when you ship a meaningful change.

Push to main, then refresh the marketplace in Cowork (or `claude plugin marketplace update claude-pm-skills` in the CLI) to pull the new version.

## Add a new plugin

1. Create a new subfolder at the repo root, e.g. `./my-new-plugin/`
2. Add `.claude-plugin/plugin.json` inside it
3. Add the plugin to the `plugins` array in `.claude-plugin/marketplace.json`
4. Commit and push

The [create-cowork-plugin](https://github.com/anthropics/claude-skills) skill in Cowork can scaffold a new plugin folder for you.

## License

MIT - see [LICENSE](./LICENSE).
