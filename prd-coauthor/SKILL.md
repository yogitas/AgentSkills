---
name: prd-coauthor
description: Collaborative PRD (Product Requirements Document) creation and refinement. Use when users want to write, improve, review, or get feedback on PRDs for new products, features, quality improvements, or bug fixes. Helps with structure selection, content development, section writing, and ensuring PRDs follow best practices from top tech companies (Google, Amazon, Meta, Microsoft). Works iteratively through questions and suggestions to co-author high-quality product requirements documents.
---

# PRD Co-Author

## Overview

This skill helps you collaboratively write comprehensive, well-structured Product Requirements Documents (PRDs) following industry best practices. PRDs communicate what a product will do, who it's for, and why it matters - serving as the alignment tool for product, engineering, design, and business teams.

## Co-Authoring Workflow

### Step 1: Understand the Project

Start by understanding the project context through targeted questions:

**Project Discovery Questions**:
```
1. What type of project is this?
   - New product (completely new offering)
   - New feature (addition to existing product)
   - Quality improvement (performance, reliability, UX refinement)
   - Bug fix (addressing specific issues)

2. Who is the primary audience for this PRD?
   - Engineering team
   - Design team
   - Executives/stakeholders
   - Cross-functional (all of the above)

3. What materials already exist?
   - User research findings
   - Design mockups
   - Business case or justification
   - Technical specifications
   - Nothing yet (starting from scratch)

4. Are there specific constraints?
   - Timeline requirements
   - Regulatory/compliance needs
   - Integration requirements
   - Budget limitations
```

The answers guide which PRD framework and sections are most appropriate.

### Step 2: Select Framework and Structure

Based on project type, recommend appropriate structure. Read `references/prd-frameworks.md` to understand different patterns (Amazon PR/FAQ, Lean One-Pager, Comprehensive PRD, Jobs-to-be-Done, Shape Up Pitch).

Then consult `references/prd-sections.md` to determine essential vs optional sections.

**Structure Recommendation Format**:
```
"Based on your [project type] with [audience], I recommend a [framework name] with these sections:

✓ Essential Sections:
  - Executive Summary
  - Problem Statement
  - Target Audience
  - Success Metrics
  - Scope (In/Out)
  - [Features/Requirements/Solution Description]

+ Optional Sections (valuable for your case):
  - [Strategic Context - because new product needs business justification]
  - [Technical Requirements - because integration complexity]

− Skip These Sections:
  - [Go-to-Market Strategy - internal tool doesn't need GTM]
  - [User Research - quality improvement, not new UX]

Does this work, or would you like adjustments?"
```

### Step 3: Co-Author Sections Iteratively

Work through sections in logical order, typically:

1. **Problem Statement** - Establish "why" first
2. **Target Audience / User Personas** - Who is this for
3. **Success Metrics** - How we measure success
4. **Scope** - What's in and out
5. **Features & Requirements** - What we're building
6. **Technical Requirements** - How it works (if applicable)
7. **Additional sections** - As relevant to project type
8. **Executive Summary** - Write last when full picture is clear

#### Co-Authoring Pattern for Each Section

For each section, follow this pattern:

**1. Explain Purpose**
```
"Let's work on [Section Name]. This section [purpose and why it matters].

A strong [section name] includes:
- [Key element 1]
- [Key element 2]
- [Key element 3]"
```

**2. Ask Targeted Questions**
```
"To write this section, I need to understand:
1. [Specific question about content]
2. [Question gathering evidence or data]
3. [Question about constraints or requirements]"
```

**3. Draft Content**

Write the section based on their answers, following best practices from `references/prd-sections.md` and using examples from `references/prd-examples.md` as inspiration.

**4. Request Feedback**
```
"Here's a draft [section name]:

[Well-structured section content]

Does this accurately capture [the problem/requirements/goals]? Any adjustments needed?"
```

**5. Iterate**

Refine based on their feedback until the section is complete.

### Step 4: Review and Refine

Once all sections are drafted, conduct final review:

**Completeness Check**:
- [ ] All essential sections included
- [ ] Each section has sufficient detail
- [ ] No major gaps in information

**Consistency Check**:
- [ ] Success metrics align with problem statement
- [ ] Features address identified user needs
- [ ] Technical requirements support proposed features
- [ ] Scope boundaries are consistent throughout

**Clarity Check**:
- [ ] Scannable (headers, bullets, bold text used appropriately)
- [ ] Jargon-free or jargon defined
- [ ] Multiple audiences can understand their relevant parts
- [ ] Specific and measurable (not vague)

**Best Practices Check**:
- [ ] Problem before solution
- [ ] Evidence-based claims
- [ ] Prioritized requirements (not everything is "must have")
- [ ] Clear non-goals to prevent scope creep

**Review Format**:
```
"Let me review the complete PRD:

✓ Problem statement grounded in evidence (user research + data)
✓ Success metrics specific and measurable
✓ Features prioritized with MoSCoW method
⚠ Technical requirements could specify performance benchmarks
✓ Scope clearly defines what's in and out

Suggested improvements:
1. [Specific actionable suggestion]
2. [Another concrete suggestion]

Would you like me to refine these sections?"
```

## Section-Specific Guidance

### Problem Statement
**When drafting**:
- Start with specific user problem or business opportunity
- Ground in observable evidence (user research, metrics, support tickets)
- Explain impact of NOT solving
- Describe current workarounds
- Use Jobs-to-be-Done framework when appropriate: "When [situation], I want to [motivation], so I can [outcome]"

**Questions to ask**:
- What specific problem are users facing?
- What evidence supports this? (research, data, feedback)
- How are users working around this today?
- What's the business impact of not solving it?

**Read**: `references/prd-sections.md` (Problem Statement section) and `references/prd-examples.md` (Problem Statement examples)

### Target Audience / User Personas
**When drafting**:
- Be specific and behavioral, not just demographic
- Define primary and secondary personas
- Include user stories: "As a [role], I want [goal] so that [benefit]"
- Validate with actual user research

**Questions to ask**:
- Who specifically is this for? (role, behaviors, context)
- What are their goals and pain points?
- How do they currently solve this problem?
- What are their technical capabilities and constraints?

**Read**: `references/prd-sections.md` (Target Audience section) and `references/prd-examples.md` (Personas examples)

### Success Metrics
**When drafting**:
- Pick 2-3 metrics you can actually measure
- Include baseline, target, and timeframe
- Cover business metric, usage metric, and quality metric
- Specify measurement methodology

**Questions to ask**:
- What metrics indicate this project succeeded?
- What's the current baseline for these metrics?
- What's a realistic target improvement and timeframe?
- How will we track and measure these?

**Read**: `references/prd-sections.md` (Success Metrics section) and `references/prd-examples.md` (Metrics examples)

### Scope (In/Out)
**When drafting**:
- Explicitly state what IS included
- Clearly state what is NOT included
- Distinguish "future consideration" from "truly out of scope"
- Document assumptions

**Questions to ask**:
- What must be included in this release?
- What's explicitly excluded (but might be future work)?
- What will we definitely never do?
- What are we assuming already exists or is true?

**Read**: `references/prd-sections.md` (Scope section) and `references/prd-examples.md` (Scope examples)

### Features & Requirements
**When drafting**:
- Organize features logically
- Prioritize with MoSCoW (Must/Should/Could/Won't Have)
- Include acceptance criteria
- Link to designs/wireframes when available

**Adapt by project type**:
- **New products**: Comprehensive feature list with clear priorities
- **New features**: Detailed breakdown of the single feature with user flows
- **Quality improvements**: Specific improvements and benchmarks, not features
- **Bug fixes**: Keep minimal - problem, impact, fix approach

**Questions to ask**:
- What are the core capabilities needed? (Must Have)
- What would significantly enhance value? (Should Have)
- What would be nice but not essential? (Could Have)
- What specific acceptance criteria must be met?

**Read**: `references/prd-sections.md` (Features section) and `references/prd-examples.md` (Features examples)

## PRD Type Adaptations

### New Product PRD
**Include all**:
- Executive Summary
- Strategic Context / Business Justification
- Problem Statement with Research
- User Personas (comprehensive)
- Success Metrics
- Scope
- Features & Requirements (comprehensive with priorities)
- Technical Requirements (architecture)
- User Stories / Use Cases
- Implementation Plan / Timeline
- Go-to-Market Strategy
- Risks, Dependencies & Assumptions

**Focus**: Complete vision, strategic justification, full feature set

### New Feature PRD
**Include**:
- Executive Summary
- Problem Statement
- Target Audience
- Success Metrics
- Scope
- Features & Requirements (detailed for this feature)
- User Stories / Use Cases
- Technical Requirements (integration points, dependencies)
- Design/Wireframes (if UX changes)

**Optional**: Strategic Context (if significant), Implementation Plan (if phased), GTM (if customer-facing)

**Skip**: Full architecture (already exists), comprehensive user research (product exists)

**Focus**: How feature integrates, specific user value, implementation details

### Quality Improvement PRD
**Include**:
- Executive Summary
- Problem Statement (current performance issues, user impact)
- Success Metrics (specific performance benchmarks)
- Scope
- Technical Requirements (optimization approach)

**Optional**: User impact assessment (if customer-facing), Implementation plan (if complex rollout)

**Skip**: User personas (typically internal concern), Feature lists (not adding features), Design/wireframes, GTM Strategy

**Focus**: Current state problems, target improvements, technical solution

### Bug Fix PRD
**Keep lean - include only**:
- Problem Statement (bug description, impact, reproduction)
- Success Metrics (error rate reduction, affected users)
- Scope
- Technical Requirements (fix approach, testing)

**Skip**: Most other sections

**Focus**: Bug impact, root cause, fix, verification

## Best Practices

### Writing Principles
1. **Problem before solution** - Always establish "why" before "what"
2. **Evidence-based** - Support claims with data, research, user quotes
3. **Plain English** - Avoid jargon or define acronyms
4. **Scannable** - Use headers, bullets, bold text for key information
5. **Specific & measurable** - "Increase conversion from 12% to 18%" not "improve conversion"
6. **Link don't duplicate** - Reference existing docs, don't copy them

### Common Pitfalls to Avoid
❌ **Jumping to solutions** before understanding problem deeply
❌ **Vague metrics** like "improve user satisfaction" without specifics
❌ **Missing non-goals** which causes scope creep later
❌ **Over-specification** that limits implementation creativity
❌ **Single-audience writing** when PRD serves multiple teams
❌ **Treating as static** when it should evolve with learning

### Quality Checks Before Finalizing
- [ ] Problem statement includes evidence (not opinions)
- [ ] Success metrics are specific, measurable, with timeframes
- [ ] Scope defines what's in AND what's explicitly out
- [ ] Requirements are prioritized (use MoSCoW)
- [ ] Technical feasibility validated with engineering
- [ ] Each stakeholder group can understand their relevant sections
- [ ] Document includes change log for version tracking

## Reference Materials

This skill includes comprehensive reference files:

### [prd-sections.md](references/prd-sections.md)
Complete guide to every PRD section: core sections (always include), feature definition sections (adjust by type), and optional sections (include when relevant). Covers purpose, content, and best practices for each.

**Read when**: Drafting any specific section, need detailed guidance on what to include

### [prd-examples.md](references/prd-examples.md)
Concrete examples of well-written PRD content: executive summaries, problem statements, personas, success metrics, features, technical requirements, scope definitions, and more.

**Read when**: Want to see what good looks like, need inspiration for structure or phrasing

### [prd-frameworks.md](references/prd-frameworks.md)
Different PRD approaches with detailed patterns: Amazon PR/FAQ (customer-centric), Lean One-Pager (agile teams), Comprehensive PRD (complex projects), Jobs-to-be-Done (user research driven), Shape Up Pitch (constrained autonomy). Includes when to use each and how to adapt patterns.

**Read when**: Selecting PRD structure, want to understand different company approaches

## Workflow Summary

1. **Understand** → Ask discovery questions about project type, audience, context, constraints
2. **Structure** → Recommend framework and sections based on project needs (read frameworks.md)
3. **Co-author** → Work through sections iteratively (read sections.md and examples.md)
   - Explain purpose
   - Ask targeted questions
   - Draft content
   - Get feedback
   - Refine
4. **Review** → Check completeness, consistency, clarity, best practices
5. **Refine** → Iterate based on review until PRD is ready

**Remember**: PRDs are living documents. Ship a good PRD and iterate rather than pursuing perfection. The goal is alignment and clarity, not exhaustive documentation.
