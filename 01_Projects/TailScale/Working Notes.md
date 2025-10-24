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

- How does Sam think about SRPF prioritization today?
- What's the idea intake process currently? Is it working?
- What's the client upgrade policy? How long do they support old versions?
- What's the revenue mix between PLG/PLS/enterprise? Target mix?
- How do sales comp plans align with product strategy?

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

-

---

## Tech Partnership Strategy: Wedging Via Hyperscalers

### The Paradox

Avery's "New Internet" vision positions AWS as the rent-seeker that Tailscale helps users avoid. But what if hyperscalers could be partners, not adversaries?

### Why Hyperscalers Might Embrace Tailscale

**AWS/GCP/Azure:**
1. **Hybrid/Multi-cloud is real** - Enterprises want workloads across clouds + on-prem
   - Current solution: Complex VPN meshes, transit gateways, expensive interconnects
   - Tailscale solution: Universal connectivity layer that makes "cloud" location-agnostic
   - AWS value: Easier to integrate AWS services into customer environments = more AWS consumption

2. **Edge computing needs better connectivity**
   - Edge devices need to talk to cloud services securely
   - Current: VPNs, IoT-specific protocols, custom solutions
   - Tailscale solution: Uniform connectivity for edge → cloud
   - Hyperscaler value: Reduces friction to adopt their edge offerings

3. **Developer experience = competitive advantage**
   - Easier connectivity → faster development → more cloud usage
   - "Powered by Tailscale" could be a differentiator vs competitors
   - Similar to how AWS embraced Docker/Kubernetes despite commoditizing compute

4. **Managed Tailscale = new revenue stream**
   - Offer Tailscale as a managed service (like AWS manages MongoDB, Elasticsearch)
   - Hyperscaler captures operational revenue, Tailscale gets distribution
   - Customer gets integrated billing, support, and SLAs

**AI Vendors (OpenAI, Anthropic, Mistral, etc.):**
1. **Model access from anywhere**
   - Customers want to call APIs from private networks, edge devices, air-gapped environments
   - Current: Complex proxy setups, VPN tunnels, security nightmares
   - Tailscale solution: Secure connectivity to AI APIs without exposing to public internet

2. **Fine-tuning and data privacy**
   - Enterprises want to fine-tune models on private data
   - Need secure channel to upload training data, download models
   - Tailscale: End-to-end encrypted data transfer

3. **AI at the edge**
   - Running inference on edge devices that need to sync with cloud models
   - Tailscale: Seamless edge ↔ cloud model synchronization

**Database/Data Warehouse Vendors (Snowflake, Databricks, MongoDB, etc.):**
1. **The connectivity pain is acute**
   - Customers constantly struggle to connect to databases securely
   - PrivateLink, VPN peering, IP whitelisting are all terrible UX
   - Tailscale: "Just connect to your database via Tailscale IP"

2. **Multi-cloud data strategy**
   - Data in Snowflake, compute in AWS, analysts on corporate network
   - Need secure connectivity across all environments
   - Tailscale: Universal data plane

3. **Compliance and audit**
   - Database access logging is critical (SOC2, HIPAA, etc.)
   - Tailscale's infra access features (audit logging, session recording) directly address this
   - Partnership: "Snowflake + Tailscale = compliant data access out of the box"

### Potential Partnership Models

**Model 1: Integration Partnership**
- Vendor integrates Tailscale into their product
- Example: Snowflake offers "Connect via Tailscale" as an option in setup wizard
- Value: Dramatically simpler onboarding for private connectivity
- Precedent: How Heroku integrated with AWS, or how Vercel integrates with various clouds

**Model 2: Marketplace/Co-sell**
- Tailscale available in AWS/GCP/Azure marketplaces
- Joint GTM motion: "Secure your multi-cloud with Tailscale"
- Hyperscaler sales reps sell Tailscale as part of landing solution
- Value: Distribution channel + credibility

**Model 3: OEM/"Powered by Tailscale"**
- Vendor white-labels Tailscale for their connectivity needs
- Example: Databricks runs Tailscale under the hood for cluster connectivity
- Customer never knows it's Tailscale (or does, as a feature)
- Value: Tailscale becomes infrastructure-level adoption

**Model 4: Managed Service**
- AWS offers "Amazon Tailscale Service" (like they offer MongoDB Atlas, Redis, etc.)
- Fully managed, integrated billing, AWS support
- Tailscale gets revenue share + massive distribution
- Value: Enterprise customers get "approved vendor" status instantly

### Strategic Fit with Bridge Strategy

This actually **reinforces** the bridge approach:

**Services + Partnerships = Platform Distribution**
- If Snowflake integrates Tailscale Services for database connectivity...
- Every Snowflake customer gets exposed to Tailscale platform capabilities
- Enterprise VPN becomes the natural expansion: "You're using it for data, why not for everything?"

**Workload Identity + Cloud IAM**
- Integrate Tailscale workload identity with AWS IAM, GCP service accounts
- Make it trivial to give cloud workloads secure connectivity
- Solves real pain point for platform teams

**Multi-tenant architecture matters**
- Hyperscaler customers often have complex org structures
- Multiple tailnets, policy fragments, identity federation = table stakes
- Bridge features enable partnership viability

### Questions to Explore

**Strategic:**
- Does partnering with AWS contradict the "New Internet" vision? Or is it pragmatic go-to-market?
- What's Tailscale's current partnership strategy? Any existing hyperscaler relationships?
- Would hyperscalers see Tailscale as complementary or competitive?

**Tactical:**
- Which vendor has the most acute connectivity pain? (Database vendors seem obvious)
- What's the integration complexity? Can it be lightweight?
- Who's the buyer for a partnership? (Engineering? BD? Product?)

**Execution:**
- Does this require dedicated partnership/BD resources?
- How does this fit into H1FY27 roadmap? Is it a distraction or accelerant?
- What proof points do you need to pitch hyperscalers? (usage data, customer testimonials)

### Potential Entry Wedges

**Easiest (Low hanging fruit):**
1. **Snowflake/Databricks** - Connectivity pain is extreme, limited workarounds exist
2. **MongoDB Atlas** - Already cloud-hosted, PrivateLink complexity is known issue
3. **AI inference providers** - Edge AI is emerging use case with no good solution

**Medium difficulty:**
1. **AWS/GCP marketplace** - Distribution play, not deep integration
2. **Kubernetes vendors** (Rancher, D2iQ) - K8s connectivity is messy, Tailscale operator exists
3. **CI/CD platforms** (GitHub Actions, GitLab) - Workload identity is natural fit

**Hardest (but highest impact):**
1. **AWS/GCP/Azure native integration** - "Connect to VPC via Tailscale" button in console
2. **OEM for hyperscaler edge** - AWS IoT/Greengrass using Tailscale under hood
3. **M&A** - Could a hyperscaler just acquire Tailscale? (probably not the plan, but worth considering)

### Connection to "New Internet" Vision

Avery's post says: *"The Internet is for everyone... To the people building the Internet, nothing mattered but getting everyone connected."*

Hyperscaler partnerships could be the **fastest path to universal adoption**:
- Piggyback on their distribution (millions of customers)
- Reduce friction (integrated, blessed solution)
- Network effects accelerate (more endpoints = more value)

It's not selling out—it's using existing networks to build the new one.

### Counter-Argument: Why This Might Not Work

**Hyperscalers may resist:**
- AWS makes money on interconnect, transit gateway, PrivateLink fees
- Tailscale reduces that revenue (even if it increases other usage)
- "Not invented here" culture at large cloud vendors

**Integration complexity:**
- Each vendor has different auth, networking, security model
- Building/maintaining integrations is engineering tax
- Could distract from core product development

**Misaligned incentives:**
- Hyperscaler wants lock-in, Tailscale enables portability
- Hard to align on pricing, revenue share, GTM motion
- Partnership BD cycles are SLOW (12-18 months typical)

**Better alternatives?**
- Focus on end customers instead of vendors
- Let organic "bring to work" drive adoption
- Partnerships are distraction from core bridge strategy

### Recommendation for Discussion

This feels like a **Q2-H2 FY27 opportunity**, not Q4-Q1:

**First (H1):** Prove bridge thesis with direct customers
- Show Services adoption, workload identity traction
- Build reference architecture for database connectivity, AI access
- Collect testimonials: "Tailscale solved our Snowflake access problem"

**Then (H2):** Approach partnerships with proof points
- "50 customers use us for Snowflake connectivity - let's make it native"
- "1000 CI/CD workloads use workload identity - let's integrate with GitHub Actions"
- Data makes the pitch credible

**Why wait:**
- Partnerships require dedicated resources (BD, eng for integrations)
- Need leverage in negotiations (usage data, customer demand)
- Bridge strategy must work standalone before partnerships amplify it

But definitely worth putting in the "future opportunities" section of H1 strategy.

---
