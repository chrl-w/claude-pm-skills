---
name: release-notes
description: >
  Generate internal release notes for Yellow crew features going out in the next release, based on
  merged commits since the last staging release in the sz-monorepo. Covers new features and fixes to
  live bugs (not bugs made during development), and bundles related PRs into one update per feature. Produces a scannable "What's changed"
  list in the standard SZ format for CS and commercial teams to review. Use this skill whenever the
  user wants to write up a release, create a changelog, or draft release notes. Also trigger when
  the user says "what's going out", "write release notes", "what did we ship", or "release summary".
---

# Release Notes

Generate internal release notes covering the **Yellow crew features** merged since the last staging release. Output follows the standard SZ release notes format. PMs review before sharing — do not attempt to determine what's behind a feature flag or ready to ship.

## Source of truth

The monorepo (`sz-monorepo`) uses git tags as the release baseline. `root@staging` marks the last deployed staging release. Everything on `main` that isn't in `root@staging` is going into the next release.

`root@staging` is a moving tag, and `git fetch --tags` does not update a moved tag that already exists locally. Force-fetch it, and compare against `origin/main` (not the local branch):

```bash
git fetch origin main
git fetch origin 'refs/tags/root@staging:refs/tags/root@staging' --force
git log -1 --format='%h %ad %s' --date=short root@staging   # sanity check: should be a recent chore(release) commit
git log root@staging..origin/main --no-merges --pretty=format:"%h %s"
```

`root@staging` can sit on a hotfix branch rather than `main`. Commits cherry-picked onto that hotfix branch appear again on `main` with a different hash — drop any commit whose subject already appears in `git log <last vX.Y.0 tag>..root@staging`.

## Commit format

Each line represents a merged PR:
`<type>: [TICKET-ID] - description (#PR-number)`

Examples:
- `feat: [YL-2710] - candidates invites on first stage (#323)`
- `fix: [NO_JIRA] - bulk shortlist fix (#372)`

## Step 1: Filter to Yellow features and live bug fixes

The notes cover two things in Yellow's areas: **new features** and **fixes to bugs that clients could hit in the live product**. They leave out bugs made and fixed during development of a feature that hasn't been released yet; CS never saw those, so they don't need to know.

Skip `chore`, `ci`, `docs`, `test`, `refactor`, `style`, `build` and reverts.

### Features (`feat`)

- Keep `feat` commits on a `YL-` ticket.
- Also keep `feat` commits on a `PDE-` ticket in a Yellow area. These are small client-requested changes made through support (e.g. hiding closed roles in an export).
- **`feat: [NO_JIRA]` or untyped PRs** — skip by default. If the title is clearly Yellow territory (see the area table), list it under "Check with the PM" instead of in the notes.
- **A `feat` with no user impact** (e.g. a backend-only step with nothing to see yet) — fold it into the feature it supports. If it supports nothing user-visible in this release, apply the CS rule below.

### Fixes (`fix`)

Live client bugs are usually **not** on `YL-` tickets — support issues are logged in the `PDE` project (e.g. the "Okapi support" epic). So check fixes across `YL-`, `PDE-` and `[NO_JIRA]`, and decide by **whether the broken thing was already live**, not by prefix:

| Fix | Include? |
|-----|----------|
| On a `PDE-` ticket, in a Yellow area (see the area table) | ✅ Include — it's a reported live issue |
| On a `YL-` ticket of type **Bug**, whose epic isn't in progress | ✅ Include |
| On a `YL-` ticket (or epic) that also has `feat` commits in this range, or whose epic is still in progress | ❌ Dev bug — fold into that feature's bullet, don't list it |
| `[NO_JIRA]` fix to a feature that is new in this range (e.g. "omnisearch QC fixes" when omnisearch ships in this release) | ❌ Dev bug — fold into the feature |
| `[NO_JIRA]` fix to something already live, in a Yellow area | ⚠️ "Check with the PM" — can't confirm the crew |
| Fix in another crew's area (AI Interviews, AI Shortlist, Interviews, Assessments) | ❌ Skip |

To check "already live": the feature's `feat` commits should be in `root@staging` (`git log root@staging --oneline | grep <ticket>`), not only in this range. If unsure, ask the PM.

Drop any fix whose commit is a hotfix cherry-pick already on `root@staging` (see Source of truth) — it's already been released.

## Step 2: Bundle into features

Release notes describe **features**, not PRs. Several PRs are often just regular development steps on one feature (backend, then UI, then a follow-up like restoring a table search or keeping a list in sync). Those become **one** bullet.

1. Fetch every remaining `YL-` and `PDE-` ticket from Jira (one JQL `key in (...)` query, fields `summary,issuetype,status,parent,description`). Issue type and parent epic status drive the fix rules above.
2. Group commits that share a ticket, or whose tickets share a parent epic.
3. Write one bullet per group, describing the outcome for the user, not the dev steps. Mention a sub-part only if CS would need to know it on its own.

Example: `YL-3163 omnisearch backend`, `YL-3163 omnisearch command palette` and `YL-3163 bring back the Roles table search and sync My roles with omnisearch` become one bullet:

> :new: [Roles] Omnisearch: find roles and candidates from one search in the company app.

## Jira configuration

**Cloud ID:** `0a01a553-0bb8-4ac1-943d-eb9a2535647e`

Fall back to the PR title if a ticket can't be found.

## Output format

Single `What's changed` section.

### Emoji

| Emoji | Meaning |
|-------|---------|
| `:new:` | New feature or capability |
| `:cake:` | Improvement to an existing feature, or a live bug fix (start fixes with "Fixed …") |

Bundle bug fixes too: several fixes to the same live issue become one bullet.

### Area tags

Each bullet gets a short `[Area]` label for Yellow's areas:

| Label | Covers |
|-------|--------|
| `[Roles]` | Roles list, role setup, role overview, requisition linking, omnisearch |
| `[Role Kick Off]` | Role kick off, intake, role skills profile, templates |
| `[Hiring Process]` | Stages, candidate pipeline, progression and rejection |
| `[Skills]` | Skills taxonomy, adding and editing skills |
| `[Admin]` | SZ admin app features owned by Yellow (admin roles table, filters, exports) |

If unsure which label to use, ask the user — don't guess.

Order bullets by that table, `:new:` before `:cake:` within each area.

### CS inclusion rule

If in doubt about whether to include something, ask: would CS need to know this to support clients, handle admin, or talk to customers? If yes, include it.

## Example output

```
**What's changed**

:new: [Roles] Omnisearch: find roles and candidates from one search in the company app.
:new: [Roles] The requisition's location now shows when linking a req and on the role overview.
:cake: [Roles] Role status changes, including closing a role, are now recorded so we can report on when roles open and close.
:cake: [Roles] The candidate results export now hides closed roles by default.
:cake: [Roles] Fixed role names not accepting =, + or @ mid-name.
:cake: [Roles] Fixed users getting stuck at login when their last workspace was no longer accessible.

**Check with the PM**
- feat: [NO_JIRA] - bulk archive roles from the roles list (#1701)
```

Finish with a one-line note of how many commits were in range, how many features and live fixes came out of them, and how many fixes were left out as dev bugs, so the PM can sanity-check the filter.
