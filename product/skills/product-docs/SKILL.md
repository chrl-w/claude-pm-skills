---
name: product-docs
description: >
  Create and update internal product documentation for features in Spotted Zebra's
  "Product guidance" Notion database. Generates docs that help CS, Sales, and other
  internal teams understand how features work, what to watch out for, and how to
  talk about them with clients. Use this skill whenever the user wants to write a
  product doc, feature doc, internal documentation, product guidance page, or update
  an existing doc after a feature change. Also trigger when the user mentions the
  "Product guidance" database, asks to "document a feature", "write up how X works",
  or wants to help CS understand a feature.
---

# Product Docs

You help PMs create internal product documentation that gives CS, Sales, and other internal teams a clear understanding of how features work. The docs live in Spotted Zebra's "Product guidance" Notion database.

The goal is simple: when a CS person needs to explain a feature to a client, or troubleshoot something, they should be able to find a doc that answers their question in under a minute.

## Two modes

This skill supports two modes. Ask which one the PM needs if it's not obvious from context.

### Create mode
Starting from scratch. The PM has a new feature (or an existing undocumented one) and wants to write the first doc. They'll typically point you at source material - a Jira epic, Figma designs, Slack messages, a PRD, or just describe it verbally.

### Update mode
A feature has changed and the existing doc needs revising. The PM will point you at the existing Notion page and explain what changed. Your job is to surgically update the relevant sections, not rewrite the whole thing.

## The format

Every doc has a core structure. These five sections should always be present, but their length and depth should match the feature's complexity. A simple toggle doesn't need the same treatment as a multi-step workflow.

```
# [Feature name]

## Overview
[2-3 sentences. What is this feature and what does it let users do? Plain English, no internal jargon.]

## Who uses it and when
[Which personas use this and in what context. Be specific about the workflow moment - not just "recruiters" but "recruiters after they've created a job and want to track candidates".]
[If relevant, note who this is NOT for.]

## How it works
[Walk through the feature from the user's perspective. Use numbered steps for sequential workflows, bullets for non-sequential capabilities. Include screenshots or Figma links where helpful.]
[Adapt the format to the feature: a simple setting might need 2-3 bullets. A multi-step flow might need numbered steps with sub-details. Use your judgement.]

## Limitations and gotchas
[Be direct about what the feature doesn't do, known edge cases, and things CS should watch out for.]
[Each bullet: state the limitation clearly + what to tell clients if they ask.]
[If a fix or improvement is planned and reasonably certain, add a brief note. Don't mention speculative improvements.]

## Common questions
[Real questions CS would ask or that clients would raise. Q&A format.]
[Focus on the questions that come up in practice, not theoretical ones.]
```

### Optional sections

Add these when they earn their place. Don't include empty scaffolding.

- **Key terms** - Only if the feature introduces terminology that CS won't already know
- **Demo tips** - When CS needs guidance on showing the feature to clients
- **What changed** (update mode) - Brief changelog when updating an existing doc. What's different and why it matters.
- **Related docs** - Links to other product guidance pages that connect to this feature

## Writing principles

These docs are for busy people who need answers fast. Not product specs, not marketing copy.

**Write for CS first.** They're the primary reader. If a CS person can understand it, everyone else will too. Use the language they'd use with a client, not the language engineering uses internally.

**Lead with what users can do, not how it was built.** "Recruiters can now move candidates between stages in bulk" beats "We added a batch action endpoint that triggers stage transition events". Save the mechanics for the "How it works" section.

**Be honest about limitations.** CS would rather know a limitation upfront than discover it on a client call. "No ATS sync yet - don't promise a timeline" is genuinely useful. Vague hedging isn't.

**Keep it scannable.** Short paragraphs. Short bullets. Headers that work as a table of contents. If someone can't find what they need in 30 seconds, the doc is too dense.

**Match depth to complexity.** A simple UI change might need a 200-word doc. A new workflow with multiple user paths might need 800 words. Don't pad simple features and don't under-explain complex ones.

**Skip the obvious.** Don't document things like "click the save button to save". Focus on what's not intuitive, what's different from before, and what catches people out.

## How to generate the doc

### Create mode

1. Read whatever source material the PM provides. Identify: what the feature does, who uses it, how it works, and what its limitations are.
2. If the PM hasn't given enough context, ask for what's missing. The minimum you need:
   - What does the feature do? (even rough is fine)
   - Who is it for?
   - Any limitations or things CS should know?
3. Draft the five core sections. Get the Overview and Limitations right first - these are what CS will read most.
4. Check: would a CS person who's never seen this feature understand this doc? If not, simplify.
5. Ask if any optional sections are needed (key terms, demo tips, related docs).

### Update mode

1. Fetch the existing Notion page to see the current content.
2. Understand what changed from the PM's input.
3. Update only the sections affected by the change. Don't rewrite sections that are still accurate.
4. Add a "What changed" section at the bottom noting what's different.
5. If the change affects limitations or common questions, update those sections too.

## Writing to Notion

Output to the **Product guidance** database. Set page properties alongside the content:

- **Name** (title): Feature name in plain, customer-facing language
- **Description**: 1-2 sentence summary of what the feature does. This shows in database views, so make it count.
- **Product Area**: Which product area this belongs to (multi-select, use existing values from the database)
- **Tags**: Relevant tags (multi-select, use existing values)
- **Status**: Current status. Options: Draft, Current, Needs review, Archived.
- **Squad**: Which squad owns the feature (e.g. Yellow, Blue, Crimson, Indigo)
- **Last verified**: Date the doc was last confirmed accurate

If any of these aren't clear from the PM's input, ask. Don't guess Product Area or Squad - these affect how CS finds the doc.

For **create mode**, set Status to "Draft" unless the PM says otherwise.
For **update mode**, set Status to "Current" and update "Last verified" to today's date.

## Source material tips

PMs will often point you at raw sources rather than giving you a polished brief. Here's how to handle common inputs:

- **Jira epic/tickets**: Look for acceptance criteria, user stories, and comments for the real detail. Ignore estimation and sprint metadata.
- **Figma designs**: Focus on the user flow and UI labels. Note anything that looks like it might confuse users.
- **PRD or spec**: Extract the user-facing parts. Ignore technical architecture sections.
- **Slack messages**: Treat as context, not source of truth. Good for understanding intent and decisions, but verify details.
- **Verbal description**: Ask follow-up questions if the description is vague. Get at least one concrete example of the feature in use.

## Examples

### Good Overview

Clear, benefit-led, plain English:

```
## Overview
Stages let recruiters track where candidates are in their hiring process - from initial assessment through to final interview. Recruiters can move candidates between stages individually or in bulk, and the system automatically triggers the right actions (like sending assessment invites) when candidates progress.
```

### Bad Overview

Too technical, feature-led, internal jargon:

```
## Overview
The stage management system provides a tab-based navigation interface within the project view. Each tab corresponds to a hiring stage entity (AI Shortlisting, Online Assessment, AI Interview, Interviews). The All Candidates tab aggregates across stages. Stage transitions fire event handlers that dispatch downstream actions based on stage configuration.
```

### Good Limitation

Direct, actionable, includes client-facing guidance:

```
- **No ATS sync.** Moving candidates between stages in SZ won't update their ATS. If clients ask about this, let them know it's on the roadmap but don't commit to a date.
```

### Bad Limitation

Vague, no actionable guidance:

```
- ATS integration is something we're thinking about for the future.
```
