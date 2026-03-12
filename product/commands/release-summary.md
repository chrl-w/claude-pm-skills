---
description: Summarise what shipped in a release using GitHub as source of truth, cross-reference Jira and Upcoming Feature Releases
argument-hint: "<release tag e.g. v2.14, or 'latest'>"
---

# Release Summary

Create a release summary for internal teams using GitHub merged PRs as the source of truth. See the **release-summary** skill for the full format, writing principles, repo configuration, and examples.

## Workflow

### 1. Identify the Release

Ask the user for the release tag (e.g. `v2.14`) or use "latest" to find the most recent one from `sz-monolith`.

### 2. Gather Merged PRs from GitHub

For each core product repo (`sz-monolith`, `sz-company-client`, `sz-admin-client`, `sz-candidate-client`, `sz-ui-components`, `sz-client-shared-sub`), use the `gh` CLI to compare tags and pull merged PRs. See the **release-summary** skill for the specific commands.

### 3. Extract and Fetch Jira Tickets

Parse PR titles for Jira ticket keys using pattern `(IC|CR|YL|BL|BK|DEVOPS|EN)-\d+`. Deduplicate across repos. Flag unlinked PRs and ask the user which to include.

Use Jira tools (cloud ID: `0a01a553-0bb8-4ac1-943d-eb9a2535647e`) to retrieve ticket details. Follow the inclusion/exclusion criteria in the **release-summary** skill.

### 4. Cross-Reference Upcoming Feature Releases

Check the Upcoming Feature Releases database for entries that match features in this release.

**Data source ID:** `collection://2ee8a21e-848a-4fb7-ba5d-60e48071534a`

For each match:
- Use the same customer-facing name already in the database.
- Check "Key things to know" for consistency.
- Flag entries that should move to "Shipped 🚀".

### 5. Draft Release Summary

Follow the format in the **release-summary** skill. Share the draft for review.

### 6. Iterate

Incorporate feedback. Confirm cross-referenced naming is consistent with Upcoming Feature Releases.

### 7. Update Upcoming Feature Releases Statuses

After the release summary is approved, present a table of entries to update:

> These features appear in the Upcoming Feature Releases database and have now shipped:
>
> | Feature name | Current status | Proposed status |
> |---|---|---|
> | [name] | Shipping Soon 👀 | Shipped 🚀 |
> | [name] | In Development | Shipped 🚀 |
>
> Should I update these?

Only update after explicit confirmation. Use the Notion tools to set the Status property to `Shipped 🚀` for each confirmed entry.

### 8. Publish to Notion

Save the release summary to Notion. On first use, ask where release summaries should be stored. See the **release-summary** skill for details.

### 9. Offer Slack Update

Offer to post the full summary or individual feature updates to Slack. Always show drafts and get confirmation before sending.
