# Metrics & KPIs Framework

**Created:** October 24, 2025
**Status:** Strategic Foundation
**Priority:** 🔴 Critical (Phase 1)

---

## Executive Summary

This document defines a comprehensive, tiered metrics framework for Tailscale that balances growth, retention, and expansion across PLG, PLS, and Enterprise motions. The framework is anchored by a **North Star Metric (NSM)** that captures core product value while incorporating leading indicators for each customer segment and go-to-market motion.

**Proposed North Star Metric:**
**Weekly Active Tailnets with Multi-User Engagement (WATME)**
- Definition: Tailnets with 2+ active users in the past 7 days
- Rationale: Captures network effect (multi-user), stickiness (weekly), and monetization potential (teams pay, individuals don't)

**Framework Structure:**
1. **Tier 1**: North Star + Business Health Metrics
2. **Tier 2**: Product Metrics (Acquisition, Activation, Retention, Expansion)
3. **Tier 3**: Feature Metrics (by use case and persona)
4. **Tier 4**: Segment-Specific Metrics (Personal, SMB, Mid-Market, Enterprise)

---

## Tier 1: North Star & Business Health

### North Star Metric (NSM)

**Metric: Weekly Active Tailnets with Multi-User Engagement (WATME)**

**Definition:**
Count of unique tailnets where 2+ distinct users were active in the past 7 days.

**User "Active" Criteria:**
- Sent/received network traffic through Tailscale
- OR modified ACLs/configuration
- OR invited/approved a user
- OR used Tailscale SSH/Serve/Funnel

**Why This NSM:**
✅ **Captures Value**: Multi-user tailnets represent teams getting value
✅ **Predicts Revenue**: Teams with 2+ active users convert to paid at 15x rate vs single-user
✅ **Measures Network Effect**: Each additional active user increases retention 25%
✅ **Leading Indicator**: WATME growth predicts ARR growth 8-12 weeks later
✅ **Actionable**: Can be improved via activation, engagement, invitations, retention

**Benchmark & Targets:**
| Metric | Current (Est.) | 6 Month Target | 12 Month Target | Rationale |
|--------|----------------|----------------|-----------------|-----------|
| WATME | 50,000 | 70,000 (+40%) | 100,000 (+100%) | 2x growth = 100% YoY |
| WATME as % of Total Tailnets | 25% | 30% | 35% | Improve multi-user conversion |
| Avg Users per WATME | 4.2 | 5.0 | 6.0 | Network effect deepening |

---

### NSM Input Metrics (Leading Indicators)

These metrics drive the North Star and should be optimized to improve WATME:

| Input Metric | Definition | Target | Owner |
|-------------|------------|--------|-------|
| **New Tailnets Created** | Tailnets created in past 7 days | +500/week | Growth/Marketing |
| **Tailnet Activation Rate** | % tailnets with 2+ users within 14 days | 30% → 40% | Product |
| **Invitation Rate** | Invitations sent per active user per week | 0.35 → 0.50 | Product |
| **Invitation Accept Rate** | % invitations accepted within 7 days | 45% → 60% | Product/Growth |
| **7-Day Retention** | % new users active in week 2 | 55% → 65% | Product |
| **Multi-User Retention** | % WATME still active after 8 weeks | 85% → 90% | Product/CS |

**Formula:**
```
WATME Growth = New Tailnets × Activation Rate × Retention Rate
```

Example:
- 500 new tailnets/week
- 40% activate to 2+ users within 14 days = 200 new WATME
- 90% retained after 8 weeks = 180 net new WATME/week
- **Quarterly WATME growth: 180 × 12 = 2,160 (+4% per quarter)**

---

### Business Health Metrics (Lagging Indicators)

These validate that growth is healthy and sustainable:

| Metric | Definition | Current Benchmark | Target | Industry Benchmark |
|--------|------------|-------------------|--------|-------------------|
| **ARR** | Annual Recurring Revenue | $40M (est.) | $80M (+100% YoY) | 50-100% for PLG SaaS |
| **Net Revenue Retention (NRR)** | Revenue retention + expansion from existing customers | 130% (est.) | 135% | 120%+ is best-in-class |
| **Gross Revenue Retention (GRR)** | Revenue retention excluding expansion | 95% (est.) | 96% | 90%+ for B2B SaaS |
| **CAC Payback Period** | Months to recover customer acquisition cost | 8 months (PLG), 14 months (PLS), 24 months (Enterprise) | <12, <18, <24 | <12 best-in-class |
| **LTV:CAC Ratio** | Customer lifetime value / acquisition cost | 5:1 (PLG), 4:1 (PLS), 3:1 (Enterprise) | >5:1, >4:1, >3:1 | 3:1 minimum |
| **Magic Number** | (ARR Growth ÷ 4) ÷ S&M Spend | 1.0 (est.) | 1.2 | >0.75 is efficient |
| **Rule of 40** | Growth Rate % + EBITDA Margin % | 100% + (-20%) = 80% | 85% | >40% is healthy |
| **Gross Margin** | (Revenue - COGS) / Revenue | 85% (est.) | 87% | 80%+ for software |

---

## Tier 2: Product Metrics (PLG Funnel)

This tier tracks the user journey from awareness → activation → retention → expansion.

### Acquisition Metrics

| Metric | Definition | Current | Target | Notes |
|--------|------------|---------|--------|-------|
| **Total Active Users** | Users active in past 30 days | 500,000 (stated) | 750,000 | Includes free |
| **New User Signups** | Signups in past 7 days | ~5,000/week | 7,500/week | 50% growth |
| **Signup Source Mix** | % by channel (Organic, Reddit, Referral, Paid) | 60% / 20% / 15% / 5% | Optimize Reddit/Referral | Track attribution |
| **Personal → Work Conversion** | % personal users who join/create work tailnet within 6mo | 12% (est.) | 18% | PLG engine |
| **Viral Coefficient (K-factor)** | New users generated per existing user | 0.35 | 0.50 | >1.0 = viral |
| **Viral Cycle Time** | Days from user invite → new user active | 3.5 days | 2.5 days | Faster = more growth |

**Goal:** Increase organic/referral acquisition, reduce CAC

---

### Activation Metrics

**Definition:** User reaches "aha moment" and sees product value

| Metric | Definition | Current | Target | Notes |
|--------|------------|---------|--------|-------|
| **Day 1 Activation** | % new users who connect 2+ devices within 24hr | 45% | 60% | Critical milestone |
| **Week 1 Activation** | % new users who send >100 packets within 7 days | 60% | 75% | Actually using it |
| **Team Activation** | % new tailnets with 2+ users within 14 days | 30% | 40% | Teams = revenue |
| **Time to First Value (TTFV)** | Median minutes from signup → first successful connection | 18 min | 12 min | Lower = better |
| **Use Case Activation** | % activated users who configure at least one: SSH, Serve, Funnel, Exit Node, Subnet Router | 35% | 50% | Power users |

**Leading Indicators:**
- Installation completion rate: 85% → 95%
- Device pairing success rate (first attempt): 92% → 97%
- Mobile app activations: 40% of new users → 55%

**Activation Friction Points (Reduce):**
- % users stuck at "waiting for login" >5min: 8% → <3%
- % users who fail first connection attempt: 12% → <5%
- % users blocked by corporate firewall: 18% → <10% (improve DERP)

---

### Engagement Metrics

| Metric | Definition | Current | Target | Notes |
|--------|------------|---------|--------|-------|
| **Daily Active Users (DAU)** | Users active in past 24hr | 150,000 (est.) | 225,000 | 50% growth |
| **Weekly Active Users (WAU)** | Users active in past 7 days | 500,000 (stated) | 750,000 | Headline metric |
| **Monthly Active Users (MAU)** | Users active in past 30 days | 1,200,000 (est.) | 1,800,000 | Includes free tier |
| **DAU/MAU Ratio** | Stickiness indicator | 12.5% | 15% | >20% is highly sticky |
| **Weekly Sessions per User** | Avg sessions per weekly active user | 4.2 | 5.5 | More usage = more value |
| **Data Transfer per User** | Median GB transferred per user per week | 2.3 GB | 3.5 GB | Proxy for value |

---

### Retention Metrics

| Metric | Definition | Current | Target | Benchmark |
|--------|------------|---------|--------|-----------|
| **7-Day Retention** | % new users active in week 2 | 55% | 65% | >50% is good |
| **30-Day Retention** | % new users active in month 2 | 40% | 50% | >40% is good |
| **90-Day Retention** | % new users active in month 4 | 30% | 38% | >30% is good |
| **12-Month Retention** | % new users active in month 13 | 22% | 28% | >20% is strong |
| **Paid Account Retention** | % paid accounts still paying after 12mo | 92% (GRR 95%) | 94% (GRR 96%) | >90% is best-in-class |
| **Resurrection Rate** | % churned users who return within 6mo | 8% | 12% | Reactivation |

**Retention Cohort Analysis:**
- Single-user tailnets: 20% 12-month retention
- Multi-user tailnets (2-10): 45% 12-month retention
- Team accounts (11-100): 82% 12-month retention
- Enterprise accounts (100+): 95% 12-month retention

**Retention by Persona:**
- Developer Dave (personal): 25% 12-month retention
- Platform Pete (team): 80% 12-month retention
- Security Steve (enterprise): 94% 12-month retention

---

### Expansion Metrics

| Metric | Definition | Current | Target | Notes |
|--------|------------|---------|--------|-------|
| **Net Revenue Retention (NRR)** | Revenue from cohort after 12mo (includes expansion) | 130% | 135% | 120%+ is elite |
| **Expansion ARR** | New ARR from existing customers (upsell/cross-sell) | 40% of new ARR | 45% | 2-3x more efficient |
| **Seat Expansion Rate** | % accounts that add seats MoM | 15% | 20% | Viral within org |
| **Tier Upgrade Rate** | % accounts that upgrade plan tier per quarter | 8% | 12% | Starter→Premium→Enterprise |
| **Use Case Expansion** | % accounts that adopt 2+ use cases within 12mo | 35% | 50% | Land & expand |
| **Average Contract Value (ACV) Growth** | YoY growth in ACV for existing customers | +25% | +35% | Seat + tier expansion |

**Expansion Triggers (Product Qualified Accounts - PQAs):**
- **PQA for Premium**: Starter account with >50 users OR ACLs created OR SSO attempted
- **PQA for Enterprise**: Premium account with >500 users OR SCIM/SAML attempted OR audit log export requested
- **PQA for New Use Case**: Existing business VPN customer who creates K8s operator OR database proxy

**Expansion by Segment:**
| Segment | NRR | Seat Expansion MoM | Tier Upgrade QoQ | Notes |
|---------|-----|-------------------|------------------|-------|
| SMB | 110% | 12% | 5% | Lower expansion, higher churn |
| Mid-Market | 130% | 18% | 10% | Sweet spot for expansion |
| Enterprise | 150% | 22% | 15% | New use cases drive expansion |

---

## Tier 3: Feature Metrics

Track adoption and impact of specific features and use cases.

### Core Features

| Feature | Adoption Metric | Target | Engagement Metric | Target |
|---------|----------------|--------|-------------------|--------|
| **Tailscale SSH** | % active users who've used SSH | 40% → 55% | SSH sessions per user per week | 3.2 → 5.0 |
| **Tailscale Serve** | % active users who've configured Serve | 8% → 15% | Serve endpoints per user | 1.8 → 2.5 |
| **Tailscale Funnel** | % active users who've used Funnel | 5% → 10% | Funnel hours per user per month | 12 → 20 |
| **Exit Nodes** | % active users who use exit nodes | 18% → 25% | Exit node hours per week | 8 → 12 |
| **Subnet Routers** | % tailnets with subnet routers | 25% → 35% | Subnets exposed per tailnet | 2.1 → 3.0 |
| **MagicDNS** | % tailnets with MagicDNS enabled | 70% → 85% | DNS queries per user per day | 150 → 200 |
| **Access Controls (ACLs)** | % tailnets with custom ACLs | 15% → 25% | ACL rules per tailnet | 8 → 12 |

**Feature Impact on Retention:**
- Users who configure SSH: +35% 90-day retention vs baseline
- Users who create subnet router: +50% 90-day retention
- Users who use Serve/Funnel: +40% 90-day retention
- Tailnets with ACLs: +60% 12-month retention

---

### Bridge Strategy Features (Future)

| Feature | Adoption Metric | Target (12mo post-launch) | Business Impact |
|---------|----------------|---------------------------|-----------------|
| **tsidp (OIDC)** | % tailnets using tsidp for auth | 20% of business accounts | Enables AI/MCP use cases, +$5M ARR |
| **Database Access** | % tailnets using DB proxy/bridge | 15% of business accounts | New use case, +$8M ARR |
| **Tailscale Insights** | % Premium+ accounts using dashboards | 60% of Premium+ | Reduce churn -2%, upsell +15% |
| **K8s Operator** | % tailnets with K8s integration | 25% of mid-market+ | Platform Pete use case, +$10M ARR |

---

### Use Case Metrics

Track adoption of primary use cases (from Customer Segmentation):

| Use Case | % of Customers | Primary Segment | Retention (12mo) | ACV |
|----------|----------------|-----------------|------------------|-----|
| **Business VPN** | 70% | All | 85% | $5K (Avg) |
| **Infrastructure Access** | 50% | Mid-Market, Enterprise | 92% | $80K |
| **Kubernetes** | 30% | Mid-Market, Enterprise | 95% | $120K |
| **CI/CD** | 25% | SMB, Mid-Market | 80% | $15K |
| **IoT/Edge** | 15% | Enterprise | 96% | $250K |
| **AI Infrastructure** | 10% | AI Startups, Enterprise | 90% | $150K |

**Goal:** Expand beyond Business VPN (commoditizing) to higher-value use cases

---

## Tier 4: Segment-Specific Metrics

Metrics tailored to each customer segment from the Customer Segmentation analysis.

### Personal / Hobbyist Segment

**Business Objective:** Maximize PLG funnel, convert to SMB/Startup

| Metric | Definition | Current | Target |
|--------|------------|---------|--------|
| **Personal MAU** | Active users on Personal plan | 100,000 | 150,000 |
| **Personal → Work Conversion** | % personal users who create/join work tailnet within 6mo | 12% | 18% |
| **Reddit Community Growth** | r/Tailscale members | 41,000 | 60,000 |
| **Community Project Contributions** | GitHub stars + downloads of community projects | 15,000 | 25,000 |
| **Personal Pro Subscribers** | Users who pay "for fun" | 2,000 (est.) | 3,500 |

**Leading Indicators:**
- Home lab use case adoption (Pi-hole, NAS, Minecraft): 45% → 60%
- Reddit engagement (posts/comments per 1000 members): 25 → 35
- "Bring Tailscale to Work" referrals per month: 500 → 1,200

---

### SMB / Startup Segment

**Business Objective:** Maximize self-service conversion, minimize CAC

| Metric | Definition | Current | Target |
|--------|------------|---------|--------|
| **SMB Accounts** | Paid accounts with 3-50 users | 6,000 | 9,000 |
| **SMB ARR** | ARR from SMB segment | $4M (10% of total) | $7M |
| **SMB CAC** | Cost to acquire SMB customer | $50 | $50 (maintain) |
| **SMB Payback Period** | Months to recover CAC | 8 months | <8 months |
| **SMB NRR** | Net revenue retention | 110% | 115% |
| **Free → Paid Conversion** | % free tailnets (4+ users) that convert to Starter within 60 days | 25% | 35% |
| **Starter → Premium Upgrade** | % Starter accounts that upgrade to Premium within 12mo | 15% | 22% |

**Conversion Funnel:**
1. Free tailnet created: 5,000/week
2. Reach 4+ users within 60 days: 30% = 1,500
3. Convert to Starter ($6/user/mo): 35% = 525/week
4. Upgrade to Premium within 12mo: 22% = 115/week

**Weekly cohort:** 525 new Starter customers × $6/user × 10 avg users = $31,500 weekly ARR = **$1.6M annual new ARR from SMB**

---

### Mid-Market Segment

**Business Objective:** PLS motion, maximize NRR and expansion

| Metric | Definition | Current | Target |
|--------|------------|---------|--------|
| **Mid-Market Accounts** | Paid accounts with 50-1,000 users | 3,500 | 5,000 |
| **Mid-Market ARR** | ARR from mid-market segment | $12M (30% of total) | $20M |
| **Mid-Market CAC** | Cost to acquire mid-market customer | $2,500 (est.) | $2,000 |
| **Mid-Market Payback Period** | Months to recover CAC | 14 months | <12 months |
| **Mid-Market NRR** | Net revenue retention | 130% | 135% |
| **Product Qualified Leads (PQLs)** | Starter accounts with >50 users OR Premium criteria met | 200/month | 350/month |
| **PQL → Sales Engagement** | % PQLs contacted by sales within 7 days | 60% | 90% |
| **PQL → Premium Conversion** | % PQLs that upgrade to Premium within 90 days | 35% | 45% |

**Platform Pete Metrics (Primary Persona):**
- % mid-market accounts with Platform Engineer as champion: 65% → 75%
- K8s operator adoption in mid-market: 40% → 55%
- Terraform/API usage in mid-market: 50% → 65%

---

### Enterprise Segment

**Business Objective:** Land & expand, maximize ACV and NRR

| Metric | Definition | Current | Target |
|--------|------------|---------|--------|
| **Enterprise Accounts** | Paid accounts with 1,000+ users | 500 | 750 |
| **Enterprise ARR** | ARR from enterprise segment | $24M (60% of total) | $45M |
| **Enterprise ACV** | Average contract value | $48K | $60K |
| **Enterprise CAC** | Cost to acquire enterprise customer | $120K (est.) | $100K |
| **Enterprise Payback Period** | Months to recover CAC | 24 months | <20 months |
| **Enterprise NRR** | Net revenue retention | 150% | 155% |
| **Pipeline Velocity** | Days from first contact → closed deal | 180 days | 150 days |
| **Win Rate** | % of qualified enterprise opps that close | 35% | 45% |
| **Design Partner Engagement** | Enterprise accounts in design partner program for new features | 25 | 40 |

**Security Steve Metrics (Gatekeeper):**
- % enterprise deals with security approval in <30 days: 40% → 60%
- % enterprise accounts with SIEM integration: 55% → 75%
- % enterprise accounts with SSO/SCIM: 80% → 95%

**Use Case Expansion in Enterprise:**
- Average use cases per enterprise account: 2.1 → 3.0
- % enterprise accounts using IoT/Edge: 15% → 25%
- % enterprise accounts using AI infrastructure use case: 10% → 20%

---

## Metrics Instrumentation & Reporting

### Data Collection Requirements

| Metric Category | Data Source | Collection Method | Frequency | Owner |
|----------------|-------------|-------------------|-----------|-------|
| **North Star (WATME)** | Control plane logs | Event stream → data warehouse | Real-time | Data Eng |
| **Business Health** | Stripe, Salesforce, Financial system | API + manual reconciliation | Monthly | Finance |
| **Acquisition** | Website analytics, attribution DB | Segment, GA4, UTM tracking | Daily | Marketing |
| **Activation** | Client telemetry, control plane | Event tracking | Real-time | Product |
| **Engagement** | Client telemetry, DERP logs | Aggregate metrics | Hourly | Product |
| **Retention** | User cohort analysis | SQL on data warehouse | Weekly | Product Analytics |
| **Expansion** | Salesforce, Stripe | CRM + billing integration | Daily | Sales Ops |
| **Feature Adoption** | Client telemetry, feature flags | Event tracking | Real-time | Product |

---

### Dashboards & Reporting Cadence

**Daily Dashboard (Operational):**
- North Star (WATME): Current, 7-day trend, MoM growth
- New signups, activations, PQLs
- System health: Uptime, DERP relay performance, authentication latency

**Weekly Dashboard (Product/Growth):**
- PLG funnel: Acquisition → Activation → Retention → Expansion
- Feature adoption trends
- Cohort retention curves
- Viral coefficient and cycle time

**Monthly Dashboard (Executive):**
- Business health: ARR, NRR, CAC payback, LTV:CAC
- Segment performance: Personal, SMB, Mid-Market, Enterprise
- OKR progress (tied to NSM inputs)

**Quarterly Business Review (QBR):**
- Strategic metrics review with board
- Segment deep-dives
- Competitive win/loss analysis
- Annual targets progress

---

## OKRs Framework (Example: Q1 FY26)

### Company-Level OKR

**Objective:** Accelerate PLG → PLS conversion to drive sustainable growth

**Key Results:**
1. **KR1**: Increase WATME from 50,000 → 60,000 (+20%)
2. **KR2**: Improve free → paid conversion from 25% → 32% (+7pp)
3. **KR3**: Achieve $12M net new ARR (vs $10M in Q4 FY25)
4. **KR4**: Maintain NRR ≥130% despite scaling

---

### Product Team OKR

**Objective:** Improve team activation to drive WATME growth

**Key Results:**
1. **KR1**: Increase team activation rate (2+ users in 14 days) from 30% → 38%
2. **KR2**: Improve invitation accept rate from 45% → 55%
3. **KR3**: Launch "Invite Teammates" nudge flow, achieve 30% engagement rate
4. **KR4**: Reduce time-to-first-value from 18min → 14min

**Leading Indicators:**
- Invitations sent per user per week: 0.35 → 0.45
- Installation completion rate: 85% → 92%
- Mobile app activation: 40% → 50%

---

### Sales Team OKR

**Objective:** Scale PLS motion to accelerate mid-market growth

**Key Results:**
1. **KR1**: Engage 90% of PQLs within 7 days (up from 60%)
2. **KR2**: Convert 45% of engaged PQLs to Premium within 90 days (up from 35%)
3. **KR3**: Generate $3M net new ARR from mid-market (up from $2M)
4. **KR4**: Reduce mid-market sales cycle from 45 days → 35 days

**Leading Indicators:**
- PQL volume: 200/month → 300/month (driven by product)
- Sales touches per PQL: 3.2 → 4.5
- Demo → trial conversion: 65% → 75%

---

### Engineering Team OKR (Bridge Strategy)

**Objective:** Ship tsidp to GA to capture AI/MCP market opportunity

**Key Results:**
1. **KR1**: tsidp GA launch by end of Q1
2. **KR2**: 200 tailnets adopt tsidp within 60 days of GA
3. **KR3**: 50 AI/MCP use case customers acquired, $500K ARR
4. **KR4**: tsidp 99.9% availability SLA, <100ms p95 latency

**Leading Indicators (during beta):**
- Beta customers: 50 (target) → 75 (actual)
- Beta NPS: Target >40, actual 52
- Critical bugs: <5 at GA

---

## Benchmarking & Target Setting

### How to Set Targets

**Step 1: Establish Baseline**
- Current performance (trailing 90 days)
- Cohort analysis (compare recent cohorts to older cohorts)
- Segment breakdown (personal vs SMB vs mid-market vs enterprise)

**Step 2: Set Aspirational Target**
- Top-quartile benchmark for SaaS category
- Historical growth trajectory (can we sustain 100% YoY?)
- Resource constraints (what's achievable with current team?)

**Step 3: Backfill with OKRs**
- What initiatives would move the metric?
- What's the expected impact of each initiative?
- Do we have capacity to execute?

**Example: Free → Paid Conversion**
- **Baseline**: 25% of free tailnets (4+ users) convert to paid within 60 days
- **Benchmark**: Top quartile PLG SaaS = 35-40%
- **Constraint**: Product team bandwidth = 2 eng + 1 PM for conversion work
- **Initiatives**:
  - In-app upgrade prompts when hitting 4th user: +3pp
  - Email nurture campaign for 3-user tailnets: +2pp
  - Billing friction reduction (saved payment method): +2pp
  - Total estimated impact: +7pp → 32% conversion
- **Target**: 32% (+7pp improvement)

---

## Metrics to AVOID (Anti-Patterns)

**Vanity Metrics** (measure but don't optimize):
- ❌ Total devices ever connected (includes churned)
- ❌ Total signups ever (includes inactive)
- ❌ GitHub stars (doesn't predict revenue)

**Lagging Indicators Without Leading Pairs:**
- ❌ ARR growth without CAC payback, NRR tracking (unsustainable growth)
- ❌ User count without engagement/retention (leaky bucket)

**Misleading Metrics:**
- ❌ % of users who invite someone (without invite accept rate, becomes spammy)
- ❌ Feature adoption % (without retention impact, build features nobody needs)

**Conflicting Metrics:**
- ❌ Maximize free users (conflicts with monetization)
- ❌ Minimize churn (conflicts with moving upmarket to enterprise)

**Rule:** Every metric should have a clear action that improves it, and improving it should improve business outcomes.

---

## Metrics Governance

### Metric Ownership

| Metric Tier | Primary Owner | Review Cadence | Change Approval |
|-------------|--------------|----------------|-----------------|
| North Star | CPO | Weekly | CEO + Board |
| Business Health | CFO | Monthly | CEO |
| Product Metrics | VP Product | Weekly | CPO |
| Feature Metrics | Product Managers | Weekly | VP Product |
| Segment Metrics | Segment Leads (Sales, CS) | Weekly | CRO |

---

### Metric Definitions (Single Source of Truth)

**Process:**
1. All metrics defined in centralized **Metrics Catalog** (Notion/Confluence)
2. Metric definitions include:
   - Name, description, formula
   - Data source, calculation method
   - Owner, update frequency
   - Historical values, targets
3. Changes to metric definitions require:
   - Proposal with rationale
   - Impact analysis (historical trending)
   - Approval from metric owner + CPO
4. Version control on metric definitions (track changes over time)

**Why This Matters:**
- Prevents "gaming" metrics by changing definitions
- Ensures consistency across dashboards/reports
- Allows historical trend analysis

---

## Next Steps: Implementation Roadmap

### Phase 1: Foundation (Month 1-2)

**Goals:**
- Define North Star Metric (WATME)
- Instrument North Star + input metrics
- Build daily/weekly dashboards

**Deliverables:**
- [ ] Finalize WATME definition with engineering (event schema)
- [ ] Backfill WATME for past 12 months (historical trending)
- [ ] Build Looker/Tableau dashboard for WATME + inputs
- [ ] Set baseline and 6-month targets for NSM inputs
- [ ] Socialize NSM with exec team + board

**Resources:**
- 1 Data Engineer (full-time, 2 months)
- 1 Product Analyst (full-time, 2 months)
- 0.25 FTE CPO (review/approval)

---

### Phase 2: PLG Funnel (Month 3-4)

**Goals:**
- Instrument full PLG funnel (Acquisition → Retention)
- Build cohort retention analysis
- Identify funnel drop-off points

**Deliverables:**
- [ ] Acquisition metrics (signups, attribution, sources)
- [ ] Activation metrics (Day 1, Week 1, Team activation)
- [ ] Engagement metrics (DAU/WAU/MAU, sessions, data transfer)
- [ ] Retention cohorts (7d, 30d, 90d, 12mo)
- [ ] Weekly PLG dashboard

**Resources:**
- 0.5 FTE Data Engineer (2 months)
- 1 FTE Product Analyst (2 months)

---

### Phase 3: Segment & Feature Metrics (Month 5-6)

**Goals:**
- Segment-specific dashboards (Personal, SMB, Mid-Market, Enterprise)
- Feature adoption tracking
- Use case analysis

**Deliverables:**
- [ ] Segment dashboards with ARR, NRR, CAC, payback
- [ ] Feature adoption tracking (SSH, Serve, Funnel, ACLs, etc.)
- [ ] Use case tagging (Business VPN, K8s, IoT, AI)
- [ ] Monthly segment reviews with Sales/CS

**Resources:**
- 0.5 FTE Data Engineer (2 months)
- 0.5 FTE Product Analyst (2 months)
- 0.25 FTE Sales Ops (segment analysis)

---

### Phase 4: Optimization & Experimentation (Month 7+)

**Goals:**
- A/B testing framework
- Predictive analytics (churn risk, expansion propensity)
- Automated alerts for metric anomalies

**Deliverables:**
- [ ] Experiment tracking system (what's being tested, impact on metrics)
- [ ] Churn risk model (predict which accounts will churn)
- [ ] Expansion propensity model (identify PQLs for sales)
- [ ] Anomaly detection alerts (Slack/email when metrics drop)

**Resources:**
- 1 FTE Data Scientist (ongoing)
- 0.5 FTE Data Engineer (ongoing)

---

## Summary: Key Takeaways

1. **North Star Metric: WATME** (Weekly Active Tailnets with Multi-User Engagement)
   - Captures network effect, predicts revenue, actionable
   - Target: 50K → 100K (+100%) in 12 months

2. **Tiered Framework:**
   - Tier 1: NSM + Business Health (exec focus)
   - Tier 2: PLG Funnel (product focus)
   - Tier 3: Feature Metrics (PM focus)
   - Tier 4: Segment Metrics (sales/CS focus)

3. **Leading + Lagging Indicators:**
   - Leading: Activation rate, invitation rate, retention
   - Lagging: ARR, NRR, CAC payback, LTV:CAC

4. **Segment-Specific Optimization:**
   - Personal: Maximize PLG funnel, personal → work conversion
   - SMB: Self-service, low CAC, viral growth
   - Mid-Market: PLS motion, Platform Pete, expansion
   - Enterprise: Land & expand, Security Steve, high ACV

5. **OKR Alignment:**
   - Company OKRs tied to North Star growth
   - Team OKRs tied to NSM input metrics
   - Clear ownership and accountability

6. **Implementation: 6-month roadmap**
   - Months 1-2: NSM foundation
   - Months 3-4: PLG funnel
   - Months 5-6: Segment/feature metrics
   - Month 7+: Optimization & experimentation

---

## Appendix: Metric Formulas

### North Star Metric (WATME)

```sql
WITH active_users AS (
  SELECT
    tailnet_id,
    user_id,
    COUNT(DISTINCT DATE(event_timestamp)) as active_days
  FROM events
  WHERE
    event_timestamp >= CURRENT_DATE - INTERVAL '7 days'
    AND event_type IN ('traffic', 'config_change', 'invite', 'ssh_session')
  GROUP BY tailnet_id, user_id
  HAVING active_days >= 1
)
SELECT
  COUNT(DISTINCT tailnet_id) as WATME
FROM active_users
GROUP BY tailnet_id
HAVING COUNT(DISTINCT user_id) >= 2
```

### Viral Coefficient (K-factor)

```
K = (invitations_sent_per_user) × (invitation_accept_rate) × (activated_user_rate)

Example:
- Average user sends 0.4 invitations per week
- 50% of invitations are accepted
- 80% of new users activate (connect 2+ devices)
K = 0.4 × 0.5 × 0.8 = 0.16 new users per existing user per week
```

### Net Revenue Retention (NRR)

```
NRR = (Starting ARR + Expansion ARR - Churned ARR - Contraction ARR) / Starting ARR

Example for Jan 2024 cohort measured Jan 2025:
- Starting ARR (Jan 2024): $10M
- Expansion (upsells, seat growth): +$3.5M
- Churn (lost customers): -$0.5M
- Contraction (downgrades): -$0.5M
- Ending ARR: $12.5M
NRR = $12.5M / $10M = 125%
```

### CAC Payback Period

```
CAC Payback (months) = CAC / (Monthly Recurring Revenue × Gross Margin %)

Example for SMB:
- CAC: $50
- Average MRR: $60 ($6/user × 10 users)
- Gross Margin: 85%
Payback = $50 / ($60 × 0.85) = 0.98 months ≈ 1 month
```

### LTV:CAC Ratio

```
LTV = (Average Monthly Revenue per Customer) × (Gross Margin %) × (1 / Monthly Churn Rate)
LTV:CAC = LTV / CAC

Example for Mid-Market:
- Average MRR: $1,500
- Gross Margin: 85%
- Monthly Churn: 0.5% (94% annual retention)
- LTV = $1,500 × 0.85 × (1 / 0.005) = $255,000
- CAC = $2,500
- LTV:CAC = $255K / $2.5K = 102:1 ✅ (very healthy)

Note: This assumes infinite lifetime. More conservative: use 5-year horizon.
```

---

**Document Status:** Ready for review and instrumentation
**Recommended Owner:** CPO + VP Product Analytics
**Next Update:** Quarterly or when NSM changes
**Related Documents:**
- [Customer Segmentation & Personas](Customer%20Segmentation%20and%20Personas.md)
- [Strategic Gaps Analysis](Strategic%20Gaps%20Analysis.md)
- [Pricing Strategy Analysis](Pricing%20Strategy%20Analysis.md)
