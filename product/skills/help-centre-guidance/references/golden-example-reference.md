# Golden Example: Reference Article

**Source article:** "User Role Permissions"
**Article type:** 📋 Reference
**What this example demonstrates:** Reference table structure, contextual overview linking to Understand articles, grouped tables with clear headers, permission notation conventions, minimal prose (this is a lookup page, not a reading page).

---

## ANNOTATIONS (remove before publishing)

> Each annotation explains a structural or tone choice. These are for the skill's reference files, not for the published article.

---

## The Rewritten Article

<!-- ANNOTATION: Reference article titles are descriptive nouns. No "How to" prefix. This is a page people bookmark and return to. -->

# User role permissions

<!-- ANNOTATION: Reference articles use a 📋 blue callout (not the 🦓 yellow used for other types). This signals "this is a lookup page" to returning users. The overview briefly contextualises the tables and links to the Understand article for anyone who needs the deeper explanation. -->

> 📋 **Reference**
> A breakdown of what each user access level can do across every product area in Spotted Zebra. Use this page to check whether a specific action is available for your access level, or to understand what access to grant new users.
>
> **This article is for:** Admins, Recruiters, and anyone managing platform access

**Table of contents**

---

<!-- ANNOTATION: Short contextual overview. Two jobs: (1) orient the reader, (2) link to the Understand article for deeper context. Reference articles should NOT try to explain concepts - that's what Understand articles are for. -->

## Overview

Spotted Zebra has three user access levels: **Full access**, **Standard access**, and **Limited access**. Each level determines what a user can view, create, and edit across the platform.

Access levels are set when a user is invited and can be changed by Full access users.

> ℹ️ For guidance on what each role is designed for and how to choose the right one, see [User roles, the project team, and assignees](/link-to-user-roles-article).

> ℹ️ To add or manage users, see [How to get access to the Spotted Zebra platform and add users](/link-to-add-users).

---

<!-- ANNOTATION: Tables are grouped by product area, matching the platform's navigation. Each section has a coloured H1 heading for scannability. Tables use ✅/❌ consistently - no mixing with "Yes"/"No" text. Header row is always present. Conditional permissions use a short inline explanation rather than footnotes. -->

## General

| Feature | Full access | Standard access | Limited access |
|---|---|---|---|
| **Invite new users** | ✅ | ✅ (Standard + Limited only) | ❌ |
| **View candidate upload history** | ✅ | ❌ | ❌ |
| **Bulk invite candidates across projects** | ✅ | ❌ | ❌ |

---

## Roles

| Feature | Full access | Standard access | Limited access |
|---|---|---|---|
| **Create new roles** | ✅ | ✅ | ❌ |
| **View all roles** | ✅ | ❌ | ❌ |
| **View roles they are collaborators of** | ✅ | ✅ | ✅ |
| **Edit and confirm roles they are collaborators of** | ✅ | ✅ | ✅ |
| **Create and configure a new project from a role** | ✅ | ✅ | ❌ |

---

## Projects

| Feature | Full access | Standard access | Limited access |
|---|---|---|---|
| **View all projects** | ✅ | ❌ | ❌ |
| **View projects they are team members of** | ✅ | ✅ | ✅ |
| **Edit project settings (as team member)** | ✅ | ✅ | ❌ |
| **Add users to the project team** | ✅ | ✅ | ❌ |
| **Create a new project from a role** | ✅ | ✅ | ❌ |
| **Access draft projects from Role Kick Off** | ✅ | ✅ | ❌ |

---

## Candidates

| Feature | Full access | Standard access | Limited access |
|---|---|---|---|
| **View all candidates** | ✅ | ❌ | ❌ |
| **View unassigned candidates** | ✅ | ✅ | ✅ |
| **View assigned candidates** | ✅ | ✅ (if assigned) | ✅ (if assigned) |
| **Manage candidate assignees** | ✅ | ❌ | ❌ |
| **Invite individual candidates** | ✅ | ✅ | ❌ |
| **Bulk invite candidates to a single project** | ✅ | ✅ | ❌ |
| **Edit candidates (reset, delete, etc.)** | ✅ | ✅ | ❌ |
| **Progress or reject candidates** | ✅ | ✅ | ❌ |

---

## Interview Guides

| Feature | Full access | Standard access | Limited access |
|---|---|---|---|
| **View Interview Guide Blueprint** | ✅ (all) | ✅ (accessible projects) | ✅ |
| **Edit Interview Guide Blueprint** | ✅ (all) | ✅ (accessible projects) | ❌ |
| **View candidate Interview Guides** | ✅ (all) | ✅ (accessible candidates) | ✅ (accessible candidates) |
| **Edit candidate Interview Guides** | ✅ (all) | ✅ (accessible candidates) | ✅ (accessible candidates) |

---

## Meetings

<!-- ANNOTATION: Where permissions differ by context (evaluator vs. non-evaluator), we split into separate rows rather than using complex conditional text in a single cell. Easier to scan. -->

| Feature | Full access | Standard access | Limited access |
|---|---|---|---|
| **View intakes and general meetings (not an attendee)** | ❌ | ❌ | ❌ |
| **Change interview type (as evaluator)** | ✅ | ✅ (unless evaluation submitted) | ✅ (unless evaluation submitted) |
| **Change interview type (not an evaluator)** | ✅ | ❌ | ❌ |
| **Change intake type** | ✅ | ✅ | ✅ |
| **Change general meeting type** | ✅ | ✅ | ✅ |

---

## Interviews

| Feature | Full access | Standard access | Limited access |
|---|---|---|---|
| **View all interviews (company-wide)** | ✅ | ❌ | ❌ |
| **View interviews linked to projects (as team member)** | ✅ | ✅ | ✅ |
| **View interviews linked to projects (not a team member)** | ✅ | ✅ (if evaluator) | ✅ (if evaluator) |
| **View interviews (unassigned candidates)** | ✅ | ✅ | ✅ |
| **View interviews (assigned candidates)** | ✅ | ✅ (if assigned or evaluator) | ✅ (if assigned or evaluator) |
| **Evaluate interviews (as evaluator)** | ✅ | ✅ | ✅ |
| **View interview results** | ✅ | ✅ (after submitting evaluation) | ✅ (after submitting evaluation) |
| **Link interview to project/candidate/stage** | ✅ | ✅ | ✅ |
| **Re-link interview (as evaluator)** | ✅ | ✅ (unless evaluation submitted) | ✅ (unless evaluation submitted) |
| **Re-link interview (not an evaluator)** | ✅ | ❌ | ❌ |

---

<!-- ANNOTATION: Quick-reference summary for the most common question: "which role should I give this person?" This wasn't in the original article and it's the #1 thing people are actually looking for when they land on this page. -->

## Quick guide: Which access level to assign

| User type | Recommended access | Why |
|---|---|---|
| **TA Lead / Admin** | Full access | Needs visibility across all projects, candidates, and interviews. Can invite users and manage assignees. |
| **Recruiter** | Standard access | Can create roles and projects, invite candidates, and manage the hiring process for projects they're part of. |
| **Hiring Manager / Interviewer** | Limited access | Can view and evaluate interviews for candidates and projects they're assigned to. Cannot make structural changes. |

> ℹ️ Access levels can be changed after a user is invited. Only Full access users can change another user's access level.

---

<!-- ANNOTATION: Related articles. Reference pages are natural "hub" pages so the links here tend to be action-oriented - "now that you know what's possible, here's how to do it." -->

## Related articles

- 📖 **Understand:** [User roles, the project team, and assignees](/link-to-user-roles) - What each role is designed for and how project teams work
- 🔧 **How to:** [Get access to the platform and add users](/link-to-add-users) - Invite new users and manage access
- 🔧 **How to:** [Evaluate an interview](/link-to-interview-evaluation) - Use skills evaluation, scoring, and feedback

---

> 💬 [Share your feedback and ideas](https://spottedzebra.typeform.com/to/ywFsWhAz)

The fastest way to reach our support team is through our [contact form](https://communications.spottedzebra.co.uk/knowledge-base/kb-tickets/new). Alternatively, email us at support@spottedzebra.co.uk.
