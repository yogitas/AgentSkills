# PRD Framework Patterns

Different companies use different PRD approaches. This reference describes major patterns to help choose the right approach.

## Amazon PR/FAQ Pattern

**Best for**: Customer-facing products where customer value must be crystal clear

**Structure**:
1. **Press Release** (1 page max)
   - Product name and brief description
   - Problem it solves from customer perspective
   - Key benefits in plain language (no jargon)
   - Customer quote (fictional but realistic)
   - How to get started

2. **FAQ** (2-5 pages)
   - External FAQ: Customer questions (pricing, features, availability)
   - Internal FAQ: Business questions (market size, revenue model, risks)

**When to use**:
- New products or major features
- Need forcing function for customer-centric thinking
- Have tendency to build "cool tech" without clear user value

**Key principle**: If you can't write a compelling press release, you don't understand the customer value

**Example Opening**:
```
FOR IMMEDIATE RELEASE

Acme Corp Announces SmartCart: AI-Powered Grocery Shopping That Saves Families $200/Month

Revolutionary meal planning and shopping app eliminates food waste while simplifying dinner decisions for busy parents

SEATTLE - June 1, 2026 - Acme Corp today announced SmartCart, an intelligent grocery shopping assistant that transforms how families plan meals and shop for groceries. SmartCart uses artificial intelligence to suggest meals based on ingredients families already have, automatically generate shopping lists, and track family food preferences - helping the average family save $200 per month in reduced food waste.

"Before SmartCart, I spent Sunday mornings planning meals and making shopping lists. Now it takes 10 minutes, and we waste so much less food," said Maria Rodriguez, a working mother of three and SmartCart beta tester. "It's like having a personal chef who knows my family's tastes and what's in my pantry."

SmartCart solves three major pain points for busy families...
```

## Lean One-Pager Pattern (Lenny's / Intercom)

**Best for**: Fast-moving teams, features (not full products), iterative development

**Structure** (fits on 1-2 pages):
1. **Problem** (2-3 sentences)
2. **Solution** (2-3 sentences)  
3. **Why Now** (timing/urgency)
4. **Success Metrics** (2-3 metrics)
5. **Scope** (what's in/out)
6. **Open Questions**

**When to use**:
- Small to medium features
- Need quick alignment without lengthy documents
- Team culture values brevity over comprehensiveness
- Agile environment with continuous iteration

**Key principle**: Minimum documentation needed for alignment, maximum room for adaptation

**Example**:
```
# One-Click Social Media Scheduling

**Problem**: Small marketing teams waste 2+ hours weekly scheduling social posts across platforms, copying content between tools.

**Solution**: One-click "use template" button that pre-fills posts for the week based on saved templates, auto-scheduling across all connected platforms.

**Why Now**: Q1 survey shows this is #2 requested feature (124 requests). Competitive gap - none of our competitors offer template-based bulk scheduling.

**Success Metrics**:
- 60% of teams with templates enabled use feature weekly
- 30% reduction in time-to-schedule reported in follow-up survey
- <5% support ticket rate

**In Scope**: Template creation, bulk scheduling, Facebook/Twitter/LinkedIn
**Out of Scope**: Instagram (API limitations), video content, analytics

**Open Questions**:
- Should templates support dynamic content (dates, names)? Testing in prototype.
- Pricing: Free or premium tier? Need business decision by March 15.
```

## Comprehensive PRD Pattern (Google / Microsoft)

**Best for**: Complex products, large organizations, regulated industries, need for detailed documentation

**Structure** (typically 10-20 pages):
1. Metadata (owner, status, version)
2. Executive Summary
3. Background & Strategic Context
4. Problem Statement with Research
5. User Personas (detailed)
6. Goals & Success Metrics
7. User Stories & Use Cases
8. Features & Requirements (comprehensive)
9. Technical Architecture
10. Design/Wireframes
11. Dependencies & Risks
12. Implementation Plan
13. Go-to-Market Strategy
14. Appendices

**When to use**:
- New product launch
- Large cross-functional teams
- Need stakeholder sign-offs
- Regulatory compliance required
- Complex technical architecture

**Key principle**: Comprehensive documentation upfront reduces ambiguity during execution

## Jobs-to-be-Done (JTBD) Pattern

**Best for**: User-centric products, when solving for specific moments/contexts

**Structure**:
1. **Job Statement**: "When [situation], I want to [motivation], so I can [outcome]"
2. **Current Alternatives**: How users solve this today
3. **Pain Points**: Why current alternatives fail
4. **Proposed Solution**: How product addresses the job
5. **Success Criteria**: How to know we've done the job well

**When to use**:
- Need to deeply understand user motivation
- Multiple user segments with different "jobs"
- Replacing existing solutions

**Example**:
```
## Job to Be Done

**Job Statement**: When I'm at the grocery store trying to decide what to buy for the week, I want to quickly recall what meals I can make with ingredients I already have, so I can avoid buying duplicates and reduce food waste.

**Current Alternatives**:
- Mental recall (often inaccurate, leads to duplicate purchases)
- Handwritten lists at home (frequently forgotten)
- Checking pantry photos on phone (time-consuming, incomplete)
- Recipe apps (don't account for existing inventory)

**Why Alternatives Fail**:
- Can't remember what's in pantry while shopping (78% of users)
- Pre-made lists don't adapt to store availability
- No way to verify if item is truly needed

**Proposed Solution**: Real-time inventory tracking with smart shopping list that shows:
- What you have vs what recipe needs
- Suggested substitutions
- Visual verification (photo of pantry state)

**Success Criteria**:
- Users report feeling "confident" about purchases (survey >4/5)
- Duplicate purchases reduced 50%
- Food waste reduced (self-reported or trash audit)
```

## Shape Up Pitch Pattern (Basecamp)

**Best for**: Teams that want to give builders freedom, avoid over-specification

**Structure**:
1. **Problem**: Raw idea or use case
2. **Appetite**: Time budget (6 weeks, 2 weeks, etc.)
3. **Solution**: Rough approach, not detailed spec
4. **Rabbit Holes**: Known risks to avoid
5. **No-Gos**: Explicitly out of scope

**When to use**:
- Experienced teams that can figure out details
- Want to constrain time, not prescribe solution
- Design and engineering should collaborate on specifics

**Key principle**: Define the boundaries and constraints, let the team solve the problem creatively within them

**Example**:
```
# Smart Notification Batching

**Problem**: Users get 20+ notifications per day from our app, causing notification fatigue. They either mute all notifications (and miss important ones) or tolerate the spam.

**Appetite**: 2 weeks

**Solution** (sketch, not spec):
Batch non-urgent notifications and deliver as a single daily digest. Truly urgent notifications (payment issues, security) still deliver immediately. User controls:
- When to receive digest (morning, evening)
- What counts as "urgent"
- Opt-out per notification type

**Rabbit Holes** (avoid these):
- Don't build complex ML urgency detection - use simple rules
- Don't create custom digest UI - use system notification
- Don't integrate with all 15 notification types - start with 5 most common

**No-Gos**:
- No email digest (this is in-app only)
- No AI summarization (future feature)
- No retroactive analysis of past notifications

**Deliverable**: Working feature in beta, tested with 100 users, metrics showing notification volume reduction.
```

## Choosing the Right Pattern

**Use Amazon PR/FAQ when**:
- Building customer-facing products
- Need to validate customer value proposition
- Team has tendency to build for internal use cases

**Use Lean One-Pager when**:
- Adding feature to existing product
- Fast iteration cycle
- Small, aligned team
- Minimal cross-functional dependencies

**Use Comprehensive PRD when**:
- New product launch
- Many stakeholders need alignment
- Regulatory or compliance requirements
- Complex technical architecture
- Need executive approval

**Use JTBD Pattern when**:
- User research shows specific contextual needs
- Replacing existing user behaviors
- Multiple user segments with different motivations

**Use Shape Up Pitch when**:
- Team has design/engineering expertise
- Want to give builders autonomy
- Have fixed time budget, flexible scope
- Problem is clear but solution needs iteration

## Adapting Patterns

**You don't need to choose just one pattern**. Effective PRDs often combine elements:

- Start with JTBD to understand the problem
- Use Lean One-Pager structure for internal alignment
- Include Amazon PR/FAQ customer section for customer-facing features
- Add Comprehensive PRD technical sections when complexity requires it
- Use Shape Up's "Rabbit Holes" to document known risks

**The right pattern depends on**:
- Company culture and norms
- Product complexity
- Team size and distribution
- Regulatory environment
- Stage (startup vs enterprise)
