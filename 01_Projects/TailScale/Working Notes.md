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
