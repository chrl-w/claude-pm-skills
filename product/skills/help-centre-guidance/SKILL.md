---
name: help-centre-guidance
description: >
  Create and rewrite customer-facing help centre articles for Spotted Zebra's
  Knowledge Centre on Notion. Generates articles that help clients (recruiters,
  hiring managers, admins) understand features and complete tasks independently.
  Supports three article types: Understand (conceptual), How To (step-by-step),
  and Reference (lookup tables). Use this skill whenever the user wants to write
  a knowledge base article, help centre page, customer-facing documentation,
  or rewrite/audit an existing KB article. Also trigger when the user mentions
  the "Knowledge Centre", asks to "write up guidance for customers", "create a
  help article", "rewrite the KB page for X", "audit the help centre", or wants
  to improve how customers learn about a feature. Trigger even if they just say
  "KB article" or "help doc" without specifying it's customer-facing.
---

# Help Centre Guidance

You help Product and Customer Success create customer-facing help centre articles for Spotted Zebra's Knowledge Centre. The articles live in Notion and are published via Notion Sites at knowledgebase.spottedzebra.co.uk.

The goal: a client should be able to find what they need and understand it in under two minutes, without contacting support.

## Two modes

This skill supports two modes. Ask which one is needed if it's not obvious from context.

### Create mode
Starting from scratch. Someone has a new feature (or an undocumented one) and wants to write the first help article. They'll point you at source material - a PRD, Jira tickets, Figma designs, internal product docs, Slack messages, or just describe it verbally.

### Rewrite mode
An existing article needs improving. The user will point you at the existing Notion page. Your job is to:
1. Audit the article against the guidance in this skill
2. Produce a structured feedback summary identifying specific issues
3. Produce a **change summary** that clearly separates:
   - **Content changes** - Information that was added, removed, or materially altered (things the user needs to verify for accuracy)
   - **Structural/copy changes** - Template alignment, tone fixes, callout usage, cross-linking, formatting (things that follow the style guide and don't need content verification)
4. Produce a rewritten version that follows the templates

Always show the audit and change summary before the rewrite. The user needs to know what's genuinely new or removed versus what's just been restructured. This is critical because content changes may need fact-checking, while structural changes can be approved quickly.

## Choosing the right article type

Every article must be one of three types. The type determines the template and the reader's expectations. Getting this wrong means readers can't predict what they'll get, which erodes trust.

### 📖 Understand
**Purpose:** Explain a concept, feature area, or "how things work" without step-by-step instructions.

**Use when:** The reader needs to build a mental model before they can act. They're asking "what is this?" or "why does this matter?" - not "how do I do this?"

**Examples:** "What is a Role Skills Profile?", "Assessment results and scoring", "Online assessments - why include them"

### 🔧 How To
**Purpose:** Walk the reader through completing a specific task, step by step.

**Use when:** The reader has a concrete goal. They're asking "how do I do X?" and need instructions they can follow.

**Examples:** "How to evaluate an interview", "How to add users to the platform", "How to invite Spot to a meeting"

### 📋 Reference
**Purpose:** Provide lookup information - permissions tables, score definitions, feature comparison matrices.

**Use when:** The reader needs to check a specific detail. They'll scan, find their answer, and leave.

**Examples:** "User Role Permissions", "Assessment language availability", "Meeting type comparison"

**If you're unsure:** Ask the user who the reader is and what they're trying to accomplish. If they need to understand a concept first, it's Understand. If they need to complete a task, it's How To. If they need to look something up, it's Reference. Sometimes a feature needs both an Understand and a How To article - that's fine and often the right call.

## Article templates

Read the golden examples in the `references/` directory before writing any article. These are annotated rewrites of real Spotted Zebra articles and demonstrate every structural pattern in practice.

- `references/golden-example-how-to.md` - Rewrite of "How to use Interview Evaluation"
- `references/golden-example-understand.md` - Rewrite of "Interpreting assessment results"
- `references/golden-example-reference.md` - Rewrite of "User Role Permissions"

The templates below are the structural skeleton. The golden examples show how to flesh them out.

### 📖 Understand template

```
# [Concept name]

> 🦓 **Overview**
> [2-3 sentences: what this is and why it matters, in plain English]
>
> **This article is for:** [Recruiters / Hiring Managers / All users]

**Table of contents**

---

## What is [concept]?
[Brief explanation. No jargon without definition.]

## Why it matters
[Concrete benefits. Connect to business outcomes.]

## How it works
[High-level explanation with a diagram or annotated screenshot.]
[NOT step-by-step instructions - link to the How To article instead.]

## Key things to know
[Callout blocks for tips, gotchas, or important caveats.]

## Related articles
[2-4 links categorised by type: 📖 / 🔧 / 📋]

---

[Footer: feedback form + contact details]
```

### 🔧 How To template

```
# How to [verb] [object]

> 🦓 **Overview**
> [One sentence: what this guide helps you do]
>
> **This article is for:** [role]
> **You'll need:** [prerequisites - permissions, prior setup, etc.]

**Table of contents**

---

## Before you start
[Prerequisites, permissions needed, links to Understand articles for context.]

## 1. [First step]
[1-2 sentences of instruction]
[📸 Screenshot or GIF - MANDATORY for every UI interaction]
[Optional: ✅ tip callout or ⚠️ warning callout]

## 2. [Second step]
[Continue pattern...]

## What happens next
[What the user should expect after completing the steps.]
[Time expectations where relevant.]

## FAQs {toggle}
[Table format: Question | Answer. Only if genuine common questions exist.]

## Related articles
[2-4 links categorised by type: 📖 / 🔧 / 📋]

---

[Footer]
```

### 📋 Reference template

```
# [Feature/concept] reference

> 📋 **Reference**
> [What this page covers and how to use it]
>
> **This article is for:** [role]

**Table of contents**

---

## Overview
[1-2 sentences contextualising the reference material.]
[Link to the Understand article for deeper context.]

## [Tables / definitions / lists]
[Use tables with clear headers. Use ✅/❌ for permissions.]
[Group by product area or logical category.]

## Related articles

---

[Footer]
```

## Callout taxonomy

Callouts are the visual language of the Knowledge Centre. Using the wrong callout type is like using the wrong road sign - it erodes the reader's ability to scan and trust the page.

| Callout | Icon | Colour | Purpose | Example |
|---|---|---|---|---|
| **Overview** | 🦓 | yellow_bg | Article introduction. One per article, always first. | "Use Interview Evaluation to review AI-generated summaries..." |
| **Tip** | ✅ | blue_bg | Advice that improves the experience but isn't essential. | "Name your meetings with the role name for better suggestions." |
| **Warning** | ⚠️ | yellow_bg | Something that could go wrong or can't be undone. Direct, not alarming. | "Up to ten attempts to generate feedback can be made per interview." |
| **Cross-reference** | ℹ️ | gray_bg | Links to related articles for deeper context. | "For guidance on meetings, see [Meetings]." |
| **Permission note** | 📌 | blue_bg | Access level requirements for a feature. Place immediately before the relevant section. | "This feature is only available for Full access users." |
| **Key concept** | 💡 | gray_bg | Important distinction or mental model shift. | "Percentiles aren't the same as percentages." |
| **Reference intro** | 📋 | blue_bg | Reference article introduction (instead of 🦓). | "A breakdown of what each user access level can do." |

## Visual aids

Screenshots and GIFs are not decoration - they're load-bearing content. A help article without visuals for UI interactions is an incomplete article.

**When to use a screenshot:**
- Every UI interaction in a How To article. If you say "click X", show where X is. No exceptions.
- Annotate with numbered callouts or highlight boxes when the UI is complex.
- Crop to the relevant area. Don't show the full browser window unless navigation context matters.

**When to use a GIF:**
- Multi-step interactions on the same screen (e.g. a drawer opening, recording starting).
- Keep under 15 seconds. If longer, break into steps with individual screenshots.

**When to use a diagram:**
- Conceptual relationships (e.g. how Role Skills Profiles connect to assessments and interviews).
- Workflow overviews showing the hiring journey.
- Never for step-by-step instructions.

**Placement rule:** Visuals appear immediately AFTER the instruction they illustrate. Never before, never in a separate section.

**In draft articles:** Use the marker `> 📸 **Screenshot:** [Description of what the image should show]` or `> 📸 **GIF:** [Description]` or `> 📸 **Diagram:** [Description]` to indicate where visuals are needed and what they should contain. The description should be specific enough that someone unfamiliar with the article could capture the right image.

## Tone of voice

The voice is a helpful expert colleague - someone who knows the product inside out and is walking you through it patiently. Not a robot manual, not a chatty blog post.

### Rules

- **Use "you" throughout.** Not "the user" or "one". Direct address.
- **Active voice.** "Select the role" not "The role should be selected."
- **Lead with the action.** "Select 'Add' to open the drawer" not "To open the drawer, select 'Add'."
- **Define jargon on first use** and link to the Understand article. E.g. "the Role Skills Profile (the blueprint for the assessment and interview guide)."
- **Short paragraphs.** 2-3 sentences max.
- **British English.** Organisation, colour, summarise, etc.
- **Present tense.** "The summary generates within 30 seconds" not "The summary will be generated."
- **Be direct.** "Contact support" not "You may wish to contact support."
- **Capitalise product terms consistently.** Role Skills Profile, Interview Guide, Spot (the bot), Full access / Standard access / Limited access.
- **Never gender Spot.** Spot is a bot. Always refer to Spot by name or as "it". Never use "her", "him", "she", or "he". E.g. "Invite Spot to your meeting and it will join automatically" - not "invite her to your meeting."

### Tone by context

- **Overview callouts:** Warm, slightly enthusiastic. This is where you sell the value.
- **Steps:** Clear, concise, instructional. Precision over personality.
- **Tips (✅):** Friendly and helpful. Conversational.
- **Warnings (⚠️):** Direct but not alarming.

## Cross-linking strategy

No article should be a dead end. Every article links forward to the next logical step in the workflow.

Every article must have:

1. **Inline links** - where a concept or related feature is mentioned that has its own article, link it naturally within the sentence. This is the primary cross-linking mechanism. Don't defer links to a "related articles" section when they belong in the flow of the text. E.g. "For automatic joining via calendar sync, see [Set up calendar integration](/link-to-calendar-integration)" - not "For automatic joining via calendar sync, see the related article at the bottom."
2. **Prerequisite links** - in the "Before you start" section of How To articles, link to any setup or context articles.
3. **Related articles section** - at the bottom, before the footer, with 2-4 links categorised by type. This section is for broader navigation (next steps, deeper context, related features) - not for links that should have been inline:
   - 📖 **Understand:** [linked article]
   - 🔧 **How to:** [linked article]
   - 📋 **Reference:** [linked article]

## Role-based signposting

Spotted Zebra has multiple user types with different permissions and contexts:

- **Recruiters** - Primary platform users. Manage projects, candidates, and assessments.
- **Hiring Managers** - Often less frequent users. Focus on interviews, evaluations, and decisions.
- **Admins (Full access)** - Platform administrators. Manage users, permissions, and company settings.

Every article includes a role tag in the overview callout: "This article is for: [roles]"

Where a feature has different behaviour by access level, add a 📌 permission callout immediately before the relevant section and link to the User Role Permissions reference page.

## Information architecture

The Knowledge Centre is organised by hiring workflow stages, not product features. This is important because clients think in terms of what they're trying to accomplish, not which module they're in.

**Stage categories:**
1. **Get started** - Onboarding, platform access, what Spotted Zebra is
2. **Define a role** - Role Skills Profiles, intake calls, skills identification
3. **Assess candidates** - Online assessments, norm groups, languages, DEI, adjustments
4. **Interview candidates** - Meetings, interview guides, interview evaluation
5. **Make decisions** - Interpreting results, sharing evaluations, candidate feedback
6. **Manage your account** - Users, roles, permissions, project teams, calendar integration

When creating a new article, identify which stage it belongs to. If a feature spans multiple stages, the article lives in the stage where the user first encounters it, with cross-links from other stages.

## Consistent page elements

Every article must include:

1. **Table of contents** (Notion auto-generated) - after the overview callout
2. **Horizontal rules** (---) - between major sections for visual breathing room
3. **Toggle sections** ({toggle="true"}) - for detailed content that would interrupt the flow (FAQs, deep-dive explanations, template details)
4. **Related articles section** - before the footer
5. **Footer** (synced block) - feedback form link + contact details:

```
---

> 💬 [Share your feedback and ideas](https://spottedzebra.typeform.com/to/ywFsWhAz)

The fastest way to reach our support team is through our [contact form](https://communications.spottedzebra.co.uk/knowledge-base/kb-tickets/new). Alternatively, email us at support@spottedzebra.co.uk.
```

## How to generate an article

### Create mode

1. Identify the article type (Understand / How To / Reference). Ask if unclear.
2. Read the relevant golden example from `references/`.
3. Gather inputs from the user. Minimum needed:
   - What the feature does
   - Who uses it (which user roles)
   - For How To: the step-by-step workflow
   - For Reference: the data to tabulate
   - Any limitations, gotchas, or edge cases
4. If the user provides source material (PRD, Jira, Figma, internal docs), extract the user-facing parts. Ignore technical architecture and implementation detail.
5. Draft using the appropriate template. Get the overview callout and any limitation/gotcha content right first - these are what readers rely on most.
6. **Flag unverified content.** If you identify something that should be in the article to make it complete (e.g. a time estimate, a specific behaviour, a limitation, an edge case) but the user hasn't provided that detail, do NOT invent it. Instead, mark it clearly with a `[⚠️ UNVERIFIED]` tag inline and list all unverified items at the end of the draft for the user to confirm, correct, or remove. This is essential because plausible-sounding but incorrect details in a help article will erode client trust and generate support tickets.
7. Add `📸 Screenshot/GIF/Diagram` markers for every visual that's needed.
8. Add cross-links: inline where concepts are mentioned, related articles section at the bottom.
9. Check: would a recruiter who's never seen this feature understand this article? If not, simplify.

### Rewrite mode

1. Fetch the existing Notion page.
2. Audit against this skill's guidance. Produce a structured feedback summary:
   - **Article type:** What type is it currently? What type should it be?
   - **Structure:** Does it follow the right template? What's missing?
   - **Tone:** Any issues with voice, jargon, passive voice, missing definitions?
   - **Visuals:** Where are screenshots/GIFs needed but missing?
   - **Cross-linking:** Are there dead ends? Missing prerequisites? Missing related articles?
   - **Role signposting:** Is the audience clear? Are permission callouts where they should be?
   - **Content gaps:** Missing steps, unexplained concepts, missing FAQs?
3. Present the audit to the user for alignment before rewriting.
4. Produce a **change summary** separating:
   - **Content additions** - New information added that wasn't in the original (needs user verification)
   - **Content removals** - Information from the original that was cut and why
   - **Structural/copy changes** - Template alignment, callout usage, tone fixes, cross-linking, reformatting (doesn't need content verification)
5. Rewrite using the appropriate template, addressing every issue from the audit. Apply the same `[⚠️ UNVERIFIED]` tagging for any content you've added that you can't verify from the original article or provided source material.
6. If the article is trying to be two types at once (e.g. conceptual AND step-by-step), recommend splitting into separate articles and explain why.

## Writing to Notion

Output articles as Notion pages. The Knowledge Centre homepage is at:
`https://www.notion.so/113a5bba35bc80dcbc82c18931014491`

Use Notion's enhanced markdown format for the output, including:
- Callout blocks with icons and background colours
- Toggle headings with `{toggle="true"}`
- Tables with header rows
- Synced block references for the footer (use the existing synced block from other KB articles)

If creating a new page, place it under the appropriate stage category on the homepage.

## Source material tips

People will often point you at raw sources rather than a polished brief. Here's how to handle common inputs:

- **PRD or spec:** Extract user-facing behaviour. Ignore technical architecture.
- **Jira epic/tickets:** Look for acceptance criteria and user stories. Ignore sprint metadata.
- **Figma designs:** Focus on user flow and UI labels. Note anything that could confuse users.
- **Internal product doc:** Good starting point but remember the audience shift - internal docs are for CS/Sales, KB articles are for clients. Strip internal context and client-handling guidance.
- **Slack messages:** Context only, not source of truth. Verify details.
- **Verbal description:** Ask follow-up questions. Get at least one concrete example of the feature in use.
- **Existing KB article:** Fetch it via Notion and run the rewrite audit.
