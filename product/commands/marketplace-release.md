---
description: Bump the product plugin version, open a PR, and return the URL
argument-hint: "<optional: patch | minor | major | x.y.z>"
---

# Marketplace Release

Automates cutting a new version of the `product` plugin in the `claude-pm-skills` marketplace. Reads both version files, summarises what changed, determines the new version, updates files, commits, and opens a PR.

## Workflow

### 1. Read current versions

Read both files and verify they agree:

- `product/.claude-plugin/plugin.json` → `version`
- `.claude-plugin/marketplace.json` → `plugins[name=="product"].version`

If the versions differ, stop and report:

> ⚠️ The two version files are out of sync:
> - `plugin.json`: X.Y.Z
> - `marketplace.json`: A.B.C
>
> Resolve this manually before releasing.

### 2. Check for uncommitted changes

```bash
git status --short
```

If any files beyond `product/.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json` are modified or staged, warn:

> ⚠️ There are uncommitted changes in the working tree (listed below). These will not be included in the release commit. Continue?

List the affected files and wait for confirmation before proceeding.

### 3. Show what changed since the last bump

```bash
git log --oneline $(git log --format="%H" --grep="^Bump product to v" | head -1)..HEAD
```

Summarise the commits in plain language. Suggest a bump type based on the changes:
- New files added (new commands or skills) → suggest **minor**
- Edits to existing files only → suggest **patch**
- Removals, renames, or structural changes → ask the user

### 4. Determine the new version

If the user passed an argument:
- `patch` → increment patch digit (0.2.2 → 0.2.3)
- `minor` → increment minor, reset patch to 0 (0.2.2 → 0.3.0)
- `major` → increment major, reset minor and patch to 0 (0.2.2 → 1.0.0)
- `x.y.z` (explicit) → use exactly as given

If no argument was passed, show the current version and your suggestion, then prompt:

> Current version: **0.2.2**
> Suggested bump: **minor** (new command file added)
> New version would be: **0.3.0**
>
> Enter bump type (patch/minor/major) or an explicit version, or press enter to accept:

### 5. Show a diff preview before making any changes

```
product/.claude-plugin/plugin.json
  "version": "0.2.2"  →  "0.3.0"

.claude-plugin/marketplace.json  (plugins[name=product])
  "version": "0.2.2"  →  "0.3.0"
```

Ask for confirmation before writing.

### 6. Update both JSON files

Use the Edit tool to update the `version` field in both files:

- `product/.claude-plugin/plugin.json` → top-level `"version"` field
- `.claude-plugin/marketplace.json` → `"version"` inside the array entry where `"name" == "product"` (not the top-level `metadata.version`)

### 7. Commit the two version files

```bash
git add product/.claude-plugin/plugin.json .claude-plugin/marketplace.json
git commit -m "Bump product to v{new_version}"
```

Only the two version files should be staged. If `git status` after staging shows additional files, abort and warn.

### 8. Create a branch, push, and open a PR

Branch name: `bump-product-to-{version-with-hyphens}` (replace dots with hyphens, e.g. `bump-product-to-0-3-0`).

```bash
git checkout -b bump-product-to-{version-with-hyphens}
git push -u origin bump-product-to-{version-with-hyphens}
gh pr create \
  --title "Bump product to v{new_version}" \
  --base main \
  --body "$(cat <<'EOF'
Bumps the product plugin from v{current_version} to v{new_version}.

## Changes since last release

{bullet list of commits from step 3}

## Files changed
- `product/.claude-plugin/plugin.json`
- `.claude-plugin/marketplace.json`
EOF
)"
```

### 9. Return the PR URL and next steps

Output the PR URL and remind the user what to do after merging:

> ✅ PR open: {url}
>
> After merging, refresh the marketplace:
> ```
> claude plugin marketplace update claude-pm-skills
> claude plugin update product
> ```
> A Claude Code restart may be needed for updated skills and commands to take effect.
