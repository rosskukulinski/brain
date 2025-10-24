---
created: 2025-10-24
updated: 2025-10-24
tags: [tailscale, partnerships, OEM, integrations, ecosystem]
status: complete
project: TailScale
---

# Tailscale OEM and Partner Ecosystem

## Partnership Program Overview

Tailscale offers three primary partnership models:

1. **Value Added Resellers (VARs)** - Promote Tailscale solutions to clients, earn competitive margins
2. **Managed Service Providers (MSPs)** - Integrate Tailscale into managed service offerings
3. **Technology Partners** - Create mutual value through technical integrations

## Hardware OEM Partners (Native Integration)

### Network Equipment

**GL.iNet** ⭐ *Primary Hardware OEM*
- **Status:** Native Tailscale built into firmware v4.x
- **Models with Native Support:**
  - Beryl AX (GL-MT3000) - Featured travel router
  - Brume 2 (GL-MT2500)
  - Flint 2 (GL-MT6000)
  - Flint 3 (GL-BE9300)
  - Flint 3e (GL-BE6500)
  - Puli AX (GL-XE3000)
  - Spitz AX (GL-X3000)
  - Slate 7 (GL-BE3600)
  - Marble (GL-B3000)
  - Plus 10+ additional WiFi 6 models
- **Market:** Travel routers, remote access, small business
- **Note:** Tailscale blog featured the Beryl AX as "great travel router"

**Zyxel Networks** 🆕 *June 2025 Partnership*
- **Status:** Recently announced official partnership
- **Products:** USG FLEX H Series firewalls (uOS v1.32+)
- **Integration:** WireGuard-based mesh VPN fully integrated into firewall management interface
- **Target Market:** Small businesses with limited IT resources
- **Pricing:** Free Tailscale Starter Plan for eligible USG FLEX H customers
- **Quote:** "VPNs are essential...but they have often been too complex for smaller organizations" - Ken Tsai, President

### NAS (Network Attached Storage) Vendors

**Synology**
- **Status:** Official app in Synology Package Center
- **Features:** Easy-to-use web UI for configuration
- **Update Cadence:** Approximately once per quarter
- **Market Position:** Consumer and SMB NAS leader

**QNAP**
- **Status:** Official app in QNAP App Center (announced June 2023)
- **Features:** Easy-to-use web UI for configuration
- **Platforms:** x86-64bit and arm-64bit models (not arm41)
- **Market Position:** Consumer and enterprise NAS

**Unraid** 🆕 *October 2024 Technology Alliance*
- **Status:** Technical Partnership established October 11, 2024
- **Integration:** Plugin fully integrated into Lime Technology repositories
- **Native Features:**
  - Unraid 7 includes native Tailscale (ts.net) certificate support
  - Docker container integration with unique machine names per container
  - Automated setup, no port forwarding required
- **Market Position:** Homelab, self-hosting, media servers

**TrueNAS**
- **Status:** Official app in TrueNAS SCALE software
- **Note:** TrueNAS CORE (FreeBSD-based) requires workarounds
- **Market Position:** Enterprise and prosumer NAS

## Cloud Platform Partners

### Major Cloud Providers

**Amazon Web Services (AWS)**
- **Status:** Authorized AWS Partner Network member (April 2024)
- **Distribution:** Available through AWS Marketplace
- **Benefits:** Simplified procurement, flexible billing, AWS credits applicable
- **Integration:** Seamless deployment in AWS environments

**Microsoft Azure**
- **Status:** Official partner
- **Distribution:** Available through Azure Marketplace
- **Benefits:** Azure infrastructure integration, consolidated billing

**Google Cloud Platform (GCP)**
- **Status:** Supported platform
- **Integration:** Documentation and deployment guides available

### Platform-as-a-Service (PaaS)

**Fly.io**
- **Status:** Community integration with official Tailscale documentation
- **Quote:** Fly.io reports being "big fans of Tailscale"
- **Use Case:** Connect Fly.io deployments to Tailnet
- **Implementation:** User-deployed via container configuration

**Heroku, Render, Railway**
- **Status:** Community-supported integrations
- **Note:** No formal partnership announcements found

## Open Source Router/Firewall Platforms

**OPNsense**
- **Status:** Official Tailscale support
- **Platform:** FreeBSD-based open source firewall
- **Documentation:** Full Tailscale integration guide

**pfSense**
- **Status:** Plugin available
- **Implementation:** Tailscale package for pfSense

**OpenWRT**
- **Status:** Official Tailscale package available
- **Note:** Powers many custom router implementations

## Identity Provider Integrations (23 Total)

### Enterprise SSO
- Okta
- Microsoft Entra ID (formerly Azure AD)
- Google Workspace
- OneLogin
- Ping Identity
- Duo
- Auth0

### Developer-Focused
- GitHub
- GitLab
- Gitea
- Codeberg

### Self-Hosted
- Keycloak
- Dex
- Ory
- Authentik
- ZITADEL
- Authelia

### Consumer
- Apple ID
- Passkeys

### Other
- AWS Cognito
- Zoho
- JumpCloud
- Custom OIDC

## MDM (Mobile Device Management) Partners

### Enterprise MDM
- **Microsoft Intune** - Native integration
- **Jamf Pro** - Apple device management
- **Kandji** - Modern Apple MDM
- **JumpCloud** - Cloud directory platform

### SMB MDM
- **SimpleMDM** - Lightweight Apple MDM
- **TinyMDM** - Minimal footprint MDM

## Security & Device Posture Partners

### Endpoint Detection & Response (EDR)
- **CrowdStrike Falcon**
- **SentinelOne**

### Device Management
- **1Password Extended Access Management (XAM)**
- **Jamf Pro** (also in MDM category)
- **Kandji** (also in MDM category)

### Security Orchestration
- **Axonius** - Asset management platform
- **Tines** - Security automation

## Infrastructure as Code (IaC) Partners

### Configuration Management
- **Terraform** - Official Tailscale provider
- **Pulumi** - Multi-language IaC
- **Ansible** - Automation platform

### Security & Compliance
- **Steampipe** - Security and compliance queries
- **Resmo** - Cloud asset inventory
- **CloudQuery** - Infrastructure-as-data

## Kubernetes & Container Platforms

### Container Orchestration
- Kubernetes (pods, services, clusters, API servers)
- K3s (lightweight Kubernetes)
- Docker
- LXC

### Hosted Kubernetes
- Amazon EKS
- Google GKE
- Azure AKS
- DigitalOcean Kubernetes

## Developer Tools & CI/CD

### Code Editors & IDEs
- **VS Code** - Official extension
- **Docker Desktop** - Docker integration
- **GitHub Codespaces** - Cloud development
- **Gitpod** - Browser-based development
- **Coder** - Self-hosted cloud IDEs
- **Raycast** - Productivity tool with Tailscale integration

### CI/CD Platforms
- **GitHub Actions** - Official integration
- **GitLab CI/CD**
- **CircleCI**
- **Dagger** - CI/CD as code

## Data & Database Platforms

### Managed Databases
- **AWS RDS** - Relational databases
- **Materialize** - Streaming SQL database
- **Crunchy Bridge** - Managed PostgreSQL

### Observability & Logging
- **Datadog** - Monitoring and analytics
- **Splunk** - Enterprise logging
- **ELK Stack** - Elasticsearch, Logstash, Kibana
- **Panther** - Security data lake
- **Cribl** - Data routing
- **Axiom** - Serverless logs

## Network Security Vendors

### Enterprise Firewalls (Community/Partner Support)
- Barracuda
- Cisco
- Fortinet
- Palo Alto Networks
- Ubiquiti UniFi (⚠️ no official partnership - community-driven)

### DNS & Privacy
- **Pi-hole** - Network-wide ad blocking
- **NextDNS** - Privacy-focused DNS
- **Mullvad** - Privacy VPN exit nodes

## Notable Absences / Opportunities

### No Official Partnership Found
- **Ubiquiti UniFi** - Community wants it, no official integration
- **Firewalla** - Users requesting native support
- **TP-Link Omada** - Users migrating away due to lack of Tailscale
- **Major consumer router vendors** (Asus, Netgear, Linksys, etc.)
- **Render** - PaaS provider, no formal integration found
- **Railway** - PaaS provider, no formal integration found

### Potential White Space
- **IoT/Edge Hardware** - Limited embedded device partnerships
- **Enterprise WAN Vendors** - SD-WAN, SASE competitors
- **Database Vendors** - No Snowflake, Databricks, MongoDB partnerships
- **Hyperscalers** - Limited visibility into Oracle, Alibaba integrations

## Partnership Strategy Insights

### Successful OEM Model Characteristics
1. **Hardware with existing connectivity needs** (routers, NAS, firewalls)
2. **Target customers with networking pain** (small business, homelab, remote work)
3. **Open/flexible platforms** (OpenWRT-based, Linux-based)
4. **Value-add differentiation** (travel routers, self-hosting platforms)

### Distribution Strategy
- **Cloud Marketplaces:** AWS, Azure (procurement simplification)
- **App Stores:** Synology, QNAP, Unraid (one-click install)
- **Native Integration:** GL.iNet, Zyxel (firmware-level)
- **Community-Driven:** Ubiquiti, pfSense, OPNsense (third-party packages)

### Market Segmentation
- **Enterprise:** MDM, EDR, cloud platforms, SSO
- **SMB:** Zyxel firewalls, Synology/QNAP NAS, MSP channel
- **Prosumer/Homelab:** Unraid, GL.iNet, open-source firewalls
- **Developer:** PaaS platforms, CI/CD, IaC tools

## Key Takeaways

1. **Hardware OEM strategy is working** - GL.iNet, Zyxel, NAS vendors provide distribution
2. **Cloud marketplace presence** - AWS, Azure simplify enterprise procurement
3. **Developer ecosystem is strong** - IaC, CI/CD, cloud-native tools well-integrated
4. **Gaps in traditional networking** - Major router vendors (Ubiquiti, TP-Link, Asus) missing
5. **Recent momentum** - Two major hardware partnerships in 2024 (Unraid Oct, Zyxel June)
6. **Community fills gaps** - Where official partnerships don't exist, community creates solutions

## Questions for Further Research

1. **Revenue split:** What % of Tailscale's business comes through partners vs direct?
2. **OEM economics:** How do GL.iNet and Zyxel deals work? Revenue share? License fees?
3. **Partner tiers:** Are there formal partner tiers with different benefits?
4. **Co-marketing:** What joint marketing exists with hardware partners?
5. **Product roadmap influence:** Do OEM partners influence Tailscale's feature roadmap?
6. **Database opportunity:** Why no partnerships with Snowflake, Databricks, MongoDB?
7. **Missing consumer hardware:** What's preventing Asus, Netgear, Linksys adoption?

## Sources

- [Tailscale Partnerships Page](https://tailscale.com/partnerships)
- [Tailscale Integrations](https://tailscale.com/integrations)
- [Zyxel Press Release (June 2025)](https://www.zyxel.com/us/en-us/newsroom/press-releases/zyxel-networks-simplifies-secure-remote-connectivity-through-integration-with-tailscale)
- [Unraid 2024 Year in Review](https://newsletter.unraid.net/p/unraid-2024-year-in-review)
- [Tailscale AWS Partnership Blog (April 2024)](https://tailscale.com/blog/aws-partner-network)
- [QNAP App Center Announcement (June 2023)](https://tailscale.com/blog/qnap-app-center)
- Various Tailscale documentation pages and community forums
