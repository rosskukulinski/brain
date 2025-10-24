---
created: 2025-10-24
updated: 2025-10-24
tags: [tailscale, partnerships, technical-requirements, database, integration]
status: analysis
project: TailScale
---

# Database Vendor Integration Requirements

*What Tailscale needs to build to enable Snowflake/Databricks to offer Tailscale as a connectivity option*

---

## The Vision: "Connect via Tailscale" Button

**User experience goal:**
1. Customer sets up new Snowflake warehouse
2. In the "Network Configuration" section, sees option: "Connect via Tailscale"
3. Clicks button, authenticates with their Tailscale account
4. Gets a stable Tailscale DNS name for their warehouse: `warehouse-123.snowflake.tailnet-name.ts.net`
5. Immediately connects from their laptop/servers using that name
6. No PrivateLink setup, no IP whitelisting, no VPN configuration

**For Databricks:**
- Similar flow for cluster connectivity
- Notebooks can access data sources via Tailscale
- Developers connect to clusters without complex networking

---

## Core Requirements

### 1. Multi-Tenant Tailscale Architecture

**Current state question:** Can a vendor run Tailscale infrastructure that serves multiple customers' tailnets?

**What's needed:**

**Option A: Vendor-Hosted Tailnet Model**
- Snowflake runs their own tailnet(s)
- Customer resources (warehouses) are nodes in Snowflake's tailnet
- Customers join Snowflake's tailnet to access their resources
- **Problem:** Customers see each other's resources (unless heavy ACL work)
- **Problem:** Doesn't fit Tailscale's security model (customers should control their own tailnet)

**Option B: Customer Tailnet Integration Model** (RECOMMENDED)
- Customer has their own tailnet
- Snowflake warehouse becomes a node in the customer's tailnet
- Snowflake acts as an "authorized device provisioner" for customer tailnets
- Customer maintains full control and visibility
- **Requirement:** Programmatic node provisioning API

**Option C: Shared Services Model (Advanced)**
- Tailscale Services allow Snowflake to expose endpoints across multiple customer tailnets
- Snowflake runs service hosts in their infrastructure
- Customer tailnets can access Services based on ACL grants
- **Requirement:** Full Services GA with multi-tenant support

**Recommended approach:** Start with Option B, evolve to Option C as Services matures

---

### 2. Programmatic Node Provisioning & Management

**What Snowflake needs to do:**
- Provision a Tailscale node when customer creates a warehouse
- Associate node with customer's tailnet (not Snowflake's)
- Manage node lifecycle (suspend, resume, delete when warehouse deleted)
- Rotate keys/credentials without customer intervention
- Handle node naming and DNS registration

**Tailscale needs to provide:**

#### 2.1 OAuth Application Framework (Enhanced)
- **Currently:** OAuth apps can create auth keys for device registration
- **Needed:** OAuth apps can provision nodes on behalf of users with delegated permissions
- **Scope:** `devices:write`, `dns:write`, `acl:read` (to validate access)

#### 2.2 Partner Node Provisioning API
```
POST /api/v2/partner/nodes
{
  "customer_tailnet": "customer-org.tailscale.net",
  "node_name": "snowflake-warehouse-123",
  "partner_metadata": {
    "partner": "snowflake",
    "resource_id": "warehouse-abc-123",
    "region": "us-west-2"
  },
  "tags": ["tag:snowflake-warehouse"],
  "auth_key_expiry": "90d"
}

Response:
{
  "node_id": "n1234567",
  "auth_key": "tskey-auth-...",
  "tailscale_ip": "100.64.1.50",
  "dns_name": "snowflake-warehouse-123.tailnet-name.ts.net",
  "expires": "2026-01-24T12:00:00Z"
}
```

**Key capabilities:**
- Create node with partner-specific metadata
- Automatic tagging for ACL management
- Node appears in customer's admin console with clear "Provisioned by Snowflake" indicator
- Customer can view, remove, but not directly manage (Snowflake controls lifecycle)

#### 2.3 Node Management API
```
# Snowflake needs to:
GET /api/v2/partner/nodes?partner_metadata.resource_id=warehouse-123
PATCH /api/v2/partner/nodes/{node_id} (update metadata, rotate key)
DELETE /api/v2/partner/nodes/{node_id} (when warehouse deleted)
GET /api/v2/partner/nodes/{node_id}/status (online/offline, connectivity health)
```

---

### 3. Identity & Authorization Integration

**The challenge:** How does Snowflake know which customer tailnet to provision into?

**Option A: OAuth Account Linking** (Simplest)
1. Customer clicks "Connect via Tailscale" in Snowflake console
2. Redirected to Tailscale OAuth consent flow
3. Customer approves: "Allow Snowflake to provision devices in [my-tailnet]"
4. Snowflake stores OAuth token linked to customer account
5. Future warehouse creations use stored token

**Option B: SCIM/Identity Federation** (Enterprise)
- Customer's IdP (Okta, Azure AD) grants Snowflake access to provision Tailscale nodes
- Leverages existing SCIM integration
- Better for enterprises with strict IdP policies
- **Requirement:** Expand SCIM scope to include partner provisioning

**Option C: Tailscale Organization Delegated Access** (Future)
- Customer creates "partner access policy" in Tailscale admin console
- "Snowflake can provision nodes with tag:snowflake in my tailnet"
- Snowflake uses customer-specific credential that's scoped
- **Requirement:** New delegation model in Tailscale

**Recommended:** Start with Option A (OAuth), plan for Option C

---

### 4. Network Connectivity Patterns

**How does traffic actually flow?**

#### Pattern 1: Agent-Based (Current Tailscale Model)
- Snowflake runs Tailscale client on warehouse infrastructure
- Warehouse gets Tailscale IP, joins customer's tailnet
- Direct peer-to-peer connection (when possible)
- Falls back to DERP relay

**Requirements:**
- Snowflake needs to run Tailscale binary in their infrastructure
- Must handle client updates, key rotation, monitoring
- Works with existing Tailscale architecture

#### Pattern 2: Agentless/Bastion (Emerging)
- Snowflake doesn't run Tailscale on every warehouse
- Tailscale bastion/proxy in Snowflake's infrastructure
- Proxies connections from customer tailnet to warehouse
- Similar to "Agentless SSH" on roadmap

**Requirements:**
- Tailscale needs to build bastion/proxy capability
- May add latency vs agent-based
- Simpler for Snowflake to deploy/operate

#### Pattern 3: Services-Based (Future)
- Snowflake warehouses exposed as Tailscale Services
- Customer tailnet can access Services via DNS
- Load balancing, health checks, etc. via Services
- Most aligned with platform vision

**Requirements:**
- Services must be GA and proven at scale
- Multi-tenant Services with isolation guarantees
- May not fit all database protocols

**Recommended:** Start with Pattern 1 (agent-based), evolve to Pattern 3 (Services) for new deployments

---

### 5. DNS & Naming

**What customers need:**
- Stable DNS name for warehouse: `warehouse-123.my-tailnet.ts.net`
- Name persists even if underlying IP changes
- Name works from any device on customer's tailnet

**Tailscale needs to provide:**

#### 5.1 Partner-Provisioned MagicDNS
- When Snowflake provisions node, automatically registers DNS name
- Format: `{resource-name}.{customer-tailnet}.ts.net`
- Optionally: `{resource-name}.snowflake.{customer-tailnet}.ts.net` for namespacing

#### 5.2 DNS CNAME Support (Advanced)
- Customer can add their own DNS: `warehouse.company.com` → `warehouse-123.tailnet.ts.net`
- Useful for tools/scripts that expect specific hostnames
- **Requirement:** MagicDNS CNAME records (may already exist?)

#### 5.3 Bring Your Own Domain (BYOD) Integration
- If customer has BYOD configured, Snowflake nodes appear under customer's domain
- Example: `warehouse-123.internal.company.com`
- **Requirement:** BYOD feature (on roadmap as "bring-your-own-domain")

---

### 6. Access Control & Security

**How do customers control who can access Snowflake resources?**

#### 6.1 ACL Tag Recommendations
Tailscale needs to provide ACL best practices/templates for partners:

```json
{
  "tagOwners": {
    "tag:snowflake-warehouse": ["autogroup:admin"],
    "tag:snowflake-readonly": ["autogroup:admin"]
  },
  "acls": [
    {
      "action": "accept",
      "src": ["group:data-analysts"],
      "dst": ["tag:snowflake-warehouse:443", "tag:snowflake-warehouse:5432"]
    },
    {
      "action": "accept",
      "src": ["tag:ci-cd"],
      "dst": ["tag:snowflake-readonly:443"]
    }
  ]
}
```

**Customer workflow:**
1. Snowflake provisions node with `tag:snowflake-warehouse`
2. Customer updates ACL to grant access to specific groups
3. Only authorized users/devices can connect
4. Snowflake never needs to manage customer's access policies

#### 6.2 Device Posture Integration (Future)
- Customer can require device posture checks for Snowflake access
- Example: "Only managed devices can access warehouse"
- Leverages Tailscale's existing device posture

#### 6.3 Audit Logging
**Critical for compliance (SOC2, HIPAA, etc.)**

Tailscale needs to provide:
- Network flow logs showing who accessed Snowflake resources
- Includes: User identity, device, timestamp, bytes transferred
- Customer can stream logs to their SIEM
- **Requirement:** Network flow logging (already on roadmap)

Snowflake integration:
- Correlate Tailscale access logs with Snowflake query logs
- "User alice@company.com accessed warehouse via Tailscale from IP 100.64.1.25 at 2025-10-24 14:30, ran query SELECT * FROM sensitive_table"

---

### 7. Multi-Tenancy & Isolation

**Snowflake security requirement:** Customer A cannot access Customer B's warehouse, even accidentally

**Tailscale architecture inherently handles this:**
- Each customer has their own tailnet (network isolation)
- Customer A's devices literally cannot see Customer B's tailnet nodes
- No shared network, no cross-tenant routing

**Edge case to handle:**
- What if two customers have same tailnet name? (Unlikely but possible)
- Solution: Use tailnet ID (numeric/UUID) in APIs, not name

**Snowflake operational security:**
- Snowflake's OAuth tokens are per-customer, scoped to that customer's tailnet
- If token leaks, only affects that one customer
- Tailscale should provide token rotation API

---

### 8. Database Protocol Support

**Which database protocols work over Tailscale?**

**Already works (TCP-based):**
- PostgreSQL (port 5432) - Snowflake, various databases
- MySQL (port 3306)
- MongoDB (port 27017)
- Redis (port 6379)
- Cassandra (port 9042)
- HTTPS APIs (port 443) - Most data warehouses

**Tailscale advantage:** Protocol-agnostic (works at IP layer)
- No special handling needed for different database protocols
- TLS/SSL encryption happens at application layer (double encryption with Tailscale)

**Potential issues:**
- Protocols that do DNS lookups mid-connection?
- Protocols that embed IP addresses in payloads? (Rare)
- Testing needed with each major vendor

---

### 9. Performance & Reliability Requirements

**Customer expectations for database connectivity:**
- Low latency (< 10ms added latency from Tailscale)
- High availability (99.9%+ uptime)
- Throughput for large queries (GB of data transfer)

**Tailscale needs to provide:**

#### 9.1 Performance SLAs
- Document expected latency: Direct connection vs DERP relay
- Bandwidth capacity per node
- Recommend architecture (agent-based vs bastion) based on workload

#### 9.2 Monitoring & Observability
- Snowflake needs API to check node health:
  ```
  GET /api/v2/partner/nodes/{node_id}/metrics
  {
    "status": "online",
    "latency_p50_ms": 5,
    "latency_p99_ms": 15,
    "using_derp": false,
    "bytes_sent": 1048576,
    "bytes_received": 524288,
    "last_seen": "2025-10-24T14:30:00Z"
  }
  ```

- Customer dashboards show Tailscale connectivity health
- Alerts if warehouse node goes offline

#### 9.3 Reliability Features
- Automatic reconnection if Tailscale client disconnects
- Graceful key rotation (no connection drops)
- Support for Snowflake's HA/multi-region architecture

---

### 10. Customer Admin Experience

**What does customer see in Tailscale admin console?**

#### 10.1 Partner-Provisioned Nodes UI
- Clear indicator: "Provisioned by Snowflake" badge on node
- Metadata displayed: Warehouse ID, region, creation date
- Customer can:
  - View node status and connection history
  - Disable node (temporarily block access)
  - Remove node (revokes access, Snowflake must re-provision)
  - View access logs for this node
- Customer cannot:
  - Directly edit node configuration (Snowflake manages)
  - SSH into node (it's Snowflake's infrastructure)

#### 10.2 Partner Integration Management Page
```
Settings > Integrations > Snowflake

Status: Connected
Connected since: Oct 24, 2025
Permissions: Provision nodes, register DNS names

Resources managed by Snowflake:
- warehouse-prod (online, 2.3 GB transferred today)
- warehouse-dev (online, 500 MB transferred today)

[Revoke Snowflake Access] [View Audit Log]
```

#### 10.3 Recommended ACLs
- Tailscale suggests ACL templates for common Snowflake patterns
- "Grant data team access to Snowflake warehouses"
- Customer can accept/modify suggestions

---

### 11. Pricing & Billing Integration

**How does pricing work for partner-provisioned nodes?**

**Option A: Customer Pays Tailscale Directly**
- Snowflake provisions nodes, customer pays Tailscale for seats/usage
- Snowflake doesn't touch billing
- **Pro:** Simple for Snowflake
- **Con:** Customer has two separate bills

**Option B: Snowflake Resells Tailscale**
- Snowflake invoices customer for "Tailscale Connectivity" add-on
- Snowflake pays Tailscale wholesale rate
- **Pro:** Single bill for customer, Snowflake captures margin
- **Con:** Complex revenue share agreement, Snowflake handles support

**Option C: Marketplace Model**
- Customer has Tailscale subscription via AWS/GCP/Azure marketplace
- Snowflake provisions nodes, counted against customer's existing subscription
- **Pro:** Leverages existing marketplace relationships
- **Con:** Requires marketplace integration

**Tailscale needs to provide:**
- API to check customer's plan limits (before provisioning)
- Usage reporting API for reseller scenarios
- Flexible licensing for partner-provisioned nodes

**Questions for business strategy:**
- Are partner-provisioned nodes free? (Drive adoption)
- Discounted? (Incentivize partnerships)
- Full price? (Sustain margins)

---

### 12. Support & Operations

**Who helps customer when things break?**

#### 12.1 Support Handoff Matrix
| Issue | First Contact | Escalation |
|-------|--------------|------------|
| Can't connect to warehouse | Snowflake support | Tailscale if Tailscale issue |
| Warehouse node offline | Snowflake support (they manage node) | N/A |
| ACL policy questions | Tailscale support or docs | N/A |
| Provisioning errors | Snowflake support (their integration) | Tailscale for API bugs |
| Performance issues | Jointly debug | - |

#### 12.2 Snowflake Needs Access To:
- **Partner Portal:** Dashboard showing all provisioned nodes across customers, health metrics
- **Support API:** Query customer's Tailscale setup when debugging issues
- **Status Page:** Tailscale incidents that affect database connectivity
- **Runbooks:** How to debug common issues

#### 12.3 Tailscale Operational Requirements:
- **Webhook notifications:** When node goes offline, notify Snowflake
- **SLA commitments:** 99.9% for DERP relay, 99.99% for control plane
- **Geographic redundancy:** Snowflake operates globally, Tailscale must too

---

### 13. Documentation & Developer Experience

**Snowflake engineering needs:**

#### 13.1 Integration Guide
- Step-by-step: Register as Tailscale partner, get OAuth credentials
- API reference with code samples (Python, Go, Java)
- Terraform module for provisioning Tailscale nodes
- Testing sandbox: Snowflake can test integration before production

#### 13.2 Customer-Facing Docs
- "How to connect to Snowflake via Tailscale" guide
- Troubleshooting common issues
- ACL examples for different access patterns
- Security best practices

#### 13.3 SDKs
- Official SDK for partner integrations (vs raw API calls)
- Handles auth, retries, rate limiting
- Example:
  ```python
  from tailscale_partner import PartnerClient

  client = PartnerClient(oauth_token="...")

  # Provision node
  node = client.provision_node(
      customer_tailnet="customer-org.tailscale.net",
      name="warehouse-123",
      tags=["tag:snowflake"]
  )

  print(f"Connect at: {node.dns_name}")
  ```

---

### 14. Security & Compliance

**Snowflake will ask these questions:**

#### 14.1 Data Residency
- **Q:** Where does Tailscale control plane run? (Customer data compliance)
- **A:** Tailscale needs to document control plane regions, support EU/US data residency

#### 14.2 Encryption
- **Q:** Is traffic encrypted end-to-end?
- **A:** Yes (WireGuard), but document clearly for SOC2/HIPAA audits

#### 14.3 Key Management
- **Q:** Who holds encryption keys? Can Tailscale decrypt traffic?
- **A:** Keys stay on nodes, Tailscale cannot decrypt (E2E encryption)

#### 14.4 Certifications
- **Q:** Is Tailscale SOC2/ISO27001/HIPAA compliant?
- **A:** Must provide compliance documentation for partner integrations

#### 14.5 Vulnerability Disclosure
- **Q:** What happens if security issue found in Tailscale?
- **A:** Responsible disclosure process, coordinated patching with partners

---

### 15. Go-to-Market Alignment

**Joint GTM with Snowflake:**

#### 15.1 Co-Marketing
- Joint blog post: "Snowflake + Tailscale = Secure Cloud Data Warehouse Access"
- Webinar: "Simplify Snowflake Connectivity"
- Case studies with mutual customers

#### 15.2 Sales Enablement
- Tailscale sales can refer database connectivity use cases to Snowflake
- Snowflake sales can upsell Tailscale connectivity to customers struggling with PrivateLink
- Joint solution brief

#### 15.3 Product Integration Milestones
```
Phase 1 (Private Beta):
- 5 design partner customers
- Agent-based connectivity
- OAuth account linking
- Basic ACL support

Phase 2 (Public Beta):
- Available to all Snowflake customers
- Full documentation and support
- Monitoring/observability
- 100+ customers using

Phase 3 (GA):
- SLA commitments
- Enterprise support tier
- Services-based connectivity (optional)
- 1000+ customers
```

---

## Technical Gaps to Close (Priority Order)

### Critical (Must-Have for Any Partner Integration)

1. **Partner Node Provisioning API**
   - Current: OAuth apps can create auth keys
   - Needed: Full node lifecycle management API
   - Effort: 2-3 months eng work
   - Owner: Platform team

2. **OAuth Scope for Device Provisioning**
   - Current: OAuth scopes are limited
   - Needed: `devices:write`, `dns:write`, `metadata:write`
   - Effort: 1 month
   - Owner: Identity team

3. **Partner Metadata Support**
   - Current: Nodes have Tailscale metadata only
   - Needed: Arbitrary key-value metadata for partners
   - Effort: 2-3 weeks
   - Owner: Platform team

4. **Network Flow Logging GA**
   - Current: Alpha/Beta, not all customers have access
   - Needed: GA with reliable streaming
   - Effort: On roadmap, Q1-Q2 FY27
   - Owner: Platform team

### Important (Greatly Improves Experience)

5. **Partner Portal/Dashboard**
   - Current: Partners would use regular API
   - Needed: Dedicated portal showing all provisioned nodes, health, usage
   - Effort: 1-2 months
   - Owner: Product + Platform

6. **Admin Console Partner Integration UI**
   - Current: Partner-provisioned nodes look like regular nodes
   - Needed: Clear "Provisioned by X" badge, special management UI
   - Effort: 1 month
   - Owner: DevEx team

7. **Agentless/Bastion Mode**
   - Current: Must run Tailscale client on every resource
   - Needed: Proxy/bastion for agentless connectivity
   - Effort: On roadmap as "Agentless SSH", 3-6 months
   - Owner: Networking team

### Nice-to-Have (Future Enhancements)

8. **Services Multi-Tenant Support**
   - Current: Services in beta, not designed for partner use case
   - Needed: Partner can run Services exposing resources to multiple customer tailnets
   - Effort: Part of Services GA roadmap, 6+ months
   - Owner: Networking team

9. **Delegated Administration**
   - Current: OAuth token has broad permissions
   - Needed: Fine-grained delegation ("Snowflake can provision nodes with tag:snowflake")
   - Effort: New feature, 3-4 months
   - Owner: Identity + Platform

10. **Usage-Based Billing API**
    - Current: Seat-based licensing
    - Needed: Track data transfer, API calls, etc. for usage billing
    - Effort: 2-3 months
    - Owner: Billing team

---

## Minimal Viable Integration (MVP)

**What's the absolute minimum to enable a Snowflake integration?**

**Required:**
1. Partner Node Provisioning API (create, delete, get status)
2. OAuth account linking (customer authorizes Snowflake)
3. Agent-based deployment (Snowflake runs Tailscale client)
4. Basic metadata (Snowflake can tag nodes)
5. MagicDNS registration (automatic DNS names)

**Customer experience (MVP):**
- Snowflake setup wizard: "Connect via Tailscale" button
- OAuth flow: Customer approves access
- Snowflake provisions node when warehouse created
- Customer gets DNS name: `warehouse-123.my-tailnet.ts.net`
- Customer updates ACL to grant team access
- Done

**What's punted to post-MVP:**
- Partner portal/dashboard (Snowflake uses raw API)
- Advanced monitoring (basic status only)
- Services-based connectivity (agent-based only)
- Fancy admin console UI (nodes look normal)
- Delegated administration (broad OAuth token)

**Timeline estimate:**
- 3-4 months eng work for Tailscale (Platform + Identity teams)
- 2-3 months integration work for Snowflake
- 1-2 months testing and private beta
- **Total: 6-9 months to private beta, 9-12 months to public beta**

---

## Recommended Phasing

### Phase 0: Validation (Now - Q1 FY27)
- Build reference architecture with existing tools
- 5-10 design partner customers manually configure Tailscale for Snowflake
- Collect feedback on pain points
- Validate demand (do customers actually want this?)

### Phase 1: MVP (Q2-Q3 FY27)
- Build partner provisioning API
- Snowflake builds integration (private beta)
- 50-100 beta customers
- Prove technical viability

### Phase 2: Scale (Q4 FY27 - Q1 FY28)
- Partner portal and monitoring
- Admin console UI improvements
- Public beta (all Snowflake customers)
- 1000+ customers using

### Phase 3: Platform (Q2 FY28+)
- Services-based connectivity
- Additional database vendors (Databricks, MongoDB)
- Usage-based billing options
- Partner ecosystem (10+ integrations)

---

## Key Questions for Tailscale Leadership

### Strategy & Timing
1. **Roadmap fit:** Does partner integration fit H1 FY27 roadmap, or is it H2/FY28?
2. **Resources:** Would this require dedicated "Partnerships Engineering" team?
3. **Prioritization:** Does partner API work compete with core bridge features?

### Business Model
4. **Pricing:** How to price partner-provisioned nodes? Free? Discounted? Full price?
5. **Revenue share:** If vendors resell Tailscale, what's the model?
6. **Support:** Can Tailscale support handle partner integration issues?

### Technical Feasibility
7. **Security architecture:** Any concerns with partners provisioning nodes into customer tailnets?
   - Does OAuth delegation model work at scale?
   - Can we prevent partner token abuse/leakage?
   - Is the security boundary clear enough?

8. **Control plane scalability:** Can control plane handle:
   - Snowflake provisioning 10,000+ nodes/day across customers?
   - API rate limits for high-volume partners?
   - Node churn (warehouses created/deleted frequently)?

9. **Multi-tenancy guarantees:** How do we ensure:
   - Customer A cannot see/access Customer B's partner resources?
   - Partner cannot access customer data outside their scope?
   - Isolation is maintained even with bugs/misconfigurations?

10. **Operational complexity:**
    - Who manages partner-provisioned nodes when issues arise?
    - What happens when Tailscale client needs updates on partner infrastructure?
    - How do we handle key rotation across thousands of partner nodes?

### Unknown Constraints
11. **Architectural limitations:** Are there fundamental architectural reasons this integration model won't work?
    - WireGuard scalability with partners creating nodes programmatically?
    - DNS registration at scale (thousands of new names/day)?
    - DERP relay capacity for partner-driven traffic?

12. **Existing learnings:** Has Tailscale explored this before?
    - Any failed/successful partnership integration attempts?
    - Lessons from OEM discussions?
    - Prior art from similar networking companies?

---

## Open Questions & Assumptions

**This analysis makes several assumptions that need validation:**

### Assumption 1: OAuth Delegation is Secure Enough
- **Assumed:** OAuth token scoped to `devices:write` is safe for partners
- **Risk:** Token leakage could allow partner to provision nodes maliciously
- **Validation needed:** Security team review of delegation model

### Assumption 2: Customer Control is Preserved
- **Assumed:** Customer can revoke partner access, remove nodes, maintain visibility
- **Risk:** UX might make customers feel they've lost control
- **Validation needed:** UX research with customers on partner-provisioned nodes

### Assumption 3: Control Plane Can Scale
- **Assumed:** Existing infrastructure handles partner-driven node creation
- **Risk:** API rate limits, database scalability, node registration throughput
- **Validation needed:** Load testing with simulated partner traffic

### Assumption 4: Multi-Tenant Services Architecture Exists
- **Assumed:** Services can be extended for partner multi-tenant use case
- **Risk:** Services might be architecturally incompatible with partner model
- **Validation needed:** Networking team review of Services for partner fit

### Assumption 5: Key Rotation Doesn't Break Connectivity
- **Assumed:** Partners can rotate keys without customer-visible outages
- **Risk:** Database connections might drop during rotation
- **Validation needed:** Test graceful key rotation with long-lived database connections

### Assumption 6: Partners Want Agent-Based Deployment
- **Assumed:** Snowflake/Databricks willing to run Tailscale binary in their infrastructure
- **Risk:** Security/compliance concerns, operational overhead
- **Validation needed:** Conversations with potential partners about deployment model

### Assumption 7: Timeline is Realistic
- **Assumed:** 3-4 months eng work for partner API
- **Risk:** Underestimated complexity, dependencies on other work
- **Validation needed:** Engineering team sizing and scoping

---

## Critical Unknowns (Need Input from Tailscale Team)

**Before pursuing this opportunity, need answers to:**

1. **Has this been explored before?**
   - Any prior partner integration discussions?
   - Why did they succeed/fail?
   - What did we learn?

2. **What are the architectural hard constraints?**
   - Things that fundamentally can't work with current architecture
   - Would require major re-architecture
   - Security model incompatibilities

3. **What's the actual engineering effort?**
   - Platform team: "Partner API is 2 months" or "6+ months, massive scope"?
   - Identity team: OAuth delegation complexity?
   - Networking team: Services multi-tenancy feasibility?

4. **What's the business priority?**
   - Is this exciting to leadership or a distraction?
   - Where does it rank vs other opportunities?
   - Worth the partnership BD overhead?

5. **What do existing customers say?**
   - Are people asking for this?
   - Would it solve a real pain point?
   - Or is it a solution looking for a problem?

**Note:** This analysis is based on public information and reasonable assumptions. Actual architectural constraints may make some/all of this infeasible. Critical to validate with Tailscale engineering and product teams before pursuing.

---

## Connection to Bridge Strategy

**This actually reinforces the bridge approach:**

**Infra Access (Bridge Feature) → Partner Integration:**
- Database access, audit logging, session recording already on roadmap
- Snowflake integration is just a productized version of infra access
- If bridge features are mature, partner integration is easier

**Services (Bridge Feature) → Partner Integration:**
- Future state: Snowflake uses Services to expose warehouses
- Services multi-tenancy directly enables partner use case
- Integration drives Services adoption

**Workload Identity (Bridge Feature) → Partner Integration:**
- OAuth flow similar to workload identity federation
- Same backend infrastructure serves both use cases

**Implication:** Building bridge features creates the foundation for partnerships. Partnerships validate and accelerate bridge adoption. Virtuous cycle.

---

## Next Steps (If Pursuing This)

**Immediate (Q4 FY26):**
1. Validate demand: Talk to 10 customers who use both Tailscale and Snowflake
2. Snowflake outreach: Gauge interest from Snowflake product/eng team
3. Technical spike: Prototype partner provisioning API (2 weeks)

**Near-term (Q1 FY27):**
4. Reference architecture: Document how to manually set up Tailscale + Snowflake today
5. Design partner program: 5 customers willing to test early integration
6. Roadmap alignment: Ensure partner API doesn't conflict with bridge priorities

**Medium-term (Q2-Q3 FY27):**
7. Build partner API (if validated)
8. Snowflake integration development (parallel)
9. Private beta launch

---

*This analysis assumes Snowflake/Databricks integration as example, but requirements apply broadly to any SaaS/PaaS vendor integration.*
