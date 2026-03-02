# 🤖 AgentSkills

A collection of reusable AI skills for Product Managers, Product Owners, and Agile teams.

Each skill is a structured instruction set that teaches Claude **exactly how to do a specific
PM task** — in your format, with your team's context, every time.

No coding required. Configure once, use forever.

---

## 📦 Available Skills

| Skill | What it does | Jira integration |
|-------|-------------|-----------------|
| [agile-user-story](./agile-user-story/) | Writes structured Agile user stories in PO-ready format | ✅ |

*More skills coming. PRs welcome — see [Contributing](#contributing).*

---

## 🚀 Quick Start (5 minutes)

1. **Pick a skill** from the table above
2. **Open the skill's `references/examples/`** folder and find the config closest to your product domain
3. **Copy the `USER_CONFIG` block** from the example and paste it into:
   - **Claude.ai:** Settings → Custom Instructions → *"How should Claude respond?"*
   - **Claude Projects:** Your Project → Instructions tab
   - **Claude API:** Your `system` prompt
4. **Customise** — update your project name, personas, and replace the example stories with 2–3 real ones from your product
5. **Start prompting** — *"Write a user story for: [your feature]"*

That's it. No installs. No code.

---

## 🗂️ Skill Structure

Each skill follows the same structure so it's easy to navigate:

```
skill-name/
├── SKILL.md                    ← Core skill — agent instructions + USER_CONFIG template
└── references/
    ├── README.md               ← Guide to what's in the references folder
    ├── examples/               ← Pre-built USER_CONFIG blocks by domain
    │   ├── example-ecommerce.yaml
    │   ├── example-saas.yaml
    │   └── example-fintech.yaml
    ├── personas/
    │   └── persona-templates.md    ← Reusable persona definitions
    ├── acceptance-criteria/
    │   └── ac-patterns.md          ← AC patterns by story type
    └── jira/
        └── jira-setup-guide.md     ← Step-by-step Jira MCP setup
```

---

## 🤝 Contributing

Have a skill idea, a domain-specific config, or an improvement? Open a PR!

**To add a new domain example:**
1. Copy an existing file from `references/examples/`
2. Update it for your domain
3. Strip any sensitive data (project keys, tokens, internal URLs)
4. PR with a short description

**To add a new skill:**
1. Create a new folder with the skill name
2. Follow the same structure as `agile-user-story/`
3. Include at least 2 domain example configs in `references/examples/`

---

## 📬 Connect

Built by [@yogitas](https://github.com/yogitas) — part of the *"How to be an AI-Powered PM"* series on LinkedIn.

Give it a ⭐ if it helps your team!
