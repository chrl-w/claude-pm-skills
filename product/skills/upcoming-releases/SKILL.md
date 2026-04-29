---
name: upcoming-releases
description: >
  Create feature release updates for commercial teams (CS and Sales) in the Upcoming Feature
  Releases Notion database. Generates a two-tier format: a simple visibility section that
  commercial teams can scan in seconds, plus optional enablement detail for deeper context.
  Use this skill whenever the user wants to create a release update, feature preview, CS update,
  commercial team update, or anything related to communicating upcoming features to sales and
  CS teams. Also trigger when the user mentions the "Upcoming Feature Releases" database,
  asks to "write up a feature for CS", or wants to communicate what's shipping to commercial teams.
---

# Release Update

You help PMs create feature release updates that give commercial teams (CS and Sales) visibility of what's coming. The format is deliberately lightweight for the PM to create, whilst giving commercial teams what they need to have the right conversations with clients.

## Gathering context automatically

Before drafting, pull context from connected tools to save the PM time.

**From Jira** (cloud ID: `0a01a553-0bb8-4ac1-943d-eb9a2535647e`):
- Search for the feature's epic or tickets using JQL. Key project prefixes: IC (Indigo), CR (Crimson), YL (Yellow), BL (Blue), BK (Black), DEVOPS (DevOps & DevEx), EN (Engineering).
- Pull the epic summary, acceptance criteria, and any linked tickets for scope and limitations.
- Check ticket status to inform the release Status field.

**From Notion**:
- Search the Upcoming Feature Releases database for existing entries on this feature to avoid duplicates.
- Search for related PRDs or design docs that might contain value propositions, user segments, or known limitations.

**From Slack**:
- Search #product-new-releases (C03GGGE0VSS) for prior posts about this feature.
- Search #pde-and-commercial (C04K6U03HJ6) for CS/Sales questions or feedback related to the feature area.

**From local files** (`/Users/charlie_watkinson/brain`):
- Search the brain folder for PRDs, one-pagers, or notes related to the feature. This is the PM's working knowledge base.
- Search `/Users/charlie_watkinson/brain/Granola` specifically for recent meeting notes that might contain product decisions, scope discussions, or stakeholder feedback relevant to the feature.

**From Figma**:
- If the user mentions a Figma URL or file, use the Figma tools to pull screenshots or design context.
- Design screenshots can help inform the "What is it" section and are useful for Tier 2 enablement detail where CS needs to understand what the feature looks like.

Use whatever context you find to pre-fill the draft. Don't block on gathering context if tools aren't connected or searches return nothing.

## The format

Every release update has two tiers. Tier 1 is always present. Tier 2 is added when the PM thinks it's needed.

There are two variants: **feature updates** (customer-facing changes) and **internal/infrastructure updates** (behind-the-scenes improvements).

### Tier 1: Visibility (always present)

This is the minimum viable update. It should be scannable in 10 seconds and work copy/pasted into a Slack message.

#### Feature update (customer-facing)

```
### 🚀 [Customer-facing feature name]

**What is it**
[1-2 lines. Plain English. What changed and what can users do now.]

**Key value**
[1-2 lines. Benefit-led, not feature-led. Why should anyone care.]

**Who cares**
[1 line. Which client segments or use cases this is most relevant for. Include who it's less relevant for if that's useful context.]

**⚠️ Key things to know**
[Optional section. Only include if there are critical guardrails or limitations CS/Sales need to be aware of.]
[Each bullet: state the limitation clearly + what to say to clients if asked.]
[Where a firmed-up improvement is planned, add a brief note e.g. "Richer rejection workflows are planned."]
[Do NOT include speculative improvements or ideas. Only mention things that are reasonably certain.]
```

#### Internal/infrastructure update

Use 🔧 instead of 🚀. These updates keep commercial teams informed about platform improvements without needing client-facing framing.

```
### 🔧 [Descriptive name for the change]

**What is it**
[1-2 lines. Plain English. What changed and why.]

**Key value**
[1-2 lines. Why the business is investing here. Frame in terms of reliability, performance, or reduced client issues. "Reduces client-reported errors and frees up engineering capacity" works. "Things are more stable under the hood" doesn't.]

**Who cares**
[1 line. Which clients or use cases are affected. If it's invisible to clients, say so.]

**⚠️ Key things to know**
[Optional. Only include if there's downtime, migration steps, or behaviour changes CS should be aware of.]
```

### Tier 2: Enablement detail (added when needed)

Below a horizontal divider. Add this when the feature is complex enough that commercial teams need deeper context for demos, onboarding, or handling client objections. Typically only needed for feature updates, not internal ones.

```
---

## 📖 Enablement detail

*Add this section when commercial teams need deeper context for demos, onboarding, or objection handling.*

### What's new in detail
[Feature bullets. Benefit-led where possible. Keep each bullet to 1-2 lines.]

### Handling [specific objection or question]
[Name the question clients will ask. Give the answer CS/Sales should use.]
[Create a separate heading for each major objection if there are several.]

### Worth highlighting: [thing]
[Optional. Call out anything CS/Sales should actively demo or mention in conversations.]

### Client message (copy/paste)
[Ready-to-send message for CS to email or Slack to clients. Conversational, not marketing-speak. 3-5 lines max.]
```

## Writing principles

Commercial teams won't read something that feels like a product spec. They need to grab the key message and move on. These principles keep the copy useful.

**Use customer-facing language.** Internal feature names like "Candidate progression and rejection and updated add flows (Projects 2.0)" are meaningless to CS or Sales. Give it a name a client would understand. If the PM's working title is internal jargon, suggest a cleaner alternative.

**Lead with value, not mechanics.** "See where every candidate is and move them forward in a few clicks" works. "We added stage tabs to the project view with an All Candidates tab" doesn't. CS and Sales need to know why this matters to clients, not how it was built. For internal/infrastructure changes, "Key value" should still communicate why the business is investing here. "Reduces client issues and frees up engineering time" is a value statement. "Things are more stable under the hood" is not.

**Keep it scannable.** Short paragraphs. Short bullets. No walls of text. If the Tier 1 section is too long for a Slack message, it's too long. Aim for the whole Tier 1 to fit on a single screen.

**Be direct about limitations.** "Key things to know" should be honest and specific. "No ATS sync. Do not promise it is coming imminently." is better than vague hedging. CS would rather know the boundary upfront than get caught out in a client conversation.

**One concept per bullet.** Each bullet in "Key things to know" should cover one limitation or guardrail. Don't combine multiple things into a single bullet.

**Improvements only when firmed up.** If something is planned and reasonably certain, add a brief note: "Richer rejection workflows are planned." Don't include ideas, things being explored, or anything that might not happen. If in doubt, leave it out.

## How to generate the update

When the PM asks you to create a release update:

1. **Gather context.** Search Jira, Notion, and Slack for relevant information (see "Gathering context automatically" above). Use whatever you find to pre-fill the draft.
2. **Determine the variant.** Is this a customer-facing feature (🚀) or an internal/infrastructure change (🔧)? If unclear, ask.
3. **Read the input carefully.** Identify: what changed, who it affects, what the limitations are, and what's coming next.
4. **Draft Tier 1 first.** This is the priority. Get this right before anything else.
5. **Suggest a customer-facing feature name.** If the PM's working title is internal jargon, propose something cleaner and check with them. For internal updates, suggest a clear descriptive name.
6. **Ask if they want Tier 2 enablement detail.** If they've provided enough context, draft it. If not, leave it as a placeholder. Internal updates rarely need Tier 2.
7. **Look for objections that CS/Sales will face.** If the feature has limitations that clients will push back on, write "Handling [objection]" sections that give CS a clear answer.

## Asking for input

If the PM hasn't provided enough context, ask for what's missing. But keep it lightweight. This should feel like a 5-minute task, not an interrogation.

The minimum you need:

- What does the feature do? (even a rough description is fine)
- Who is it for?
- Any critical limitations or things CS shouldn't promise?

Everything else can be inferred or added later. Don't block on perfection.

## Writing to Notion

When outputting to the Upcoming Feature Releases database, use the Notion tools to create a page in the database.

**Database ID:** `e8cfad90-b747-4d23-b2b9-feafe5d57007`
**Data source ID:** `collection://2ee8a21e-848a-4fb7-ba5d-60e48071534a`

Set the page properties:

- **Feature name** (title): Customer-facing name (or descriptive name for internal updates).
- **tl'dr** (rich_text): 1-2 line summary. Should match or closely mirror the "What is it" section.
- **Status** (select): Current status. Options are exactly: `Coming up 🙏`, `In Development`, `Shipping Soon 👀`, `Shipped 🚀`.
- **Target timeline** (rich_text): When it's expected to ship (e.g. "Late March", "Q2 2026").
- **Squad** (multi_select): Which squad(s) own the feature. Options: `Indigo`, `Crimson`, `Yellow`, `Blue`. Map from Jira project keys: IC=Indigo, CR=Crimson, YL=Yellow, BL=Blue.

If any of these aren't clear from the PM's input, ask.

## Slack distribution (optional)

After writing to Notion, offer to post a summary to #pde-and-commercial (channel ID: `C04K6U03HJ6`). This is where commercial teams pick up product updates.

Format the Slack message as the Tier 1 content only. It should work as a standalone message without needing to click through to Notion. Include a link to the Notion page at the bottom for anyone who wants the full detail.

Before sending, always show the PM the draft message and get confirmation.

## Examples

### Good Tier 1 (feature update)

Scannable. Benefit-led. Customer-facing name. Clear guardrails.

```
### 🚀 Candidate Pipeline Management

**What is it**
Candidates can now be progressed between hiring stages, rejected, and managed in bulk. No ATS sync.

**Key value**
See where every candidate is and move them forward in a few clicks. Bulk actions make large campaigns dramatically faster.

**Who cares**
Multi-stage hiring clients and early careers teams with high volumes. Less relevant for single-assessment-only clients.

**⚠️ Key things to know**
- No ATS sync. Progressing or rejecting in SZ will not update their ATS. ATS sync is on the roadmap but not yet scheduled.
- Rejection is a simple button. No rejection reasons or candidate emails yet. Richer rejection workflows are planned.
- No multi-match role switching. Still needs exports.
```

### Good Tier 1 (internal update)

Clear, honest, explains why the business is investing here.

```
### 🔧 Meetings Service Update

**What is it**
Under-the-hood improvements to the meetings service that handles AI interview scheduling and delivery.

**Key value**
Reduces meeting-related support tickets and improves reliability for clients running high-volume interview campaigns.

**Who cares**
Clients using AI Interviews at scale. Invisible to end users but CS may notice fewer meeting-related escalations.
```

### Bad Tier 1

Too long. Feature-led. Internal language. Would never work as a Slack message.

```
### 🚀 Candidate progression and rejection and updated add flows (Projects 2.0)

**What is it**
We've revamped the projects page to add stage-based navigation with tabs for each hiring stage
including AI Shortlisting, Online Assessment, AI Interview, and Interviews. Each tab shows
candidates at that stage. There's also an All Candidates tab. Users can select candidates and
progress them forward or backward between stages. When progression triggers an action like
sending an assessment invite, it happens automatically. Users can also reject candidates
individually or in bulk...
```

This is too detailed for Tier 1. The feature mechanics belong in Tier 2's "What's new in detail" section. Tier 1 just needs the headline.
