---
created: 2025-10-24
updated: 2025-10-24
tags: [tailscale, github, customer-research, pain-points]
status: complete
project: TailScale
---

# Tailscale GitHub Repository Analysis

**Research Date:** October 24, 2025
**Repository:** github.com/tailscale/tailscale
**Analysis Focus:** Top issues, customer pain points, common themes

## Executive Summary

Analysis of Tailscale's GitHub repository reveals several critical themes affecting user adoption and satisfaction:

1. **DNS & Custom Domain Management** - Highest engagement (multiple top-10 issues)
2. **Multi-Network Access** - Major blocker for enterprise/multi-context users
3. **Local Network Optimization** - Performance and routing intelligence gaps
4. **Mobile Platform Parity** - Battery life and feature gaps on iOS/Android
5. **Enterprise Features** - Kubernetes, advanced networking, certificate management

## Top Issues by Engagement

### By Reactions (👍)

1. **Custom DNS Records in MagicDNS** (#1543) - Users need friendly hostname aliases
2. **Custom Domains for MagicDNS** (#4221) - Internal domain namespacing
3. **Mullvad Account Integration** (#9301) - Use existing Mullvad subscriptions
4. **Multiple Tailnets Simultaneously** (#183) - Connect work + home networks
5. **mDNS Support** (#1013) - Local service discovery
6. **Wake-on-LAN** (#306) - Remote machine wake capability
7. **Custom Domains for Funnel** (#11563) - Use own domains with Funnel feature
8. **Subnet Sharing** (#1390) - Share entire subnets between users
9. **Sub-subdomains for Funnel** (#8729) - Nested subdomain support
10. **TLS Wildcard Certificates** (#7081) - Certificate management flexibility

### By Comments (Discussion Volume)

1. **Bypass Relay with Local Routes** (#1227, 155+ comments) - Smart routing
2. **Synology Use Cases** (#1995) - NAS platform compatibility
3. **Custom DNS Records** (#1543) - Highest overall engagement
4. **mDNS Support** (#1013) - Service discovery patterns
5. **Mobile Battery Drain** (#3363) - iOS/Android optimization

## Critical Customer Pain Points

### 1. DNS & Custom Domain Management

**Pain:** Users cannot create custom DNS aliases within MagicDNS. Teams need to run external DNS servers for simple hostname mappings.

**Use Cases:**
- Friendly names for services (e.g., "git.company.internal" → staging-server-3)
- Multi-environment namespacing (nas.home vs nas.office)
- Internal service discovery without external dependencies

**Current Workarounds:**
- Run dedicated DNS servers (adds infrastructure complexity)
- Use external DNS providers
- Remember cryptic machine names

**Blockers to Implementation:**
- OS-level DNS routing varies by platform
- Conflict resolution with machine names
- Upstream DNS detection challenges
- ACME certificate integration questions

**Impact:** High - Multiple top-10 issues related to DNS customization

---

### 2. Multi-Tailnet Access

**Pain:** Users cannot connect to multiple Tailscale networks simultaneously on one device.

**Critical Quote:**
> "We're working on a team project with two S&P 500 companies. We already use Tailscale, so we can't juggle our internal network with another one."

**Use Cases:**
- Work + personal networks simultaneously
- Multi-client consulting/contracting
- Enterprise partnerships and collaboration
- Development + production environment access

**Current Workarounds:**
- Run multiple systemd instances (fragile, breaks on updates)
- Proxy through secondary devices with different credentials
- Abandon one network or switch contexts frequently

**Impact:** CRITICAL - Blocks enterprise adoption and partnerships
- 276+ reactions, 52 comments
- Priority: P3 (Can't get started)
- Affects: L4 (Most users)

---

### 3. Local Network Route Optimization

**Pain:** When subnet routes are advertised, Tailscale forces traffic through relay nodes even when machines have direct local network access.

**Technical Issue:**
- Route metrics get changed, prioritizing Tailscale over direct interfaces
- Machines lose direct access to their own local subnet
- Violates principle: direct connections should always win

**Use Cases:**
- Incremental zero-trust rollout in enterprises
- Hybrid environments (some machines on Tailscale, others not)
- Performance-sensitive local network applications

**Compounding Factors:**
- ACL restrictions block unnecessarily routed traffic
- Bandwidth waste for local-to-local communication
- Added latency for direct-capable connections

**Impact:** High - Blocks practical enterprise deployment
- 88+ reactions, 155+ comments
- Priority: P3 (Can't get started)

---

### 4. Mobile Battery Drain

**Pain:** Tailscale can reduce iOS device runtime by 50% in certain configurations.

**Worst-Case Scenario (Confirmed by Team):**
- Always-on exit node routing all traffic
- Subnet routes through exit node
- DNS routing through custom internal servers

**Status:**
- Team acknowledges the issue
- "Largely dependent on configuration"
- No universal quick fix available
- Tracking optimization opportunities

**Impact:** Medium-High - Affects mobile user experience and adoption

---

### 5. Wake-on-LAN Support

**Pain:** Cannot wake sleeping machines on home/office networks through Tailscale.

**Use Case:**
> "I often need to SSH to my Mac at home, but sometimes it's asleep."

**Proposed Solutions:**
- Automatic: Detect unresponsive peer, auto-send wake packet
- Explicit: `tailscale wake <node_name>` command

**Technical Challenge:**
- L2 network identification is difficult with current architecture
- Privacy concerns: WoL packets contain MAC addresses
- Risk of sending to wrong network

**Dependencies:**
- LAN-based peer discovery infrastructure
- Better local network intelligence
- Explicit "LAN ID" properties

**Impact:** Medium - Quality of life feature with clear use case

---

## Common Themes & Patterns

### DNS/Networking Intelligence
- Multiple top-10 issues relate to DNS customization
- Users want Tailscale to be "DNS-aware" and flexible
- Demand for custom domains, CNAME support, mDNS, DoH/DoT
- Pattern: Teams want to reduce external infrastructure dependencies

### Enterprise Adoption Blockers
1. Multi-tailnet support (partnerships impossible)
2. Local route optimization (rollout friction)
3. Advanced certificate management (DevOps workflows)
4. Kubernetes-specific issues (container networking)

### Platform Parity Gaps
- **Windows:** Non-admin installation requested (#2791)
- **Android:** Missing VPN On Demand (#12086)
- **macOS:** System/server mode requested (#987)
- **iOS/Android:** Battery optimization needed (#3363)

### Smart Routing Demands
- Bypass relays when local routes available (#1227)
- Auto-enable exit nodes on untrusted networks (#3302)
- Exclude specific interfaces from discovery (#1552)
- Better VPN interoperability (#1381)

### Service Discovery & Local Network
- mDNS support (#1013) - 4th most discussed
- Wake-on-LAN (#306) - Top 6 by reactions
- Virtual IPs for services (#465)
- Tag-based DNS resolution (#4324)

## Repository Metadata

**Total Labels:** 132 organized labels

**Key Label Categories:**
- **Platforms:** OS-{android, ios, linux, macos, windows, freebsd, etc.}
- **Priority:** P1-P6 (Nuisance → Blocks build)
- **Likelihood:** L1-L5 (Very few → All users)
- **Types:** T0-T8 (New feature → Crash)
- **Features:** dns, exit-node, funnel, ssh, taildrop, acl, kubernetes
- **Status:** needs-triage, needs-decision, planned, on-hold

**Common Issue Types:**
- Feature requests (fr label)
- Connectivity issues (connectivity)
- Platform-specific bugs (OS-* labels)
- Kubernetes/container networking
- VPN interoperability (vpn-interop)

## Strategic Insights

### High-Impact Quick Wins
1. **Custom DNS records** - Reduces infrastructure needs, high demand
2. **Auto exit node on untrusted WiFi** - Security + convenience
3. **Mobile battery optimization** - Directly impacts user satisfaction

### Ecosystem Expansion Opportunities
1. **Multi-tailnet support** - Unlocks B2B partnerships and collaboration
2. **Mullvad integration** - Expands VPN market reach
3. **Browser extensions** - New user touchpoints

### Enterprise Must-Haves
1. Local route intelligence (hybrid deployments)
2. Advanced certificate management (DevOps workflows)
3. Kubernetes operator improvements (cloud-native adoption)
4. Better ACL tooling (security teams)

### Long-Term Architecture Needs
1. LAN discovery and intelligence
2. Multiple network stack handling
3. Cross-platform DNS consistency
4. Service mesh-like capabilities

## Recommended Next Steps

1. **Deep-dive specific issues:**
   - Read full thread of #183 (multi-tailnet) for enterprise objection handling
   - Review #1227 (local routing) for zero-trust rollout guidance
   - Study #1543 (custom DNS) for internal service discovery patterns

2. **Competitive analysis:**
   - How do competitors handle multi-network scenarios?
   - What DNS flexibility do alternatives provide?
   - Battery life comparison with WireGuard, OpenVPN

3. **Customer interviews:**
   - Talk to users blocked by multi-tailnet limitation
   - Understand DNS customization use cases in depth
   - Validate enterprise hybrid deployment patterns

4. **Product strategy implications:**
   - Does Tailscale prioritize simplicity over power-user features?
   - What's the philosophy on feature complexity vs ease-of-use?
   - How does the team balance consumer vs enterprise needs?

## References

- [Tailscale GitHub Repository](https://github.com/tailscale/tailscale)
- [Top Issues by Reactions](https://github.com/tailscale/tailscale/issues?q=is%3Aissue+is%3Aopen+sort%3Areactions-%2B1-desc)
- [Top Issues by Comments](https://github.com/tailscale/tailscale/issues?q=is%3Aissue+is%3Aopen+sort%3Acomments-desc)
- Key Issues Analyzed:
  - #1543 - Custom DNS records
  - #183 - Multiple tailnets
  - #1227 - Local route bypass
  - #3363 - Mobile battery
  - #306 - Wake-on-LAN

---

**Analysis Methodology:** WebFetch of GitHub issues sorted by reactions and comments, detailed analysis of top 5 issues, label taxonomy review, pattern identification across 20+ top issues.