# presentation-helper

An [Agent Skill](https://docs.anthropic.com/en/docs/agents-and-tools/agent-skills) that generates brand-consistent PowerPoint presentations from any reference deck.

Give it a reference `.pptx` with your company's branding and a topic — it extracts the visual identity (colors, fonts, logos, layouts) and generates a polished first draft that looks like it came from your template.

## How It Works

```
Reference PPTX ──► extract_master_styles.py ──► styles.json ──► AI generates slides
                                                                 using branded layouts
```

1. **Extract** — A Python script analyzes the reference PowerPoint and produces a JSON file with theme colors, typography, layout blueprints, logo positions, footer shapes, and more.
2. **Generate** — The AI agent (Claude) reads the JSON, loads the reference file as a template, and creates new slides using the exact same layouts, fonts, colors, and decorative elements.

## Quick Start

### Prerequisites

```bash
pip install python-pptx
```

### As a Claude Agent Skill

1. Place this folder in your skills directory (e.g. `~/.claude/skills/presentation-helper/`)
2. Ask Claude: *"Create a presentation about [topic] using [reference.pptx] as the template"*
3. Claude will:
   - Ask about your target audience
   - Run the extraction script on your reference file
   - Generate a branded slide deck

### Standalone Usage (Extraction Only)

```bash
# Extract styles from any PowerPoint file
python scripts/extract_master_styles.py my-deck.pptx

# Specify output path
python scripts/extract_master_styles.py my-deck.pptx --output styles.json
```

The extraction script outputs a comprehensive JSON with:
- Theme color palette (dark, light, accent1–6, hyperlinks)
- Font families and size hierarchies
- All available layout blueprints with placeholder maps
- Master slide decorative elements (logos, lines, watermarks)
- Footer and department-code shapes
- Picture placeholder locations
- Background fill information

## Project Structure

```
presentation-helper/
├── SKILL.md                          # Skill instructions (read by Claude)
├── README.md                         # This file
├── scripts/
│   └── extract_master_styles.py      # Style extraction script (core tool)
└── examples/
    ├── README.md                     # Examples documentation
    ├── templates/                    # Reference PowerPoint templates
    │   └── Your_Reference_ppt_deck.pptx
    └── outputs/                      # Sample generated presentations
        └── Claude_Skills_for_Product_Managers.pptx
```

| File | Purpose |
|---|---|
| `SKILL.md` | Agent instructions — defines the 4-step workflow Claude follows |
| `scripts/extract_master_styles.py` | Analyzes any `.pptx` and outputs a JSON style reference |
| `examples/templates/` | Reference PowerPoint templates for testing |
| `examples/outputs/` | Sample generated presentations showcasing the skill |

## What Gets Extracted

The extraction script captures everything needed to reproduce a deck's visual identity:

| Category | Details |
|---|---|
| **Colors** | Full Office theme palette, accent colors, text/background colors |
| **Typography** | Font families, sizes per placeholder type, bold/italic patterns |
| **Layouts** | Every layout with name, classification, and placeholder positions (EMU + inches) |
| **Logos** | SmartArt/ORG_CHART placeholders with embedded blip images |
| **Footers** | Department codes, page numbers, confidential labels on master |
| **Pictures** | Which layouts have PICTURE placeholders and whether they're filled |
| **Backgrounds** | Solid, gradient, or picture fills on master and layouts |
| **OLE Objects** | think-cell and other embedded objects (preserved, not modified) |

## Key Design Decisions

### Why load the reference as a template?

Instead of building slides from scratch with `python-pptx`, the skill loads the reference file and deletes its slides while keeping the master, layouts, and all embedded assets. This preserves:
- Exact logo images and positions
- Footer shapes with department codes
- OLE objects (think-cell, etc.)
- Background fills and gradients
- Font definitions not available in python-pptx

### Why not just copy the template?

The extraction JSON is still generated so the AI agent understands _what_ is available — layout names, placeholder indices, color values, font names. Without it, the agent would have to guess.

### Handling branded elements

- **Logo placeholders** — Leave untouched. They inherit from the layout automatically.
- **Footer shapes** — Live on the master slide. Inherit to all new slides.
- **Empty PICTURE placeholders** — Either insert an image or remove the XML element to avoid blank frames.
- **OLE objects** — Tiny hidden shapes (e.g. think-cell). Preserved automatically.

## Example Output

The `examples/` folder contains:

### Templates
- **Corporate Brand Template** - Professional corporate template with multiple layouts
- Brand colors: Custom accent colors, text, and background colors
- Corporate typography and fonts
- Integrated logos and footer elements

### Generated Presentations
- **Claude Skills for Product Managers** (13 slides)
- Demonstrates brand consistency, smart content generation
- Professional slide structure with proper placeholder handling
- Ready for executive presentation

**Key Features Demonstrated:**
- Loading reference PPTX and preserving master elements
- Smart placeholder detection with multiple fallback methods
- Brand color application ensuring readable text
- Layout classification and appropriate content structure
- Quality validation preventing empty or broken slides

## Contributing

Contributions welcome! Areas where help is appreciated:

- **More layout intelligence** — Better auto-classification of layouts (title vs content vs divider)
- **Chart/SmartArt extraction** — Currently detected but not deeply parsed
- **DOCX support** — The SKILL.md references report generation but no extraction script exists yet
- **Theme font resolution** — Resolving theme font references to actual font names

## License

MIT
