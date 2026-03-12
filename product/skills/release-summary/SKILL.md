---
name: release-summary
description: >
  Create release summaries for internal teams (CS, Sales, Support) after each release. Pulls merged
  PRs from GitHub, extracts Jira ticket keys, cross-references the Upcoming Feature Releases database
  for consistency, and publishes to Notion. Use this skill whenever the user wants to summarise what
  shipped, write up a release, create a changelog, or draft a post-release update. Also trigger when
  the user says "what went out", "write up this release", "release summary", "ship notes", or
  "what did we ship".
---

# Release Summary

Create clear, scannable release summaries for internal teams after each product release. Uses GitHub as the source of truth for what shipped, links back to Jira for context, and cross-references the Upcoming Feature Releases database for consistency.

## Workflow

1. **Identify the release** — Get the release tag from the user
2. **Gather merged PRs from GitHub** — Pull PRs between tags across repos
3. **Extract and fetch Jira tickets** — Parse PR titles for ticket keys, fetch details
4. **Cross-reference upcoming-releases** — Check what was already communicated
5. **Draft release summary** — Write in standard format, share for review
6. **Iterate** — Refine based on feedback
7. **Update upcoming-releases statuses** — Move shipped entries to "Shipped 🚀"
8. **Publish to Notion** — Save the summary
9. **Offer Slack update** — Optional per-feature announcements

## Configuration

### GitHub Organisation
`Spotted-Zebra-UK`

### Core Product Repos
These repos are checked by default for every release:
- `sz-monolith`
- `sz-company-client`
- `sz-admin-client`
- `sz-candidate-client`
- `sz-ui-components`
- `sz-client-shared-sub`

### Jira Ticket Key Pattern
Project prefixes: `IC`, `CR`, `YL`, `BL`, `BK`, `DEVOPS`, `EN`
Regex: `(IC|CR|YL|BL|BK|DEVOPS|EN)-\d+`

## Step 1: Identify the Release

Ask the user:
> Which release should I summarise? Give me the tag (e.g. `v2.14`) or say "latest" and I'll find the most recent one.

If the user says "latest", use the `gh` CLI to find the most recent release tag:
```bash
gh release list --repo Spotted-Zebra-UK/sz-monolith --limit 2 --json tagName,publishedAt
```

This returns the current and previous tags, which are needed for the comparison.

## Step 2: Gather Merged PRs from GitHub

For each core product repo, get the merged PRs between the previous release tag and the current one.

Use the `gh` CLI via Desktop Commander to compare tags:
```bash
gh api repos/Spotted-Zebra-UK/{repo}/compare/{previous_tag}...{current_tag} \
  --jq '[.commits[].sha]'
```

Then get the PRs associated with those commits:
```bash
gh pr list --repo Spotted-Zebra-UK/{repo} --state merged \
  --json title,number,mergedAt,headRefName,body \
  --limit 200 \
  --search "merged:{previous_release_date}..{current_release_date}"
```

If a repo doesn't use the same tag scheme, fall back to date-based filtering using the release dates from the monolith tags.

Compile a combined list of all merged PRs across repos. Note which repo each PR came from.

## Step 3: Extract and Fetch Jira Tickets

### Extract ticket keys
Parse each PR title for Jira ticket keys using the pattern `(IC|CR|YL|BL|BK|DEVOPS|EN)-\d+`.

Deduplicate: the same ticket may have PRs across multiple repos. Merge these into a single entry.

### Flag unlinked PRs
PRs without a Jira reference in the title get collected separately. Present these to the user:
> These PRs don't reference a Jira ticket. Should any be included in the release summary?
> - PR #142 (sz-company-client): "Update dependency versions"
> - PR #87 (sz-monolith): "Fix typo in error message"

Let the user decide which (if any) to include.

### Fetch Jira details
Use Jira tools (cloud ID: `0a01a553-0bb8-4ac1-943d-eb9a2535647e`) to retrieve details for each extracted ticket key.

**Include if:**
- User-facing change (new feature, enhancement, bug fix visible to customers)
- Behaviour change CS/Sales need to know about
- Deprecation or removal
- Admin-only change that affects internal workflows

**Exclude:**
- Backend refactors with no user impact
- Feature flag removals (unless behaviour changes)
- Minor UI polish (unless specifically requested)
- Internal tooling changes

## Step 4: Cross-Reference Upcoming Feature Releases

Check the Upcoming Feature Releases Notion database for entries that match features in this release.

**Database ID:** `e8cfad90-b747-4d23-b2b9-feafe5d57007`
**Data source ID:** `collection://2ee8a21e-848a-4fb7-ba5d-60e48071534a`

For each match:
- Use the same customer-facing name already in the database.
- Check "Key things to know" for consistency. The release summary must not contradict limitations or guardrails already communicated.
- Flag entries whose status should move to "Shipped 🚀".

If no matching entries exist, carry on. Not everything goes through pre-release comms.

## Step 5: Draft Release Summary

### Format

```markdown
## Release Summary — [Date]

**User facing changes**
- [Emoji] [App - Product Area] Description.

**SZ facing changes (internal users only initially 🚩)**
- [Emoji] [App - Product Area] Description.

**⚠️ Key things to know for CS:**
- Bullet points for operational context.
```

### Emoji Legend

| Emoji | Meaning |
|-------|---------|
| 🆕 | New feature |
| 🍰 | Enhancement (improvement to existing functionality) |
| 🐛 | Bug fix |
| ☠️ | Deprecation or removal |

### App - Product Area Tag

Format: `[App - Product Area]`

**App options:** Company, Admin, Company & Admin

**Product Area examples:** Role Kick Off, Stages, Interview Guide, Projects, Company Settings, Candidates, Reports

### Writing Style

- One sentence per bullet, ending with full stop.
- Active voice, present tense ("Users can now..." not "Users will be able to...").
- Benefit-led where possible ("Faster project setup" not "Changed default value").
- No jargon — write for CS/Sales, not engineers.
- If a feature was already announced via upcoming-releases, match the language used there.

## Step 6: Share and Iterate

Present the draft. If features were cross-referenced from Upcoming Feature Releases, note which ones and confirm naming is consistent.

## Step 7: Update Upcoming Feature Releases Statuses

After the release summary is approved, present entries to update:

> These features appear in the Upcoming Feature Releases database and have now shipped:
>
> | Feature name | Current status | Proposed status |
> |---|---|---|
> | [name] | Shipping Soon 👀 | Shipped 🚀 |
> | [name] | In Development | Shipped 🚀 |
>
> Should I update these?

Only update after explicit confirmation.

## Step 8: Publish to Notion

On first use, ask where release summaries should live:
> Where should I save release summaries in Notion? You can give me:
> - A page URL (I'll create child pages under it)
> - A database URL (I'll add entries to it)
> - Or tell me to create a new page somewhere

Create the page with:
- **Title**: "Release Summary — [Date]"
- **Content**: The full release summary

## Step 9: Offer Slack Update

Ask if the user wants a Slack announcement for any specific features or the full summary. Always show drafts and get confirmation before sending.

### Slack Update Format (per feature)

```markdown
🚀 **New: [Feature name]**

[1-2 sentence summary of what's new]

⚙️ **How it works:**
- Bullet points explaining the change

✨ **Why this matters:**
- Benefit-focused bullet points

⚠️ **Key things to know:**
- Operational notes for CS/Support (if applicable)
```

Keep Slack updates under 150 words per feature. Show drafts before sending.
