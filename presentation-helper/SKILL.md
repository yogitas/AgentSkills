---
name: presentation-helper
description: |
  Creates presentations and reports by extracting brand styling
  from a reference PowerPoint master slide and applying it consistently.
  Invoke when a user wants to create a new presentation, slide deck, or
  report that matches an existing brand or template. Always runs the master
  slide extraction script before generating any content.
---

# Presentation Helper Skill

Generate polished, brand-consistent presentations and reports,
grounded in the visual identity extracted from any reference PowerPoint file.
---

## Invocation Checklist

When this skill is invoked, follow step by step guide ALWAYS **in order**:

1. **Extract master styles** — Run the extraction script on the reference PPTX (Step 1) — **NEVER SKIP**
2. **Build a style reference** — Parse the extracted JSON (Step 2)
3. **Gather audience & content** — Ask the user (Step 3) — **NEVER SKIP**
4. **Generate the deliverable** — Create slides or report using extracted styles (Step 4)

---

## Step 1 — Extract Master Slide Styling (MANDATORY)

**CRITICAL: This step must run every time, even if you think you already know the styles.**

### Locating the Reference PPTX

The reference PowerPoint can come from:
- A file uploaded by the user
- A path specified in the user's message
- A `.pptx` file already present in the workspace

### Running the Extraction Script

```bash
# Install dependencies if needed
pip install python-pptx lxml --break-system-packages -q

# Run extraction — adjust paths to your environment
python scripts/extract_master_styles.py \
    "<path_to_reference.pptx>" \
    --output extracted_styles.json

# Optional: use --verbose for detailed output
python scripts/extract_master_styles.py reference.pptx -o styles.json --verbose
```

The script is located at `scripts/extract_master_styles.py` relative to the skill root.

After running, read and parse `extracted_styles.json`.

### What the Extractor Captures (v2.0 — Comprehensive)

#### Theme (Complete)
- **Color scheme** — full palette (dk1, dk2, lt1, lt2, accent1–6, hlink, folHlink) with color transforms (tint, shade, alpha, luminance)
- **Font scheme** — heading (`majorFont`) and body (`minorFont`) typefaces with Latin, East Asian, Complex Script variants + locale-specific fonts
- **Format scheme** — fill styles, line styles, effect styles from theme
- **Background fill styles** — theme-defined background options
- **Theme name** — metadata from the Office theme

#### Master Slide (Complete)
- **Text styles at all 9 levels** — title style, body style, other style with full font/bullet/spacing per level
- **Color map** — color overrides (bg1, bg2, tx1, tx2, accents, hlink, folHlink)
- **Placeholders** — all 18+ types with position, size, typography
- **Decorative shapes** — logos, lines, watermarks with z-order, fill, line, effects
- **Effects** — shadows (inner/outer), glow, soft edges, reflection, 3D format

#### Layout Blueprints (Complete per layout)
- **Classification** — `title_slide`, `section_divider`, `content`, `closing`, `blank`, `comparison`, `picture`, `quote`, `keynote`
- **Background** — inherit flag or override fill
- **Show master shapes** — flag for master element visibility
- **Color map overrides** — per-layout color customization
- **Placeholder summary** — count by type

#### Shape Extraction (Comprehensive)
- **All shape types** — AutoShape, Picture, Group (recursive), Table, Chart, SmartArt, Connector, OLE, Media
- **AutoShape geometry** — rectangle, oval, arrow, etc.
- **Fill** — solid, gradient (with stops/angle), picture, pattern, none
- **Line/stroke** — color, width, dash style, compound, cap, join
- **Effects** — outer/inner shadow, glow, soft edge, reflection, 3D format/scene
- **Shape locking** — noMove, noResize, noRot, noTextEdit, etc.
- **Z-order** — rendering order for layered elements
- **Table cells** — structure, cell styles, borders
- **Chart info** — chart type, legend presence

#### Text & Font (Complete)
- **Full font properties** — name, size, bold, italic, underline styles, caps, strikethrough, baseline offset (sub/superscript)
- **Character spacing/kerning** — precise letter spacing
- **Latin/EA/CS fallback fonts** — font fallbacks for different scripts
- **Color** — solid RGB, theme reference with transforms
- **Bullet/numbering** — type (char, auto-number, picture, none), char, font, color, size, scheme
- **Hyperlinks** — detection and relationship IDs
- **Paragraph** — margins, indents, line spacing, tab stops
- **Text frame** — columns, rotation, margins, anchor

#### All Placeholder Types Tracked
```
TITLE, CENTER_TITLE, SUBTITLE, BODY, OBJECT, CHART, TABLE, SMART_ART,
MEDIA_CLIP, PICTURE, CLIP_ART, ORG_CHART, DATE, FOOTER, SLIDE_NUMBER,
HEADER, BITMAP, MIXED, BLANK, VERTICAL_TITLE, VERTICAL_BODY, VERTICAL_OBJECT
```

#### Other Extractions
- **Slide dimensions** — width/height in EMU, inches, and points; aspect ratio (16:9, 4:3, 16:10, 3:2, portrait, custom)
- **Notes master** — layout for speaker notes pages
- **Handout master** — detection for print handout layout
- **Footer visibility** — per-slide flags for date, footer, slide number
- **Actual slides** — categorized samples with notes preview

#### Validation & Reporting
- **Extraction statistics** — counts of masters, layouts, slides, shapes, images, tables, charts, etc.
- **Extraction warnings** — logged issues during extraction
- **Completeness check** — validation of required elements (colors, fonts, layouts, placeholders)

---

## Step 2 — Build Style Reference

After extraction, build an internal style reference from the JSON:

### JSON Structure Overview
```
{
  "source_file": "...",
  "extraction_version": "2.0.0",
  "slide_dimensions": {...},
  "theme": {
    "colors": {...},
    "font_scheme": {...},
    "format_scheme": {...},
    "background_fill_styles": [...]
  },
  "slide_masters": [{...}],
  "all_layout_blueprints": [...],
  "canonical_layouts": {...},
  "actual_slides": {...},
  "style_summary": {...},
  "extraction_stats": {...},
  "extraction_warnings": [...],
  "completeness_check": {...}
}
```

### Color Palette
From `style_summary.colors.semantic` (friendly-named) and raw `theme.colors`:
- **Primary text** — `dk1` → `primary_text`
- **Secondary text** — `dk2` → `secondary_text`
- **Background primary** — `lt1` → `background_primary`
- **Background secondary** — `lt2` → `background_secondary`
- **Accents** — `accent1` → `accent_primary`, `accent2` → `accent_secondary`, through `accent6`
- **Hyperlink** — `hlink` → `hyperlink`
- **Followed hyperlink** — `folHlink` → `followed_hyperlink`

Full palette with transforms available in `style_summary.colors.palette`.

### Typography
From `style_summary.typography`:
- `fonts_used` — sorted list of all detected font names
- `heading_font` and `body_font` from the theme's font scheme
- `by_role` — font, alignment, spacing, bullet info per role:
  - `master_title`, `title_slide_title`, `title_slide_subtitle`
  - `content_slide_title`, `content_slide_body`, `section_header`
- `text_styles_by_level.body` — full styling for all 9 body text levels (bullets, fonts, margins, spacing)

### Master Text Styles (9 Levels)
From `slide_masters[0].text_styles`:
- `title_style` — styling for title text at each level
- `body_style` — styling for body/bullet text at levels 1-9 (includes bullets, fonts, margins)
- `other_style` — default styling for other shapes

Each level includes: `default_font` (size, bold, italic, color, latin_font), `bullet` (type, char, font, color, size), `margin_left_in`, `indent_in`, `space_before_pt`, `space_after_pt`

### Layouts
From `all_layout_blueprints` and `canonical_layouts`:
- Layout names and classification: `title_slide`, `section_divider`, `content`, `closing`, `blank`, `comparison`, `picture`, `quote`, `keynote`
- `placeholder_summary` — count by placeholder type per layout
- `show_master_shapes` — whether master decorative elements appear
- `inherit_background` — whether layout uses master background
- `color_map_override` — per-layout color customization
- Placeholder details: idx, type, category (`title`, `body`, `subtitle`, `object`, `footer`), position, typography

### Design Elements
From `slide_masters[0]` and `style_summary`:
- `style_summary.master_decorative_elements` — non-placeholder shapes (lines, boxes)
- `style_summary.branding_elements` — logos, images, confidential labels
- `style_summary.footer_elements` — footer shapes with text content

Each element includes: name, position (EMU + inches), z_order, fill, line, effects

### Completeness Validation
From `completeness_check`:
- `is_complete` — boolean indicating all major elements found
- `missing_elements` — list of missing components
- `warnings` — extraction issues
- `coverage` — counts of layouts, slides, placeholder types, logo/footer presence

---

## Step 3 — Audience & Content Discovery

Before touching any file, ask the user:

> "To create your first draft, I need two quick things:
> 1. **Who is the target audience?** (e.g. executive leadership, engineering team, clients)
> 2. **What is the topic/content?** A brief description, key points, links, or notes."

- If the user provides URLs, fetch the content and use it as source material.
- If the user attaches a PDF or document, extract the content for slide material.

---

## Step 4 — Generate the Deliverable

### MINIMUM QUALITY REQUIREMENTS (NON-NEGOTIABLE)

**Every generated presentation MUST meet these baseline standards:**

#### Content Requirements
- [ ] **All slides have visible content** — no empty slides or missing text
- [ ] **All titles are populated** — every slide has a meaningful title
- [ ] **All bullet points are visible** — content placeholders filled with actual text
- [ ] **Minimum 5 slides** unless explicitly requested otherwise
- [ ] **Each content slide has 2-5 bullet points** — no single-bullet slides

#### Visual Requirements
- [ ] **Text is readable** — font colors extracted from the theme, not default black on dark backgrounds`
- [ ] **Text size appropriate and color is brand consistent** — readable in presentation mode, not too small
- [ ] **Brand colors applied** — text uses extracted brand colors, not default black
- [ ] **Consistent fonts** — all text uses fonts from the extracted theme
- [ ] **No placeholder errors** — all placeholders either filled or properly removed
- [ ] **Images display correctly** — no broken image placeholders

#### Technical Requirements
- [ ] **Presentation opens without errors** — file is not corrupted
- [ ] **All slides advance properly** — no layout issues preventing navigation
- [ ] **Print preview works** — slides display correctly in print mode

### General Approach

1. **Load the reference PPTX** as the template (preserves master, layouts, logos, footers).
2. **Delete existing slides** while keeping layouts and masters intact.
3. **Extract images** from original slides' PICTURE placeholders before deleting — save them for reuse.
4. **Add new slides** using the reference layouts by name.
5. **Populate placeholders** by robust detection — use multiple fallback methods.
6. **Apply brand colors and fonts** — verify text is visible and branded.
7. **Validate all content** — ensure no empty slides or missing text.
8. **Save as a new `.pptx`** file.

### Key Implementation Patterns

#### Loading & Cleaning the Reference

```python
from pptx import Presentation

prs = Presentation("reference.pptx")

# Delete existing slides, keep layouts & masters
sldIdLst = prs.slides._sldIdLst
for sldId in list(sldIdLst):
    rId = None
    for attr, val in sldId.attrib.items():
        if attr.endswith("}id") or attr == "r:id":
            rId = val
            break
    if rId:
        try:
            prs.part.drop_rel(rId)
        except Exception:
            pass
    sldIdLst.remove(sldId)
```

#### Adding Slides by Layout Name

```python
def get_layout(prs, name):
    for sl in prs.slide_masters[0].slide_layouts:
        if sl.name == name:
            return sl
    raise ValueError(f"Layout '{name}' not found")

slide = prs.slides.add_slide(get_layout(prs, "Content | 1"))
```

#### Robust Placeholder Detection & Filling

**CRITICAL: Use multiple detection methods - never rely only on hardcoded indices**

```python
def find_title_placeholder(slide):
    """Find title placeholder with multiple fallback methods."""
    # Method 1: Try common title indices
    for idx in [0, 1]:
        try:
            ph = slide.placeholders[idx]
            if ph.has_text_frame and ('title' in str(ph.placeholder_format.type).lower() or idx == 0):
                return ph
        except (KeyError, IndexError):
            continue
    
    # Method 2: Search by placeholder type
    for ph in slide.placeholders:
        try:
            if 'title' in str(ph.placeholder_format.type).lower():
                return ph
        except:
            continue
    
    # Method 3: Find any text placeholder
    for ph in slide.placeholders:
        if ph.has_text_frame:
            return ph
    return None

def find_content_placeholder(slide):
    """Find content/body placeholder with multiple fallback methods."""
    # Method 1: Try common content indices
    for idx in [1, 2, 10, 13, 14, 15, 17]:
        try:
            ph = slide.placeholders[idx]
            if ph.has_text_frame and ph.placeholder_format.idx != 0:
                return ph
        except (KeyError, IndexError):
            continue
    
    # Method 2: Find largest text placeholder (likely content)
    largest_ph = None
    max_area = 0
    for ph in slide.placeholders:
        try:
            if ph.has_text_frame and ph.placeholder_format.idx != 0:
                area = ph.width * ph.height
                if area > max_area:
                    max_area = area
                    largest_ph = ph
        except:
            continue
    
    return largest_ph

def apply_brand_colors(text_frame, brand_color_hex):
    """Apply brand colors ensuring text is visible."""
    from pptx.dml.color import RGBColor
    
    # Convert hex to RGB
    hex_color = brand_color_hex.lstrip('#')
    rgb = tuple(int(hex_color[i:i+2], 16) for i in (0, 2, 4))
    
    for paragraph in text_frame.paragraphs:
        for run in paragraph.runs:
            run.font.color.rgb = RGBColor(*rgb)
            # Also set font family from extracted styles
            run.font.name = extracted_font_name

# Usage with validation
title_ph = find_title_placeholder(slide)
if title_ph:
    title_ph.text = slide_content["title"]
    apply_brand_colors(title_ph.text_frame, brand_color)
else:
    print(f"WARNING: No title placeholder found for slide '{slide_content['title']}'")

content_ph = find_content_placeholder(slide)
if content_ph:
    content_ph.text_frame.clear()
    for i, bullet in enumerate(slide_content["content"]):
        p = content_ph.text_frame.paragraphs[0] if i == 0 else content_ph.text_frame.add_paragraph()
        p.text = bullet
        p.level = 0
    apply_brand_colors(content_ph.text_frame, brand_color)
else:
    print(f"ERROR: No content placeholder found for slide '{slide_content['title']}'")
    # This is a critical error - log and potentially skip slide
```

#### Handling Branded Elements

- **Logo placeholders** (often ORG_CHART or SmartArt type with embedded blip images) — **never remove or modify these**. They inherit from the layout.
- **Footer shapes** (e.g. page numbers, department codes, confidential labels) — these live on the master slide and inherit to all slides automatically. Don't recreate them.
- **OLE objects** (think-cell, etc.) — tiny hidden shapes; leave untouched.
- **PICTURE placeholders** — either insert an image or remove the empty placeholder from the slide XML to avoid blank frames:
  ```python
  ph._element.getparent().remove(ph._element)
  ```

### Presentation Content Rules

#### Brand Consistency (NON-NEGOTIABLE)
- Use **exact hex colors** from the extracted palette (`style_summary.colors`)
- Use **exact font names** from `style_summary.typography.fonts`
- Replicate header/footer shapes with correct dimensions (EMU values from extraction)
- Match background fill type and color from the master

#### Content Principles (Pyramid Structure)
- **Title slide** — project/company name, presentation title, department code
- **Start with WHY** — lead with the problem or motivation before explaining what/how
- **One key message per slide** — the slide TITLE is the takeaway, not a topic label
- **Max 3–5 bullets per slide** — prefer visuals over text walls
- **Closing slide** — next steps or recommendations, clearly actionable

#### Slide Title = The Takeaway
- Bad: "Q3 Performance"
- Good: "Q3 Revenue Exceeded Target by 12% — Driven by APAC Growth"

### Layout Selection Guide

| Slide Purpose | Layout to Use | Classification |
|---|---|---|
| Title / cover | First layout or "Title Slide" | `title_slide` |
| Section divider | "Section Header" or divider layout | `section_divider` |
| Content with bullets | "Title and Content" or content layout | `content` |
| Two-column comparison | "Two Content" or "Comparison" | `comparison` |
| Image / diagram focus | "Blank" or "Picture" layout | `picture` or `blank` |
| Quote / key message | "Quote" or "Key Note" layout | `quote` or `keynote` |
| Closing / next steps | "Title and Content" or closing layout | `closing` |

---

## Error Handling & Quality Assurance

### Critical Errors (STOP EXECUTION)

| Problem | Resolution |
|---|---|
| No reference PPTX provided | Ask user to upload one; **NEVER proceed without it** |
| Extraction script fails completely | Debug output, check file permissions, **do not continue** |
| No placeholders found on any slide | **STOP** - template may be corrupted, ask for different reference |
| All brand colors are black/white | **STOP** - extraction failed, manually confirm colors with user |
| Cannot save final presentation | Check file permissions, disk space, **do not deliver broken file** |

### Warning Issues (CONTINUE WITH FIXES)

| Problem | Resolution | Validation Required |
|---|---|---|
| `.pptm` file (macros) | Strip macros via zip manipulation → save as `.pptx` | Test opening |
| Script fails to extract fonts | Check `extraction_warnings`; fallback to Calibri + theme fonts | **Verify fonts display** |
| Some colors not extracted | Use `completeness_check.missing_elements`; apply safe brand colors | **Check text contrast** |
| Layout name not found | Use fuzzy matching, then `canonical_layouts.content` default | **Verify layout works** |
| PICTURE placeholder empty | Remove from slide XML or insert relevant stock image | **No broken placeholders** |
| python-pptx/lxml not installed | Script auto-installs; try `--user` flag if needed | Test import after install |
| Theme extraction partial | Use `theme._extraction_error`; proceed with slide-level styles | **Check visual consistency** |

### Content Quality Issues (IMMEDIATE FIX REQUIRED)

| Problem | Fix | Validation |
|---|---|---|
| Empty slides created | **Find placeholders by multiple methods** + fill with default content | Every slide has visible text |
| Text invisible (black on dark) | **Apply extracted brand colors** + check contrast | Text is readable |
| Font not applied | **Force font family from extracted styles** | Check font consistency |
| Bullets not showing | **Clear text frame + rebuild paragraphs** | All bullet points visible |
| Placeholders overlap | **Use extracted position data** or remove conflicting ones | Clean layout |
| Images don't load | **Validate image paths** + use fallback placeholder removal | No broken image boxes |

### Automated Validation Checklist

**Run these checks before saving any presentation:**

```python
def validate_presentation_quality(prs):
    """Validate presentation meets minimum quality standards."""
    errors = []
    warnings = []
    
    if len(prs.slides) == 0:
        errors.append("No slides created")
        return errors, warnings
    
    for i, slide in enumerate(prs.slides):
        slide_num = i + 1
        
        # Check for content
        has_title = False
        has_content = False
        
        for ph in slide.placeholders:
            if ph.has_text_frame and ph.text_frame.text.strip():
                if ph.placeholder_format.idx == 0:
                    has_title = True
                else:
                    has_content = True
        
        if not has_title:
            errors.append(f"Slide {slide_num}: No title text")
        if not has_content and slide_num > 1:  # Allow title slide to have no body
            warnings.append(f"Slide {slide_num}: No body content")
    
    return errors, warnings

# Usage
errors, warnings = validate_presentation_quality(prs)
if errors:
    print("CRITICAL ERRORS - Cannot save presentation:")
    for error in errors:
        print(f"  ❌ {error}")
    return False  # Do not save

if warnings:
    print("Warnings - Fixed automatically:")
    for warning in warnings:
        print(f"  ⚠️  {warning}")
```

---

## Output Checklist

### MANDATORY PRE-DELIVERY VALIDATION

**Before finalizing any deliverable, ALL items must be verified:**

#### Technical Validation
- [ ] **Extraction script was run and JSON was parsed** — verify `extracted_styles.json` exists
- [ ] **`completeness_check.is_complete` is true** (or all warnings addressed with fallbacks)
- [ ] **Presentation opens without errors** — test in PowerPoint/LibreOffice
- [ ] **All slides advance correctly** — no navigation issues
- [ ] **File size reasonable** — not corrupted (typical range: 500KB-50MB)

#### Content Validation
- [ ] **All slides have visible content** — NO empty slides allowed
- [ ] **All slide titles are populated** — every slide has a meaningful title
- [ ] **Slide titles are takeaway statements** — not just topic labels
- [ ] **Each content slide has 2-5 bullet points** — no single bullets or walls of text
- [ ] **All bullet points are visible** — content placeholders properly filled

#### Visual Validation
- [ ] **Text is readable** — NOT black on dark backgrounds or white on light
- [ ] **Font matches extracted values** — from `style_summary.typography.fonts_used`
- [ ] **Colors match extracted hex values** — from `style_summary.colors.semantic`
- [ ] **Text size appropriate** — readable in presentation mode
- [ ] **No broken placeholders** — all filled or properly removed

#### Brand Validation
- [ ] **Logo/branding placeholders present** — check `style_summary.branding_elements`
- [ ] **Footer elements inherit from master** — check `style_summary.footer_elements`
- [ ] **Body text uses correct bullet styles** — from `text_styles_by_level.body`
- [ ] **Consistent visual hierarchy** — titles larger than body text
- [ ] **Brand colors applied** — not default black text

#### Final Quality Check
- [ ] **PICTURE placeholders filled or removed** — no blank image frames
- [ ] **No placeholder overlap** — clean layout on all slides
- [ ] **Spelling checked** — no obvious typos
- [ ] **File saved successfully** — verify file integrity
- [ ] **User requirements met** — audience and content objectives achieved

### DELIVERY STANDARDS

**If ANY mandatory item fails, DO NOT deliver the presentation. Fix issues or inform user of limitations.**

#### Minimum Acceptable Output
- 5+ slides with meaningful content
- All text visible and readable
- Brand colors and fonts applied
- No technical errors
- Professional appearance

#### Preferred Output
- Compelling narrative structure
- Strong visual hierarchy
- Consistent branding
- Engaging content
- Ready for executive presentation

**Remember: It's better to deliver a delayed, high-quality presentation than a fast, broken one.**

---

## File Locations

| File | Path (relative to skill root) |
|---|---|
| This skill file | `SKILL.md` |
| Extraction script | `scripts/extract_master_styles.py` |
| Extracted styles (output) | `extracted_styles.json` (working directory) |
| Reference PPTX | Provided by user |
| Generated presentation | Saved to working directory or user-specified path |
