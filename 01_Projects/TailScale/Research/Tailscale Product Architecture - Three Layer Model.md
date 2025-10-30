---
created: 2025-10-30
updated: 2025-10-30
tags: [tailscale, architecture, product-architecture, technical-architecture, diagram]
status: active
project: TailScale
---

# Tailscale Product Architecture - Three Layer Model

*Comprehensive view of Tailscale's product stack organized by Runtime, Platform, and Applications layers*

---

## Architecture Overview

Tailscale's architecture follows a three-layer model optimized for peer-to-peer mesh networking with minimal infrastructure dependency. This design delivers **structural cost advantages** and **superior performance** compared to traditional hub-and-spoke VPN architectures.

---

## Three-Layer Cake Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         APPLICATIONS LAYER                                   │
│                    (User-Facing Products & Modules)                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                               │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐          │
│  │  Tailscale VPN   │  │  Tailscale       │  │  Infrastructure  │          │
│  │   (Core Base)    │  │    Services      │  │     Access       │          │
│  │                  │  │                  │  │                  │          │
│  │ • Remote Access  │  │ • Service        │  │ • SSH Recording  │          │
│  │ • Site-to-Site   │  │   Discovery      │  │ • DB Query Logs  │          │
│  │ • Multi-Cloud    │  │ • Load Balancing │  │ • K8s Audit      │          │
│  └──────────────────┘  │ • Health Checks  │  │ • Session Replay │          │
│                        └──────────────────┘  └──────────────────┘          │
│                                                                               │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐          │
│  │   Workload       │  │     Funnel       │  │   Kubernetes     │          │
│  │    Identity      │  │                  │  │    Operator      │          │
│  │                  │  │ • Public Expose  │  │                  │          │
│  │ • tsidp (OIDC)   │  │ • HTTPS Ingress  │  │ • Service Mesh   │          │
│  │ • CI/CD Auth     │  │ • Custom Domains │  │ • Pod Networking │          │
│  │ • Ephemeral Creds│  │ • Zero Config    │  │ • Multi-Cluster  │          │
│  └──────────────────┘  └──────────────────┘  └──────────────────┘          │
│                                                                               │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐          │
│  │     Clients      │  │  AI Gateway      │  │   Observability  │          │
│  │                  │  │   (Future)       │  │    (Future)      │          │
│  │ • CLI            │  │                  │  │                  │          │
│  │ • GUI (macOS,    │  │ • LLM Routing    │  │ • Network Flows  │          │
│  │   Windows, Linux)│  │ • Token Mgmt     │  │ • Device Health  │          │
│  │ • Mobile (iOS,   │  │ • Cost Tracking  │  │ • ACL Viz        │          │
│  │   Android)       │  │ • Observability  │  │ • Dashboards     │          │
│  └──────────────────┘  └──────────────────┘  └──────────────────┘          │
│                                                                               │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│                           PLATFORM LAYER                                     │
│                      (Core Services & Capabilities)                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                               │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐          │
│  │    MagicDNS      │  │  Access Control  │  │  Authentication  │          │
│  │                  │  │     (ACLs)       │  │    & Identity    │          │
│  │ • Automatic DNS  │  │                  │  │                  │          │
│  │ • Service Names  │  │ • Policy Engine  │  │ • SSO (SAML,     │          │
│  │ • Split DNS      │  │ • User Groups    │  │   OIDC, OAuth)   │          │
│  │ • CNAME Support  │  │ • Tag-based      │  │ • MFA            │          │
│  └──────────────────┘  │   Access         │  │ • API Keys       │          │
│                        │ • Zero Trust     │  │ • Service Accts  │          │
│  ┌──────────────────┐  └──────────────────┘  └──────────────────┘          │
│  │  Subnet Routers  │                                                        │
│  │                  │  ┌──────────────────┐  ┌──────────────────┐          │
│  │ • Network Relay  │  │   Exit Nodes     │  │  Tailscale SSH   │          │
│  │ • Site-to-Site   │  │                  │  │                  │          │
│  │ • Legacy Access  │  │ • Internet       │  │ • Certificate-   │          │
│  └──────────────────┘  │   Gateway        │  │   Based Auth     │          │
│                        │ • Regional Exit  │  │ • No SSH Keys    │          │
│  ┌──────────────────┐  │ • Fail-safe      │  │ • ACL-Enforced   │          │
│  │   Node Discovery │  └──────────────────┘  └──────────────────┘          │
│  │   & Key Exchange │                                                        │
│  │                  │  ┌──────────────────┐  ┌──────────────────┐          │
│  │ • Peer Matching  │  │    Taildrop      │  │  Network Logs    │          │
│  │ • Cryptographic  │  │                  │  │   & Audit        │          │
│  │   Identity       │  │ • P2P File Xfer  │  │                  │          │
│  │ • Handshake      │  │ • No Size Limit  │  │ • Flow Logs      │          │
│  │   Coordination   │  │ • Encrypted      │  │ • Audit Trails   │          │
│  └──────────────────┘  └──────────────────┘  │ • Compliance     │          │
│                                               └──────────────────┘          │
│                                                                               │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│                            RUNTIME LAYER                                     │
│                   (Infrastructure & Protocol Foundation)                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                               │
│  ┌──────────────────────────────────────────────────────────────────────┐   │
│  │                      WireGuard Protocol                               │   │
│  │                                                                        │   │
│  │  • Modern cryptography (Noise protocol framework)                     │   │
│  │  • Kernel-level performance (on Linux, FreeBSD, etc.)                 │   │
│  │  • Lightweight (~4,000 lines of code vs 400,000 for OpenVPN)          │   │
│  │  • Peer-to-peer encrypted tunnels                                     │   │
│  │  • Roaming support (seamless network transitions)                     │   │
│  │  • Battery efficient (mobile-optimized)                               │   │
│  └──────────────────────────────────────────────────────────────────────┘   │
│                                                                               │
│  ┌────────────────────────┐  ┌──────────────────────────────────────┐      │
│  │  Coordination Server   │  │        DERP Relay Network            │      │
│  │    (Control Plane)     │  │         (Data Plane Backup)          │      │
│  │                        │  │                                       │      │
│  │ • Hosted on AWS        │  │ • Global relay servers (~100 nodes)  │      │
│  │ • Node registration    │  │ • Encrypted passthrough              │      │
│  │ • Peer discovery       │  │ • NAT traversal fallback             │      │
│  │ • ACL distribution     │  │ • Geographic distribution            │      │
│  │ • Key coordination     │  │ • Fair queuing & rate limiting       │      │
│  │ • Metadata only        │  │ • Used only when P2P fails           │      │
│  │ • Scales to 100x       │  │ • Low-cost hosting providers         │      │
│  │   current volume       │  │ • Never sees plaintext data          │      │
│  └────────────────────────┘  └──────────────────────────────────────┘      │
│                                                                               │
│  ┌──────────────────────────────────────────────────────────────────────┐   │
│  │                    NAT Traversal & Connectivity                       │   │
│  │                                                                        │   │
│  │  • STUN (Session Traversal Utilities for NAT)                         │   │
│  │  • Hole punching (UDP & TCP)                                          │   │
│  │  • Direct connections preferred (bypasses DERP when possible)         │   │
│  │  • Continuous optimization of peer-to-peer paths                      │   │
│  │  • Automatic failover to DERP when direct connection unavailable      │   │
│  └──────────────────────────────────────────────────────────────────────┘   │
│                                                                               │
│  ┌──────────────────────────────────────────────────────────────────────┐   │
│  │                   Peer-to-Peer Mesh Network                           │   │
│  │                                                                        │   │
│  │  • Decentralized data plane (no central bottleneck)                   │   │
│  │  • End-to-end encryption (zero-knowledge architecture)                │   │
│  │  • Direct device-to-device connections                                │   │
│  │  • Zero marginal bandwidth cost (traffic doesn't touch Tailscale)    │   │
│  │  • Heavy users = zero additional cost (P2P advantage)                 │   │
│  └──────────────────────────────────────────────────────────────────────┘   │
│                                                                               │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Layer Descriptions

### Runtime Layer (Infrastructure Foundation)

**Purpose:** Low-level infrastructure and protocol that makes Tailscale work

**Key Components:**

1. **WireGuard Protocol**
   - Modern cryptography foundation
   - Lightweight and fast (4,000 LOC vs OpenVPN 400,000)
   - Kernel-level performance on supported OSes
   - Battery efficient for mobile devices

2. **Coordination Server (Control Plane)**
   - AWS-hosted control plane
   - Handles node registration, peer discovery, ACL distribution
   - **Never sees user data** - metadata only
   - Can scale to **100x current volume** (per 2022 blog post)

3. **DERP Relay Network (Data Plane Backup)**
   - Global network of ~100 relay servers
   - **Encrypted passthrough** - relays cannot decrypt
   - Only used when NAT traversal fails (backup only)
   - Low-cost hosting (doesn't need trust, just bandwidth)
   - **Most traffic bypasses DERP** via direct P2P connections

4. **NAT Traversal & Peer-to-Peer Mesh**
   - STUN, hole punching (UDP/TCP)
   - Direct device-to-device connections (no middlebox)
   - **Zero marginal bandwidth cost** (traffic doesn't touch Tailscale infra)
   - Automatic failover to DERP when direct connection fails

**Cost Characteristics:**
- Coordination server: Scales with active devices (NOT bandwidth)
- DERP relay: Only for NAT traversal failures (~10-20% of traffic)
- P2P mesh: Zero cost (traffic on user networks/ISPs)

**Key Insight:** This architecture delivers **structural cost advantage** - heavy usage = zero additional cost (unlike traditional VPNs where bandwidth scales linearly with usage)

---

### Platform Layer (Core Services)

**Purpose:** Services and capabilities built on top of the runtime that enable user-facing features

**Key Components:**

1. **MagicDNS**
   - Automatic DNS resolution within tailnet
   - Service names (e.g., `device-name.tailnet-name.ts.net`)
   - Split DNS support
   - CNAME records for custom domains

2. **Access Control Lists (ACLs)**
   - Policy engine for Zero Trust access
   - User groups, tags, and tag-based access
   - Centrally managed, distributed to nodes
   - Example: `engineering` group can SSH to `prod-servers` tag

3. **Authentication & Identity**
   - SSO integration (SAML, OIDC, OAuth)
   - Multi-factor authentication (MFA)
   - API keys for programmatic access
   - Service accounts (workload identity)

4. **Subnet Routers**
   - Network relay for legacy infrastructure
   - Site-to-site connectivity
   - Access to non-Tailscale devices on remote networks

5. **Exit Nodes**
   - Internet gateway functionality
   - Regional exit points
   - Fail-safe routing

6. **Tailscale SSH**
   - Certificate-based authentication (no SSH keys)
   - ACL-enforced access policies
   - Eliminates SSH key management

7. **Node Discovery & Key Exchange**
   - Peer matching and handshake coordination
   - Cryptographic identity per node
   - Automatic key rotation

8. **Taildrop**
   - Peer-to-peer file transfer
   - No size limits (unlike Airdrop)
   - End-to-end encrypted

9. **Network Logs & Audit**
   - Network flow logs (who connected to what, when)
   - Audit trails for compliance
   - Exportable to SIEM systems

**Key Insight:** Platform services are **identity-native** and **Zero Trust** by default. Every access decision considers: who, what device, from where, to what resource, with what policy.

---

### Applications Layer (User-Facing Products)

**Purpose:** Complete products and modules that solve specific customer jobs-to-be-done

**Key Products & Modules:**

#### **1. Tailscale VPN (Core Base Product)**

**What it is:** Mesh VPN for remote access, site-to-site, and multi-cloud connectivity

**Use cases:**
- Remote employee access to corporate resources
- Site-to-site connectivity (office-to-office, office-to-cloud)
- Multi-cloud networking (AWS ↔ GCP ↔ Azure)
- Developer access to staging/production environments

**Pricing:** $6/user/month (Starter) to $20/user/month (Enterprise)

**Market:** $5B+ enterprise VPN market

---

#### **2. Tailscale Services (Service Discovery & Load Balancing)**

**What it is:** Lightweight service mesh capabilities without full Istio/Linkerd complexity

**Use cases:**
- Service-to-service connectivity in microservices
- Load balancing across multiple instances
- Health checks and automatic failover
- API gateway alternative

**Target customers:**
- Platform teams building distributed systems
- AI/ML companies (training clusters, inference endpoints)
- CI/CD pipelines (ephemeral build agents)

**Pricing:** Usage-based (per service, per connection)

**Market:** $2.5B service mesh market (growing to $29B by 2032)

---

#### **3. Infrastructure Access (SSH, DB, K8s with Audit)**

**What it is:** Privileged access management with session recording and audit trails

**Use cases:**
- SSH access with session recording (compliance)
- Database query logging (SOC2, HIPAA, PCI)
- Kubernetes audit logs (who ran what kubectl command)
- Just-in-time (JIT) access workflows

**Target customers:**
- Enterprises with compliance requirements
- Security-conscious organizations
- Companies replacing Teleport, StrongDM, BastionZero

**Pricing:** Add-on module ($25-50/user/month estimated)

**Market:** $1-2B infrastructure access subset of PAM market

---

#### **4. Workload Identity (tsidp - OIDC Provider)**

**What it is:** Use Tailscale identity for workload authentication (CI/CD, services)

**Use cases:**
- CI/CD pipeline authentication (GitHub Actions, CircleCI)
- Service-to-service auth without long-lived credentials
- Ephemeral credentials for cloud resources
- OIDC integration with AWS, GCP, Azure

**Target customers:**
- Platform teams automating infrastructure
- DevOps teams eliminating long-lived secrets
- Security teams enforcing Zero Trust for workloads

**Pricing:** Likely bundled with Services or Infrastructure Access

**Market:** Emerging (part of $15B+ platform market)

---

#### **5. Funnel (Public Expose Service)**

**What it is:** Expose internal services to public internet via HTTPS

**Use cases:**
- Share development preview with external stakeholders
- Webhook receivers (GitHub, Stripe)
- Quick demos without deployment
- Personal projects (blog, side project)

**Target customers:**
- Developers (personal use)
- Small teams (quick sharing)
- Hobbyists (homelab exposure)

**Pricing:** Included in Premium tier

**Market:** Developer tools (competing with ngrok, Cloudflare Tunnels)

---

#### **6. Kubernetes Operator**

**What it is:** Service mesh lite for Kubernetes clusters

**Use cases:**
- Pod-to-pod networking across clusters
- Multi-cluster service mesh
- Secure K8s ingress
- Connect K8s to non-K8s workloads

**Target customers:**
- Platform engineering teams
- Multi-cloud Kubernetes users
- Teams seeking "Istio alternative" (simpler)

**Pricing:** Bundled with Services module

**Market:** $1.2B Kubernetes service mesh market

---

#### **7. Clients (CLI, GUI, Mobile)**

**What it is:** User interfaces for all platforms

**Platforms:**
- CLI (Linux, macOS, Windows, FreeBSD)
- GUI (macOS, Windows, Linux)
- Mobile (iOS, Android)

**Key features:**
- One-click connect/disconnect
- Network status visibility
- Exit node selection
- Subnet router configuration
- ACL management (admin)

---

#### **8. AI Gateway (Future - Planned via LiteLLM Fork)**

**What it is:** LLM routing and observability for AI applications

**Use cases:**
- Multi-provider LLM routing (OpenAI, Anthropic, Google)
- Cost optimization and budgeting
- Token usage tracking and observability
- Semantic caching (reduce LLM costs)
- Secure AI agent connectivity

**Target customers:**
- AI/ML engineering teams
- Companies building LLM applications
- Platform teams managing AI infrastructure

**Pricing:** Usage-based (per token, per model, or monthly subscription)

**Market:** $14M (2024) → $182M (2031), 45.7% CAGR

**Status:** Planned (fork LiteLLM, acqui-hire maintainers, integrate with Tailscale)

---

#### **9. Observability (Future - Planned Build)**

**What it is:** Network flow visualization, device health, ACL visualization

**Use cases:**
- Network topology visualization
- Real-time flow analysis
- Device health monitoring
- ACL policy troubleshooting
- Security incident investigation

**Target customers:**
- Network operations teams
- Security teams
- Platform engineering teams

**Pricing:** Add-on module ($5-10/device/month estimated)

**Market:** $147M funding in observability startups (2025)

**Status:** Planned build (consolidate 4+ community projects: TSFlow, tailscale-healthcheck, Network Topology Mapper)

---

## Cross-Layer Dependencies

### How the Layers Work Together

**Example 1: Remote Employee Access (VPN Use Case)**

```
Application: Tailscale VPN client on laptop
     ↓
Platform: ACLs check if user authorized, MagicDNS resolves server name
     ↓
Runtime: WireGuard establishes P2P tunnel, DERP relay if NAT traversal fails
     ↓
Result: Secure, encrypted connection to corporate resources
```

**Example 2: AI Agent Accessing Database (Platform Use Case)**

```
Application: AI Gateway routes LLM request to Claude
     ↓ (needs database context)
Platform: Workload Identity (tsidp) issues ephemeral credential
     ↓
Platform: Infrastructure Access logs database query for compliance
     ↓
Runtime: WireGuard P2P tunnel to database server (via subnet router if needed)
     ↓
Result: Secure, audited database access with identity-based auth
```

**Example 3: Service-to-Service in Kubernetes (Service Mesh Use Case)**

```
Application: Kubernetes Operator manages pod networking
     ↓
Application: Tailscale Services provides load balancing and health checks
     ↓
Platform: MagicDNS resolves service names, ACLs enforce access policies
     ↓
Runtime: WireGuard P2P tunnels between pods (even across clusters)
     ↓
Result: Lightweight service mesh without Istio complexity
```

---

## Economic Model by Layer

### Runtime Layer Economics

**Cost Structure:**
- **Coordination Server:** $X per active device (scales sub-linearly)
- **DERP Relay:** $Y per GB relayed (but only 10-20% of traffic)
- **P2P Mesh:** $0 (zero marginal cost)

**Key Insight:** Heavy usage = zero additional cost (P2P advantage)

**Gross Margin Impact:** 85-90% gross margins achievable (vs 60-70% for traditional VPNs)

---

### Platform Layer Economics

**Cost Structure:**
- **MagicDNS, ACLs, SSH:** Included in base product (no additional COGS)
- **Audit Logs, Network Logs:** Storage costs (scales with retention period)

**Key Insight:** Platform services are **software-only** with minimal incremental cost

**Pricing Strategy:** Bundled in base tiers (table stakes), upsell on storage/retention

---

### Applications Layer Economics

**Cost Structure:**
- **VPN Client:** One-time dev cost, zero marginal cost
- **Services, Infra Access, AI Gateway:** Usage-based pricing → high gross margins
- **Observability:** Compute + storage costs (but customer pays for usage)

**Key Insight:** Add-on modules enable **land-and-expand** with high NRR

**Pricing Strategy:**
- Base VPN: Seat-based ($6-20/user/month)
- Modules: Usage-based or add-on pricing (high-value upsells)

---

## Competitive Differentiation by Layer

### Runtime: P2P Mesh vs Hub-and-Spoke

| Feature | Tailscale (P2P) | Traditional VPN | SASE (Cloudflare, Zscaler) |
|---------|-----------------|-----------------|----------------------------|
| **Architecture** | Peer-to-peer mesh | Hub-and-spoke | Centralized edge |
| **Performance** | ✅ Direct connections | ❌ Backhauled through HQ | ⚠️ Routed through edge PoP |
| **Bandwidth Cost** | ✅ Zero (P2P) | ❌ High (all traffic) | ⚠️ Medium (edge routing) |
| **Scalability** | ✅ Unlimited (P2P) | ❌ Hardware constrained | ✅ Cloud-scaled |

**Tailscale advantage:** P2P mesh = better performance + lower cost

---

### Platform: Zero Trust Native vs Bolt-On

| Feature | Tailscale | Traditional VPN | SASE |
|---------|-----------|-----------------|------|
| **Zero Trust** | ✅ Native (identity-based ACLs) | ❌ Perimeter-based | ✅ Native |
| **MagicDNS** | ✅ Built-in | ⚠️ Manual DNS config | ✅ Built-in |
| **SSH Keys** | ✅ Certificate-based (no keys) | ❌ Manual key mgmt | ⚠️ Depends on vendor |
| **ACL Policy** | ✅ Centralized, YAML | ❌ Device-by-device | ✅ Centralized |

**Tailscale advantage:** Zero Trust by default, not bolt-on

---

### Applications: Developer Experience vs Enterprise Checklist

| Feature | Tailscale | Traditional VPN | SASE |
|---------|-----------|-----------------|------|
| **Setup Time** | ✅ Minutes | ❌ Weeks | ⚠️ Days |
| **Deployment** | ✅ No hardware | ❌ On-prem appliances | ✅ Cloud-native |
| **Developer UX** | ✅ Best-in-class | ❌ Clunky, slow | ⚠️ Good |
| **Feature Breadth** | ⚠️ VPN + Infra Access | ⚠️ VPN only | ✅ VPN + SWG + CASB + DLP |

**Tailscale advantage:** Developer love, ease of use, fast deployment

**Tailscale gap:** Missing SASE security features (SWG, CASB, DLP) - addressed via partnerships

---

## Strategic Insights

### 1. Architecture Enables Business Model

**Runtime (P2P mesh) → Low COGS → Generous Free Tier → PLG Motion**

- P2P architecture = zero marginal bandwidth cost
- Can offer 100 devices, 3 users free (vs competitors limit free tier)
- Free tier drives PLG: Personal use → Work adoption → Team expansion

**Platform (Zero Trust native) → Security positioning → Enterprise sales**

- Identity-based ACLs = Zero Trust by default
- Compliance-friendly (audit logs, session recording)
- Enterprises trust Tailscale for security (not just convenience)

**Applications (Modular) → Land-and-expand → High NRR**

- Start with VPN ($6/user/month)
- Upsell Services ($25/service/month)
- Upsell Infra Access ($50/user/month)
- Add AI Gateway (usage-based)
- **Result:** 130%+ NRR via expansion revenue

---

### 2. Bridge Strategy Maps to Architecture

**VPN Market (Enterprise IT buyers):**
- Use: Runtime (P2P mesh) + Platform (ACLs, SSH) + Application (VPN client)
- Positioning: "Replace Cisco/Palo Alto with modern, fast, Zero Trust VPN"

**Platform Market (Developer buyers):**
- Use: Runtime (P2P mesh) + Platform (Services, Workload Identity) + Application (K8s Operator, AI Gateway)
- Positioning: "Infrastructure connectivity for distributed systems, CI/CD, AI/ML"

**Both markets share same runtime + platform** = operational leverage

---

### 3. Community Projects Validate Product Roadmap

**Community built:**
- TSFlow (network flow visualization) → Validates observability need
- tsidp (OIDC provider) → Validates workload identity need
- K8s operator (service mesh) → Validates Services positioning
- docker-mod, ScaleTail → Validates platform use cases

**Tailscale strategy:** Let community prove demand (v0), then productize (v1 GA)

---

### 4. Future Architecture Evolution

**Planned additions (next 12-24 months):**

**Runtime Layer:**
- Peer relay servers (customer-hosted DERP) - Q4 FY26
- Improved NAT traversal (reduce DERP usage further)

**Platform Layer:**
- ACL Policy Builder UI (GUI for YAML editing)
- Advanced routing policies (traffic shaping, QoS)
- Network observability (flow logs, topology viz)

**Applications Layer:**
- AI Gateway (fork LiteLLM, integrate) - H1 FY27
- Infrastructure Access GA (session recording, DB query logs) - H2 FY26
- Observability (Tailscale Insights) - FY27
- Service Mesh Lite features (L7 routing, canary deployments) - H2 FY27

---

## Conclusion

Tailscale's three-layer architecture delivers:

1. **Runtime advantage:** P2P mesh = better performance + lower cost than competitors
2. **Platform advantage:** Zero Trust native + developer-friendly = high adoption
3. **Applications advantage:** Modular products = land-and-expand with high NRR

**Key insight:** The runtime layer (WireGuard + P2P mesh) creates a **structural moat** that competitors with centralized architectures cannot replicate without complete rebuild.

**Strategic implication:** Tailscale's architecture enables simultaneous pursuit of VPN market ($5B) and Platform market ($15B) with **shared infrastructure** = operational leverage and margin expansion as scale increases.

---

## References

- Tailscale COGS and Infrastructure Economics (from "How our free plan stays free" blog post)
- Product Packaging Strategy - Services, Workload Identity, Infra Access
- Community Projects Bridge Strategy Analysis
- Strategic M&A Analysis (AI Gateway, Infrastructure Access)

---

*This architecture model is based on publicly available information (blog posts, docs) and strategic analysis from TailScale project research.*

