---
description: Create or rewrite a customer-facing Knowledge Centre article
argument-hint: "<feature name or 'rewrite [page URL/name]'>"
---

# Help Centre Article

Create or rewrite a customer-facing help centre article for Spotted Zebra's Knowledge Centre. See the **help-centre-guidance** skill for the full format, article types, callout taxonomy, tone rules, and golden examples.

## Workflow

### 1. Determine mode

If the user's argument starts with "rewrite" or "audit" or they mention an existing article/page, use **rewrite mode**. Otherwise use **create mode**.

- **Create mode**: New article from scratch. Expect source material (PRD, Jira, Figma, internal docs, verbal description).
- **Rewrite mode**: Audit and rewrite an existing article. Expect a pointer to the Notion page.

### 2. Determine article type

Every article is one of three types:

- **📖 Understand** - Conceptual. "What is X?" / "Why does X matter?"
- **🔧 How To** - Step-by-step. "How do I do X?"
- **📋 Reference** - Lookup tables. Permissions, score definitions, comparisons.

If unclear, ask. Sometimes a feature needs both an Understand and a How To - that's fine.

### 3. Gather context

Read the golden examples from the skill's `references/` directory before drafting. Then:

**Create mode:**
- What the feature does
- Who uses it (Recruiters / Hiring Managers / Admins)
- The step-by-step workflow (for How To) or data to tabulate (for Reference)
- Limitations, gotchas, edge cases

**Rewrite mode:**
- Fetch the existing Notion page
- Run the structured audit
- Present audit + change summary before rewriting

### 4. Draft and review

Follow the skill's generation instructions for the chosen mode. Flag any unverified content with `[⚠️ UNVERIFIED]`. Present to the user for review.

### 5. Publish

Once approved, create or update the Notion page under the appropriate stage category in the Knowledge Centre.
