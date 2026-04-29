---
description: Create or update internal product documentation in the Product guidance Notion database
argument-hint: "<feature name or 'update [page name]'>"
---

# Product Doc

Create or update a product guidance doc for internal teams (CS, Sales, PMs). See the **product-docs** skill for the full format, writing principles, Notion schema, and examples.

## Workflow

### 1. Determine mode

If the user's argument starts with "update" or they mention an existing doc, use **update mode**. Otherwise use **create mode**.

- **Create mode**: New doc from scratch. Expect source material (Jira, Figma, verbal description).
- **Update mode**: Revise an existing doc after a feature change. Expect a pointer to the Notion page + what changed.

### 2. Gather context

**Create mode:**
Ask for source material if not already provided. The minimum you need:
- What does the feature do?
- Who is it for?
- Any limitations or things CS should know?

Accept Jira tickets, Figma links, PRDs, Slack threads, or verbal descriptions. Follow the source material tips in the **product-docs** skill.

**Update mode:**
Fetch the existing page from the Product guidance database (ID: `58fa11361cc641e592f85de1ff53eea4`) using Notion tools. Understand what changed from the user's input.

### 3. Draft the doc

Follow the **product-docs** skill format:
- 5 core sections: Overview, Who uses it and when, How it works, Limitations and gotchas, Common questions
- Optional sections only if they earn their place: Key terms, Demo tips, What changed, Related docs
- Apply the writing principles (CS-first, benefit-led, honest limitations, scannable)

### 4. Review with the PM

Share the draft for feedback. Iterate until the PM is happy.

### 5. Publish to Notion

Save to the **Product guidance** database using Notion tools.

Set properties per the **product-docs** skill schema:
- Name, Description, Product Area, Tags, Status, Squad, Last verified
- Create mode: Status = "Draft"
- Update mode: Status = "Current", Last verified = today
