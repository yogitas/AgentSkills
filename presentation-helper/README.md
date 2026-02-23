# presentation-helper

[Agent Skill](https://docs.anthropic.com/en/docs/agents-and-tools/agent-skills) that generates brand-consistent PowerPoint presentations from any reference deck.

Extracts visual identity (colors, fonts, logos, layouts) from a `.pptx` template and creates new presentations that match the branding.

## How It Works

1. **Extract** — Python script analyzes reference PowerPoint → JSON file with theme data
2. **Generate** — AI agent uses JSON to create branded slides with matching layouts and styles

## Quick Start

### Prerequisites
```bash
pip install python-pptx
```

### Usage
1. Place in your skills directory: `~/.claude/skills/presentation-helper/`
2. Ask Claude: *"Create a presentation about [topic] using [reference.pptx] as the template"*

### Standalone Extraction
```bash
python scripts/extract_master_styles.py my-deck.pptx --output styles.json
```

## Project Structure

```
presentation-helper/
├── SKILL.md                          # Skill instructions for Claude
├── README.md                         # This file
├── scripts/
│   └── extract_master_styles.py      # Style extraction script
└── examples/
    ├── templates/                    # Reference PowerPoint templates
    └── outputs/                      # Sample generated presentations
```

## What Gets Extracted

- **Colors** — Theme palette and accent colors
- **Typography** — Font families and sizes
- **Layouts** — All layouts with placeholder positions
- **Branding** — Logos, footers, backgrounds
- **Elements** — Pictures, OLE objects (preserved)



