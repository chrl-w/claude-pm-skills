---
name: create-analytics-event
description: Create, name, and parameterise Heap analytics events following Spotted Zebra's event taxonomy. Use this skill whenever someone asks to create an analytics event, name a Heap event, track an action, add tracking to a feature, implement event tracking, or asks "what should I call this event?". Also trigger when reviewing PRs that include Heap tracking, when a squad asks about analytics naming conventions, or when anyone mentions Heap events, event taxonomy, or analytics tracking in the context of product work.
argument-hint: "<describe the user action to track>"
---

# Create Analytics Event

You help squads at Spotted Zebra name and parameterise Heap analytics events correctly. Your goal is to produce event names that are deterministic, reusable, and consistent with the company taxonomy.

## Source of truth

The canonical taxonomy lives on Notion and may be updated as new domains or actions are approved. Before naming any event, fetch the latest version:

**Notion page:** `310a5bba35bc80ef859dcf96220f8fd5` (Analytics Governance)

Use the `notion-fetch` tool with this page ID to get the current controlled lists for domains, actions, and parameters. If the Notion tool is unavailable, fall back to the reference snapshot below, but always prefer the live Notion page.

## The format

Event names follow this pattern:

```
{domain}-{object}-{action}   (when the object differs from the domain)
{domain}-{action}             (when the domain entity is the direct target)
```

Each part can be multi-word with hyphens (e.g. `add-candidates`, `priority-skills`, `candidate-row`).

**When to include the object:** Include it when the thing being acted on differs from the domain entity. For example, `candidate-filter-selected` — the candidate isn't being selected, the filter is.

**When to omit the object:** Omit it when the domain entity is the direct target of the action. For example, `candidate-added` — the candidate is what's being added. Adding an object here would either be redundant (`candidate-candidate-added`) or ambiguous (`candidate-stage-added` reads as "a stage was added to the candidate"). Put the context in parameters instead.

**Parsing logic:** Domain is matched from the start against the controlled list. Action is matched from the end against the controlled list. Everything in between is the object (which may be empty). This makes parsing deterministic even with multi-word parts.

## User intake

If the user invoked this skill with an argument, use it directly. Otherwise ask: "What user action do you want to track?"

Accept any level of specificity:
- A specific interaction ("user clicks the filter for role match on the pipeline")
- A feature area ("we need tracking for the new bulk invite flow")
- A vague description ("track something when they use the calendar sync")

If the description is ambiguous, ask **one** focused clarifying question. Don't over-ask — make a recommendation and let the user correct it.

## How to name an event

Follow this sequence for every event. It maps directly to the decision tree in the taxonomy doc.

### Step 1: Pick the domain

Domain represents **what entity owns the thing being acted on**, not where the user navigated from. Location goes into the `source` parameter instead.

Ask yourself: "If we moved this UI element to a different page tomorrow, would the domain still make sense?" If not, you've picked a navigation-based domain rather than an entity-based one.

Fetch the controlled domain list from the Notion page. If unavailable, the current snapshot is:

| Domain | When to use |
|---|---|
| `role` | The role as a container: hiring team, role settings, structural changes like adding/removing stages (`role-stage-added`), tab navigation within a role (`role-tab-selected`). Not stage internals (that's `stage`) or candidate management (that's `candidate`). |
| `skill-profile` | Editing the Role Success Profile: skills, competencies, weightings, profile configuration. Formerly `rsp`. |
| `candidate` | Actions where candidates are the entity being acted on - whether one or many. Includes: viewing, selecting, filtering, searching, sorting, paginating, adding, removing, inviting, progressing, rejecting, shortlisting, exporting, and copying links. Covers both individual and bulk operations (differentiate with `isBulk` and `candidateCount` params). Use `source` to indicate where the action was triggered. |
| `interviews` | Interview Guide Blueprint: CIG, scoring, calibration, behaviours, feedback. Not the AI notetaker (that's `meetings`). |
| `meetings` | AI notetaker: meeting recordings, summaries, transcripts. Not interview scoring or guides (that's `interviews`). |
| `online-assessment` | Actions unique to the Assessment stage: assessment-specific reports, settings, configuration. |
| `ai-interview` | Actions unique to the AI Interview stage: AI-interview-specific reports, settings, configuration. |
| `shortlist` | Actions unique to the Shortlist stage. |
| `nav` | Top-level app navigation, support links, feedback. Not tab navigation within a role (that's `role`). |
| `user` | User account settings, profile, preferences. |
| `workspace` | Platform-level actions outside any single role: inviting users to the platform, workspace settings, admin configuration. |

If the feature doesn't fit an existing domain, flag it. New domains need Product approval.

### Step 2: Identify the object (or decide to omit it)

**First, check:** Is the domain entity the direct target of the action? If so, omit the object entirely and use `{domain}-{action}`. For example, `candidate-added` — the candidate is what's being added, so there's no separate object. The context (which stage, which method) goes into parameters.

**If the object differs from the domain**, include it. The object should tell someone **what happened** without needing to read the parameters. Use the most specific noun phrase that describes the interaction. Multi-word objects with hyphens are fine and often better.

**The test:** Read `{domain}-{object}-{action}` aloud. Does it make sense as a sentence? "candidate move-target selected" is clear. "candidate target selected" is ambiguous (what target?).

Good objects: `search`, `filter`, `move-target`, `invite-language`, `assignee`, `report`, `template`, `recording`, `calibration`, `behaviour`, `team-member`, `candidate-row`, `score-type`, `tab`, `feedback`, `priority-skills`, `stage`, `invite-link`, `score-override`, `bulk-action-bar`, `results`, `stage-tab`, `selection`, `decision`, `link`

Bad objects: bare nouns that don't describe the action context (e.g. `candidates` when you mean `move-target`, `stage` when you mean `stage-settings`). Also avoid UI element names (`accordion`, `modal`, `dropdown`, `button`) — name the feature or content instead.

**Flow disambiguation:** When a single object has multiple distinct flows (e.g. add, edit, invite), include the flow verb in the object to avoid ambiguity. For example, `team-member-add-opened` and `team-member-edit-submitted` are clearer than `team-member-opened` and `team-member-submitted`. The test: if removing the flow verb makes the event name ambiguous about which user journey it belongs to, keep it in.

If the object could apply across multiple domains (e.g. `search`, `filter`), that's a signal it should be one event with domain/source in parameters, not separate events per location.

### Step 3: Pick the action

Always past tense. Fetch the controlled action list from the Notion page. Current snapshot:

| Action | Use when |
|---|---|
| `clicked` | Button, link, or element tap |
| `selected` | Dropdown choice, tab switch, option pick |
| `changed` | Text input, search query typed |
| `submitted` | Form submission, final confirmation |
| `toggled` | Toggle switch, tickbox |
| `copied` | Copy to clipboard |
| `updated` | Settings, configuration, or properties saved/changed (use instead of `submitted` for settings mutations) |
| `searched` | A search query is executed or search filters are applied |
| `cleared` | Search cleared, filter reset |
| `opened` | Modal, drawer, accordion expanded |
| `closed` | Modal, drawer, accordion collapsed |
| `viewed` | Page or section seen (pageview-like) |
| `removed` | Item deleted from a list |
| `added` | Item added to a list |
| `invited` | Invitation or communication sent to join the platform or a resource |
| `progressed` | Entity moved forward to a next stage or step in a workflow |
| `rejected` | Entity rejected or declined from a stage or process |
| `unrejected` | A previous rejection is reversed or undone |
| `shortlisted` | Entity flagged as a favourite or priority pick within a group |
| `exported` | Data exported from the platform (e.g. CSV download, report generation) |

**Prefer existing actions first.** Most interactions fit an existing action. Before proposing a new one, ask: "Could I make the object more descriptive and use an existing action?" For example, "bulk reject candidates" is better as `candidate-rejected` (with `isBulk: true`) than inventing a new action.

**If no existing action genuinely fits:**
1. Propose the new action to the user with a clear rationale for why existing ones don't work.
2. The action must be past tense, one word, and describe the verb generically (not specific to one feature).
3. If the user approves, **add the new action to the Notion taxonomy page** in the Actions table so future events can reuse it. Use the `notion-update-page` tool to append to the actions section.

### Step 4: Check for reuse in the codebase

Before finalising a name, read the existing event constants from the monorepo:

**File:** `~/sz-monorepo/clients/company-client/src/helpers/analytics/analyticsConstants.ts`

Check whether an event with the same or equivalent name already exists:

- **Exact match** → reuse it; differentiate with parameters only. Add a `♻️ Reusing existing event` callout in the output.
- **No match** → proceed with the new event name.

When reusing an existing event, include a note in the Jira ticket:
> ♻️ This reuses the existing `{event-name}` event — no new constant required. Parameters only.

### Step 5: Add parameters

Parameters always use **camelCase**. Never kebab-case, never snake_case.

Fetch the full parameter lists from the Notion page. The three tiers below are a current snapshot.

**Global parameters** — include on every event whenever available:

| Parameter | Description |
|---|---|
| `companyId` | Company ID of the active workspace |
| `userAccessLevel` | `full`, `standard`, or `limited` |

**Domain-specific parameters** — nearly always include when the event is in the listed domain, if available in the flow. May also be relevant in other domains:

| Parameter | Domains | Description |
|---|---|---|
| `roleID` | role, candidate, skill-profile, interviews, online-assessment, ai-interview, shortlist | The role (project) ID. Include on all events scoped to a role. |
| `hiringTeamRole` | role, candidate, skill-profile, interviews, online-assessment, ai-interview, shortlist | Role of the logged-in user on this role (e.g. `"recruiter"`, `"hiring-manager"`). Pass `null` when the user is not on the hiring team — the distinction is meaningful for segmentation. |
| `productSolution` | role, candidate, skill-profile, interviews, online-assessment, ai-interview, shortlist | Product solution context (e.g. `professional-hiring`, `early-careers`, `volume`). Include on all role-scoped events. |
| `meetingId` | meetings | The subId of the meeting. |
| `meetingType` | meetings | Type of meeting: `intake`, `general`, `interview`. |

**Contextual parameters** — include when they add meaningful context to the event. Always check the Notion taxonomy for the full current list before proposing new ones:

| Parameter | When to use |
|---|---|
| `source` | Where the action was triggered from (e.g. `results-tab`, `candidate-drawer`, `hiring-process-tab`). **Required** when the same action can be triggered from two or more entry points — without it, Heap cannot distinguish which flow fired the event. |
| `stageId` | The specific stage instance ID |
| `stageType` | `shortlist`, `online-assessment`, `ai-interview`, `interview` |
| `filterType` | What kind of filter was applied |
| `filterValue` | The value of the filter |
| `value` | Generic selected/entered value (prefer a specific parameter name where possible) |
| `skillName` | Human-readable skill name |
| `tabNumber`, `itemNumber` | Ordinal position (1-indexed) |
| `state` | `on`/`off`, `opened`/`closed`, `ticked`/`unticked` |
| `targetStageId`, `targetStageName`, `targetStageType` | When the action moves a candidate to a specific stage |
| `candidateCount` | Number of candidates affected |
| `isMixedSelection` | Whether the selection spans multiple stage types |
| `affectedCount`, `skippedCount` | For bulk operations: how many succeeded and how many were skipped |
| `inviteLanguage` | Language selected for a candidate invite |
| `scoreCategory`, `isEvaluator`, `hasResults` | Interview/assessment context |
| `method`, `actionType`, `settingName` | For settings or configuration events |

**Prefer fewer parameters.** If one parameter already communicates the same information as another, drop the redundant one. For example, if `value` is `"shortlist"` then a separate `stageType` parameter is redundant.

### Step 6: Sanity check

Ask: "Could this event be reused if the same action appears in a new location or stage?" If not, context is probably baked into the name.

### Step 7: Add dev implementation notes

For each event, consider whether the **firing condition** needs clarifying for the developer. The event name describes *what* is tracked, but devs also need to know *when* to fire it.

**Rule: Fire on mutation success, not on button click.**
If the event tracks an outcome (add, remove, progress, reject, update), fire it when the API mutation resolves successfully — not when the user clicks the button. Click-time fires create false positives when the mutation fails.
_Exception:_ Fire on click only if the user is navigating to an external system and no mutation outcome is trackable (e.g. opening an ATS link in a new tab).

Other cases to call out:
- **Debounce:** If the event is triggered by typing (e.g. search), specify that it should fire after a debounce (recommend 300-500ms) or on Enter, not on every keystroke.
- **Pageview-like events:** If using the `viewed` action, clarify whether it fires on component mount, route change, or tab render.

Include these as a "Dev note" beneath the event's parameter table. Keep them short and specific.

### Step 8: Update the taxonomy with new parameters

After finalising all events, check whether any parameters you have used are **not already listed** in the Notion taxonomy page (`310a5bba35bc80ef859dcf96220f8fd5`).

For each new parameter:
1. Confirm with the user that it should be added to the taxonomy.
2. Write a **generic description** that explains the parameter's purpose without tying it to the specific feature. Other squads should be able to reuse it.
3. Use the `notion-update-page` tool to append the new parameters to the relevant parameters table.

This keeps the taxonomy page as the single source of truth and prevents parameter drift across squads.

## Anti-patterns to catch

When reviewing events (yours or someone else's), watch for these:

| Problem | Fix |
|---|---|
| Stage type in the event name (`candidate-shortlist-filter-clicked`) | One event `candidate-filter-selected` with `stageType: "shortlist"` param |
| UI element in the name (`-button`, `-modal-`, `-dropdown-`) | Remove it; name the feature or content instead |
| Location in the name (`results-tab-search-changed`) | Use `source` param instead |
| Wrong parameter casing (`project_id`, `filter-type`) | Always camelCase |
| Missing global or domain-specific params | Add `companyId`, `userAccessLevel`, `roleID`, `hiringTeamRole` when available |
| Separate events for the same action in different places | Merge into one event with `source` param |

**Positive example — discriminator parameter:**
Instead of `candidate-shortlist-filter-clicked`, `candidate-interview-filter-clicked`, `candidate-assessment-filter-clicked` (three separate events), use one event:
`candidate-filter-selected` with `stageType: "shortlist" | "interview" | "online-assessment"`. One reusable event, sliced in analysis by the discriminator param.

## Output format

When proposing events, use this format for each event:

```
Event name: {domain}-{object}-{action}   (or {domain}-{action} when object is omitted)
Parameters:
  - paramName: "example value"
  - paramName: "example value"
```

If reusing an existing event:
```
♻️ Reusing existing event: {event-name}
Parameters:
  - paramName: "example value"
```

If reviewing multiple events, use the same format for each, and flag any that break the rules.

### Writing up as a Jira ticket

Once events are agreed, the default deliverable is a **Jira engineering ticket**. Ask the user which epic to file it under if not already specified. The ticket should include:

1. **Overview** summarising the scope (e.g. "4 Heap events for candidate actions in the pipeline view").
2. **One section per event** with: event name, firing condition, parameter table (parameter, type, example, notes), and any dev notes.
3. **Acceptance criteria** for each event, written so a QC engineer can verify without needing to understand the feature context. Each AC should cover: the user action that triggers the event, the expected event name in Heap, and a check that each parameter is present with the correct value. Use Given/When/Then format. Example:
   - *Given* a recruiter is viewing the pipeline on a role with `productSolution: "professional-hiring"` / *When* they apply a Decision filter / *Then* `candidate-filter-selected` fires with `filterType: "decision"`, `roleID`, `hiringTeamRole: "recruiter"`, `companyId`, and `userAccessLevel` set correctly.
4. **Global parameters** reminder (`companyId`, `userAccessLevel`).
5. **Implementation notes** linking to the Notion taxonomy page.

Use the Jira MCP tools to create the ticket. If the user provides a Figma link as the source, include it in the ticket description for context.

## Key domain distinctions

These are the most common points of confusion:

- **`role` structure vs stage config**: `role` owns the structure (adding/removing stages, role-level settings, team members). Stage configuration events (criteria, priority skills, stage settings) belong to the most specific applicable domain — typically `role` or the stage-type domain (`online-assessment`, `ai-interview`, `shortlist`, `interviews`).
- **`meetings` vs `interviews`**: `meetings` is the AI notetaker function (recordings, summaries, transcripts). `interviews` is the Interview Guide Blueprint (scoring, calibration, behaviours, feedback).
- **`candidate` scope**: covers all actions where candidates are the entity - individual or bulk. Filtering a candidate list, selecting candidates, progressing one candidate from a drawer, or bulk-rejecting 50 from the toolbar are all `candidate-` domain. Use `isBulk`/`candidateCount` params for cardinality, `source` for entry point. Not for role structure (adding stages, team members).
- **`nav` vs `role` tabs**: Top-level app navigation is `nav`. Tab switches within a role are `role-tab-selected`.

**The one rule:** domain = the entity being acted on. If you're doing something to candidates, it's `candidate-`. If you're changing the role's structure, it's `role-`. If you're configuring a stage, it's `stage-`.
