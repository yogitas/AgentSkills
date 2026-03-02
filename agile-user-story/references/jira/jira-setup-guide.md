# 🔧 Jira MCP Setup Guide

Complete reference for connecting the Agile User Story skill to your Jira instance
so stories are pushed directly without any copy-paste.

---

## Prerequisites

- A Jira Cloud or Jira Server instance
- An Atlassian account with permission to create issues in your target project
- Claude Desktop (or an agent environment that supports MCP servers)

---

## Step 1 — Generate Your Jira API Token

1. Go to: https://id.atlassian.com/manage-profile/security/api-tokens
2. Click **Create API token**
3. Give it a descriptive label (e.g., `claude-userstory-skill`)
4. Copy the token immediately — **you won't be able to see it again**

> ⚠️ Never commit your API token to GitHub.
> Store it only in your MCP config file and add that file to `.gitignore`.

---

## Step 2 — Find Your Jira Project Key

Your project key appears in every Jira issue URL:
`https://your-org.atlassian.net/browse/PROJ-123`
→ Project key = `PROJ`

You can also find it at:
**Your Project → Project Settings → Details → Key**

---

## Step 3 — Find Your Story Points Field ID

Story Points are stored in a custom field whose ID varies by Jira instance.

**Method 1 — Via Jira Settings (easiest):**
1. Go to **Jira Settings → Issues → Custom Fields**
2. Search for "Story Points"
3. Click the field → look at the page URL for the field ID
   e.g. `...customFieldId=10016` → your field ID = `customfield_10016`

**Method 2 — Via Jira REST API:**
```
GET https://your-org.atlassian.net/rest/api/3/field
Authorization: Basic base64(email:api_token)
```
Search the JSON response for `"name": "Story Points"` and note the `id` value.

**Common field IDs across Jira instances:**

| Field ID | Notes |
|---|---|
| `customfield_10016` | Most common for Jira Cloud |
| `customfield_10028` | Common on some Cloud instances |
| `customfield_10004` | Some Jira Server setups |

---

## Step 4 — Configure Claude Desktop

Open your Claude Desktop MCP config file:
- **Mac:** `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

Add this block (create the file if it doesn't exist yet):

```json
{
  "mcpServers": {
    "jira": {
      "command": "npx",
      "args": ["@atlassian/jira-mcp"],
      "env": {
        "JIRA_BASE_URL": "https://your-org.atlassian.net",
        "JIRA_API_TOKEN": "your-api-token-from-step-1",
        "JIRA_EMAIL": "you@yourcompany.com"
      }
    }
  }
}
```

Restart Claude Desktop after saving.

---

## Step 5 — Update USER_CONFIG

In your Claude Custom Instructions or Project Instructions, update:

```yaml
jira:
  enabled: true                              # ← change from false to true
  project_key: "PROJ"                        # ← your key from Step 2
  story_points_field: "customfield_10016"    # ← your field ID from Step 3
```

---

## Step 6 — Test It

Ask Claude: *"Write a user story for [anything] and push it to Jira."*

Claude will write the story, ask for confirmation, then create the Jira issue and
return the issue URL.

---

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| "Authentication failed" | Wrong API token or email | Regenerate token; ensure email matches your Atlassian login |
| "Project not found" | Wrong project key | Double-check key in Jira Project Settings → Details |
| "Field not found" for story points | Wrong field ID | Use the REST API method above to find the correct ID |
| Story created but no epic link | Epic link field ID differs | Check your instance — epic link is often `customfield_10014` |
| MCP server not appearing in Claude | JSON syntax error in config file | Validate your JSON at jsonlint.com |
| `npx` not found | Node.js not installed | Install Node.js from nodejs.org |

---

## Jira Description Formatting Reference

When the skill pushes a story, it uses Jira wiki markup:

| Element | Jira Wiki Markup |
|---|---|
| Section header | `h3. Motivation` |
| Bullet point | `* Item text` |
| Checkbox (AC) | `[ ] AC text` |
| Info panel | `{info}As a user...{info}` |
| Bold text | `*bold*` |
| Hyperlink | `[Link text\|https://url]` |
| Horizontal rule | `----` |

---

## Self-Hosted / Custom MCP Alternative

If your org uses a self-hosted Jira or a custom MCP wrapper, ensure the MCP server
exposes a `jira_create_issue` tool that accepts:
`project`, `summary`, `issue_type`, `description`, `labels`

Then configure the `mcpServers` block in your Claude Desktop config to point at
your custom server's command instead of the Atlassian npx package.
