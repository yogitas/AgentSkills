# PRD Section Reference Guide

This reference provides detailed guidance for each PRD section. Read the sections relevant to your PRD type.

## Core Sections (Always Include)

### Executive Summary / Overview
**Purpose**: One-page overview that busy stakeholders can read to understand the project
**Content**:
- Product/feature name and brief description (1-2 sentences)
- Core problem being solved
- Primary solution approach
- Key success metrics (2-3 max)
- Target launch timeframe
**Best practices**:
- Write this LAST after all other sections are complete
- Keep to maximum 200 words
- Make it scannable - use bullet points
- Think "elevator pitch" not comprehensive overview

### Problem Statement
**Purpose**: Clearly articulate WHY this project exists
**Content**:
- Specific user problem or business opportunity
- Evidence from user research, data, support tickets
- Impact of NOT solving this problem
- Current workarounds users employ
**Best practices**:
- Ground in observable evidence, not assumptions
- Use Jobs-to-be-Done framework: "When [situation], I want to [motivation], so I can [expected outcome]"
- Avoid solution language - focus on the problem
- Include supporting data: "27 support tickets in Q3 report..."

### Target Audience / User Personas
**Purpose**: Define WHO this is for with specificity
**Content**:
- Primary persona: role, goals, pain points, behaviors
- Secondary personas (if applicable)
- User story format: "As a [role], I want [goal] so that [benefit]"
**Best practices**:
- Be specific and behavioral, not demographic: "Small marketing teams at early-stage startups who schedule social content weekly" not "marketers age 25-40"
- Validate with actual user research
- Include what they DON'T need (helps with scope)

### Success Metrics / KPIs
**Purpose**: Define measurable success criteria
**Content**:
- 2-3 key metrics aligned with product goals
- Baseline current state
- Target improvement with timeframe
- How metrics will be tracked/measured
**Best practices**:
- Pick metrics you can actually measure
- Include one business metric (revenue, conversion, retention)
- Include one usage metric (adoption, DAU, time spent)
- Include one quality metric (support tickets, NPS, error rates)
- Be specific: "Increase user satisfaction score from 6.2 to 7.5 within 3 months" not "improve user satisfaction"

### Scope: What's In / What's Out
**Purpose**: Set clear boundaries to prevent scope creep
**Content**:
- What IS included in this release
- What is explicitly NOT included (but may be future)
- Assumptions about what already exists
**Best practices**:
- Non-goals section prevents misunderstandings
- Be explicit about future vs. out-of-scope
- Document "good ideas for later" in Future Considerations

## Feature Definition Sections (Adjust by Type)

### Features & Requirements
**Purpose**: Define WHAT will be built
**Content**:
- Feature descriptions organized logically
- Prioritization (MoSCoW: Must/Should/Could/Won't)
- Acceptance criteria for each feature
- User flows and interactions
**Best practices**:
- For new products: comprehensive feature list with priorities
- For features: detailed breakdown of single feature
- For quality improvements: specific improvements, not features
- Use MoSCoW to enable trade-offs during development
- Link to wireframes/mockups when available

### User Stories / Use Cases
**Purpose**: Show how users will interact with the product
**Content**:
- Scenario-based descriptions
- Step-by-step user flows
- Edge cases and error states
**Best practices**:
- Format: "As a [user], I want to [action] so that [benefit]"
- Include happy path and error scenarios
- Keep focused on user goals, not UI implementation

### Technical Requirements
**Purpose**: Define technical constraints and specifications
**Content**:
- Performance requirements (load times, throughput)
- Security requirements
- Scalability needs
- Integration requirements
- Platform/browser support
**Best practices**:
- For new products: comprehensive technical architecture
- For features: integration points and dependencies only
- For quality improvements: performance benchmarks and targets
- Include non-functional requirements (reliability, maintainability)

## Optional Sections (Include When Relevant)

### Strategic Context / Business Justification
**When to include**: New products, major features, or when business case needs validation
**Content**:
- Market opportunity and competitive analysis
- Alignment with company OKRs/strategy
- Revenue potential or cost savings
- RICE score (Reach, Impact, Confidence, Effort)
**Skip for**: Small features, quality improvements, internal tools

### User Research & Validation
**When to include**: New products or features based on user insights
**Content**:
- Summary of user research conducted
- Key findings and quotes
- Journey mapping insights
- Pain points discovered
**Skip for**: Quality improvements, technical debt work

### Design / Wireframes
**When to include**: Features with significant UX changes
**Content**:
- Links to Figma/design files
- User flow diagrams
- Key interaction patterns
**Skip for**: Backend features, API work, quality improvements

### Implementation Plan / Timeline
**When to include**: Large projects requiring phased rollout
**Content**:
- Development phases/milestones
- Resource requirements
- Key dependencies and blockers
- Release plan and rollout strategy
**Skip for**: Small features that ship in one sprint

### Go-to-Market / Launch Strategy
**When to include**: Customer-facing features or new products
**Content**:
- Marketing approach
- User onboarding plan
- Communication strategy
- Training needs
**Skip for**: Internal tools, backend improvements, bug fixes

### Risks, Dependencies & Assumptions
**When to include**: Complex projects with significant unknowns
**Content**:
- Technical risks and mitigation strategies
- Cross-team dependencies
- Assumptions requiring validation
- Regulatory or compliance considerations
**Skip for**: Straightforward features with clear requirements

### Open Questions / Decisions Needed
**When to include**: Early-stage PRDs or complex projects
**Content**:
- Unresolved technical questions
- Design decisions pending
- Business decisions needed
- Research gaps
**Skip for**: Well-defined projects ready for development

## PRD Types: Section Selection Guide

### New Product PRD
**Include**:
- All Core Sections
- Strategic Context
- User Research
- Comprehensive Features & Requirements
- Technical Requirements (architecture)
- Implementation Plan
- Go-to-Market Strategy
- Risks & Dependencies

**Optional**: Design (if ready), Open Questions

### New Feature PRD
**Include**:
- All Core Sections
- Features & Requirements (detailed)
- User Stories
- Technical Requirements (integration focused)
- Design/Wireframes (if UX changes)

**Optional**: Strategic Context (if significant), Implementation Plan (if phased), GTM Strategy (if customer-facing), Risks

**Skip**: Comprehensive architecture (already exists)

### Quality Improvement / Performance PRD
**Include**:
- Executive Summary
- Problem Statement (focus on current issues/metrics)
- Success Metrics (performance benchmarks)
- Scope
- Technical Requirements (specific improvements)

**Optional**: User impact (if customer-facing), Implementation Plan (if complex rollout)

**Skip**: User personas (typically internal), Features list (not adding features), Design/wireframes, GTM Strategy

### Bug Fix / Technical Debt PRD
**Include**:
- Problem Statement (bug impact or tech debt consequences)
- Success Metrics (reduction in errors, improved performance)
- Scope
- Technical Requirements (fix approach)

**Skip**: Most other sections - keep it lean

## Writing Tips Across All Sections

1. **Lead with the problem**: Always establish "why" before "what"
2. **Use plain English**: Avoid jargon, acronyms without definition, and technical terminology unless necessary
3. **Make it scannable**: Headers, bullet points, bold for key information
4. **Link, don't duplicate**: Reference existing docs, don't copy them
5. **Version control**: Include change log for significant updates
6. **Seek input early**: Circulate draft for feedback before finalization
