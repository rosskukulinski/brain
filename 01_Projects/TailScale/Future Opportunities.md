---
created: 2025-10-24
updated: 2025-10-24
tags: [tailscale, strategy, partnerships, future]
status: future
project: TailScale
---

# Future Opportunities (H2 FY27+)

*Strategic opportunities that could amplify the bridge strategy after H1 validation*

---

## Tech Partnership Strategy: Hyperscaler & Vendor Partnerships

### Timeline: H2 FY27 - FY28

### The Opportunity

Leverage existing vendor distribution channels to accelerate Tailscale adoption, particularly for database/data warehouse connectivity where pain is most acute.

### Why Partnerships Make Sense (Eventually)

**The Paradox:**
Avery's "New Internet" vision positions AWS as the rent-seeker that Tailscale helps users avoid. But hyperscalers could actually be the **fastest path to universal adoption**—piggyback on their distribution to build the new network.

**Strategic Fit with Bridge:**
- If Snowflake integrates Tailscale Services for database connectivity...
- Every Snowflake customer gets exposed to Tailscale platform capabilities
- Enterprise VPN becomes the natural expansion: "You're using it for data, why not for everything?"

### Target Vendors (Prioritized)

#### Tier 1: Database/Data Warehouse (Highest Priority)
**Why:** Connectivity pain is extreme, limited workarounds exist, direct fit with infra access bridge features

1. **Snowflake**
   - Pain: PrivateLink setup is complex, IP whitelisting is brittle
   - Opportunity: "Connect via Tailscale" as first-class option in setup
   - Scale: 10,000+ enterprise customers
   - Fit: Database access + audit logging already on roadmap

2. **Databricks**
   - Pain: Cluster connectivity across clouds, notebook access from corporate networks
   - Opportunity: Seamless connectivity to clusters and data sources
   - Scale: 10,000+ customers, heavy AWS/Azure/GCP multi-cloud usage
   - Fit: K8s integration, Services for notebook access

3. **MongoDB Atlas**
   - Pain: PrivateLink per-region is expensive, VPN peering is complex
   - Opportunity: "Tailscale endpoint" as alternative to PrivateLink
   - Scale: 45,000+ customers
   - Fit: Simple database access story

#### Tier 2: AI Vendors
**Why:** Emerging use case, edge AI needs connectivity, privacy concerns drive demand

1. **OpenAI/Anthropic API access**
   - Pain: Enterprises want private API access, not public internet
   - Opportunity: Private API endpoints via Tailscale
   - Fit: Workload identity for auth, Services for routing

2. **Edge AI platforms (NVIDIA Fleet Command, etc.)**
   - Pain: Edge model synchronization with cloud
   - Opportunity: Secure edge ↔ cloud connectivity
   - Fit: IoT/embedded use case (future Rust client)

#### Tier 3: Cloud Marketplaces & CI/CD
**Why:** Distribution play, lighter integration lift

1. **AWS/GCP/Azure Marketplace**
   - Opportunity: Listed offering, integrated billing
   - Fit: Enterprise procurement prefers marketplace purchases
   - Effort: Lower than native integration

2. **GitHub Actions / GitLab CI**
   - Pain: Accessing private resources from CI/CD
   - Opportunity: Workload identity integration
   - Fit: Already on roadmap, formalize partnership

3. **Kubernetes vendors (Rancher, D2iQ)**
   - Pain: K8s networking is complex
   - Opportunity: Tailscale operator as blessed solution
   - Fit: Already exists, needs partnership GTM

### Partnership Models

**Model 1: Integration Partnership** (Target for DB vendors)
- Vendor integrates Tailscale into their product
- Example: Snowflake setup wizard has "Connect via Tailscale" button
- Precedent: How Heroku integrated with AWS

**Model 2: Marketplace/Co-sell**
- Tailscale available in cloud marketplaces
- Joint GTM with hyperscaler sales teams
- Value: Distribution + credibility

**Model 3: OEM/"Powered by Tailscale"**
- Vendor white-labels Tailscale (may not even expose branding)
- Example: Databricks runs Tailscale for cluster connectivity under the hood
- Value: Infrastructure-level adoption

**Model 4: Managed Service**
- Cloud offers "Managed Tailscale Service" (like MongoDB Atlas on AWS)
- Fully managed, integrated billing
- Value: Enterprise "approved vendor" instant credibility

### Why Wait Until H2 FY27?

**Need proof points first (H1 FY27):**
- 50+ customers using Tailscale for Snowflake connectivity
- 1000+ CI/CD workloads using workload identity
- Reference architectures and case studies
- Clear data on adoption and expansion patterns

**Partnerships require resources:**
- Dedicated BD/partnerships team
- Engineering bandwidth for integrations
- Joint GTM and marketing efforts
- 12-18 month BD cycles are typical

**Strategy must work standalone:**
- Bridge strategy needs to prove itself with direct customers
- Can't rely on partnerships to validate product-market fit
- Partnerships amplify success, they don't create it

### Success Metrics (When Pursued)

**H2 FY27 (Setup phase):**
- 3+ partnership conversations initiated with proof points
- 1+ LOI or partnership agreement signed
- Integration specs defined with at least one vendor

**FY28 (Execution phase):**
- 1+ live integration (e.g., Snowflake "Connect via Tailscale")
- 20%+ of new customers come via partnership channel
- Partner-sourced customers have higher LTV (validate thesis)

### Risks & Mitigations

**Risk: Misaligned incentives**
- Hyperscalers make money on interconnect fees (Tailscale reduces that)
- Mitigation: Show data that easier connectivity → more cloud usage overall

**Risk: Integration complexity**
- Each vendor has different auth, networking, security models
- Mitigation: Build flexible integration layer as part of bridge foundation

**Risk: Partnership distraction**
- Long sales cycles, engineering tax, misaligned priorities
- Mitigation: Only pursue after H1 validation, with dedicated resources

**Risk: "Not invented here" culture**
- Large vendors resist integrating third-party solutions
- Mitigation: Start with vendors who have partnership DNA (MongoDB, Snowflake vs AWS)

### Connection to "New Internet" Vision

From Avery's post: *"The Internet is for everyone... To the people building the Internet, nothing mattered but getting everyone connected."*

Hyperscaler partnerships aren't selling out—they're **using existing networks to build the new one**:
- Piggyback on distribution (millions of customers)
- Reduce friction (integrated, blessed solution)
- Accelerate network effects (more endpoints = more value)

It's pragmatic go-to-market for an idealistic vision.

### Recommended Approach

**H1 FY27 (Now - Q2):**
- Mention partnerships as "future opportunity" in strategy docs
- Track which customers use Tailscale for database/cloud connectivity
- Build reference architectures (informal partnerships with design partners)
- No dedicated resources yet

**H2 FY27 (Q3-Q4):**
- Review H1 data: Is there a pattern worth partnering around?
- If yes: Initiate conversations with 3-5 target vendors
- Allocate dedicated BD resource (0.5-1 FTE)
- Engineering: Build flexible integration primitives

**FY28:**
- Execute on 1-2 partnerships
- Measure impact on adoption and expansion
- Scale what works, cut what doesn't

---

## Other Future Opportunities

### [Add other strategic opportunities here as they emerge]

---
