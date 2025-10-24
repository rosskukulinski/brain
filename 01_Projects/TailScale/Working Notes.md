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

---
