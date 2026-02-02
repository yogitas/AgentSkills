# PRD Examples and Patterns

This reference provides concrete examples of well-written PRD sections.

## Executive Summary Examples

### Example 1: New Feature
```
# Smart Email Categorization for Gmail

## Executive Summary
Gmail users receive an average of 120 emails daily but lack an intelligent way to prioritize important messages. We're building an AI-powered categorization system that automatically identifies and surfaces high-priority emails, reducing inbox overwhelm.

**Core problem**: Users miss time-sensitive emails buried in high-volume inboxes
**Solution**: ML-based email prioritization with smart notifications
**Key metrics**: 
- Reduce "important email response time" from 4 hours to 1 hour
- Increase user-reported "inbox control" satisfaction from 3.2 to 4.5/5
**Timeline**: Q2 2026 launch
```

### Example 2: Quality Improvement
```
# Search Performance Optimization

## Executive Summary
Search response times have degraded to 1.2s average (up from 400ms), causing 15% of users to abandon searches before results load. This project optimizes our search infrastructure to restore sub-500ms response times.

**Problem**: Slow search is driving user abandonment
**Impact**: $2.3M annual revenue at risk from search abandonment
**Solution**: Database query optimization + caching layer
**Target**: <500ms response time for 95th percentile
**Timeline**: 6 weeks
```

## Problem Statement Examples

### Example 1: User-Centric Problem
```
## Problem Statement

Customer support leads at small companies spend 2-3 hours daily pulling reports from multiple tools (Zendesk, Intercom, Slack) just to understand team performance. Our user interviews with 15 support leads revealed:

- "I spend my mornings copy-pasting data into spreadsheets instead of coaching my team" (Sarah, Support Lead at Acme Corp)
- 27 support tickets in Q3 requesting "a dashboard to see team metrics"
- Session recordings show 89% of support leads visit 3+ tools during morning standup prep

**Impact of not solving**: Support leads lack real-time visibility into team performance, delaying intervention on underperforming agents and missing opportunities to recognize top performers. This directly impacts team morale and customer satisfaction scores.

**Current workaround**: Manual data aggregation in spreadsheets, updated weekly at best, often incomplete or outdated.
```

### Example 2: Business Problem
```
## Problem Statement

Our checkout completion rate dropped from 68% to 61% over the past quarter (Q4 2025), representing $4.2M in lost annual revenue. Analytics show:

- 23% of users abandon at payment information screen
- Average time-on-page increased from 45s to 2m 15s
- Mobile abandonment is 2.3x higher than desktop

User research (n=50) identified key pain points:
- "Too many form fields" (78% of respondents)
- "Don't trust entering credit card info" (45%)
- "Page took too long to load" (34%)

**Impact**: Every 1% improvement in checkout completion = $570K annual revenue
```

## Target Audience / Personas Examples

### Example 1: B2B Persona
```
## Target Audience

**Primary Persona: Small Team Support Lead**
- Role: Manager of 3-8 customer support agents at early-stage B2B SaaS companies
- Goals: Maintain response time SLAs, coach team effectively, identify training gaps
- Current behavior: Checks multiple dashboards 2-3x daily, exports data for weekly team meetings
- Pain points: No single view of team performance, relies on outdated weekly reports, can't spot issues until too late
- Tech comfort: High - uses 5+ SaaS tools daily
- Decision criteria: Must save at least 5 hours/week, integrate with existing tools, cost <$500/month

**User Story**: "As a support team lead, I want to see real-time team performance in one dashboard so that I can identify and address issues the same day they occur."

**Secondary Persona: Support Agent**
- Role: Individual contributor handling customer inquiries
- Use case: Self-service access to personal performance metrics
- Note: Solution must not feel like "big brother" monitoring
```

### Example 2: Consumer Persona
```
## Target Audience

**Primary Persona: Busy Parent Home Cook**
- Demographics: Parents with children under 12, working full-time
- Behaviors: 
  - Meal plans on weekends, cooks 5+ dinners/week
  - Shops for groceries 1-2x per week
  - Uses recipe apps but finds planning cumbersome
- Pain points:
  - "What's for dinner?" decision fatigue
  - Waste from ingredients bought but not used
  - Family members have different dietary preferences
- Goals: Reduce meal planning time, minimize food waste, accommodate picky eaters
- Tech savvy: Medium - comfortable with apps but won't troubleshoot

**User Story**: "As a working parent, I want meal suggestions based on what I already have so that I can reduce decision fatigue and food waste."

**Anti-persona** (explicitly out of scope):
- Professional chefs or culinary enthusiasts seeking complex recipes
- Single individuals or couples without children
```

## Success Metrics Examples

### Example 1: Feature Launch Metrics
```
## Success Metrics

**Primary Metrics** (measure within 30 days of launch):

1. **Feature Adoption**
   - Baseline: N/A (new feature)
   - Target: 40% of active users try smart categorization within first month
   - Measurement: Feature flag analytics + activation events

2. **User Engagement**
   - Baseline: Average 3.2 email app opens per day
   - Target: Increase to 4.5 opens per day for users with categorization enabled
   - Measurement: Daily active usage analytics

3. **Time to Important Email**
   - Baseline: 4 hours average response time to high-priority emails
   - Target: <1 hour for categorized emails
   - Measurement: Timestamp analysis (receipt → open → reply)

**Secondary Metrics** (track but not release blockers):
- User satisfaction: CSAT survey for feature, target 4.0+/5.0
- Categorization accuracy: User correction rate <15%

**Guardrail Metrics** (ensure we don't harm core experience):
- Overall email engagement must not decrease
- App performance: <100ms overhead for categorization
```

### Example 2: Performance Improvement Metrics
```
## Success Metrics

**Performance Targets** (measured over 7-day period post-release):

1. **Response Time**
   - Current: 1.2s average, 2.8s at p95, 4.5s at p99
   - Target: <500ms average, <1s at p95, <2s at p99
   - Measurement: Server-side latency monitoring

2. **Search Abandonment**
   - Current: 15% of searches abandoned before results load
   - Target: <5% abandonment rate
   - Measurement: Analytics event: search_initiated → no search_results_viewed

3. **User Satisfaction**
   - Current: 3.2/5 satisfaction with search
   - Target: >4.0/5
   - Measurement: In-app NPS survey to 10% of search users

**Impact Metrics** (business value, 30-day window):
- Conversion rate from search: expect 8% increase
- Search-to-purchase: expect $2.3M revenue recovery
```

## Features & Requirements Examples

### Example 1: MoSCoW Prioritization
```
## Features & Requirements

### MUST HAVE (MVP)
These features are critical for launch and solving the core problem:

**M1: Real-time Performance Dashboard**
- Display key metrics: response time, resolution rate, customer satisfaction
- Auto-refresh every 60 seconds
- Filter by agent, time range (today/week/month)
- Acceptance criteria:
  - Dashboard loads in <2s with full data
  - Metrics accurate within 5-minute lag
  - Mobile responsive design

**M2: Individual Agent View**
- Each agent sees their own performance metrics
- Comparison to team average (anonymized)
- Acceptance criteria:
  - Agents cannot see other agents' individual data
  - Privacy-preserving team averages shown
  - Opt-out option available

### SHOULD HAVE (Phase 2)
Important features that enhance value but not critical for MVP:

**S1: Trend Analysis**
- 7-day and 30-day trend graphs
- Anomaly detection and alerts
- Export to CSV

**S2: Integration with Slack**
- Daily performance summary posted to channel
- Alert notifications for SLA breaches

### COULD HAVE (Nice to have)
Features that add polish if time permits:

**C1: Custom Metric Builder**
- Allow leads to define custom KPIs
- Formula-based calculations

### WON'T HAVE (Explicitly out of scope)
Document to prevent scope creep:

**W1: Automated Coaching Recommendations**
- Future roadmap item, requires ML investment
**W2: Call Recording Analysis**
- Complex compliance requirements, defer to 2027
```

### Example 2: User Flow Based Requirements
```
## Features & Requirements

### Core Flow: Creating a Meal Plan

**Step 1: Inventory Input**
- User enters or scans ingredients they have
- System suggests items from past purchases (requires grocery integration)
- Dietary preferences applied (vegetarian, allergies, etc.)

**Step 2: Meal Suggestions**
- AI generates 3-5 dinner options using available ingredients
- Each suggestion shows:
  - Missing ingredients (if any)
  - Prep time
  - Difficulty level
  - Family rating (if previously cooked)
- User can regenerate suggestions or manually search recipes

**Step 3: Plan Confirmation**
- Drag-and-drop to assign meals to specific days
- Auto-generate shopping list for missing ingredients
- Save plan and receive daily reminder notifications

**Edge Cases**:
- No ingredients entered: Prompt with popular recipes
- All suggestions rejected: Offer recipe search or manual entry
- Dietary restrictions conflict: Clear error message with resolution path
```

## Technical Requirements Examples

### Example 1: New Feature Technical Specs
```
## Technical Requirements

### Integration Requirements
- Must integrate with existing Gmail API v1
- Use current OAuth 2.0 authentication flow
- Compatible with Google Workspace and consumer Gmail accounts

### Performance Requirements
- Email categorization: <100ms additional processing time
- Dashboard load time: <2s for up to 10,000 emails
- Background sync: Updates every 5 minutes without blocking UI

### Data & Privacy
- Store categorization metadata only (no email content)
- GDPR compliant: User can export/delete all categorization data
- Encryption: TLS 1.3 for data in transit, AES-256 at rest

### Scalability
- Support 100M daily active users at launch
- Auto-scaling to handle 10x traffic spikes
- 99.9% uptime SLA

### Browser Support
- Chrome/Edge: Last 2 versions
- Safari: Last 2 versions
- Firefox: Last 2 versions
- Mobile: iOS 15+, Android 11+
```

### Example 2: Performance Improvement Specs
```
## Technical Requirements

### Current State Analysis
- Database: PostgreSQL 13, single primary with 2 read replicas
- Current bottleneck: N+1 query pattern in product search (avg 47 queries per search)
- Infrastructure: AWS EC2 t3.large instances, no caching layer

### Proposed Improvements

**Database Optimization**
- Implement query result caching with Redis (TTL: 5 minutes)
- Add composite index on (category_id, price, created_at)
- Batch database queries to eliminate N+1 pattern
- Expected impact: Reduce query time from 800ms to <100ms

**Application Layer**
- Implement GraphQL DataLoader for batched fetching
- Add CDN caching for product images
- Lazy load non-critical data (reviews, related products)
- Expected impact: Reduce initial page load from 2.3s to <1s

**Infrastructure**
- Upgrade to c5.xlarge instances (CPU optimized)
- Add ElasticSearch cluster for search queries
- Implement auto-scaling based on request rate
- Expected impact: Handle 10x current traffic with <500ms response

### Rollout Strategy
- Phase 1: Database optimizations (Week 1-2)
- Phase 2: Application layer changes (Week 3-4)
- Phase 3: Infrastructure upgrades (Week 5-6)
- Dark launch to 10% traffic, monitor for 48 hours before full rollout
```

## Scope Examples

### Example 1: Clear Boundaries
```
## Scope

### In Scope for V1 Launch (Q2 2026)
✅ Email categorization for Gmail (web and mobile app)
✅ Smart notifications for high-priority emails
✅ User-configurable priority rules
✅ Integration with Google Calendar for meeting-related emails
✅ Export categorization data

### Explicitly Out of Scope
❌ Outlook/Exchange support → Planned for Q4 2026
❌ Email summarization → Requires LLM integration, Q3 2026
❌ Automatic email replies → Deferred pending user research
❌ Corporate/enterprise accounts → Different privacy model needed

### Assumptions
- Users have granted Gmail API permissions
- Google Workspace APIs remain stable during development
- Email volume <10,000 emails per user (handle gracefully but deprioritize optimization for >10K)

### Future Considerations (Ideas for Later)
- AI-powered email drafting assistance
- Team-level categorization rules for organizations
- Third-party email client integration (Superhuman, Spark)
```

## Open Questions Example

```
## Open Questions & Decisions Needed

**Technical Decisions**:
1. **ML Model Deployment**: Cloud-based or on-device categorization?
   - Cloud: More accurate but privacy concerns, requires internet
   - On-device: Privacy-first but limited model complexity
   - **Decision needed by**: March 15 (architecture freeze)
   - **Owner**: Engineering Lead

2. **Data Retention**: How long to store categorization history?
   - Option A: 90 days (GDPR minimum)
   - Option B: Indefinite with user control
   - **Decision needed by**: March 20 (database design)
   - **Owner**: Privacy/Legal + Product

**Design Decisions**:
3. **Notification Strategy**: Push, in-app, or email digest?
   - Requires A/B test to determine user preference
   - **Test planned**: Week of March 25
   - **Owner**: Design Lead

**Business Decisions**:
4. **Freemium vs Premium**: Categorization free or paid feature?
   - Impacts GTM strategy and development priorities
   - **Decision needed by**: April 1 (pricing finalization)
   - **Owner**: Product Lead + Business Team

**Research Gaps**:
5. **Accuracy Threshold**: What categorization accuracy is "good enough"?
   - Plan user testing with 85%, 90%, 95% accuracy variants
   - **Research scheduled**: April 1-15
   - **Owner**: UX Research
```
