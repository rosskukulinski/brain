---
created: 2025-10-24
updated: 2025-10-24
tags: [tailscale, gap-analysis, roadmap, github, customer-feedback]
status: complete
project: TailScale
sources:
  - EPD Team Q4 FY26 Plan.csv
  - GitHub Repository Analysis - 2025-10-24.md
---

# Q4 Roadmap vs GitHub Issues - Gap Analysis

Cross-reference of Q4 FY26 roadmap items against top GitHub customer pain points to identify coverage and gaps.

## Executive Summary

**Coverage Score: 60% (3 of 5 critical pain points addressed)**

### Addressed Pain Points ✅
1. **DNS & Custom Domain Management** - Multiple Q4 items
2. **Multi-Tailnet Access** - Partially addressed (multi-tenancy alpha)
3. **Local Network Route Optimization** - Traffic steering improvements

### Major Gaps ❌
4. **Mobile Battery Drain** - NO roadmap items
5. **Wake-on-LAN Support** - NO roadmap items

### Additional Gaps
- **mDNS Support** (4th most discussed issue) - NO roadmap items
- **Mullvad Integration** (3rd highest reactions) - NO roadmap items
- **Platform Parity Issues** - Limited attention

---

## Detailed Pain Point Mapping

### 1. DNS & Custom Domain Management ✅ WELL COVERED

**GitHub Issues:**
- #1543 - Custom DNS Records (highest engagement)
- #4221 - Custom Domains for MagicDNS
- #11563 - Custom Domains for Funnel
- #7081 - TLS Wildcard Certificates

**Q4 Roadmap Items:**

| Item | Priority | Stage | Team | Driver | Status |
|------|----------|-------|------|--------|--------|
| **MagicDNS names** | P3 | GA | Networking | Kabir Sikand | Problem doc done, 1-pager in progress |
| **Bring your own domain** | P2 | Alpha | Networking | Kabir Sikand | Not started |
| **SplitDNS rule configuration** | P2 | Beta | Networking | Kabir Sikand | Problem doc done, 1-pager done |

**Analysis:**
- ✅ Strong Q4 focus on DNS customization
- ⚠️ "MagicDNS names" is only P3 despite being #1 GitHub issue
- ✅ Multiple approaches (custom records, BYOD, split rules)
- ⚠️ Documentation incomplete for BYOD (not started)

**Coverage: 90%** - Well addressed but priority misalignment

---

### 2. Multi-Tailnet Access ⚠️ PARTIALLY ADDRESSED

**GitHub Issue:**
- #183 - Multiple Tailnets Simultaneously (276+ reactions, 52 comments)
- Priority: P3 "Can't get started"
- Impact: L4 "Most users"
- **CRITICAL:** "Blocks enterprise adoption and partnerships"

**Q4 Roadmap Items:**

| Item | Priority | Stage | Team | Driver | Commit | Status |
|------|----------|-------|------|--------|--------|--------|
| **Multiple IdP and domain support for MT alpha** | P1 | Stretch/Alpha | Identity | Sam Linville | Stretch | Not started |
| **Tailnet access policies for MT alpha** | P2 | Alpha | Identity | Sam Linville | No | Not started |
| **Tailnet sharing (peering)** | P0 | (none) | GM | Sam Linville | No | Unstaffed by PM |

**Analysis:**
- ⚠️ Multi-tenancy (MT) != Multi-tailnet access
  - MT allows one org to manage multiple networks
  - Users want to connect to multiple networks simultaneously
- ❓ "Tailnet sharing (peering)" might address this but is **unstaffed by PM**
- ⚠️ P0 item with no PM staffing is a red flag
- ❌ Original GitHub issue may not be fully addressed

**Coverage: 40%** - Related work, but not the same problem

**Critical Question:** Does "Tailnet sharing" solve #183, or is this organizational multi-tenancy only?

---

### 3. Local Network Route Optimization ✅ ADDRESSED

**GitHub Issue:**
- #1227 - Bypass Relay with Local Routes (88+ reactions, 155+ comments)
- Priority: P3 "Can't get started"
- **Pain:** Forces traffic through relay even with direct local access

**Q4 Roadmap Items:**

| Item | Priority | Stage | Team | Driver | Commit | Status |
|------|----------|-------|------|--------|--------|--------|
| **Traffic steering** | P1 | Beta | Data plane | Kabir Sikand | No | Problem doc done |
| **Next-generation app connector** | P0 | POC | Networking | Kabir Sikand | Yes | Problem doc done |
| **Option to not drop CGNAT** | ? | ? | ? | ? | ? | Empty row |

**Description (Traffic Steering):**
> "Iterate on Regional Routing to provide a more reliable and accurate steering algorithm for selection of overlapping subnet routes, app connectors, exit nodes, and Services."

**Analysis:**
- ✅ "Traffic steering" directly addresses routing intelligence
- ✅ P1 priority, Beta stage - good progress
- ⚠️ "Option to not drop CGNAT" row is empty - unclear status
- ✅ Next-gen app connector may improve hybrid deployment scenarios

**Coverage: 80%** - Strong technical approach, unclear execution timeline

---

### 4. Mobile Battery Drain ❌ NOT ADDRESSED

**GitHub Issue:**
- #3363 - Mobile Battery Drain (iOS/Android)
- **Impact:** Can reduce iOS runtime by 50%
- Team acknowledges issue, "largely dependent on configuration"

**Q4 Roadmap Items:**
- ❌ **NONE FOUND**

**Possibly Related:**
- "Automated testing" (line 59, P0, Tooling/Clients) - Could include battery benchmarking?
- "Feature parity work for Windows client" (line 7, P2) - No mobile focus
- "Windowed client" work (macOS/Windows) - Desktop only

**Analysis:**
- ❌ Major gap - no Q4 items specifically address mobile optimization
- ⚠️ High user impact (50% battery reduction)
- ❓ May be deprioritized due to "configuration-dependent" nature
- 💡 Opportunity: Mobile optimization sprint or investigation

**Coverage: 0%** - Critical gap

---

### 5. Wake-on-LAN Support ❌ NOT ADDRESSED

**GitHub Issue:**
- #306 - Wake-on-LAN (Top 6 by reactions)
- **Use Case:** Wake sleeping home/office machines remotely

**Q4 Roadmap Items:**
- ❌ **NONE FOUND**

**Analysis:**
- ❌ Not on Q4 roadmap
- ℹ️ Likely deprioritized as "quality of life" vs critical
- ℹ️ Technical challenges noted: L2 network ID, privacy concerns
- ℹ️ Dependencies: LAN discovery infrastructure (not on roadmap either)

**Coverage: 0%** - Not planned for Q4

---

## Additional High-Engagement Issues

### mDNS Support ❌ NOT ADDRESSED

**GitHub Issue:**
- #1013 - mDNS Support (4th most discussed, 100+ comments)
- **Use Case:** Local service discovery (printers, Chromecast, etc.)

**Q4 Roadmap:**
- ❌ **NONE FOUND**

**Coverage: 0%**

---

### Mullvad Integration ❌ NOT ADDRESSED

**GitHub Issue:**
- #9301 - Mullvad Account Integration (3rd highest reactions)
- **Use Case:** Use existing Mullvad VPN subscriptions with Tailscale

**Q4 Roadmap:**
- ❌ **NONE FOUND**

**Analysis:**
- May be strategic decision (separate products)
- Could be partnership/business decision rather than technical

**Coverage: 0%**

---

### Platform Parity Issues ⚠️ PARTIALLY ADDRESSED

**GitHub Issues:**
- #2791 - Windows non-admin installation
- #12086 - Android VPN On Demand
- #987 - macOS system/server mode

**Q4 Roadmap Items:**

| Item | Platform | Priority | Stage |
|------|----------|----------|-------|
| **Windowed client for Windows** | Windows | P1 | Beta |
| **Windowed client for macOS** | macOS | P2 | GA |
| **Feature parity work for Windows client** | Windows | P2 | N/A |

**Analysis:**
- ✅ Active Windows/macOS GUI improvements
- ❌ No Android-specific improvements
- ❌ No non-admin Windows installation work
- ⚠️ Desktop focus, mobile gaps

**Coverage: 30%** - Desktop improvements only

---

## Coverage Summary by Strategic Theme

### Core VPN (22 Q4 items)
- ✅ DNS customization (MagicDNS names, BYOD, SplitDNS)
- ✅ Traffic steering and routing improvements
- ✅ Desktop client improvements (Windows/macOS)
- ❌ Mobile battery optimization
- ❌ Wake-on-LAN
- ❌ mDNS support

### Tailscale as a Platform (17 Q4 items)
- ✅ Services architecture (multiple items)
- ✅ Workload identity (P0, GA)
- ⚠️ Multi-tailnet/sharing (unstaffed)
- ❌ Mullvad integration

### Enterprise & Identity
- ✅ Self-serve domain verification (P0)
- ✅ Self-serve IdP changes (P0)
- ✅ User sessions (P1)
- ⚠️ Multi-tenancy alpha (stretch goal)

---

## Critical Gaps Analysis

### High-Impact Gaps (Should Consider)

1. **Mobile Battery Drain** - 0% coverage
   - **Impact:** High (affects UX and adoption)
   - **Difficulty:** Medium (acknowledged complexity)
   - **Recommendation:** Add investigation/optimization item

2. **mDNS Support** - 0% coverage
   - **Impact:** Medium-High (4th most discussed)
   - **Difficulty:** Medium (architectural implications)
   - **Recommendation:** Consider for Q1 or add design doc

3. **Multi-Tailnet True Support** - 40% coverage
   - **Impact:** CRITICAL (blocks enterprise partnerships)
   - **Difficulty:** High (architectural challenge)
   - **Recommendation:** Clarify if "Tailnet sharing" solves this; if not, prioritize

### Acceptable Gaps (Can Defer)

4. **Wake-on-LAN** - 0% coverage
   - **Impact:** Medium (quality of life)
   - **Difficulty:** Medium-High (dependencies)
   - **Rationale:** Nice-to-have, not blocking

5. **Mullvad Integration** - 0% coverage
   - **Impact:** Low-Medium (partnership/business decision)
   - **Difficulty:** Unknown
   - **Rationale:** May be strategic choice

### Priority Misalignments

**GitHub #1 Issue vs Q4 Priority:**
- **GitHub:** Custom DNS Records (#1543) - Highest overall engagement
- **Q4:** MagicDNS names - **Only P3**

**Recommendation:** Consider elevating MagicDNS names to P1 or P2

---

## Roadmap Coverage by Team

### Well-Aligned Teams
- **Networking (Kabir Sikand)** - Addressing DNS and routing pain points
- **Identity (Sam Linville)** - Self-serve features reduce friction
- **DevEx** - Platform capabilities for developers

### Gap Areas by Team
- **Clients Team** - No mobile optimization work
- **Data Plane Team** - Could own battery/performance optimization
- **Platform Team** - Could own mDNS and local discovery

---

## Key Recommendations

### Immediate (Q4 Scope Changes)

1. **Clarify Tailnet Sharing Intent**
   - Is "Tailnet sharing (peering)" solving GitHub #183?
   - If yes: Add PM staffing (currently unstaffed)
   - If no: Add true multi-tailnet item or push to Q1

2. **Elevate MagicDNS Names Priority**
   - Currently P3, but #1 GitHub issue
   - Recommend: P1 or P2

3. **Add Mobile Battery Investigation**
   - At minimum: Add discovery/investigation item
   - Could be lightweight P2 for Data plane or Clients team

### Near-Term (Q1 Planning)

4. **mDNS Support Design Doc**
   - High community demand (4th most discussed)
   - Dependencies: Local network intelligence
   - Recommendation: Add to Q1 as design doc or POC

5. **Wake-on-LAN Design Doc**
   - Quality of life improvement with clear demand
   - Dependencies: LAN discovery
   - Recommendation: Bundle with mDNS investigation

### Strategic Considerations

6. **Multi-Tailnet Architecture**
   - Critical enterprise blocker
   - May require significant architectural work
   - Recommend: Dedicated project team if not already planned

7. **Mobile Platform Investment**
   - Battery optimization
   - Android feature parity (VPN On Demand)
   - iOS feature parity
   - Recommend: Dedicated mobile quarter in FY26

---

## Coverage Metrics

| Category | GitHub Issues | Q4 Items | Coverage |
|----------|---------------|----------|----------|
| **DNS Customization** | 4 top issues | 3 items | 90% ✅ |
| **Multi-Tailnet Access** | 1 critical issue | 1-3 items | 40% ⚠️ |
| **Routing Optimization** | 1 critical issue | 2-3 items | 80% ✅ |
| **Mobile Battery** | 1 high-impact issue | 0 items | 0% ❌ |
| **Wake-on-LAN** | 1 popular issue | 0 items | 0% ❌ |
| **mDNS Support** | 1 highly-discussed | 0 items | 0% ❌ |
| **Platform Parity** | 3+ issues | 2-3 items | 30% ⚠️ |

**Overall Coverage: 60%** (3 of 5 critical pain points substantially addressed)

---

## Questions for Product Leadership

1. **Multi-tailnet vs Multi-tenancy:**
   - Does "Tailnet sharing (peering)" solve the GitHub #183 issue?
   - Why is this P0 item unstaffed by PM?

2. **Mobile Strategy:**
   - Why no Q4 items for mobile battery optimization?
   - Is this deferred to Q1 or deprioritized?

3. **Priority Alignment:**
   - MagicDNS names is #1 GitHub issue but P3 in Q4 - why?
   - What's the philosophy on community feedback vs roadmap?

4. **Local Network Features:**
   - mDNS and Wake-on-LAN have high demand but no roadmap items
   - Is there a strategic reason (architecture, complexity)?

5. **Coverage Gaps:**
   - Are the 40% of unaddressed pain points intentionally deferred?
   - What's the plan for closing these gaps?

---

## Conclusion

The Q4 roadmap shows **strong alignment** with customer pain points in DNS/networking and routing optimization. However, **critical gaps exist** in mobile optimization and true multi-tailnet access.

**Strongest Alignment:**
- DNS customization (3 dedicated items)
- Self-serve enterprise features
- Routing intelligence improvements

**Biggest Risks:**
- Multi-tailnet access may not be truly solved
- Mobile battery drain completely unaddressed
- Popular features (mDNS, WoL) not planned

**Strategic Recommendation:** Consider adding at least one mobile optimization item to Q4 or early Q1, and clarify the multi-tailnet strategy urgently given its enterprise blocking status.
