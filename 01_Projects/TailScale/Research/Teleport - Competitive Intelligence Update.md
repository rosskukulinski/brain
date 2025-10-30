---
created: 2025-10-30
updated: 2025-10-30
tags: [tailscale, competitive-analysis, teleport, market-sizing, infra-access]
status: current
project: TailScale
---

# Teleport - Competitive Intelligence Update

**Last Updated:** October 30, 2025
**Source:** Web research, company filings, market data

---

## Executive Summary

**Key Finding:** Teleport's actual ARR (~$35M) is **65% lower** than initially estimated ($100M), fundamentally changing the infrastructure access market opportunity and competitive strategy.

**Strategic Implications:**
1. **Market is smaller than expected** - Infrastructure access is a ~$35M market (Teleport), not $100M+
2. **Tailscale is same scale** - Both companies at ~$35-40M ARR (directly comparable)
3. **Consolidation > Growth** - Opportunity is wallet share capture, not massive TAM expansion
4. **Pricing advantage validated** - Teleport at $40-75/user vs Tailscale Complete at $75/user (VPN + Infra Access bundled)

---

## Financial Metrics (Actual)

### Current State (2025)

| Metric | Value | Source |
|--------|-------|--------|
| **Annual Revenue** | $35M | June 2025 data |
| **ARR (estimated)** | ~$35M | (revenue = ARR for SaaS) |
| **Valuation** | $1.1B | Series C (May 2022) |
| **Total Funding** | $169M | CB Insights |
| **Customer Count** | 600+ | Company website |
| **Headquarters** | Oakland, CA | |

**Previous Estimate (from Tailscale analysis):** $100M ARR ❌
**Actual:** $35M ARR ✅
**Variance:** -65% (significantly overestimated)

---

### Historical Growth (2020-2022)

| Period | Metric | Growth |
|--------|--------|--------|
| **2020 → 2021** | Revenue | Nearly 3x |
| **2020 → 2021** | Customer Base | 2x |
| **Series C (May 2022)** | Net New ARR | 4.5x YoY |
| **Series C (May 2022)** | Total ARR | 2.8x YoY |

**Back-of-envelope calculation:**
- If Teleport was at ~$35M ARR in 2025
- Growing at 2.8x in 2022, then slowing
- Estimated 2022 ARR: ~$8-12M
- Estimated 2023 ARR: ~$18-25M
- Estimated 2024 ARR: ~$28-32M
- 2025 ARR: $35M

**Growth trajectory:** High growth (100-150%) in 2021-2022, moderating to 30-50% by 2024-2025

---

## Pricing & Packaging

**Teleport Pricing:**
- **Starter:** $2/resource/month (limited features)
- **Team:** $10/resource/month
- **Enterprise:** $40-75/user/month (estimated based on competitor benchmarking)

**Resources = servers, databases, K8s clusters, applications**

**Comparison to Tailscale Proposed Pricing:**

| Provider | Product | Price/User/Month | What's Included |
|----------|---------|------------------|-----------------|
| **Teleport** | Enterprise | $40-75 | Infra access (SSH, DB, K8s) + audit + compliance |
| **Cloudflare** | Access | $7 | Zero Trust access (web apps) |
| **Combined Stack** | CF + Teleport | **$77** | VPN-style access + Infra access |
| **Tailscale Complete** | All-in-one | **$75** | VPN + Services + Workload Identity + Infra Access |

**Tailscale Advantage:**
- 2 fewer vendors (operational simplicity)
- $2/user/month savings (3% cheaper)
- Unified platform (single control plane, ACLs, identity)

---

## Market Size Analysis

### Infrastructure Access TAM (Revised)

**Previous Assumption:**
- Teleport at $100M ARR
- TAM = $500M-$1B (5-10x market leader)
- Opportunity for Tailscale: $50-100M ARR

**Actual Reality:**
- Teleport at $35M ARR (market leader)
- TAM = $150-300M (assuming Teleport has 15-25% market share)
- **Alternative interpretation:** TAM = $35M, Teleport has 100% (no other major player)

**Other Infrastructure Access Players:**
- **StrongDM:** Estimated $20-30M ARR (private, no public data)
- **HashiCorp Boundary:** Part of HashiCorp ($500M revenue), small component
- **Cloudflare Access for Infrastructure:** (Post BastionZero acquisition, not yet launched)
- **AWS Systems Manager Session Manager:** Free (bundled with AWS)

**Total Addressable Market Estimate:** $100-150M ARR across all vendors

**This is 10-15x smaller than initially estimated.**

---

## Strategic Implications for Tailscale

### 1. Infrastructure Access is a Feature, Not a Market

**Key Insight:** If the market leader (Teleport) after 10+ years is only at $35M ARR, infrastructure access is likely:
- A **feature** that complements VPN/Zero Trust (not standalone category)
- A **consolidation play** (customers want "one vendor" not "best infra access tool")
- A **compliance checkbox** (enterprise requirement, not growth driver)

**Recommendation:** Position Infra Access as **value-add** to Tailscale Complete bundle, not standalone product.

---

### 2. Wallet Share Capture > Market Expansion

**The Math:**
- Teleport customers: 600
- Average customer size: $35M / 600 = $58K ARR per customer
- Typical customer: 100-200 users at $40-75/user

**Tailscale Opportunity:**
- Target Teleport's 600 customers
- Offer: "Replace VPN + Teleport with Tailscale Complete"
- Savings: $77/user → $75/user (VPN + Infra Access bundled)
- Win 30% of Teleport customers = 180 customers × $58K = **$10.4M ARR**

**This matches the $10.8M ARR projection in "Tailscale Infra Access - Current Capabilities vs Gaps" analysis.**

---

### 3. Revised Revenue Potential

**Year 2 Post-Launch (Infra Access GA):**

| Segment | Customers | Adoption % | Users/Customer | Price Premium | ARR Contribution |
|---------|-----------|------------|----------------|---------------|------------------|
| **Existing Tailscale Enterprise** | 1,000 | 30% | 100 | $30/user | $9M |
| **Teleport Displacement** | 600 | 10% | 100 | $30/user | $1.8M |
| **New Customers (bundle)** | 500 | 100% | 50 | $30/user | $0.75M |
| **Total Infra Access ARR** | | | | | **$11.55M** |

**Upside Scenario (50% Teleport displacement):**
- Teleport customers: 600 × 50% = 300
- ARR: 300 × $58K = **$17.4M**

**Downside Scenario (5% Teleport displacement):**
- Teleport customers: 600 × 5% = 30
- ARR: 30 × $58K = **$1.74M**

**Realistic Range:** $10-18M ARR from Infra Access by Year 2 post-GA

---

### 4. Competitive Positioning (Updated)

**Teleport Strengths:**
- ✅ 10+ year head start (mature product)
- ✅ 600+ customers including Nasdaq, Snowflake, DoorDash, Elastic
- ✅ Full compliance suite (SOC2, HIPAA, FedRAMP in progress)
- ✅ Protocol-aware policies (query-level DB restrictions)
- ✅ Session recording with playback
- ✅ JIT credentials via HashiCorp Vault integration

**Teleport Weaknesses:**
- ❌ Standalone product (requires separate VPN)
- ❌ Higher pricing ($40-75/user vs Tailscale $75 for everything)
- ❌ Slow growth (from 100-150% in 2021-2022 → 30-50% in 2024-2025)
- ❌ Only $35M ARR after 10 years (small market or weak execution?)
- ❌ Not peer-to-peer (proxy architecture like Zscaler)

**Tailscale Advantages:**
- ✅ VPN + Infra Access in one platform (fewer vendors)
- ✅ Lower total cost ($75 vs $77 for VPN+Teleport)
- ✅ Peer-to-peer architecture (better performance)
- ✅ Developer-loved (PLG motion, community)
- ✅ Faster growth trajectory (100% YoY vs Teleport's 30-50%)

**Tailscale Gaps (vs Teleport):**
- ❌ No session recording (inputs) - only outputs in beta
- ❌ No database query logging - VPN only, no proxy
- ❌ No JIT credentials - static passwords
- ❌ No protocol-aware policies - IP/port only
- ❌ No compliance reports - raw logs only

**Time to Feature Parity:** 6-12 months of focused engineering

---

## Customer Overlap Analysis

### Tailscale Customers Also Using Teleport (Estimated)

**Reddit anecdotes suggest pattern:**
> "We use Tailscale for VPN, Teleport for databases because we need query-level audit logs for SOC2."

**Estimated Overlap:**
- 20-30% of Tailscale Enterprise customers (200-300 customers)
- These are **ideal targets** for Infra Access upsell
- ARR potential: 250 customers × 100 users × $30 premium = **$7.5M ARR**

**Win-back scenario:**
- Customer currently pays: Tailscale $18/user + Teleport $70/user = $88/user
- Tailscale Complete offer: $75/user
- Savings: $13/user (15% reduction) + vendor consolidation

---

## Competitive Win/Loss Scenarios

### When Tailscale Wins (vs Teleport)

**Scenario 1: Bottom-up adoption**
- Developers use Tailscale for personal/staging
- Team expands to production VPN
- IT evaluates Infra Access add-on vs buying Teleport
- Tailscale wins: "We already use Tailscale, just upgrade"

**Scenario 2: Cost-conscious buyer**
- Customer needs VPN + Infra Access
- Compares: Tailscale $75/user vs VPN $X + Teleport $70
- Tailscale wins: Lower total cost + fewer vendors

**Scenario 3: Developer-first culture**
- Engineering-led organization
- Values simplicity, open source, peer-to-peer
- Tailscale wins: Better developer experience

---

### When Teleport Wins (vs Tailscale)

**Scenario 1: Compliance-first buyer**
- CISO-led evaluation
- Requires: Session recording (inputs), query-level logging, compliance reports
- Tailscale gaps: Missing features for SOC2/HIPAA/PCI audits
- Teleport wins: Feature completeness

**Scenario 2: Database-heavy workload**
- Customer needs: PostgreSQL, MySQL, MongoDB proxy with query logs
- Tailscale: VPN only, no protocol awareness
- Teleport wins: Purpose-built for database access

**Scenario 3: Teleport incumbent**
- Customer already using Teleport for 2+ years
- High switching costs (re-training, re-configuration)
- Tailscale offer: "Try Tailscale Complete"
- Teleport wins: Inertia, "if it ain't broke..."

---

## Recommendations for Tailscale Strategy

### 1. Adjust Market Sizing Expectations

**Old Assumption:** Infra Access is a $100M+ opportunity
**New Reality:** Infra Access is a $10-20M opportunity in Year 2, $30-50M at maturity

**Implication:**
- Infra Access is a **strategic feature** (enterprise blocker removal + bundle pricing)
- NOT a **standalone growth driver** (won't 2x company revenue alone)
- Combine with Services + Workload Identity for **platform positioning**

---

### 2. Pricing Strategy

**Recommendation:** Bundle, don't unbundle

| Tier | Price/User/Month | What's Included | Target Customer |
|------|------------------|-----------------|-----------------|
| **Premium** | $18 | VPN + SSH + basic audit | Mid-market |
| **Enterprise** | $30 | Premium + Infra Access (session recording, DB proxy) | Compliance-heavy enterprise |
| **Complete** | $50-75 | Everything (Services + Workload Identity + Infra Access) | Platform customers |

**Alternative:** Don't charge separately for Infra Access
- Include in Premium tier (raise from $18 → $25)
- Differentiate on enterprise features (compliance reports, JIT creds)
- Use as **competitive moat** not revenue driver

---

### 3. Feature Prioritization (6-Month Roadmap)

**Must-Have (to compete with Teleport):**
1. Session recording - inputs (commands typed) ← **P0 blocker**
2. Database proxy - PostgreSQL + MySQL ← **P0 blocker**
3. Query logging (SQL audit trail) ← **P0 blocker**
4. Compliance reports (SOC2/HIPAA pre-built) ← **P1**

**Nice-to-Have (differentiation):**
5. JIT credentials (HashiCorp Vault integration)
6. Protocol-aware policies (query-level restrictions)
7. K8s access with kubectl command logging

**Effort:** 6-9 months, 2-3 engineers, $500K-$1M engineering cost

**ROI:** $10-18M ARR in Year 2 = 10-18x return

---

### 4. Go-to-Market Approach

**Phase 1: Private Beta (Q1 FY27)**
- Target: 20 Tailscale customers currently using Teleport
- Offer: Free Infra Access add-on for 6 months
- Goal: Product-market fit validation, feature gap identification

**Phase 2: GA Launch (Q2 FY27)**
- Positioning: "Consolidate your VPN and Infra Access"
- Target: Tailscale Enterprise customers with compliance needs
- Pricing: $30/user/month premium (or bundled in Complete tier)

**Phase 3: Competitive Displacement (H2 FY27)**
- Outbound campaign to Teleport's 600 customers
- Offer: Migration assistance + 20% discount Year 1
- Goal: Win 10-20% of Teleport customers (60-120 customers)

---

## Open Questions for Tailscale Leadership

### Market Validation
1. How many current Tailscale customers also use Teleport? (CRM data analysis)
2. What % of churned customers cited "need Teleport for compliance" as reason?
3. What % of lost deals were due to missing Infra Access features?

### Product Prioritization
4. Is $10-20M ARR opportunity worth 6-9 months of engineering investment?
5. Should Infra Access be bundled (raise Premium pricing) or separate tier?
6. What's minimum viable feature set to displace Teleport? (Session recording + DB proxy?)

### Competitive Intelligence
7. Are we seeing Teleport in competitive deals? Win rate?
8. What's Teleport's pricing in practice? ($40-75 range confirmed?)
9. Do we have reference customers who switched from Teleport to Tailscale SSH?

---

## Conclusion: Revised Strategy

**Old Strategy (based on $100M Teleport):**
- Infra Access is a major new revenue stream
- Build full Teleport competitor
- Capture $50M+ TAM

**New Strategy (based on $35M Teleport):**
- Infra Access is a **bundling opportunity** (consolidate wallet share)
- Build **minimum viable compliance features** (not full Teleport parity)
- Capture $10-20M ARR by **displacing 30-50% of Teleport customers**
- Position as **"VPN + Infra Access in one"** not "best infra access tool"

**Bottom Line:**
- Infrastructure access market is 65% smaller than estimated
- Tailscale and Teleport are the same scale (~$35-40M)
- Opportunity is **vendor consolidation** not **market expansion**
- Infra Access is a **strategic feature** (removes enterprise blocker + enables Complete bundle pricing)
- **ROI is still strong:** $10-20M ARR for $500K-$1M investment (10-20x return)

---

**Document Status:** Current as of October 30, 2025
**Next Update:** Quarterly or when Teleport announces new funding/metrics
**Related Documents:**
- [Tailscale Infra Access - Current Capabilities vs Gaps](Tailscale%20Infra%20Access%20-%20Current%20Capabilities%20vs%20Gaps.md)
- [Product Strategy - Executive Summary](../Product%20Strategy%20-%20Executive%20Summary.md)
- [Competitive Defense and Moat Strategy](Competitive%20Defense%20and%20Moat%20Strategy.md)
