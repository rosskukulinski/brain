---
created: 2025-10-24
tags: [tailscale, kong, strategic-analysis, product-strategy, plg, multi-product, platform, ross-insights]
status: complete
project: TailScale
attachment: [[tailscale-kong-star-history.png]]
---

# Kong vs Tailscale: Strategic Comparison & Growth Analysis

**By Ross Kukulinski** | Interview Preparation Notes
**Image Reference:** `05_Attachments/tailscale-kong-star-history.png`

## Executive Summary

Analysis of GitHub star growth reveals striking parallels between Kong and Tailscale's developer-led adoption, but crucial strategic differences in business models and GTM evolution. While both execute successful PLG strategies in infrastructure, Kong pursued OSS→Enterprise with higher ACV/fewer customers, whereas Tailscale has mastered OSS→PLG transition with broader market appeal. Tailscale's accelerating growth (now exceeding Kong's rate despite 5-year disadvantage) validates their PLG-first approach. Strategic opportunities ahead: sustaining PLG advantage through careful licensing decisions, leveraging Headscale ecosystem, and eventual platform evolution to multi-product company (Series D/E stage).

**Ross's Unique Value:** I've lived Kong's growth journey and can pattern-match their OSS→Enterprise evolution against Tailscale's more successful OSS→PLG execution. I understand both playbooks and can help Tailscale navigate the transition to platform/multi-product future.

---

## Growth Metrics Comparison (Mid-2025)

### Kong (`kong/kong`)
- **GitHub Stars:** 41,000-42,000
- **Timeline:** Mid-2015 to present (~10 years)
- **Growth Pattern:** Consistent linear ~4,100 stars/year
- **Customers:** ~10,000 paid customers (as of recent public data)
- **Revenue Model:** Higher ACV, fewer customers (enterprise-focused)
- **Maturity:** Established market leader, steady state

### Tailscale (`tailscale/tailscale`)
- **GitHub Stars:** 25,000-26,000
- **Timeline:** Late 2019/early 2020 to present (~5 years)
- **Growth Pattern:** Exponential with mid-2021 inflection
- **Current Growth Rate:** Exceeds Kong's rate (~5,000-5,200/year overall, higher recently)
- **Customers:** 10,000+ paid customers (achieved 2024)
- **Revenue Model:** Lower ACV, higher volume (PLG-driven)
- **Maturity:** High-growth acceleration phase

### Critical Insight: Customer Economics

**Kong's Model:**
- **~10,000 customers** at significantly higher company revenue
- **Implication:** Much higher ACV per customer
- **Strategy:** Enterprise-first, large deal focus
- **Sales Motion:** Traditional enterprise sales-led

**Tailscale's Model:**
- **10,000+ customers** achieved through PLG
- **Implication:** Lower ACV but higher volume
- **Strategy:** Freemium → upgrade, bottom-up adoption
- **Sales Motion:** Product-led with enterprise expansion

**Ross's Analysis:** Tailscale's customer acquisition cost will always be much lower due to PLG motion. This is a significant competitive advantage that should be carefully protected.

---

## GitHub Stars: Context & Caveats

### Important Disclaimer

**GitHub stars are primarily a vanity metric.** They don't directly correlate to:
- Revenue
- Enterprise adoption
- Customer retention
- Market share

### What Stars Actually Measure

**However, they are useful for understanding:**
1. **Broad reach of an OSS project** - Developer awareness and interest
2. **Community health** - Active engagement signals
3. **Leading indicator** - Early signal of product-market fit
4. **Developer mindshare** - Critical for PLG motion
5. **Trend direction** - Growth acceleration or deceleration patterns

**For this analysis:** Stars help us understand the **breadth of developer adoption** and validate that both Kong and Tailscale have achieved significant community traction. The growth patterns reveal strategic execution differences, not absolute success measures.

---

## Strategic Divergence: OSS → Enterprise vs OSS → PLG

### Kong's Journey: OSS → Enterprise (2015-2025)

**Initial Strategy:**
- Open-source Kong Gateway drives adoption
- Enterprise edition with premium features
- Direct sales to large organizations

**Evolution:**
- Successfully built enterprise business (high ACV model)
- **Never made the OSS → PLG transition**
- OSS → Enterprise motion, not OSS → PLG → Enterprise
- **Only now trying to figure out PLG/PLS** (product-led sales)

**Challenges:**
- Higher customer acquisition costs (sales-led)
- Slower growth velocity (enterprise sales cycles)
- Later to PLG game (market shifted)
- Trying to retrofit PLG onto enterprise DNA

**Result:**
- Fewer customers, higher ACV
- Stable but slower growth rate
- Mature but potentially constrained model

### Tailscale's Journey: OSS → PLG → Enterprise (2019-2025)

**Initial Strategy:**
- WireGuard foundation (open-source protocol)
- Free tier powerful enough for real use
- Freemium → Enterprise upgrade path

**Evolution:**
- **Successfully executed OSS → PLG transition**
- Product-led growth from day one
- Community ecosystem (Headscale support)
- Enterprise features drive upsell

**Advantages:**
- Lower customer acquisition costs
- Faster growth velocity
- Network effects from free tier
- Bottom-up enterprise expansion

**Result:**
- More customers, lower ACV (but growing)
- Accelerating growth rate
- Vibrant community (broader appeal)

**Strategic Decision: Bringing on Headscale creator was brilliant**
- Signals commitment to open ecosystem
- Reduces friction with self-hosting community
- Maintains trust with privacy-conscious users
- Demonstrates enlightened approach to OSS competition

---

## Ross's Strategic Insights

### 1. Protect the PLG Advantage

**Key Recommendation:**
> Tailscale should continue to focus on fueling the PLG transition because customer acquisition cost will always be much lower than enterprise sales-led models.

**Why This Matters:**
- Kong's struggle to retrofit PLG proves it's hard to add later
- Tailscale has PLG in their DNA from founding
- Unit economics favor PLG over enterprise-only
- Market has shifted to expect free/trial options

**Future Strategic Licensing Decisions Should Be Made Carefully:**
- Any restrictions on free tier could damage PLG motion
- Balance between free value and enterprise upsell is delicate
- Open-source ecosystem (Headscale) provides competitive release valve
- Overly aggressive monetization could backfire (users flee to Headscale/competitors)

**What to Preserve:**
- Free tier remains valuable for individuals/small teams
- Headscale community stays supported (hiring Kristoffer was smart)
- Enterprise upsell based on value-add (compliance, scale, support) not feature gates
- Bottom-up adoption pathway stays frictionless

**What to Evolve:**
- Enterprise features that don't cannibalize free tier
- Packaging/pricing that scales with customer value
- Self-service upgrade paths
- Expansion revenue from existing customers

### 2. Community Breadth: The Hobbyist Advantage

**Observation:**
> It's interesting just how active the Reddit forums are for Tailscale. It has much broader appeal—in particular to hobbyists—than Kong ever had.

**Kong's Community:**
- r/Kong exists but less active
- Primarily enterprise developers
- Infrastructure/DevOps professional focus
- Less personal/hobby use

**Tailscale's Community:**
- r/Tailscale has 41,000+ members, very active
- Mix of enterprise AND hobbyists
- Homelab enthusiasts, 3D printer users, IoT tinkerers
- Personal use cases drive workplace adoption

**Why This Is a Strategic Asset:**

**1. Broader Funnel:**
- Hobbyists become workplace champions
- Personal use validates product before work introduction
- Network effects from diverse use cases

**2. Product Innovation:**
- Hobbyists discover unexpected use cases
- Community feedback drives feature ideas
- Beta testing and early adoption

**3. Viral Growth:**
- Passionate hobbyists evangelize aggressively
- Reddit/HackerNews organic advocacy
- User-generated content and tutorials

**4. Retention:**
- Emotional connection to product (vs just "work tool")
- Multiple use cases (work + home) increase stickiness
- Community support reduces churn

**Ross's Insight:** Kong tried to build enterprise-first and never achieved this hobbyist breadth. Tailscale's wider appeal is a moat that should be protected and nurtured. Any product decisions should consider impact on both enterprise AND hobbyist segments.

### 3. Platform Evolution: The Series D/E Challenge

**Future Vision:**
> Eventually, Tailscale will need to evolve into a multi-product company (Series D/Series E stage) with more than one product growing at 20M+ ARR.

**Ross's Analysis:**

**Current State:**
- Single primary product (Tailscale mesh VPN/network)
- Strong growth but single revenue stream
- Platform under the hood but not exposed

**Why Multi-Product Matters:**

**1. Growth Ceiling:**
- Single product eventually hits TAM limits
- VCs expect multi-product at later stages
- Series D/E valuations require multiple growth vectors

**2. Customer Lifetime Value:**
- Cross-sell opportunities increase LTV
- Platform lock-in reduces churn
- Land-and-expand across products

**3. Market Positioning:**
- "Point solution" vs "platform" perception
- Competitive moat from integrated suite
- Enterprise preference for consolidated vendors

**Timing Recommendation:**
> I don't think we need to launch any new products now, but we should start thinking about how we'll transition Tailscale Cloud into a platform that makes it easy for us to launch new products and enable the product teams to deliver value independently.

**Strategic Priorities (Sequencing):**

**Near-Term (Now - Series C):**
- Focus on core product growth
- Achieve strong Series C position
- Build platform foundations quietly

**Mid-Term (Series C - Series D):**
- **Platform Thinking:**
  - Architecture: Transition Tailscale Cloud → platform
  - APIs: Enable internal teams to build on platform
  - Infrastructure: Multi-tenancy, shared services
  - Organization: Structure for multi-product teams

**Longer-Term (Series D/E):**
- Launch adjacent products on platform
- Target: 2-3 products at 20M+ ARR each
- Examples: Identity/SSO, DNS/filtering, firewall, observability, etc.

**Why Start Thinking Now:**
- Platform transitions take 18-24 months
- Can't wait until Series D pressure hits
- Architecture decisions made today enable/constrain future
- Team structure and culture need evolution

**Ross's Experience:**
- Saw Kong navigate single → multi-product
- Understand organizational challenges
- Know what platform foundations are needed
- Can help plan transition without disrupting current growth

**Key Questions to Explore:**

1. **Platform Foundations:**
   - Is Tailscale Cloud architected for multi-product?
   - What refactoring is needed for platform approach?
   - How to enable independent product team velocity?

2. **Product Strategy:**
   - What adjacent products fit Tailscale's strengths?
   - Which problems do our customers already have?
   - What can leverage existing Tailscale network?

3. **Organizational:**
   - How to structure for multi-product?
   - When to hire dedicated product leads?
   - How to maintain startup velocity at scale?

4. **Market Timing:**
   - When does single-product limit growth?
   - What's the right Series C → D timeframe?
   - How to communicate platform vision without diluting focus?

---

## Detailed Growth Pattern Analysis

### Timeline: 2015-2025 (10 Years)

**Key Phases:**
- **2015-2019:** Kong dominance, pre-Tailscale era
- **2019-2021:** Tailscale emergence, foundation building
- **2021-2025:** Tailscale acceleration, Kong steady state

### Kong: The Steady Leader (Blue Line)

**Pattern: Remarkably Linear**
- Nearly perfect straight-line growth since 2015
- ~4,100 stars/year sustained for decade
- No visible inflection points or slowdowns

**Interpretation:**
- Mature product with consistent market presence
- Proven staying power and relevance
- Reached steady-state adoption curve
- Enterprise focus = predictable but slower growth

**Strengths:**
- Long-term viability proven
- Sustainable growth model
- Market leadership maintained

**Constraints:**
- Linear growth limits (not exponential)
- Plateau effect visible
- Harder to accelerate from mature base

### Tailscale: The Rapid Riser (Orange/Red Line)

**Pattern: Exponential with Inflection**

**Phase 1: Foundation (Late 2019 - Mid 2021)**
- Moderate, steady initial growth
- Building product-market fit
- Community awareness building
- Rate: Slower than Kong's steady state

**Phase 2: Acceleration (Mid-2021 - Present)**
- **Major inflection point around mid-2021**
- Dramatically steeper slope
- Current rate exceeds Kong's mature rate
- Sustained acceleration for 4+ years

**Inflection Catalysts (Mid-2021):**

**Product Maturity:**
- Enterprise features (ACLs, SSO, audit logs) reached viability
- Stability and reliability for production use
- Feature parity with traditional VPN alternatives

**Market Timing:**
- COVID remote work surge (2020-2021)
- Zero-trust security trend acceleration
- Cloud-native infrastructure adoption
- WireGuard becoming mainstream

**Fundraising:**
- Series A ($12M, May 2020) → early scale
- Series B ($100M, May 2022) → GTM expansion
- Capital enabled marketing, sales, support scaling

**Word-of-Mouth:**
- Network effects reaching critical mass
- Reddit/HackerNews viral discussions
- User-generated content explosion
- Community ecosystem (Headscale) validation

**Content Marketing:**
- Avery Pennarun's blog posts (viral technical content)
- "The New Internet" vision resonating
- Technical depth attracting engineers

**Customer Validation:**
- Major logos (Instacart, Duolingo, etc.)
- Public case studies demonstrating value
- Enterprise credibility building

**Competitive Positioning:**
- Clear differentiation vs traditional VPNs
- "It just works" vs OpenVPN complexity
- WireGuard performance advantage proven

---

## Strategic Implications for Tailscale

### 1. Similar Playbooks, Different Execution

**Shared Characteristics:**
- Infrastructure category (developer tools)
- Open-source alignment strategy
- Developer-first GTM approach
- Bottom-up adoption motion
- Freemium → Enterprise path
- Community investment (Reddit, GitHub, docs)
- Network effects and viral growth

**Critical Difference: PLG Execution**
- Kong: OSS → Enterprise (sales-led)
- Tailscale: OSS → PLG → Enterprise (product-led)

**Result:**
- Tailscale achieving faster growth with better unit economics
- Kong trying to retrofit PLG (harder, later)
- Validates Tailscale's PLG-first approach

### 2. Current Position: High-Growth Inflection

**Not at Plateau (Unlike Kong):**
- Kong reached steady state ~2018-2019
- Tailscale still accelerating (4+ years post-inflection)
- Opportunity for continued high growth

**Advantages:**
- More growth potential ahead
- Can influence trajectory at critical moment
- Market still expanding (tailwinds)
- Product-market fit proven and scaling

**Challenges:**
- Sustaining acceleration is hard
- Competition increasing (ZeroTier, Netmaker, Twingate)
- Enterprise sales motion still maturing
- International expansion needed

### 3. Ross's Unique Value Proposition

**I've Navigated This Exact Phase at Kong (~2018-2019):**

**Product Experience:**
- Balancing enterprise features vs community needs
- Feature prioritization at scale
- Technical debt management during growth
- Platform vs point-solution decisions

**GTM Experience:**
- 10,000+ customer scaling challenges
- Support and documentation scaling
- Partner ecosystem development
- International expansion

**Organizational Experience:**
- Team structure for growth
- Hiring and culture at inflection point
- Process vs velocity trade-offs
- Cross-functional alignment

**Strategic Experience:**
- OSS licensing decisions (saw Kong's challenges)
- Enterprise vs PLG balance (Tailscale doing it better)
- Multi-product evolution thinking (preparing for Series D/E)
- Market category definition and positioning

**Pattern Matching:**
- Tailscale ~2024 = Kong ~2018-2019
- I know what works and what doesn't
- Can anticipate challenges before they hit
- Understand both enterprise and PLG playbooks

---

## Competitive Positioning: Kong vs Tailscale

### Category Differences

**Kong: API Gateway / Management**
- Developer infrastructure
- Backend/microservices focus
- Enterprise IT/platform teams
- Technical/professional use

**Tailscale: Mesh VPN / Networking**
- Developer AND hobbyist infrastructure
- Broad use case spectrum
- IT, DevOps, AND individuals
- Professional + personal use

**Market Implications:**
- Tailscale's broader appeal = larger TAM potential
- Hobbyist segment drives virality
- Multiple use cases per user increase stickiness
- Community breadth is competitive moat

### GTM Differences

**Kong:**
- Enterprise sales-led (higher touch)
- Longer sales cycles
- Higher ACV, fewer deals
- Traditional enterprise motion

**Tailscale:**
- Product-led growth (lower touch)
- Faster adoption cycles
- Lower ACV, higher volume
- Modern SaaS motion

**Unit Economics:**
- Tailscale's CAC inherently lower (PLG)
- Kong's LTV potentially higher (larger deals)
- Tailscale can scale faster (self-service)
- Kong more capital-intensive (sales team)

### Community Differences

**Kong:**
- Professional developer community
- Enterprise-focused discussions
- Less personal attachment
- Utilitarian relationship

**Tailscale:**
- Broader community (professionals + hobbyists)
- Passionate advocacy
- Emotional connection to product
- Community-driven innovation

**Strategic Insight:** Tailscale's community breadth is a competitive advantage that Kong never achieved and is difficult to build retroactively.

---

## Key Takeaways for Interview

### 1. Demonstrate Deep Understanding

**Data-Driven Analysis:**
- Researched GitHub star growth trajectories
- Compared against Kong's proven playbook
- Identified key inflection points and drivers
- Understand metrics beyond vanity (CAC, ACV, customer counts)

**Strategic Pattern Recognition:**
- Both execute PLG in infrastructure
- Tailscale doing it better (OSS→PLG vs OSS→Enterprise)
- Currently at exciting growth inflection
- Your Kong experience directly applicable

### 2. Unique Value Proposition

**You've Lived This Journey:**
- Navigated Kong through similar phase (~2018-2019)
- Understand scaling challenges at 10K+ customers
- Know product/GTM trade-offs at inflection points
- Can pattern-match Kong's evolution to Tailscale's future

**Both Playbooks:**
- Understand enterprise sales-led (Kong)
- Appreciate PLG advantages (Tailscale doing better)
- Can help protect PLG while building enterprise
- Know pitfalls of each approach

### 3. Strategic Insights to Highlight

**PLG Protection:**
- Tailscale's CAC advantage is significant
- Strategic licensing decisions are critical
- Headscale hire was smart (ecosystem support)
- Free tier fuels enterprise pipeline

**Community Breadth:**
- Hobbyist appeal is unique asset
- Broader than Kong's enterprise-only community
- Drives viral growth and innovation
- Should inform product decisions

**Platform Future:**
- Multi-product evolution needed (Series D/E)
- Start planning now, execute later
- Platform foundations enable independent teams
- Adjacent products leverage Tailscale network

**Growth Trajectory:**
- Not at plateau (advantage over Kong)
- Inflection sustained 4+ years (not a fluke)
- Rate exceeds Kong's (bullish signal)
- Potential to surpass Kong's scale

### 4. Questions to Ask in Interview

**Product Strategy:**
- What caused the mid-2021 inflection? Can we trigger another?
- How are you thinking about free vs paid tier evolution?
- What's the vision for platform vs point solution?
- How do you balance enterprise features with hobbyist appeal?

**GTM Evolution:**
- How are you scaling enterprise sales without losing PLG advantage?
- What's the international expansion strategy?
- How do you think about CAC and unit economics?
- What's the path to multiple 20M+ ARR products?

**Organizational:**
- How is the team structured for this growth phase?
- What are the scaling challenges you're facing?
- How do you maintain velocity while adding process?
- What keeps you up at night about the next 12-24 months?

**Headscale/Ecosystem:**
- How do you think about Headscale relationship long-term?
- What licensing decisions are you considering?
- How do you balance openness with monetization?

### 5. Compelling Interview Narrative

**Opening:**
> "I analyzed Tailscale's GitHub star growth against Kong's trajectory. The parallels are striking—both executing successful PLG in infrastructure—but Tailscale is doing it better. You've nailed the OSS→PLG transition that Kong never achieved. Your growth rate now exceeds Kong's despite being 5 years younger, and you're at the exact inflection phase I experienced at Kong around 2018-2019."

**Value Proposition:**
> "I've navigated this journey before. I know what works—protecting your PLG advantage, nurturing the hobbyist community that Kong never had, planning for the multi-product platform evolution you'll need at Series D/E. The star history proves you're on a proven path. I've already successfully walked it, and I can help you execute the next phase even better than Kong did."

**Strategic Depth:**
> "What excites me most is that you haven't plateaued. Kong reached steady state; you're still accelerating. I understand both the enterprise sales-led and PLG playbooks. I can help you scale enterprise without sacrificing the PLG magic that's driving your growth. And I'm thinking ahead—how do we build the platform foundations now that enable independent product teams when you need multiple 20M+ ARR products in a few years?"

**Personal Connection:**
> "Your community breadth—especially the hobbyist appeal—is something Kong never achieved. I find it fascinating how active r/Tailscale is. That's a strategic moat. Those hobbyists become workplace champions. They discover use cases you'd never imagine. That passion is precious and should inform how we think about product evolution, licensing decisions, and the Headscale ecosystem."

---

## Conclusion

The Kong vs Tailscale comparison reveals two successful infrastructure companies at different maturity stages executing variations of the same PLG playbook. Kong demonstrates long-term viability with steady 4K stars/year growth over a decade, but never fully transitioned to product-led growth. Tailscale shows superior execution of OSS→PLG motion, achieving accelerating growth that now exceeds Kong's rate despite a 5-year disadvantage.

**For Ross:** This analysis demonstrates you understand both playbooks intimately. You've lived Kong's OSS→Enterprise journey and can see where Tailscale's OSS→PLG approach is superior. Your pattern recognition from Kong's evolution (2015-2025) maps directly to Tailscale's current phase (2019-2025). You can help them:

1. **Protect their PLG advantage** through careful licensing decisions
2. **Leverage their community breadth** (hobbyists + professionals) as a moat
3. **Plan platform evolution** for multi-product future (Series D/E readiness)
4. **Sustain growth acceleration** by learning from Kong's plateau

The star history isn't just interesting—it's evidence that Tailscale is on a proven path, executing it better than Kong did, at the exact inflection point where your experience is most valuable. You're not just bringing general product leadership; you're bringing pattern-matched wisdom from having lived this exact journey at a parallel company.

**Strategic Positioning:** You understand their present (Kong ~2019), their immediate future (Kong ~2020-2022), and their long-term challenge (multi-product platform). You've already navigated this path successfully. Now you can help them navigate it even better.

---

## Appendix: Data Sources & Methodology

**GitHub Star History:**
- Image: `05_Attachments/tailscale-kong-star-history.png`
- Source: star-history.com comparison tool
- Timeline: 2015-2025 (10 years)
- Data points: Continuous tracking, annual markers

**Customer Counts:**
- Kong: ~10,000 paid customers (public data)
- Tailscale: 10,000+ paid customers (announced 2024)

**Revenue/ACV Inference:**
- Kong: Higher ACV implied by revenue vs customer count ratio
- Tailscale: Lower ACV, higher volume (PLG model)
- Methodol: Directional based on public data, not precise

**Community Metrics:**
- r/Tailscale: 41,000+ members, highly active
- r/Kong: Exists but significantly less active
- Source: Reddit subscriber counts, post frequency

**Limitations:**
- GitHub stars are vanity metric (directional, not absolute)
- Customer counts may not be exactly comparable (SMB vs Enterprise mix)
- Revenue figures not publicly disclosed for precise ACV calculation
- Community engagement subjective (activity levels vs just member counts)

**Analysis Confidence:**
- Growth pattern trends: High confidence (visual data clear)
- Strategic insights: Medium-high (based on public info + Ross's Kong experience)
- Future projections: Speculative (trend-based, not guaranteed)
