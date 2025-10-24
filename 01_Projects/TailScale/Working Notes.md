---
created: 2025-10-24
updated: 2025-10-24
tags: [tailscale, notes, working-thoughts]
status: active
project: TailScale
---

# TailScale Working Notes

*A place for unstructured ideas, thoughts, and observations*

---

## Initial Thoughts (2025-10-24)

### SRPF Framework
**Security > Reliability > Performance > Features**

Priority hierarchy for decision-making. When trade-offs are required, this is the order of importance.

Questions:
- How does Tailscale currently prioritize these?
- Does the bridge strategy align with SRPF?
- Where do enterprise security features (DNS filtering, DLP) fit if they're "theater"?

---

### Idea Capture & Communication

**Challenge:** Need systematic ways to capture and catalog ideas from multiple sources:
- GitHub issues/discussions
- Sales feedback from customer conversations
- Reddit community requests
- Internal employee submissions (any employee should be able to submit)

**Communication needs:**
- Internal roadmap visibility (what's coming, what's not, why)
- Customer roadmap (transparency without over-committing)
- External/public roadmap (community engagement)

Questions:
- What's current process? Is it ad-hoc or structured?
- How do you prevent "loudest voice wins" vs strategic priorities?
- How do bridge criteria help filter the idea backlog?

---

### Runtime Duality Problem

**The constraint:** Tailscale has two very different deployment models:

1. **Clients ("runtime")** - Deployed on user devices, not easily upgraded
   - MTBF (Mean Time Between Failures) - how long until something breaks
   - Users may stay on old versions for months/years
   - Breaking changes are extremely costly
   - Backward compatibility is critical

2. **Cloud platform** - Centrally controlled, continuously deployed
   - MTTF (Mean Time To Failure) - how quickly can you fix when it breaks
   - Can iterate rapidly
   - Can roll back instantly
   - Feature velocity is high

**Strategic implications:**
- Client stability must be rock-solid (aligns with Reliability in SRPF)
- Platform can move faster and take more risks
- Bridge features that span both (Services, workload identity) need careful interface design
- API versioning and compatibility become critical

Questions:
- How does this affect the "faster to build" engineering goal?
- Does Rust client help or hurt this problem?
- What's the policy for deprecating client versions?

---

### PLG/PLS vs Enterprise Sales Tension

**Three go-to-market motions with different incentives:**

1. **PLG (Product-Led Growth)** - Free plan, viral adoption, self-serve conversion
   - Optimizes for: Ease of use, time-to-value, individual delight
   - Revenue: Many small transactions
   - Feedback loop: Usage data, NPS, activation metrics

2. **PLS (Product-Led Sales)** - Free usage triggers sales outreach
   - Optimizes for: Usage signals, "bring to work" conversion, land-and-expand
   - Revenue: Identify power users at target companies, convert teams
   - Feedback loop: Usage patterns indicating buying intent

3. **Top-Down Enterprise** - Sales-led, compliance-driven, long cycles
   - Optimizes for: Feature checklists, procurement requirements, RFP responses
   - Revenue: Large contracts, seat-based pricing
   - Feedback loop: Lost deals, competitive intelligence, buyer requirements

**The tradeoffs:**
- PLG wants simplicity → Enterprise wants control
- PLG wants free forever → Enterprise wants predictable pricing
- PLG wants fast iteration → Enterprise wants stability/certification
- PLS sits in middle but requires good instrumentation

**How does bridge strategy help?**
- Services/workload identity work for both PLS (developers) and Enterprise (IT approves)
- Cutting "security theater" is a bet on PLS/PLG over pure enterprise checklist
- Risk: Lose top-down deals to competitors with better security story

Questions:
- What % of revenue is PLG/PLS vs enterprise sales today?
- What's the target mix in 2 years?
- How do compensation/incentives align with this strategy?

---

## R&D Planning Overhead

**Observation from Q4 FY26 Plan CSV:**
Looking at the planning artifact (58 items, 10 teams, multiple PMs, extensive documentation requirements), there seems to be significant overhead in the quarterly planning process.

**Questions:**

1. **Planning Time & Work Investment**
   - How many person-weeks go into each quarterly planning cycle?
   - What's the ratio of planning time to execution time?
   - Are we spending 2-3 weeks every quarter on planning exercises?
   - Is this the right rhythm? Would semi-annual or rolling planning work better?

2. **Cross-Team Coordination Burden**
   - Looking at the CSV: 10 teams, 5 PMs, complex interdependencies
   - How much time is spent on cross-team alignment and dependencies?
   - Examples from the plan:
     - Services features span Networking, DevEx, Billing, GM teams
     - Identity work touches Enterprise, Platform, DevEx teams
     - Kubernetes work depends on Networking (Services integration)
   - Are we creating unnecessary coupling through the planning process itself?

3. **Teams as APIs: Looser Coupling**
   - **Current model (implied):** Teams need extensive coordination, shared planning artifacts, cross-functional alignment
   - **Proposed model:** Teams operate more like APIs with clear interfaces
     - Well-defined contracts between teams
     - Minimal synchronous coordination
     - Each team ships independently within their domain
     - Integration happens via stable interfaces, not planning meetings

   **Questions:**
   - What would it take to move to an API-style team model?
   - Which teams could operate more independently today?
   - What interfaces/contracts need to be defined?
   - Is the platform architecture mature enough to support this?

4. **Executive Buy-In Overhead**
   - CSV shows multiple approval stages: Problem doc → 1-pager → Project doc → Commit status
   - Analysis shows low completion rates (Kabir: 14-21%, Samuel: 0%)
   - Are we requiring too many checkpoints?
   - Questions:
     - Who needs to approve each stage?
     - How many departments must sign off on committed items?
     - Is this gatekeeping adding value or just friction?
     - Could we push decision-making authority down to teams?

**Potential Problems:**

1. **Planning theater:** Lots of docs and meetings that don't actually improve outcomes
2. **Decision paralysis:** Too many stakeholders = slow decisions
3. **Lost velocity:** Engineering time spent in planning/alignment instead of building
4. **Innovation tax:** Novel ideas get squeezed out by process overhead
5. **PM burnout:** Kabir managing 14 items with 14% doc completion = unsustainable

**Hypothesis to Test:**

> Large-scale quarterly planning worked when Tailscale was smaller (2-3 teams). Now at 10+ teams, the coordination costs exceed the benefits. We should move toward:
> - **Continuous planning** (rolling 6-week cycles, not quarterly big-bang)
> - **Team autonomy** (clear interfaces, minimal cross-team dependencies)
> - **Reduced checkpoints** (fewer approval stages, faster iteration)
> - **Smaller blast radius** (teams ship independently, integration is continuous)

**Comparison to Kong:**
At Kong, we had similar scaling challenges around ~8-10 teams. What worked:
- Platform teams published APIs/contracts (not just code)
- Product teams built on those contracts without asking permission
- Quarterly planning was high-level themes, not 58-item spreadsheets
- Teams shipped weekly/biweekly, not waiting for quarter boundaries

**Questions for Interview:**

1. "I noticed the Q4 plan has 58 items across 10 teams with extensive documentation requirements. How much time does the organization spend on quarterly planning?"

2. "Have you considered treating teams more like APIs with looser coupling? What would that look like here?"

3. "Looking at the low documentation completion rates (some PMs at 14-21%), is the planning process helping or hindering execution?"

4. "What's the decision-making authority level for each team? Can teams commit to work without extensive cross-functional buy-in?"

5. "At Kong, we found quarterly planning became a bottleneck around 8-10 teams. Have you seen that pattern here?"

---

## Feature Flagging & Progressive Rollout

**UPDATE (2025-10-24):** Tailscale has **BUILT their own feature flag system called "controlknobs"** - they do NOT use LaunchDarkly.

### Current State: Homegrown "Controlknobs" System

**Architecture:**
- Package: `control/controlknobs` in Tailscale codebase
- Mechanism: Control plane pushes configuration to clients via MapResponse
- Remote kill switches for experimental/risky features
- 20+ configurable knobs for network, DNS, platform-specific features
- No client updates needed to toggle features

**Key Features:**
- `DisableUPnP`, `KeepFullWGConfig`, `RandomizeClientPort` (network)
- DNS forwarder controls, split DNS handling
- Platform-specific: Linux netfilter selection, Windows NRPT, captive portal detection
- Real-time updates from control plane to all clients

**Design Goal:** "Make it possible to disable experimental/risky functionality from the control plane, derisking client releases, knowing we can roll things back to the old behavior if it turns out bad."

### Buy vs Build Question

**They chose BUILD. Why might this make sense?**

**Pros of their homegrown approach:**
1. **Tight integration with control plane** - Leverages existing MapResponse protocol
2. **No external dependency** - Critical infrastructure stays internal
3. **Purpose-built for client/server duality** - Addresses their specific runtime model
4. **Lower latency** - No third-party API calls
5. **Cost** - No $5-10K/month SaaS fees
6. **Security** - Sensitive feature flags don't leave their infrastructure

**Cons / Potential gaps:**
1. **Limited to binary on/off** - May not support percentage rollouts easily
2. **No built-in A/B testing** - LaunchDarkly has experimentation features
3. **Less sophisticated targeting** - LaunchDarkly offers complex user segmentation
4. **Maintenance burden** - Issue #14788 notes "too much boilerplate" when adding flags
5. **No UI** - Likely requires code changes to add/modify flags
6. **Limited observability** - No dashboard showing which flags are enabled where

**When might "BUY" make sense?**

Consider LaunchDarkly/Split/Statsig if:
- Need percentage-based rollouts (10% → 50% → 100%)
- Want A/B testing for pricing, UX experiments
- Need non-technical stakeholders to control flags (PM, sales, support)
- Want detailed analytics on flag usage and impact
- Need feature flags for web app, not just backend/clients

**Hybrid approach?**
- Keep controlknobs for low-level client features (performance, network)
- Add LaunchDarkly for higher-level product features (pricing, UI, experiments)
- Controlknobs = infrastructure flags, LaunchDarkly = product flags

### Why This Matters:

Looking at the Q4 roadmap, there are multiple items at different stages (Alpha, Beta, GA, POC). Feature flags could be a powerful enabler for:

### 1. Incremental Release to Various Audiences

**Current Challenge (from roadmap):**
- 6 items in Alpha (10%)
- 8 items in Beta (14%)
- 9 items in GA (16%)

**With Feature Flags:**
- **Free tier users:** Test new features first (opt-in alpha/beta)
- **Paid tiers:** Gradual rollout (10% → 50% → 100%)
- **Enterprise customers:** Controlled rollout with kill switches
- **Specific tailnets:** Early access program / design partners
- **Geographic regions:** Test in smaller markets first
- **Client versions:** Only enable for clients ≥ version X

**Example:**
```
// Workload Identity (P0, committed to GA in Q4)
if (featureFlag.enabled('workload-identity', {
  tailnetId,
  plan: 'enterprise',
  clientVersion: '>= 1.54'
})) {
  // Enable workload identity features
}
```

### 2. Unblock Engineering Experimentation While Respecting SRPF

**The SRPF Alignment:**

**Security:**
- Feature flags as kill switches for security issues
- Rollback vulnerable features instantly (no deploy required)
- Test security features with internal tailnets first
- Gradual exposure reduces attack surface during rollout

**Reliability:**
- Reduce blast radius of new features (start with 1% of users)
- Monitor error rates, rollback if reliability degrades
- Canary deployments become trivial
- "Escape hatch" for problematic releases

**Performance:**
- A/B test performance impact before full rollout
- Enable expensive features only for users who need them
- Gradual load increase on infrastructure
- Measure performance regression per cohort

**Features:**
- Experiment freely without affecting stable users
- Multiple variants in production simultaneously
- Rapid iteration on feature UX
- Data-driven decisions on feature adoption

**Engineering Experimentation Examples:**

1. **Peer Relay (P0, committed to GA):**
   - Flag: Roll out to 10% of tailnets with high NAT traversal failure rates
   - Monitor: DERP usage reduction, connection success rate
   - Expand: If metrics improve, increase to 50% → 100%
   - Kill switch: If connection failures spike, disable immediately

2. **Rust Client (P0, in development):**
   - Flag: Enable for internal employees first
   - Then: Opt-in beta program (enthusiasts who report bugs)
   - Then: Specific OSes where resource usage is critical
   - Kill switch: Fallback to Go client if issues arise

3. **Services Pricing (P2, not committed):**
   - Flag: Test different pricing models with different cohorts
   - A/B test: Usage-based vs seat-based pricing
   - Measure: Conversion rates, revenue per customer
   - Optimize: Choose winning variant based on data

### 3. Benefits for Runtime Duality Problem

**Recall the constraint:** Clients deploy slowly (MTBF focus), Cloud deploys fast (MTTF focus)

**Feature Flags Bridge This Gap:**

**Client-Side Flags:**
- Client ships with feature code but disabled
- Server-side flag controls enablement
- No need to wait for client upgrades to ship features
- Rollback = server-side config change (instant)

**Example Flow:**
```
1. Deploy v1.60 client with "Services support" code (disabled by default)
2. Wait for 80% of clients to upgrade (2-3 months)
3. Server-side flag enables Services for client v1.60+
4. If issues arise, disable flag instantly (no client rollback needed)
```

**This Enables:**
- Faster feature velocity (no waiting for client adoption)
- Safer experimentation (kill switch always available)
- Better backward compatibility (old clients ignore unknown flags)
- Reduced coordination between client and server teams

### 4. Alignment with Current Roadmap Stages

Looking at their stage definitions, feature flags could smooth these transitions:

**POC (3 items):**
- Internal-only feature flags
- Engineering tests without affecting customers

**Alpha (6 items):**
- Feature flag: `opt_in: true`
- Only users who explicitly enable see it
- Example: "Device posture error messages on client" (P2)

**Beta (8 items):**
- Feature flag: `rollout_percentage: 25`
- Gradual rollout to subset of users
- Example: "Windowed client for Windows" (P1)

**GA (9 items):**
- Feature flag: `rollout_percentage: 100, kill_switch: available`
- All users, but can disable if issues arise
- Example: "Peer relay" (P0)

### 5. Reduces Planning Overhead

**Connection to R&D Planning Discussion:**

If teams have feature flags, they can:
- Ship code to production without coordinating release timing
- Reduce cross-team dependencies (each team controls their flags)
- Experiment without executive approval for every iteration
- Validate hypotheses quickly (enable for 5% of users, measure)

**This Supports "Teams as APIs" Model:**
- Team A ships feature behind flag (100% disabled)
- Team B integrates when ready (enables flag for their use cases)
- No synchronous coordination required
- Each team controls their own rollout pace

### Questions for Interview:

1. **Current State (we now know they use controlknobs):**
   - "I saw you have controlknobs for infrastructure flags. How well is that working?"
   - "What's the process for adding new controlknobs? Is the boilerplate issue from #14788 still a pain point?"
   - "How do you manage progressive rollouts? Controlknobs seem binary (on/off) - do you have percentage-based rollouts?"
   - "Who can toggle controlknobs in production? Is it engineering-only or can PMs/support do it?"

2. **SRPF Alignment:**
   - "How have controlknobs helped with the Security > Reliability > Performance > Features framework?"
   - "When a feature threatens reliability, how quickly can you disable it via controlknobs?"
   - "Any examples where controlknobs saved you from a major incident?"

3. **Engineering Velocity:**
   - "Do client teams wait for full client adoption before enabling features via controlknobs?"
   - "How do controlknobs help with the client/server deployment mismatch?"
   - "Are there feature types where controlknobs aren't sufficient? (A/B tests, UX experiments?)"

4. **Buy vs Build Consideration:**
   - "Have you considered adding a product-level feature flag tool (LaunchDarkly) for higher-level experiments?"
   - "Controlknobs seem great for infra flags - would you want a separate system for product/pricing/UX flags?"
   - "Any pain points with the homegrown approach? Where does it fall short?"

5. **Organizational Impact:**
   - "Do teams have autonomy to add/toggle their own controlknobs?"
   - "Could expanded feature flagging enable smaller batch sizes and faster iteration?"
   - "How would better feature flag observability (dashboard, analytics) help teams?"

### Potential Concerns & Tradeoffs:

**Complexity:**
- Feature flag sprawl (hundreds of flags, hard to manage)
- Technical debt (old flags never cleaned up)
- Code complexity (if/else branches everywhere)

**Mitigation:**
- Flag lifecycle management (auto-expire flags after 90 days)
- Regular cleanup sprints (remove flags after full rollout)
- Wrapper abstractions (hide flag complexity from core logic)

**Cost:**
- LaunchDarkly/Split: $1K-$10K/month depending on scale
- Homegrown: Engineering time to build/maintain

**Tradeoff Analysis:**
- Cost: $5K/month for LaunchDarkly Enterprise
- Benefit: Faster iteration, reduced blast radius, engineering velocity
- ROI: If saves 1 week of engineering time per quarter = $50K+ value
- **Verdict: Likely worth it at Tailscale's scale**

### Recommendation:

**They already have controlknobs (homegrown infrastructure flags). Next steps could be:**

**Short-term (improve existing):**
1. Reduce controlknobs boilerplate (address #14788 pain points)
2. Add controlknobs observability dashboard (which flags are on/off across fleet)
3. Document controlknobs best practices for teams
4. Expand team autonomy to add/toggle their own knobs

**Medium-term (fill gaps):**
1. **Add percentage-based rollouts** - Extend controlknobs or buy LaunchDarkly for:
   - Gradual rollouts: 10% → 50% → 100%
   - A/B testing for pricing experiments
   - Cohort-based targeting (free vs paid, region, client version)

2. **Consider hybrid approach:**
   - Keep controlknobs for low-level infrastructure (performance, network, security)
   - Add LaunchDarkly for product-level features (pricing, UX, experiments)
   - Let PMs/support control product flags without engineering

3. **Use flags to enable "teams as APIs" model:**
   - Teams ship features behind flags (disabled by default)
   - Other teams integrate when ready (enable flags for their use)
   - Reduces cross-team coordination in quarterly planning

**ROI Analysis:**
- LaunchDarkly cost: ~$5-10K/month for their scale
- Value: Faster iteration, A/B testing, PM autonomy, reduced coordination overhead
- If saves 1 week of engineering time per quarter: $50K+ annual value
- **Verdict: Likely worth it IF they need product-level experiments beyond infrastructure flags**

---

## KPIs & Metrics for Bridge Strategy

**Proposed North Star Metric:** Number of concurrent connected devices across all tailnets

**Proposed Secondary Metric:** Number of tailnets (rough proxy for customers)

### Analysis: Are These the Right Metrics?

**Strengths of "Concurrent Connected Devices":**
- Maps directly to coordination service COGS (the actual infrastructure cost driver)
- Indicates actual product usage (not just signups)
- Grows with both enterprise (more employees) and platform (more workloads)
- Network effects: More devices = more value = more connections

**Weaknesses of "Concurrent Connected Devices":**
- Doesn't distinguish between paying and free users
- Doesn't tell you if usage is VPN (low value) or platform (high value)
- Can be gamed (spin up thousands of ephemeral nodes)
- Doesn't directly correlate to revenue (one customer with 10K devices vs 10K customers with 1 device)

**Strengths of "Number of Tailnets":**
- Clear proxy for customers
- Easy to segment (free, paid, enterprise)
- Maps to support COGS (largest cost driver = onboarding per customer)

**Weaknesses of "Number of Tailnets":**
- Doesn't capture expansion revenue (customer goes from 10 → 1000 devices)
- Doesn't distinguish between active and dormant tailnets
- Platform use cases might use single tailnet with many workloads
- Multiple tailnets feature complicates this (one customer = many tailnets)

---

### Recommended: Multi-Tier Metrics Framework

**Bridge Strategy Insight:** We need metrics that validate the "bridge thesis"—that Services, Identity, and Workload Connectivity serve BOTH markets.

#### Tier 1: North Star Metric (Single Number)

**Proposed: Active Device-Hours per Week**
- **Definition:** Sum of (concurrent connected devices × hours connected) across all tailnets
- **Why better than concurrent devices:** Captures usage intensity, not just peak
- **Maps to value:** More device-hours = more infrastructure managed = more value created
- **Maps to costs:** Coordination service scales with active devices, not total signups

**Alternative: Weekly Active Devices (WAD)**
- Similar to MAU but shorter cycle (infrastructure products used daily/weekly)
- Easier to reason about than device-hours
- Industry standard (easier to benchmark)

#### Tier 2: Bridge Strategy Validation Metrics

These metrics specifically test whether the bridge features are working:

**1. Hybrid Customer Percentage**
- **Definition:** % of paying customers using BOTH VPN features AND platform features
- **Platform signal:** Using Services, workload identity, or ephemeral tailnets
- **VPN signal:** >10 human users, using ACLs, using exit nodes or app connectors
- **Why it matters:** This IS the bridge thesis—same customers using both
- **Target:** 40%+ by end of H1 FY27

**2. Services Adoption Rate**
- **Definition:** % of tailnets with at least one Service advertised
- **Why it matters:** Services is the strategic center of gravity for bridge
- **Segments to track:**
  - Free tailnets (hobbyists experimenting)
  - Paid <100 devices (SMB/startups)
  - Paid >100 devices (enterprise)
- **Target:** 25% of paid tailnets by end of H1 FY27

**3. Workload Identity Usage**
- **Definition:** Number of workload identities created per week (CI/CD, K8s, cloud)
- **Why it matters:** This is the "infra access + platform" bridge
- **Segment:** Workload devices as % of total devices
- **Target:** 15%+ of all devices are workloads (not humans) by H2 FY27

#### Tier 3: Growth & Revenue Metrics

**Leading Indicators (predict future revenue):**

1. **New Tailnet Creation Rate**
   - Weekly new signups
   - Segment: From personal (PLG) vs from work email (PLS signal)

2. **Activation Rate**
   - % of new tailnets that connect >3 devices in first week
   - Maps to support COGS (activated users = more onboarding support)

3. **"Bring to Work" Conversion**
   - Track users who start personal, then create work tailnet
   - Track free personal → paid company (via email domain clustering)
   - This validates PLG → PLS motion

4. **Platform API Call Volume**
   - Total API calls per week (programmatic usage signal)
   - Services API calls specifically
   - Track growth rate (should be 10%+ MoM if platform is working)

**Lagging Indicators (revenue outcomes):**

5. **ARR (Annual Recurring Revenue)**
   - Standard SaaS metric
   - Segment by: Free, Starter, Enterprise

6. **Net Revenue Retention (NRR)**
   - Cohort-based expansion revenue
   - **Critical for bridge thesis:** Are VPN customers expanding to platform (adding devices/workloads)?
   - Target: 120%+ (best-in-class SaaS)

7. **Average Revenue Per Customer (ARPC)**
   - Better than ACV for device-based pricing
   - Tracks expansion within accounts

#### Tier 4: Efficiency & Health Metrics

**COGS-Related (based on our economics analysis):**

8. **Support Tickets per New Tailnet**
   - Largest COGS driver = support during onboarding
   - Should DECLINE over time as UX improves
   - Target: <2 tickets per new tailnet by H1 FY27

9. **DERP Relay Usage Rate**
   - % of connections requiring DERP fallback
   - Should be <10% (peer-to-peer is cost advantage)
   - Spike = infrastructure problem or product issue

10. **Time to First Value (TTFV)**
    - How long from signup to first device connection?
    - Free tier: Target <5 minutes
    - Enterprise: Target <24 hours (incl. SSO setup)

**Product Quality (SRPF Framework):**

11. **Reliability - Control Plane Uptime**
    - Target: 99.9%+ (aligns with SRPF: Reliability > Features)
    - Segment: Coordination service vs DERP availability

12. **Security - Mean Time to Patch (MTTP)**
    - How quickly do critical security issues get fixed?
    - Target: <24 hours for critical, <7 days for high

13. **Performance - p95 Connection Establishment Time**
    - How fast can two devices connect?
    - Direct connection vs DERP fallback
    - Target: <2 seconds p95

#### Tier 5: Market Position Metrics

14. **Developer Mindshare**
    - GitHub stars growth rate
    - Reddit/HN mentions (sentiment analysis)
    - Stack Overflow questions/answers
    - "Tailscale" search volume trends

15. **Competitive Win Rate**
    - % of deals won vs Twingate, Zscaler, Cisco, etc.
    - Track by segment (enterprise vs SMB)
    - Track by use case (VPN vs infra access)

---

### How to Validate "Bridge" Thesis with Data

**The Key Question:** Do bridge features actually serve both markets?

**Hypothesis Testing (Q1 FY27):**

**Test 1: Do enterprise VPN customers adopt platform features?**
- Cohort: Customers who signed up for "Business VPN"
- Measure: % that create Services, use workload identity, or create multiple tailnets within 6 months
- Success: >30% adopt at least one platform feature
- Failure: <15% adopt platform features → VPN and platform are separate markets

**Test 2: Do platform users expand to org-wide VPN?**
- Cohort: Customers who started with Services/workload identity
- Measure: % that expand to >50 human users (VPN use case)
- Success: >20% expand to VPN use case
- Failure: <10% expand → Platform customers don't need VPN

**Test 3: Does hybrid usage drive higher revenue?**
- Segment customers into: VPN-only, Platform-only, Hybrid (both)
- Measure: ARPC for each segment
- Success: Hybrid ARPC is 2x+ higher than either segment alone
- Failure: No revenue difference → Bridge doesn't create more value

**Test 4: Do bridge features reduce churn?**
- Cohort: Customers who use bridge features vs those who don't
- Measure: Retention rate at 6, 12, 24 months
- Success: Hybrid customers have <5% churn (vs 15-20% for single-use)
- Failure: No retention difference → Bridge doesn't create lock-in

---

### Connection to COGS Economics

**Recall from COGS analysis:**
- Support (50-60%): Scales with NEW customers, not usage
- Coordination service (20-30%): Scales with active devices
- DERP bandwidth (10-20%): Minimized by peer-to-peer

**Metrics that Optimize Unit Economics:**

1. **Support Tickets per New Tailnet** → Directly reduces largest COGS
2. **Activation Rate** → Better UX = fewer support tickets
3. **DERP Usage Rate** → Keep bandwidth costs negligible
4. **Device-Hours per Customer** → Revenue grows faster than costs (sub-linear infrastructure scaling)

**The Virtuous Cycle:**
- Better product (lower TTFV, higher activation) → Fewer support tickets → Lower COGS
- More usage (device-hours) → More value → Higher willingness to pay
- Network effects (more devices) → Better peer-to-peer connectivity → Lower DERP costs
- Platform adoption → Workload devices (high margin, no support burden)

---

### Open Questions for Interview

**1. Current Metrics:**
- "What metrics do you track today as north star?"
- "How do you measure success for Services vs VPN features?"
- "Do you segment customers by usage patterns (VPN-only vs platform-only)?"

**2. Bridge Strategy Validation:**
- "What would prove or disprove the bridge thesis?"
- "Are you tracking hybrid customers (using both VPN and platform)?"
- "What's the current overlap? Is it growing?"

**3. Data Infrastructure:**
- "Do you have the instrumentation to track platform API usage?"
- "Can you identify when a VPN customer starts using platform features?"
- "How quickly can you answer 'which features drive retention'?"

**4. Team Alignment:**
- "Do different teams optimize for different metrics? (VPN team vs Platform team)"
- "How do you avoid local optimization that hurts global strategy?"
- "If we adopt the bridge strategy, what would be the shared metric across teams?"

---

### Final Thought: Metrics Drive Behavior

**Critical Principle:** The metrics you choose shape team incentives and behavior.

**Bad Outcome:**
- VPN team optimizes for "number of users"
- Platform team optimizes for "API calls"
- No one owns "hybrid customers"
- Strategy fails despite hitting both metrics

**Good Outcome:**
- Shared metric: "Hybrid Customer Revenue"
- VPN team asks: "How do we convert VPN users to platform?"
- Platform team asks: "How do we expand platform users to VPN?"
- Everyone aligned on bridge strategy

**Therefore:**
- North Star should be shared (Active Device-Hours across all use cases)
- Bridge metrics should be highly visible (Hybrid Customer % in every exec review)
- Team metrics should ladder up to bridge success (not create conflicting incentives)

---

## Questions to Explore

### Strategy & Prioritization
- How does Sam think about SRPF prioritization today?
- What's the idea intake process currently? Is it working?
- What's the revenue mix between PLG/PLS/enterprise? Target mix?
- How do sales comp plans align with product strategy?

### Technical Architecture
- What's the client upgrade policy? How long do they support old versions?
- **Partner integration feasibility:** Are there architectural constraints that make vendor integrations (like Snowflake) harder than the analysis suggests?
  - Can customer tailnets safely allow third-party provisioning?
  - Security model implications of partners creating nodes in customer networks?
  - Control plane scalability with massive partner-driven node creation?
  - Key rotation and lifecycle management at scale?
  - Multi-tenant Services architecture—is it ready for partner use cases?

### Current State
- What's Tailscale's current partnership strategy? Any existing vendor relationships?
- Has anyone approached Tailscale about integration (databases, cloud providers, etc.)?
- What lessons from existing OEM/partnership discussions?

---

## Random Observations

-

---

## Things to Investigate

- Look at client release cadence and adoption curves
- Review how other infra companies (Cloudflare, Datadog) handle runtime vs platform duality
- Study PLG→Enterprise transitions (Slack, Figma, Notion) for lessons

---

## Interview Prep Notes

-

---

## Potential Talking Points

-

---

## Concerns or Challenges

-

---

## Connections & Insights

- SRPF framework aligns well with "Reliability" focus in bridge strategy (control plane scalability, Packet Filter v2)
- Runtime duality problem suggests client stability must come first → validates prioritizing tech debt
- PLG/PLS tension resolved by bridge features that work for both developer-led and IT-approved buying
- Partnership opportunities (see Future Opportunities.md) could amplify bridge strategy in H2/FY28
- **Community as innovation engine:** The community builds v0 (proof of concept), validates demand, then Tailscale productizes v1 (production-ready). This de-risks product development—you don't have to guess what to build, the community is showing you. (See Community Projects Bridge Strategy Analysis.md)

---
