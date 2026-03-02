# 📖 Agile User Story Writer

An AI skill that writes **well-structured, refinement-ready Agile User Stories** in seconds.
Designed for **Product Owners, Agile Coaches, and Product Managers** who want consistent,
discussion-ready stories without the blank-page problem.

Works with **GitHub Copilot, Claude, ChatGPT**, and any AI agent that supports custom instructions.
Optional **Jira MCP integration** pushes the finished story directly to your board — no copy-paste needed.

---

## 🗂️ Files in This Folder

```
agile-user-story/
├── README.md          ← You are here — setup and usage guide
├── SKILL.md           ← The skill itself — load this into your AI agent
└── references/
    ├── README.md               ← Guide to the references folder
    ├── examples/               ← Ready-made USER_CONFIG blocks by product domain
    │   ├── example-ecommerce.yaml
    │   ├── example-saas.yaml
    │   └── example-fintech.yaml
    ├── personas/
    │   └── persona-templates.md    ← Reusable persona definitions
    ├── acceptance-criteria/
    │   └── ac-patterns.md          ← AC writing patterns by story type
    └── jira/
        └── jira-setup-guide.md     ← Step-by-step Jira MCP setup
```

---

## 📋 What the Skill Produces

Every story follows this fixed structure so your whole team gets a consistent format:

| Section | What it contains |
|---|---|
| **Story Title** | Short, verb-led title — e.g., *"User can filter products by price range"* |
| **Motivation** | Strict `As [persona], I want to [goal] so that [benefit]` format |
| **Relevant Information** | Design links, API details, business rules, related tickets, analytics notes |
| **Open Questions** | 4–6 edge-case and UX questions ready to paste into your refinement invite |
| **Acceptance Criteria** | 4–6 Given/When/Then criteria, user-perspective only, formatted as checkboxes |
| **Out of Scope** | At least 3 explicit exclusions to prevent scope creep |

---

## ⚡ Setup in 3 Steps

### Step 1 — Pick a starter config

Open [`references/examples/`](references/examples/) and choose the file closest to your product domain:

| File | Best for |
|---|---|
| [`example-ecommerce.yaml`](references/examples/example-ecommerce.yaml) | Retail, marketplace, shopping apps |
| [`example-saas.yaml`](references/examples/example-saas.yaml) | B2B SaaS, dashboards, internal tools |
| [`example-fintech.yaml`](references/examples/example-fintech.yaml) | Payments, banking, financial services |

Copy the `USER_CONFIG` YAML block from your chosen file.

---

### Step 2 — Customise the config

Open the copied YAML and update these fields:

```yaml
project:
  name: "Your Product Name"      # ← Change this
  domain: "e-commerce"           # ← Change to your domain
  team_size: "4 devs, 1 designer" # ← Helps the agent calibrate detail

personas:
  - name: "Shopper"              # ← Replace with your real user roles
    description: "A logged-in customer browsing products"

design_references:
  figma_base_url: "https://www.figma.com/file/YOUR_ID"  # ← Your Figma link
  design_system: "Material UI v5"                        # ← Your design system

examples:                        # ← MOST IMPORTANT: replace with 2–3 real stories
  - title: "Your real story title"    # from your own product backlog
    motivation: >
      As a [persona], I want to [goal] so that [benefit].
    acceptance_criteria:
      - "Given ..., when ..., then ..."
```

> 💡 **The `examples` section has the biggest impact on quality.** The more your examples reflect your
> product's real language, personas, and story style, the better every generated story will be.
> See [`references/personas/persona-templates.md`](references/personas/persona-templates.md) for
> reusable persona definitions and [`references/acceptance-criteria/ac-patterns.md`](references/acceptance-criteria/ac-patterns.md) for AC patterns.

---

### Step 3 — Load the skill into your agent

You need to give your agent **two things**: the `SKILL.md` content (the agent instructions) **and** your customised `USER_CONFIG` block. The simplest approach is to combine them into one paste.

#### GitHub Copilot (VS Code) — Recommended for teams

**Option A: Repo-level** *(best — version-controlled, shared with the whole team)*

1. Create `.github/copilot-instructions.md` in your repository root
2. Paste the full contents of `SKILL.md` into it
3. Append your customised `USER_CONFIG` YAML block at the bottom
4. Commit and push — every team member instantly gets the same setup

**Option B: User-level** *(applies to all repos on your machine)*

1. Open VS Code Settings (`Ctrl+,`)
2. Search for `github.copilot.chat.codeGeneration.instructions`
3. Click **Edit in settings.json** and add:

```json
"github.copilot.chat.codeGeneration.instructions": [
  {
    "file": ".github/copilot-instructions.md"
  }
]
```

Then start a Copilot Chat with `Ctrl+Alt+I` and type your prompt.

---

#### Claude.ai

1. Go to **Settings → Custom Instructions**
2. Paste the full `SKILL.md` content into *"How should Claude respond?"*
3. Append your `USER_CONFIG` block directly below it
4. Save — applies to every new conversation

---

#### Claude Projects *(best for Claude — shared with your squad)*

1. Open your Project → **Instructions** tab
2. Paste `SKILL.md` + your `USER_CONFIG` block there
3. Every chat inside the project inherits the config automatically

---

#### ChatGPT

1. Go to **Settings → Personalization → Custom Instructions**
2. Paste `SKILL.md` + your `USER_CONFIG` into the *"How would you like ChatGPT to respond?"* field
3. Save — applies to all new conversations

---

#### Any Agent API

Pass the `SKILL.md` content + your `USER_CONFIG` as the `system` prompt before any user message.

---

## 💬 How to Use It

Once configured, just describe the feature in plain language. Trigger phrases the skill recognises:

- *"Write a user story for: [feature description]"*
- *"Create a ticket for: [user need]"*
- *"Draft an Agile story about: [feature]"*
- *"Write a Jira story for: [feature]"*

**Example prompts:**

```
Write a user story for: shoppers want to filter products by price range
```
```
Draft a user story — as an admin I need to bulk-deactivate user accounts
```
```
Create a ticket for: users should get an email when their order ships
```

The agent will ask for any missing details, then produce the full structured story. You review it, request any edits, and it's ready for your backlog.

---

## 🔌 Optional: Jira Integration

If you have a Jira MCP server configured, the skill can push the finished story directly to your board.

Enable it in your `USER_CONFIG`:

```yaml
jira:
  enabled: true                          # ← Change to true
  project_key: "SHOP"                    # ← Your Jira project key
  issue_type: "Story"
  default_epic_link: "SHOP-42"           # ← Optional: link to parent epic
  story_points_field: "customfield_10016" # ← Verify in your Jira instance
  labels: ["ai-generated", "needs-refinement"]
```

See [`references/jira/jira-setup-guide.md`](references/jira/jira-setup-guide.md) for the full
step-by-step Jira MCP setup, including how to find your custom field IDs.

---

## 📬 Connect

Built by [@yogitas](https://github.com/yogitas) — part of the *"How to be an AI-Powered PM"* series on LinkedIn.

Give it a ⭐ if it helps your team! PRs welcome — share your domain config by adding a file to `references/examples/`.
