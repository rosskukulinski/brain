---
created: 2025-10-24
source: VP Product Interview Materials
author: Sam Linville
published: 2025-08-08
tags: [tailscale, product-strategy, roadmap, interview-materials]
status: complete
project: TailScale
---

# H2 FY26 / Early FY27 Product Strategy notes

## Draft [Sam Linville](mailto:sam@tailscale.com) Aug 8, 2025

## 18-month vision from offsite

* **Tailscale is faster to build on and easier to scale.** We pay down compounding technical debt in core areas. Re-architecture makes it possible to develop outside the core. DevEx and tooling improve so teams can move independently and safely 

* **Tailscale wins with IT for org-wide VPN deployments.** We are the top choice for IT teams at eng-forward companies in NA/EU. We’ve built the key features that unblock security and compliance concerns. Pricing/packaging support IT-led purchasing and seat-based scale

* **Tailscale’s platform powers a new class of integrations and products.** Tailnets can be embedded in OEM devices, CI/CD tools, and partner workflows. “Powered by Tailscale” use cases expand via node sharing, ephemeral tailnets, and Tailnets v5. Design partners are shipping products on top of Tailscale

* **Tailscale’s free plan fuels a wave of viral growth.** Consumer use cases (“family & friends IT”) are polished and supported. Product improvements reduce friction for less technical users. We convert free tailnets into a stronger MAU funnel and social growth loop

Ultimately the way that I read the IT/security and platform goals together is that **we want Tailscale to be a complete network for a company to build everything on.**

Here’s how I’m thinking about the interplay of these four things:

Making Tailscale faster to build and scale and polishing the personal plans are **foundational goals** that support our two revenue-generating goals.

### Faster to build and scale

If we are able to develop software faster, with more confidence in its quality, then we can achieve greater velocity on all of our user-facing work. This is more engineering strategy and less product strategy, so at this point I think it’s outside the scope of this doc.

### Personal plan work

It’s important to continue to nurture our personal plans because they are an integral source of inbound deal flow and self-serve revenue; while we have always struggled to get very specific data on this, we know from anecdata that the “bring to work” mechanism is not a fantasy.

We should avoid meaningfully shifting the persona that our personal plans target; to the extent that we want more non-technical personal users in our product, we want them as **additional members of a tailnet** that is administered by a technical person (ie, the “family IT guy”).

To the extent that we want to lower the barrier to entry for administering a tailnet, it’s because we want the “family IT guy” to include folks who have slightly less technical experience; less of a r/homelab mod, closer to someone who bought their first Raspberry Pi.

## Win with eng-forward IT/Security

There are a lot of easy opportunities here but generally speaking, I think that our path to winning here looks like:

* Give IT the best VPN on the market that **meaningfully reduces the day-to-day maintenance burden**: amount of support tickets and user complaints they need to deal with on a day to day basis.

* Give Security easy-to-deploy tools that can **replace costly and complex infra access solutions** for engineering teams

  * My intuition is that it will be **more** important as we build our Platform story; when you’re building your application/infra connectivity on top of Tailscale, you’ll also need a way for your developers to access that infra.

  * Some criticism of this product line is that the total revenue potential isn’t astronomical; this is true **but** it’s very complementary to our existing product offering that’s already very appealing to engineers. Important part of zero-trust for eng-forward orgs, and helps folks migrate off of $75/u Teleport seats. It’s also pretty easy to get these last features checked off, and very easy for us to create pipeline using these features.

* Allow IT/Security at eng-focused orgs to **layer security measures** on top of the best VPN on the market so they can achieve their goals without compromising on user experience (as forced by Zscaler, Netskope, PANW Prisma)

  * DNS filtering, packet inspection, and DLP are the big three things to focus on here.

    * Risk: DNS filtering is pretty UX-neutral, but packet inspection and DLP force full-tunnel configurations that degrade one of the core value propositions of Tailscale (performant direct connections). Traffic steering will need to be *really* good.

* Continued development of the multiple tailnets story for delegation of administrative domains (team or environment segmentation)

## Mature the platform

We have talked a lot about “H2M” and “M2M” and I think that distinction is going to become clunky. I think what we’re actually talking about is **core VPN** or **app connectivity**.

**Core VPN:** You’re using Tailscale for a business VPN or infra access.

**App connectivity:** You’re using Tailscale to provide the connectivity layer between distributed services or infrastructure.

App connectivity can look like an internal platform or CI/CD, end-user product, or internal tooling. The internal tooling piece is a little bit muddy because the internal tool is likely deployed into the Core VPN for employees to access, but I think it’s actually a great bridge to help people who bought us for the Core VPN think about Tailscale being useful for app connectivity

Our path to winning here looks like:

* Solid SDKs, boilerplate/starter projects, devrel that can illustrate the power of Tailscale’s platform for developers and help fuel the virality of the platform

  * An expanding catalog of community projects or officially supported projects that build “outside the Tailscale core” as a way to illustrate the concept

* A story for Kubernetes service\<-\>service communication that appropriately melds the K8s-native way of doing things with our own opinions about how Tailscale can improve those workflows.

* Implementation of the tailnetsv5 vision for resource sharing between tailnets in a secure and scalable way

* Continued development of the multiple tailnets story for programmatic or even ephemeral tailnet creation.

We have also been thinking about K8s work as the foundational element of “M2M” work, and while our earliest design partners are using K8s, I think we should be careful that we don’t overindex on K8s-centric workflows. I think our opportunity here is a lot bigger than just a K8s workflow, as evidenced by \[Customers\].

## Next 9 months

### Win with eng-forward IT/security teams (Core VPN)

| Use case/Category | Feature | Timeline | Revenue potential |
| :---- | :---- | :---- | :---- |
| Infra access *Replace:Teleport, StrongDM, Vault \[specific use cases\], Boundary, complex home-grown solutions* | DB access/recording | Beta/GTM in Q1 | Medium |
|  | K8s API proxy audit logging | Beta/GTM in Q4 |  |
|  | Agentless/Bastion Tailscale SSH | Beta/GTM in Q2(I’d really like to see if this can be sooner…) |  |
| Business VPN Focus: Day to day experience *Replace:PANW GP, Cisco AnyConnect, Fortigate, Sonicwall, OpenVPN, Twingate* | Network flow logging improvements | Spans Q3 \+ Q4 | High |
|  | Connectors v2 | ? |  |
|  | Traffic Steering | Beta/GTM in Q3 |  |
|  | Peer Relay | Beta/GTM in Q3 |  |
|  | Client UI improvements | Spans Q3 \+ Q4 |  |
|  | Device posture failure notifications | Beta in Q4 |  |
|  | ACL access denial notifications | Beta in Q1 |  |
|  | Debugging tools | Spans Q3 \+ Q4 |  |
| Multiple tailnets | Initial beta functionality | Beta in Q3 | High |
|  | Tailnet access policies (loginPolicies) | Alpha in Q4 |  |
|  | Multiple IdPs/Domains | Alpha in Q4 |  |
| Security tools *Replace:Netskope \[specific use case\], DNSFilter, Cisco Umbrella, ScoutDNS* | DNS filtering (built into the product) | Alpha in Q1, Beta in Q2 (I’d really like to see if this can be sooner…) | Low |

### Mature the platform (App connectivity)

| Use case/Category | Feature | Timeline | Revenue potential |
| :---- | :---- | :---- | :---- |
| IoT with resource constraints *Replace:Traditional approaches here include SMS, competitors like AWS offer MQTT-based systems* | Rust client | ? | High |
|  | Tailnets v5 sharing | ? |  |
|  | libtailscale | Beta in Q1 assuming Rust client is done |  |
| General platform work *Replace:There aren’t specific solutions that we replace as neatly as we do in the infra access or business VPN categories, but we make something incredibly complex turn into something very simple and secure.* | Expanded SDK languages (Python, JS is a good start) | Beta in Q1 assuming Rust client is done |  |
|  | Services | Beta/GTM in Q3 |  |
|  | Multiple tailnets API | Ongoing, but already “done” |  |
|  | Workload identity federation | Beta/GTM in Q3 |  |
|  | Client metadata | Beta in Q3 |  |

There is a much scarier version of this in a spreadsheet here, that I was using to sanity check that we could do all of this without completely abandoning things prior to GA; I think this could also be a decent foundation for figuring out what staffing for these projects would realistically need to be.