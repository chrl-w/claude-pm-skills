---
description: Name and parameterise a Heap analytics event following the Spotted Zebra taxonomy
argument-hint: "<describe the user action to track>"
---

# Name Event

Name a Heap analytics event for Spotted Zebra's product.

## Workflow

### 1. Fetch the taxonomy

Before anything else, fetch the latest taxonomy from Notion:

**Notion page:** `310a5bba35bc80ef859dcf96220f8fd5` (Jobs Governance > Analytics)

Use the `notion-fetch` tool with this page ID to get the current controlled lists for domains, actions, and parameters. If the Notion tool is unavailable, fall back to the reference in the `heap-event-naming` skill.

### 2. Understand the action

If the user provided an argument, use it. Otherwise ask: "What user action do you want to track?"

Accept any of:
- A specific interaction ("user clicks the filter for role match on the pipeline")
- A feature area ("we need tracking for the new bulk invite flow")
- A vague description ("track something when they use the calendar sync")

If the description is ambiguous, ask one focused clarifying question. Don't over-ask — make a recommendation and let the user correct it.

### 3. Apply the taxonomy

Follow the 6-step process from the `heap-event-naming` skill:

1. **Pick the domain** — entity ownership, not navigation location
2. **Identify the object** — descriptive enough to understand without reading params
3. **Pick the action** — prefer existing actions, propose new ones if genuinely needed
4. **Check for reuse** — could an existing event cover this with different params?
5. **Add parameters** — standard params first, then contextual
6. **Sanity check** — would this survive a UI reshuffle?

### 4. Present the result

Show the event in this format:

```
Event name: {domain}-{object}-{action}
Parameters:
  - paramName: "example value"
  - paramName: "example value"
```

Briefly explain why you chose the domain (one sentence) and flag any assumptions made.

### 5. Handle new actions or domains

If you proposed a new action and the user approved it, update the Notion taxonomy page using `notion-update-page` to add the new action to the Actions table. This keeps the controlled list current for all squads.

If the feature doesn't fit any existing domain, flag it clearly — new domains need Product approval.
