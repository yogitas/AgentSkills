# 📚 References Directory

This folder contains **supporting material to help you configure the Agile User Story Writer skill**.

It is intentionally separate from `SKILL.md` so that:
- The skill file stays clean and focused on agent instructions
- POs can browse and copy-paste reference material without touching the skill itself
- Teams can contribute domain examples without modifying core files

---

## 📂 What's in Here

### `examples/`
Pre-built `USER_CONFIG` blocks for common product domains.
Pick the one closest to your product, copy it into your AI agent's custom instructions (see `SKILL.md` for agent-specific setup steps), and customise.

| File | Best for |
|------|----------|
| `example-ecommerce.yaml` | Retail, marketplace, shopping products |
| `example-saas.yaml` | B2B SaaS, dashboards, internal tools |
| `example-fintech.yaml` | Payments, banking, financial services |

### `personas/`
Reusable persona definitions to drop into `USER_CONFIG.personas`.
Covers common roles across consumer, B2B, fintech, and healthcare products.

### `acceptance-criteria/`
AC writing patterns and templates for common story types.
Use these to seed better AC or validate agent output before refinement.

### `jira/`
Step-by-step Jira MCP setup guide including field ID lookup and troubleshooting.

---

## ➕ Contributing Your Own References

Have a great `USER_CONFIG` for your domain? Please share it!

1. Add your file to the appropriate subfolder
2. Strip any sensitive data (project keys, API tokens, internal URLs)
3. Open a PR with a short description of the domain/team type
