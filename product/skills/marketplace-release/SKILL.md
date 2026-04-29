---
name: marketplace-release
description: >
  Release a new version of the claude-pm-skills plugin marketplace. Bumps version numbers, creates
  a PR, and syncs the update into Claude Code. Use this skill whenever the user wants to release or
  publish an update to the product plugin, bump the plugin version, cut a new release of the
  marketplace, or run "claude plugin update". Also trigger for phrases like "release the plugin",
  "push the skills update", "bump the version", or "publish a new version".
---

# Marketplace Release

Release a new version of the `claude-pm-skills` plugin marketplace. The process has two phases: creating the version bump PR, and syncing it into Claude Code after merge.

## Repo

`github.com/chrl-w/claude-pm-skills`

## Files that need updating

Both files must stay in sync — they should always show the same version:

| File | Field |
|------|-------|
| `product/.claude-plugin/plugin.json` | `"version"` |
| `.claude-plugin/marketplace.json` | `"version"` inside the `product` entry |

## Step 1: Decide the version bump

Ask the user what changed since the last release, then suggest the bump type:

| Type | When to use | Example: 0.2.2 → |
|------|-------------|-----------------|
| **Patch** | Minor content edits, wording tweaks, bug fixes in a skill | `0.2.3` |
| **Minor** | New skill or command added, meaningful workflow change | `0.3.0` |
| **Major** | Breaking changes, significant restructure | `1.0.0` |

If the user isn't sure, ask: *"What changed — did you add anything new, or just tweak existing skills?"* Patch is usually right for small edits; minor for anything new.

Check the current version first by reading `product/.claude-plugin/plugin.json`.

## Step 2: Bump the version

Edit both files, setting the new version string:

**`product/.claude-plugin/plugin.json`:**
```json
{
  "name": "product",
  "version": "X.X.X",
  ...
}
```

**`.claude-plugin/marketplace.json`** — update the `version` field inside the `product` entry (not the top-level `metadata.version`):
```json
"plugins": [
  {
    "name": "product",
    "version": "X.X.X",
    ...
  }
]
```

## Step 3: Commit, push & open PR

Use `/commit-push-pr` with the message:
```
Bump product to vX.X.X
```

## Step 4: Wait for PR merge

Tell the user:
> PR is open — merge it when you're ready, then let me know and I'll sync the update into Claude Code.

## Step 5: Sync into Claude Code

Once the user confirms the PR is merged, run both commands:

```bash
claude plugin marketplace update claude-pm-skills
claude plugin update product
```

These pull the latest version from GitHub and install it locally. A Claude Code restart may be required for the updated skills to take effect.

## Done ✅

Confirm the version is live:
> Product plugin updated to vX.X.X. You may need to restart Claude Code for the new skills to take effect.
