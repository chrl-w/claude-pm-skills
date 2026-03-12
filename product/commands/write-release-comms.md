---
description: Create a feature release update for commercial teams (CS and Sales)
argument-hint: "<feature name or description>"
---

# Write Release Comms

Create a release update for the Upcoming Feature Releases database in Notion. See the **upcoming-releases** skill for the full format, writing principles, and examples.

## Workflow

### 1. Gather Context

Search connected tools for information about the feature:

**Jira** (cloud ID: `0a01a553-0bb8-4ac1-943d-eb9a2535647e`):
- Search for the feature's epic or tickets. Project prefixes: IC (Indigo), CR (Crimson), YL (Yellow), BL (Blue), BK (Black).
- Pull scope, acceptance criteria, and status.

**Notion**:
- Check the Upcoming Feature Releases database for existing entries to avoid duplicates.
- Search for related PRDs or design docs.

**Slack**:
- Search #product-new-releases and #pde-and-commercial for prior discussion.

**Local files** (`/Users/charlie_watkinson/brain`):
- Search for PRDs, one-pagers, or notes related to the feature.
- Check `/Users/charlie_watkinson/brain/Granola` for recent meeting notes with relevant product decisions or scope discussions.

**Figma**:
- If the user provides a Figma URL, pull design context or screenshots to inform the update.

If tools aren't connected or searches return nothing, move on.

### 2. Determine the Variant

Ask the user (if not obvious from context):
- **🚀 Feature update**: Customer-facing change. Needs customer-friendly name, value framing, and "Who cares" targeting.
- **🔧 Internal/infrastructure update**: Behind-the-scenes improvement. Needs honest framing of why the business is investing here.

### 3. Collect Missing Context

The minimum needed:
- What does the feature do?
- Who is it for?
- Any critical limitations or things CS shouldn't promise?

Don't block on perfection. Everything else can be inferred or added later.

### 4. Draft Tier 1

Draft the Tier 1 (Visibility) section first. This is the priority. It must be scannable in 10 seconds and work as a Slack message.

Follow the writing principles in the **upcoming-releases** skill: customer-facing language, value-led, scannable, direct about limitations.

### 5. Offer Tier 2

Ask if the user wants Tier 2 enablement detail. This is typically needed for complex features where CS needs deeper context for demos, onboarding, or objection handling. Internal updates rarely need it.

### 6. Write to Notion

Create a page in the Upcoming Feature Releases database.

**Data source ID:** `collection://2ee8a21e-848a-4fb7-ba5d-60e48071534a`

Set properties:
- **Feature name**: Customer-facing name (or descriptive name for internal updates)
- **tl'dr**: 1-2 line summary matching the "What is it" section
- **Status**: One of `Coming up 🙏`, `In Development`, `Shipping Soon 👀`, `Shipped 🚀`
- **Target timeline**: e.g. "Late March", "Q2 2026"
- **Squad**: `Indigo`, `Crimson`, `Yellow`, or `Blue` (mapped from Jira project keys)

### 7. Offer Slack Distribution

Offer to post the Tier 1 content to #pde-and-commercial (C04K6U03HJ6) with a link to the Notion page. Always show the draft and get confirmation before sending.

## Tips

- If the PM gives you an internal feature name, suggest a cleaner customer-facing alternative.
- "Key things to know" should be honest. CS would rather know the boundary upfront than get caught out.
- Only mention planned improvements if they're reasonably certain. If in doubt, leave it out.
- Keep the whole Tier 1 to a single screen. If it's too long for Slack, it's too long.
