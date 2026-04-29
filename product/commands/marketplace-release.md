---
description: Release a new version of the claude-pm-skills plugin — bumps version, opens a PR, and syncs into Claude Code
argument-hint: "<optional: patch | minor | major>"
---

# Marketplace Release

Bump the plugin version, open a PR, and sync the update into Claude Code. See the **marketplace-release** skill for the full workflow.

## Workflow

### 1. Decide the version bump

Read `product/.claude-plugin/plugin.json` to find the current version, then ask the user what changed. Suggest the bump type:
- **Patch** — content tweaks, wording fixes, no new skills
- **Minor** — new skill or command added
- **Major** — breaking changes or major restructure

If the user passed an argument (`patch`, `minor`, or `major`), use that directly.

### 2. Bump both version files

Update the `"version"` field in:
- `product/.claude-plugin/plugin.json`
- `.claude-plugin/marketplace.json` (inside the `product` entry)

Both must match.

### 3. Commit, push & open PR

Use `/commit-push-pr` with message: `Bump product to vX.X.X`

### 4. Wait for merge

Tell the user to merge the PR, then come back to trigger the sync.

### 5. Sync into Claude Code

Once the PR is merged, run:
```bash
claude plugin marketplace update claude-pm-skills
claude plugin update product
```

See the **marketplace-release** skill for full details.
