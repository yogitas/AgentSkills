# 📖 Agile User Story Writer — SKILL.md

**Author:** [Your Name / LinkedIn Handle]
**Version:** 1.1.0
**Repository:** https://github.com/yogitas/AgentSkills
**License:** MIT

---

## 🎯 What This Skill Does

This skill guides an AI agent to write **well-structured Agile User Stories** in a consistent,
PO-friendly format. Designed for **Product Owners, Agile Coaches, and Product Managers** who
want discussion-ready stories fast.

When a **Jira MCP server is configured**, the skill pushes the completed story **directly to
your Jira project** — no copy-paste needed.

---

## ✅ When To Trigger This Skill

Trigger this skill when any of the following are true:

- The user says: *"write a user story"*, *"create a ticket"*, *"draft a Jira story"*, *"write an Agile story"*
- The user describes a feature or user need and wants it structured
- The user provides example stories and asks for more in the same style
- The user asks to *"push a story to Jira"*

---

## 📐 User Story Format

Every story produced by this skill **must follow this exact structure**:

---

### [STORY TITLE]
> Short, descriptive title (e.g., *"User can reset password via email"*)

---

### Motivation

**As** [persona], **I want to** [goal] **so that** [benefit].

> 💡 *Tip for POs: Persona = a real user role. Benefit = business or user value, not technical detail.*

---

### Relevant Information

Context bullets for developers and designers:

- 🎨 **Design references** — Figma/Zeplin links, design system components
- 🔗 **APIs / Interfaces** — Existing endpoints or third-party services to use
- 📋 **Business rules** — Constraints or policies that apply
- 📁 **Related tickets** — Parent epics, dependencies, related stories
- 📊 **Data / analytics** — Tracking events or reporting considerations
- ⚙️ **Technical notes** — Relevant architectural decisions or patterns to follow

> 💡 *Tip for POs: Even partial info here saves time in refinement. Mark unknowns as `[TBD]`.*

---

### Open Questions

Questions to spark discussion at the **refinement meeting**:

- ❓ [Edge case or user flow question]
- ❓ [Design or UX decision question]
- ❓ [Scope boundary question]
- ❓ [Data, permissions, or state question]
- ❓ [Technical approach or constraint question]

> 💡 *Tip for POs: Share these before refinement so your team comes prepared.*

---

### Acceptance Criteria

Draft AC from the **user's perspective** — update and finalise during refinement:

- [ ] **AC1:** Given [context], when [action], then [outcome]
- [ ] **AC2:** Given [context], when [action], then [outcome]
- [ ] **AC3:** [User-facing observable behaviour]
- [ ] **AC4:** [Edge case or error state the user would experience]

> 💡 *Tip for POs: AC must be testable and user-focused — never describe implementation.*

---

### Out of Scope

What is explicitly **NOT** in this story:

- ❌ [Feature or behaviour excluded]
- ❌ [Related functionality deferred to a later story]
- ❌ [Technical work belonging in a separate ticket]

---

## ⚙️ Configuration Guide for POs

> 📌 **Where to paste this config — pick whichever matches how you use Claude:**
>
> - **Claude.ai (simplest):** Go to **Settings → Custom Instructions** → paste into the *"How should Claude respond?"* box. Done. No installs needed.
> - **Claude Projects:** Open your Project → **Instructions** tab → paste there. All chats inside that project will use it automatically.
> - **Claude API / developer setup:** Paste into your `system` prompt field.
>
> A single paste is all it takes. No code, no installs required.

Paste the `USER_CONFIG` block below into your chosen location, then fill in your project details:

```yaml
# ─────────────────────────────────────────────────────────────
# USER STORY SKILL — PROJECT CONFIGURATION
# Paste into Claude Custom Instructions / Project Instructions
# and customise the values below for your product
# ─────────────────────────────────────────────────────────────

project:
  name: "My Product Name"           # e.g., "PayFlow Mobile App"
  domain: "fintech / e-commerce / healthcare / SaaS / ..."
  team_size: "5 devs, 1 designer"   # helps agent calibrate detail level

personas:
  # Define the real user roles for your product.
  # The agent uses these when writing "As a [persona]..."
  - name: "Registered User"
    description: "A logged-in customer who has completed onboarding"
  - name: "Admin"
    description: "An internal team member managing the platform"
  - name: "Guest User"
    description: "An unauthenticated visitor browsing the product"
  # ➕ Add your own personas — see references/personas/persona-templates.md

design_references:
  figma_base_url: "https://www.figma.com/file/YOUR_FILE_ID"
  design_system: "Material UI v5 / Tailwind / Custom — [add link]"
  component_library: "[Storybook or component docs link]"

jira:
  enabled: false                         # Set to true once Jira MCP is configured
                                         # See references/jira/jira-setup-guide.md
  project_key: "PROJ"                    # e.g., "PAY", "SHOP", "CORE"
  issue_type: "Story"                    # "Story" or "User Story"
  default_epic_link: ""                  # Optional: Epic to link new stories to
  story_points_field: "customfield_10016" # Check your Jira instance for the right ID
  labels: ["ai-generated", "needs-refinement"]

examples:
  # ── YOUR EXAMPLES GO HERE ────────────────────────────────────
  # Replace these with 2–3 real stories from your own product.
  # The more specific your examples, the better the agent will
  # match your team's language and style.
  # See references/examples/ for domain-specific starter configs.
  # ─────────────────────────────────────────────────────────────

  - title: "User can filter products by category"
    motivation: >
      As a registered user, I want to filter products by category
      so that I can find relevant items faster without scrolling
      through the full catalogue.
    relevant_info:
      - "Design: Figma — Product Listing Page > Filter Panel"
      - "API: GET /v2/products?category={id} supports the category param"
      - "Categories returned by GET /v1/categories"
      - "Related epic: PROJ-42 — Product Discovery"
    open_questions:
      - "Should multiple categories be selectable (multi-select)?"
      - "Do we show result counts per category before filtering?"
      - "Empty state design when a category has 0 results?"
    acceptance_criteria:
      - "Given I am on the listing page, when I select a category, then only products in that category are shown"
      - "Given a category is selected, when I clear the filter, then all products reappear"
      - "Given I am on mobile, when I open the filter, then it opens as a bottom sheet"
    out_of_scope:
      - "Price range filtering (PROJ-58)"
      - "Saving filter preferences across sessions"
      - "Backend taxonomy changes"

  - title: "Admin can export user list as CSV"
    motivation: >
      As an admin, I want to export the user list as a CSV
      so that I can analyse user data in external tools without
      needing database access.
    relevant_info:
      - "Design: Admin Portal > Users — export button mocked in Figma"
      - "Max export: 10,000 rows (confirmed with backend)"
      - "Fields: user_id, email, created_at, last_login, plan_type"
      - "Related epic: PROJ-71 — Admin User Management"
    open_questions:
      - "Should soft-deleted users be included in the export?"
      - "Do we need to log exports for GDPR audit purposes?"
      - "Support filtered exports (e.g., Pro plan users only)?"
    acceptance_criteria:
      - "Given I am on the admin users page, when I click 'Export CSV', then a CSV file downloads to my device"
      - "Given active filters are applied, when I export, then only filtered users are included"
      - "Given export exceeds 10,000 rows, when I trigger it, then I see an error explaining the limit"
    out_of_scope:
      - "Excel (.xlsx) format"
      - "Scheduled / automated exports"
      - "Exporting other entity types (orders, payments)"
```

---

## 🤖 Agent Behaviour Instructions

When this skill is activated, follow these **4 steps in order**:

### Step 1 — Gather Input

Ask the user for:
1. A brief description of the feature or need (1–3 sentences is enough)
2. The primary persona (or use `USER_CONFIG.personas`)
3. Known design links, API details, or constraints

If input is minimal, make reasonable assumptions and **clearly label them** as
`[Assumption — PO to validate]`.

### Step 2 — Generate the User Story

Write the full story using the format above. Rules:

- **Motivation:** Always strictly follow `As [persona], I want to [goal] so that [benefit]` — no variations
- **Relevant Information:** Use user input + `USER_CONFIG.design_references`. Unknown items → `[TBD — PO to confirm]`
- **Open Questions:** Generate 4–6 meaningful questions covering edge cases, UX decisions, data/permissions, and scope
- **Acceptance Criteria:** Write 4–6 AC in Given/When/Then. User perspective only — no implementation details
- **Out of Scope:** List at least 2–3 explicit exclusions

### Step 3 — Confirm With User

Display the complete story and ask:
*"Does this look good? Any changes before I push to Jira?"*

Apply any requested edits, then re-confirm before proceeding.

### Step 4 — Push to Jira (if MCP configured)

**Only if `jira.enabled: true` AND a Jira MCP server is connected.**

```
MCP Tool: jira_create_issue
Parameters:
  project:       USER_CONFIG.jira.project_key
  summary:       [Story Title]
  issue_type:    USER_CONFIG.jira.issue_type
  description:   [Full story in Jira markdown / ADF format]
  labels:        USER_CONFIG.jira.labels
  epic_link:     USER_CONFIG.jira.default_epic_link  (if set)
```

**Jira description formatting:**
- `h3.` for section headers (Motivation, Relevant Information, etc.)
- `*` for bullet points
- `[ ]` for AC checkboxes
- Wrap the Motivation statement in a `{info}` panel macro for visibility

Return the created Jira issue URL to the user.

**If Jira MCP is NOT configured:** Skip this step. Display the story as
copyable Markdown and remind the user to check `references/jira/jira-setup-guide.md`
when they are ready to enable the Jira push.

---

## 🔄 Changelog

| Version | Date     | Notes                                                                 |
|---------|----------|-----------------------------------------------------------------------|
| 1.1.0   | 2026-03  | Added USER_CONFIG paste instructions for non-technical POs            |
| 1.0.0   | 2026-03  | Initial release — story format, Jira MCP push, configurable examples |

---

## 🤝 Contributing

👉 **https://github.com/yogitas/AgentSkills**

PRs welcome! Share your domain-specific `USER_CONFIG` examples by adding a
file to the `references/examples/` folder.

---

*Built with ❤️ for the Agile community. Give it a ⭐ if it helps your team!*
