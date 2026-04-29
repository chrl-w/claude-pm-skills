---
name: release-notes
description: >
  Generate internal release notes for what's going out in the next release, based on merged
  commits since the last staging release in the sz-monorepo. Produces a scannable "What's changed"
  list in the standard SZ format for CS and commercial teams to review. Use this skill whenever
  the user wants to write up a release, create a changelog, or draft release notes. Also trigger
  when the user says "what's going out", "write release notes", "what did we ship", or
  "release summary".
---

# Release Notes

Generate internal release notes covering everything merged since the last staging release. Output follows the standard SZ release notes format. PMs review before sharing — do not attempt to determine what's behind a feature flag or ready to ship.

## Source of truth

The monorepo (`sz-monorepo`) uses git tags as the release baseline. `root@staging` marks the last deployed staging release. Everything between `root@staging` and `HEAD` is going into the next release.

```bash
git fetch --tags
git log root@staging..HEAD --pretty=format:"%s"
```

## Commit format

Each line represents a merged PR:
`<type>: [TICKET-ID] - description (#PR-number)`

Examples:
- `feat: [YL-2710] - candidates invites on first stage (#323)`
- `fix: [NO_JIRA] - bulk shortlist fix (#372)`
- `limit email invite to max 5 (#342)`

## Ticket ID pattern

`(IC|CR|YL|BL|BK|DEVOPS|EN)-\d+`

Commits with `[NO_JIRA]` or no ticket at all are still included — use the PR title as the description.

## Jira configuration

**Cloud ID:** `0a01a553-0bb8-4ac1-943d-eb9a2535647e`

Fetch: title, description, epic. Fall back to PR title if a ticket can't be found.

## Output format

Single `What's changed` section. No user-facing/SZ-facing split. No squad grouping.

### Emoji

| Emoji | Meaning |
|-------|---------|
| `:new:` | New feature or capability |
| `:cake:` | Improvement or bug fix |

### Area tags

Each bullet gets a short `[Area]` label. Area label only — no app prefix.

| Label | Covers |
|-------|--------|
| `[Roles]` | Role creation, setup, pipeline |
| `[AI Shortlist]` | AI shortlisting, CV upload, shortlist stage |
| `[AI Interviews]` | AI interview product, candidate config, integrity |
| `[Assessments]` | Assessment stages, scoring, reports |
| `[Interviews]` | Interview guides, evaluations |
| `[Meetings]` | Meetings page, participants, summaries |

If unsure which label to use, ask the user — don't guess.

### Grouping and order

Group bullets by area. Order areas by user journey:
1. Roles
2. AI Shortlist
3. AI Interviews
4. Assessments
5. Interviews
6. Meetings

### What to include

- All merged commits, including `[NO_JIRA]` and unlinked PRs
- Bug fixes that affect end users (client users or SZ admin users)
- Everything — let PMs decide what to share; do not filter by feature flag status

### What to exclude

- Pure infrastructure changes with no user impact (CI fixes, dependency bumps, code cleanup)
- Duplicate entries for the same change

### CS inclusion rule

If in doubt about whether to include something, ask: would CS need to know this to support clients, handle admin, or talk to customers? If yes, include it.

## Example output

```
**What's changed**

:new: [AI Shortlist] Recruiters can now bulk shortlist and unshortlist candidates in a single action, removing the need to action candidates one at a time.
:new: [AI Shortlist] The shortlist view now supports column headers and sorting, making it easier to scan and compare candidates across a role.
:cake: [AI Shortlist] Filter colours updated for improved clarity.
:cake: [AI Shortlist] Candidate invites via email are now capped at 5 per send.
:cake: [AI Shortlist] Fixed an issue where uploaded CVs could get stuck in a processing state indefinitely.

:new: [Meetings] Participants can now be added to existing meetings and evaluators to existing interviews after initial setup.
:new: [Meetings] The meetings page now supports filtering by user or attendee.
:cake: [Meetings] Fixed an issue where some participants were seeing other participants' meeting summaries.

:cake: [AI Interviews] Candidates now see a dedicated configuration screen before their AI interview begins, on both desktop and mobile.
:new: [AI Interviews] Integrity monitoring is now live — signals are collected during AI interviews and flagged in the admin interface.
:new: [AI Interviews] The AI agent used per interview stage can now be configured from the admin UI, without requiring a code change.
```
