# 📬 EPD Newsletter|Q3, September 2025 go/newsletters

---

## Q3 GOALS

Read more about our Q3 plan here  
63 Committed Projects  
🟢*On track: 23*   
🟡*Slipping: 6*  
🟠*Blocked: 1*  
⚫*Paused/ Deprioritized: 7*   
*🔵Complete: 14*  
*⚪ Not Started: 12*

## Quick Highlights

1. **👷 Peer relays:** We’ve now onboarded 5 customers to Peer Relays in an alpha stage, and their feedback has been incredibly valuable. The go-to-market teams helped significantly in this push. The list includes \[redacted customers\] (who moved off but still gave valuable feedback). We have multiple prospective users \[redacted\] in the pipeline.  
2. **🔁 Priority Changes:** Traffic Steering, Tailperf, and Client Metadata Betas were all pushed off the Q3 plan. User Sessions will remain in progress, but is no longer expected to ship in Q3.  
   1. **🔽 Traffic Steering, 🔼 Alternate Connectivity Endpoints :** Traffic Steering has been put on pause while the team works to deliver critical work for a \[redacted customer\]. We have communicated this thoroughly and do not expect any significant impacts to deals. The customer needed to have an alternative endpoint for control plane connectivity, to reduce chances of failures on hostile networks; we didn’t have enough resourcing on the Engineering team to cover this work.  
   2. **🔽 Tailperf,  🔼 Per-tailnet DERP Metrics:** Peer Relay rollout exposed a need for visibility into \[redacted customers’\] use of DERP; as such the Data Plane team is focusing on this internal visibility instead of Tailperf.  
   3. **🔽 Client Metadata Beta, 🔼 Ephemeral Node Scalability:** The team staffed on this project has a heavy focus on scalability for ephemeral workloads, initially focusing on proposals like Fast Path Node Addition and validating Packet Filters v2. This was an explicit tradeoff that will push Client Metadata Beta out of Q3.  
   4. **🔴 User Sessions beta:** For similar reasons as above, working through deployment issues, staffing, and higher priority on Seamless Key Renewal, User Sessions beta is not expected to be delivered in Q3, but is actively in progress.  
3. **🔥 App Connectors incident:** Connectors with many quick route changes finally caused an outage (inc-151); as a result we capped the number of routes a connector can auto-approve to 3000\. Customers can still manually approve routes in the admin panel UI or via API.    
   1. **Challenge:** Connectors have long relied on auto-approval as a mechanism to quickly expose routes to the tailnet. That code path had a fundamental assumption around the rate of approvals that we broke in this new Connector model. It is fairly surprising it took so long to break.  
   2. **Solution:** We capped the number of routes any given connector can automatically approve to 3000\.

Thanks for reading\! 

## **🚢 Shipped**

| ✅ Recent Releases  [Windowed UI for macOS (beta)](#windowed-ui-for-macos-\(beta\)) [Visual Editor GA](#visual-editor-ga-\(ga\)) [Auto Approved Route Limits](#auto-approved-route-limits) [AWS Preset App for App Connectors](#aws-preset-app-for-app-connectors) [Exit Nodes and Subnet Routers can be deployed on K8s](#exit-nodes-and-subnet-routers-can-be-deployed-on-kubernetes) [SplitDNS staged rollout](#splitdns-staged-rollout-\(alpha\)) [New DERP infra in SYD, TOK, SIN](#new-derp-infrastructure-in-syd,-tok,-sin) | ✅Approved DACIs & Process Flows PRD: Connector improvements Tailscale UI component library DACI: [console.tailscale.com](http://console.tailscale.com) Services: Nous and Verbs |
| :---- | :---- |

#### **Windowed UI for MacOS (beta)** {#windowed-ui-for-macos-(beta)}

**Release Date:** Sep 10, 2025

**Highlights:** Users on macOS can now interact with Tailscale in a windowed app that makes checking connection status, changing exit nodes, and reading device information clear. Features like Taildrop and ping are now much easier to find than they previously were in the menu bar. We have received a lot of feedback both internally and from users pointing out bugs and improvements and the team has been working on these for the 1.90 release.   
**More Details:** [Tailscale’s windowed macOS UI is now in beta](https://tailscale.com/blog/windowed-macos-ui-beta)

####  **Visual Editor GA (GA)** {#visual-editor-ga-(ga)}

**Release Date:** Code Complete by Sep 30, though we won’t launch until late Oct.

**Highlights:** After a very smooth beta, we have promoted the visual policy editor to GA\! The team spent some time this quarter cleaning up a relatively short list of bugs and polish items. We quietly promoted this to GA, and will do a marketing push as part of the Fall Update EOQ.

#### **Auto Approved Route Limits** {#auto-approved-route-limits}

**Release Date:** Sep 25, 2025 

**Highlights:** App connectors have long relied on auto-approval as a mechanism to quickly expose discovered routes to the tailnet. That code path had a fundamental assumption around the rate of approvals that we broke in this new App connector model. We now cap auto-approvals at 3000 per machine to prevent further overloading our control servers. Customers can still manually approve routes or use our APIs for bulk approvals.

#### **AWS Preset App for App Connectors** {#aws-preset-app-for-app-connectors}

**Release Date:** Sep 29, 2025

**Highlights:** Customers exposing AWS resources via App Connectors can now use a number of Preset App configurations to set up their AWS connections, leading to less thrash and enabling more stable customer experiences when exposing AWS resources like Cloudfront, S3, EC2, RDS, and more.  
![][image1]

#### **Exit Nodes and Subnet Routers can be deployed on Kubernetes** {#exit-nodes-and-subnet-routers-can-be-deployed-on-kubernetes}

**Release Date:** Sep 18, 2025

**Highlights:** Exit Nodes and Subnet Routers can now be easily deployed on Kubernetes infrastructure in HA configurations. This allows k8s-heavy or k8s-exclusive teams to leverage some of our most widely used networking features.  
**More Details:** [Changelog](https://tailscale.com/changelog#2025-09-18)

#### **SplitDNS Staged Rollout (Alpha)** {#splitdns-staged-rollout-(alpha)}

**Release Date:** Sep 30, 2025

**Highlights:** A select group of customers will now be able to scope Split DNS rules to specific users, groups, and devices. This allows administrators at companies to roll out DNS changes slowly to test groups or less critical infrastructure, before making those changes tailnet-wide. This also allows admins at companies to grant access to internal DNS nameservers (and the domains they resolve) to specific users and groups, while not granting that access for others. 

#### **New DERP infrastructure in SYD, TOK, SIN** {#new-derp-infrastructure-in-syd,-tok,-sin}

**Release Date:** Sep 11, 2025

**Highlights:** We continued planned rollout of Linode/Akamai hosting for DERPs in SYD, TOK, and SIN per initial proposals in Linode (Akamai) as a DERP hosting provider design doc.  
**More Details:** [Changelog](https://tailscale.com/changelog#2025-09-09)

---

## **In Progress** [Read more about what’s shipping here](https://tailscale.atlassian.net/jira/plans/16/scenarios/16/timeline?vid=98)

### **🚢 Upcoming Releases**

- [Seamless Key Renewal GA](#seamless-key-renewal-ga) (Oct)  
- [Actor IDs in network flow logs](#actor-ids-in-network-flow-logs) (Oct)  
- [GCS log streaming](#gcs-log-streaming) (Oct)  
- [Grants in Serve headers](#grants-in-serve-headers) (Oct)  
- [tsnet support for Services](#tsnet-support-for-services) (Oct)  
- [Services Beta](#services-beta) (Oct)  
- [Per tailnet DERP metrics](#heading=h.74gzeykoplkf) (Oct)  
- [Peer relay beta](#peer-relay-beta) (Oct)  
- [Workload identity beta](#workload-identity-beta) (Oct)  
- [Multiple tailnets, sales-gated beta](#multiple-tailnets,-sales-gated-beta) (Oct)  
- [Kubernetes API proxy audit logging, private alpha](#kubernetes-api-proxy-audit-logging,-private-alpha) (Oct)  
- [Windowed UI for Windows (internal POC)](#windowed-ui-for-windows-\(internal-poc\)) (Nov)  
- [Static IP rollout for logging infrastructure](#static-ip-rollout-for-logging-infrastructure) (Nov)  
- [console.tailscale.com rollout](#console.tailscale.com-rollout) (Nov)  
- [Network flow logging in the admin console](#network-flow-logging-in-the-admin-console) (Q4)  
- [Group membership in Serve headers and tsnet](#group-membership-in-serve-headers) (Q4)  
- [Alternate Connectivity Endpoints (ACE)](#alternate-connectivity-endpoints) (Q4)  
- [Policy fragments beta](#policy-fragments-\(beta\)) (Q4)  
- [User Sessions Beta](#user-sessions-beta) (Q4)  
- [User approval \- org invite fast path](https://docs.google.com/document/d/1jfcheE2IlcKdHPPWKlUHKlXHZysMbOpJlJEuvy0nsFg/edit?usp=sharing) (Oct)

#### **Seamless Key Renewal GA** {#seamless-key-renewal-ga}

**Estimated:** Oct 22, 2025(client release 1.90)  
🟢 On track  
Enterprise Pod ([James Sanderson](mailto:jsanderson@tailscale.com)[Alex Chan](mailto:alexc@tailscale.com)[Megan Walsh](mailto:meganw@tailscale.com))  
**Highlights:** Seamless key renewal allows TCP connections to remain active during renewal of node keys as opposed to having a blip in connectivity. This is changing the default way we renew node keys and does not require any action from the admin or user to enable (besides updating their client to 1.89+).

#### **Network flow logging in the admin console** {#network-flow-logging-in-the-admin-console}

**Estimated:** Q4  
🟡Slipping into Q4  
DevEx Pod ([Samuel Jinadu](mailto:samuel@tailscale.com)[Rodrigo Tello Medina](mailto:rodrigo@tailscale.com)[Danni Popova](mailto:danni@tailscale.com))  
**Highlights:** We are adding a new UI to interface with network flow logs natively in the admin console. As of today, such an experience exists for configuration logs, but you cannot consume network flow logs without first querying our API or streaming them to a SIEM and using its dashboard. Currently, this initiative is in the initial design phase.

#### **Actor IDs in network flow logs** {#actor-ids-in-network-flow-logs}

**Estimated:** Oct 30, 2025  
🟢On track  
Platform Pod ([Samuel Jinadu](mailto:samuel@tailscale.com)[Eric Weinstein](mailto:ericw@tailscale.com)[Joseph Tsai](mailto:joetsai@tailscale.com))  
**Highlights:** We are introducing Actor IDs (human-readable identifiers) into our network flow logs to enhance the troubleshooting experience for IT/Security personas who consume our logs. This benefits accounts streaming to a SIEM/bucket, as well as those who will utilize our upcoming UI for these logs in the admin console. These are planned as additional fields in the JSON schema, so this will not be a breaking change.

#### **GCS Log Streaming** {#gcs-log-streaming}

**Estimated:** Oct 15, 2025  
🟢 On track  
Platform Pod ([Samuel Jinadu](mailto:samuel@tailscale.com)[Eric Weinstein](mailto:ericw@tailscale.com)[Jim Scott](mailto:jim@tailscale.com))  
**Highlights:** Adding first-class support for GCP’s object store to enable easier streaming to Google SecOps and Big Query. This initially started as a deal blocker, and multiple customers are also interested in this solution.

#### **Grants in Serve headers** {#grants-in-serve-headers}

**Estimated:** Oct 31, 2025  
🟢 Finalizing Technical Design  
DevEx ([Gesa Stupperich](mailto:gesa@tailscale.com)), [Kabir Sikand](mailto:kabir@tailscale.com)  
**Highlights:** Customers building with tsnet have historically had access to Application Capabilities and User Identities within the tsnet APIs. A long-standing request for developers has been to bring this same functionality to `tailscale serve`; this enables applications to read in application capabilities defined in Tailscale Grants to back end infrastructure like internal apps, workloads, databases, etc. With the upcoming release of Services, this becomes even more critical functionality.

#### **Group membership in Serve headers** {#group-membership-in-serve-headers}

**Estimated:** Oct 31, 2025  
🟢 Planning  
DevEx ([Gesa Stupperich](mailto:gesa@tailscale.com)), [Kabir Sikand](mailto:kabir@tailscale.com)  
**Highlights:** Customers want to read group membership in their applications and use it in application or gateway logic; this feature brings group membership information into `tailscale serve` request headers.

#### **tsnet support for Services** {#tsnet-support-for-services}

**Estimated:** Oct 31, 2025  
🟢 Finalizing Technical Design  
Networking ([Harry Harpham](mailto:harry@tailscale.com)), [Kabir Sikand](mailto:kabir@tailscale.com)  
**Highlights:** Customers want to build Tailscale-native applications, and they often use tsnet to do so. Customers’ tsnet applications should be able to be registered to custom MagicDNS names, load balanced, and allow for granular access controls via Services. tsnet will expose a new API for registering a tsnet instance as a Service host.

#### **Services Beta** {#services-beta}

**Estimated:** Oct 23, 2025  
🟢 On Track  
Networking ([Naman Sood](mailto:naman@tailscale.com), [Adrian Dewhurst](mailto:adrian@tailscale.com), [Kevin Liang](mailto:kevinliang@tailscale.com), [Fran Bull](mailto:fran@tailscale.com)), [Kabir Sikand](mailto:kabir@tailscale.com), Designer: [Rodrigo Tello Medina](mailto:rodrigo@tailscale.com)  
**Highlights:** After a largely successful Alpha period, we’re addressing user feedback with better documentation, UX workflows, CLI feedback, error messaging, declarative configuration, remote target support, network flow logs support, and minor internal visibility enhancements to bring Services to a Public Beta on October 27th.

#### **Alternate Connectivity Endpoints** {#alternate-connectivity-endpoints}

**Estimated:** Nov 30, 2025  
🟢 On Track  
Special Project ([Simon Law](mailto:sfllaw@tailscale.com), [Brad Fitzpatrick](mailto:bradfitz@tailscale.com), [James Tucker](mailto:james@tailscale.com)), [Kabir Sikand](mailto:kabir@tailscale.com)  
**Highlights:** Connectivity-sensitive customers need backup endpoints to reach control from hostile networks where Tailscale is blocked, with device trust built in. This precludes use of a traditional proxy setup. Instead, Tailscale will provide (as an Enterprise add-on) [Alternate Connectivity Endpoints](https://docs.google.com/document/d/1C_6UvO2vWvPIpTUb_mHPxZ4YGTZWg2IAI4-SnbTTVaw/edit?tab=t.0#heading=h.ffjqvxgb4dfn), which uses a lightweight token-based authentication on top of a fleet of proxies to provide secondary connectivity paths to Tailscale control plane.

#### **Per Tailnet DERP Metrics**

**Estimated:** November  
🟢 Technical Design  
Data Plane ([Jordan Whited](mailto:jordan@tailscale.com), [Mike O'Driscoll](mailto:mikeo@tailscale.com)), [Kabir Sikand](mailto:kabir@tailscale.com)  
**Highlights:** Our Data Plane teams and Support teams need visibility into DERP use across tailnets and within a single tailnet. This can help with debugging, reduce escalation needs and timelines, and provide GTM teams a method to identify accounts that may benefit from a Peer Relay.

#### **Peer Relay Beta** {#peer-relay-beta}

**Estimated:** Oct 20, 2025  
🟢 On Track  
Data Plane ([Jordan Whited](mailto:jordan@tailscale.com)), [Kabir Sikand](mailto:kabir@tailscale.com)  
**Highlights:** Peer Relays are being instrumented, led by customer feedback, with better documentation and more customer debugging tools and visibility. This will allow Peer Relays to go into a Public Beta at the end of October.

#### **Policy fragments (beta)** {#policy-fragments-(beta)}

**Estimated:** First half of Q4 for public launch  
🟢Implementing  
DevEx ([Danni Popova](mailto:danni@tailscale.com), [Percy Wegmann](mailto:percy@tailscale.com), [Max Coulombe](mailto:max@tailscale.com), [Mario Minardi](mailto:mario@tailscale.com), [Gesa Stupperich](mailto:gesa@tailscale.com), [Clare Adrien](mailto:clare@tailscale.com))  
**Highlights:** Allow tailnets to create external fragments of policy, managed by an API, that can change out-of-band with the main policy file itself. Allows for automation to coexist peacefully with version-controlled or Terraform-managed tailnets.

#### **Allow `autogroup:self` destinations against more sources**

**Estimated:**  
🟢Implementing  
DevEx ([Max Coulombe](mailto:max@tailscale.com), [Sam Linville](mailto:sam@tailscale.com))  
**Highlights:** Provide more flexibility in policies by allowing autogroup:self to be used as a destination with any user target as the source. This is a longstanding feature request that was raised again by a customer.

#### **Workload Identity Beta** {#workload-identity-beta}

**Estimated: Late October, 2025**  
🟢Implementing  
Security ([Patrick O'Doherty](mailto:patrick@tailscale.com)) and DevEx ([Mario Minardi](mailto:mario@tailscale.com), [Sarah Wolfsont](mailto:sarahw@tailscale.com), [Sam Linville](mailto:sam@tailscale.com))  
**Highlights:** Workload identity is moving to public beta, with a redesigned Oauth keys page, a dedicated setup workflow, custom claim support, and an updated GitHub Action.  
More details: Figma prototype

#### **Kubernetes API proxy audit logging, private alpha** {#kubernetes-api-proxy-audit-logging,-private-alpha}

**Estimated: End of Q3**  
🟢Implementing  
Kubernetes ([Tom Proctor](mailto:thomas@tailscale.com), [Tom Meadows](mailto:tmeadows@tailscale.com), [David Bond](mailto:davidb@tailscale.com))  
**Highlights:** The tsrecorder container will be able to log *all* API calls made through the operator’s API proxy, allowing full auditability of access to clusters via the operator. This work also includes an improved tsrecorder UI.

#### **Multiple tailnets, sales-gated beta** {#multiple-tailnets,-sales-gated-beta}

**Estimated: End of Q3**  
🟢Implementing  
Identity ([Will Norris](mailto:will@tailscale.com), [Sonia Appasamy](mailto:sonia@tailscale.com), [Dasol Yoon](mailto:dasol@tailscale.com), [Richard Castro](mailto:richard@tailscale.com), [Nikita Uppal](mailto:nikita@tailscale.com), [Sara Farquharson](mailto:sara@tailscale.com), [Nick Marrone](mailto:nickm@tailscale.com), [Christine Lee](mailto:christine@tailscale.com), [Sam Linville](mailto:sam@tailscale.com))  
**Highlights:** We are working on features that will allow us to publicly talk about Multiple Tailnets and allow any customer to join the beta by talking to Sales. Sales/SEs will have easy self-serve tools for creating multiple tailnets that do not need to be run by a select group. Customers will be able to prevent a tailnet from being seen by their entire organization, though this first iteration will not allow selectively showing tailnets based on groups.

#### **User Sessions Beta** {#user-sessions-beta}

**Estimated: End of Q3**  
🔴 Delayed, planned Q4 release  
Enterprise ([James Sanderson](mailto:jsanderson@tailscale.com), [Alex Chan](mailto:alexc@tailscale.com), [Megan Walsh](mailto:meganw@tailscale.com))  
**Highlights:** User Sessions helps customers build a layered security model for commonly used daily reauthentication policies. Sessions gives customers a device posture attribute that can be used to optionally grant access to less sensitive devices like Exit Nodes without an active session. 

#### **Windowed UI for Windows (internal POC)** {#windowed-ui-for-windows-(internal-poc)}

**Estimated: Late November**  
🟡 At risk due to interrupts   
Client ([Aaron Klotz](mailto:aaron@tailscale.com)[Nick Khyl](mailto:nickk@tailscale.com)[Megan Walsh](mailto:meganw@tailscale.com))  
**Highlights:** Users on Windows will be able to interact with Tailscale in a windowed app that makes checking connection status, changing exit nodes, and reading device information clear. Features like Taildrop and ping are now much easier to find than they previously were in the menu bar. Builder issues and customer interrupts put us about \~1 month behind on delivering the internal POC. Still likely in a good place to land the customer-facing beta in Q4.

#### **Static IP rollout for logging infrastructure** {#static-ip-rollout-for-logging-infrastructure}

**Estimated:** Nov 13, 2025  
🟢 Planned  
Platform Pod ([Samuel Jinadu](mailto:samuel@tailscale.com)[Eric Weinstein](mailto:ericw@tailscale.com)[Jason O'Donnell](mailto:jason@tailscale.com))  
**Highlights:** Roll out static IP ranges to our logging infrastructure to provide a predictable IP range for customers who need to specifically allowlist IP ranges for our control infra.

#### [**console.tailscale.com**](http://console.tailscale.com) **rollout** {#console.tailscale.com-rollout}

**Estimated: Mid November**  
🟢 On track  
Platform ([Brad Fitzpatrick](mailto:bradfitz@tailscale.com), [Megan Walsh](mailto:meganw@tailscale.com))  
**Highlights:** We will be changing the URL for the admin console from [login.tailscale.com](http://login.tailscale.com) to [console.tailscale.com](http://console.tailscale.com) to reflect the contents of the page. In addition, other common URLs for admin console pages ([app.tailscale.com](http://app.tailscale.com), [admin.tailscale.com](http://admin.tailscale.com), and [portal.tailscale.com](http://portal.tailscale.com)) will also redirect to the admin console.

#### **Node Key Sealing GA and Node Key attestation Alpha**

**Estimated:** Nov 13, 2025  
🟢 Ready for upcoming release  
Security Pod ([Patrick O'Doherty](mailto:patrick@tailscale.com)[Andrew Lytvynov](mailto:awly@tailscale.com))  
**Highlights:** Node Key Sealing is going GA in the next client release. GA here means that it will be opt-out instead of opt-in, bringing node key protection to many more users (a.k.a. secure-by-default). Node Key Attestation Alpha will also land in the next client release, with all nodes generating attestation keys by default and control selectively enforcing them in MapRequest.  
**More Details:** Node Key Sealing was one of the efforts that came out of a customer deal blocker, as well as being flagged by pentesters. The customer has been using this since 1.86, so it’s got decent mileage. Node Key Attestation is another customer related initiative that provides even better protection against node cloning than sealing. It ensures that a cloned node cannot establish a map session with control. In the future we will do a similar check on node-to-node connections to lock things down further.

#### **User invites \- Org joiner UX cleanup**

**Estimated:** Nov 19, 2025  
🟢On track  
Growth Pod ([Amr Fouad](mailto:amr.fouad@tailscale.com)[Christine Lee](mailto:christine@tailscale.com)[Sarah Wolfsont](mailto:sarahw@tailscale.com))  
**Highlights:** Improve the UX for tailnet joiners coming through a custom domain+org. Cleans up the process of inviting and joining a tailnet as an internal user. (Does not affect tailnet-wide approval setting.)

### **⏭️ What Else?**

### Infrastructure, Security, KTLO, Tech Debt

#### **Firstbase \- Corporate Device Asset Management** 

**Estimated:** Nov 14, 2025  
🟡 Slipping  
Security Pod ([Keli Velázquez](mailto:keli@tailscale.com)[Christian Corrales](mailto:christianc@tailscale.com))  
**Highlights:** We’ve been underresourced in this area (Corporate IT Security) but with the addition of a recent new hire I believe we’ll catch up to where we want to be by the end of the year. First batch of devices sent out to new hires using Firstbase’s platform. SecOps is manually enrolling new hires into Firstbase, and will soon sync with BambooHR to pull in new hires and update existing hires on a synced schedule. Once fully onboarded, Firstbase will handle procurement, shipping new devices, tracking, and offboarding employee devices automatically, and will positively impact our speed and accuracy. 

#### **FleetDM \- Rollout** 

**Estimated:** Nov 14, 2025  
🟡 Slipping  
Security Pod ([Keli Velázquez](mailto:keli@tailscale.com)[Christian Corrales](mailto:christianc@tailscale.com))  
**Highlights:** We’ve been underresourced in this area (Corporate IT Security) but with the addition of a recent new hire I believe we’ll catch up to where we want to be by the end of the year. Approx. 40 devices remain and will need to be manually enrolled in Fleet.iPads purchased by Tailscale or Firstbase now automatically enroll in Fleet, and can be locked down and/or remotely wiped if lost or stolen. We’ve started collecting device posture data on devices enrolled in Fleet, and have enacted a minimum OS version for macOS devices to stay ahead of vulnerabilities. 

#### **Internal CA**

🔵 Completed  
Security Pod ([Patrick O'Doherty](mailto:patrick@tailscale.com)[Andrew Lytvynov](mailto:awly@tailscale.com))  
**Highlights:** Ahead of an October 1st external deadline we performed a successful zero-downtime migration of all shards and trunkds from using Let's Encrypt issued certificates for mutual-TLS client authentication to instead use certificates issued by a new private Certificate Authority in certd.  
**Background**: we use mTLS to secure shardAPI traffic. The Let's Encrypt issued certificates that we previously relied on are being phased out starting in October requiring us to find an alternative. We opted to build a private Certificate Authority into certd, our TLS cert management service that monitors and renews certificates with Let's Encrypt and uses setec to distribute the private material to applications. All internal HTTP clients across Tailscale codebases have been updated to consume the new trust roots via the `trustedca#CertPool` API in corp.

#### **Threat Intel program planning (Increased instances of reported or found abuse)**

**Estimated: End of Q3**  
🟢 Status  
Security Pod  
**Highlights:** Over the last 2mo we’ve seen an increase in third-parties contacting Security and/or Legal related to abuse on the Tailscale platform, as well as domain look-alike reports, and solicitations to our users on freelancing websites to share their tailnets/exit nodes. While still in the single digits, these instances were namely all initiated by third-parties rather than our own active research. These instances haven’t been massive distractions, but it has given rise to us starting planning a bit earlier than we had expected on what a Threat-Intel program can and should look like at Tailscale given our relative size and where we’re headed.

#### **ISO 27001 Readiness**

**Estimated: End of Q4**  
🟢 On-track  
Security Pod ([KaShonna Evans](mailto:kashonna@tailscale.com))  
**Highlights:** For ISO 27001 readiness, we’ve completed a self-assessed gap analysis with SOC 2 mapping and found that it covers \~70% of ISO controls. We’re working through breaking down the outstanding items and have a better understanding of what is applicable to our scope. Gap analysis like these play an important role in how we will continue to shape Tailscale’s Information Security posture over time and informs our decision-making during security roadmap planning.

#### **Funnel abuse** 

**Estimated: End of Q3**  
⚫ Paused  
Security Pod  
**Highlights:** We paused this to focus on Internal CA work, bastion monitoring, and responses to incidents/abuse.  

#### **Insider Risk** 

**Estimated: End of Q3**  
⚫ Paused  
Security Pod  
**Highlights:** We paused this to focus on Internal CA work, bastion monitoring, and responses to incidents/abuse. 

## **Learnings**

### **🔥 Incidents** Read more about Incidents & our Post Mortem process here

Incidents are opportunities to learn\! Recent incidents are listed below; we also include a brief summary of our findings (root causes, improvements we are making to the system as a result of these incidents, \&c), as well as links to incident debriefs/summaries and to our weekly operational health decks.

**Recent Incidents**

* INC-150 \- A trunkd deploy seems to have caused a thundering herd failure mode, resulting in trunkd crashlooping \- [Eric Weinstein](mailto:ericw@tailscale.com)  
* INC-151 \- App Connectors hit Auto Approval rate limits \- [Rhea Ghosh](mailto:rhea@tailscale.com)  
* INC-152 \- Shards with large tailnets (6 and 10\) were showing unusually long map batch run times, but only occasionally (debrief/summary) \- [Eric Weinstein](mailto:ericw@tailscale.com)  
* INC-157 \- A ramp-up experiment to migrate AuthPathDetails lookup from SQLite to DynamoDB introduced a `–1` sentinel value other parts of the code weren't expecting. This prevented a subset of users from logging into Tailscale until the experiment was stopped (debrief/summary) \- [Eric Weinstein](mailto:ericw@tailscale.com)  
* INC-159 \- During a control deploy on October 3rd, shard 1 experienced a slow increase in nodecop latency and eventual failures, seemingly as a result of a memory leak (debrief/summary) \- [Eric Weinstein](mailto:ericw@tailscale.com)

**Summary of Causes, Trends, and Remediations**

Many of these incidents were caused by deployments, unforeseen consequences of code changes, or difficulty operating the system manually. A theme the Platform team has begun to raise is that “our ability to operate the system must be more automated” (which would help mitigate deployment failures, shard provisioning and rebalancing, and help make experimentation safer). To that end, we will review a range of immediate options (as well as for Q4FY26 and beyond) to help prevent incidents of this nature from recurring, including adjustments/improvements to our deploy process, building out process and automation to make shard provisioning, scaling, resizing, and rebalancing easier, and reducing accidental complexity in the system in order to make it easier for engineers to evolve the codebase and make changes to the system safer. We look forward to sharing those improvements in future newsletters\!

**Links to Production Operational Health Decks**

The below decks comprise summaries of operational health on a weekly basis, including shard availability, node rejoin latency, DERP uptime, and more (including recaps of recent incidents and alerts).

* Week Beginning 01 September  
* Week Beginning 08 September  
* Week Beginning 15 September  
* Week Beginning 22 September  
* Week Beginning 29 September

### **🔍 Research** Read more about Research here and in UXR FY26 Plan

* CI/CD Use Cases and Market Study \- [Kabir Sikand](mailto:kabir@tailscale.com)  
* Services Usage Dashboard \- [Kabir Sikand](mailto:kabir@tailscale.com)  
* Database access \+ recording project plans \- [Samuel Jinadu](mailto:samuel@tailscale.com)

###  	**🔍Current UX Research**

* 🟢On track. Oct 17, 2025 | CI/CD Use Case Research | Survey to understand use cases, motivations, and tooling in customers’ CI/CD workloads | [Kabir Sikand](mailto:kabir@tailscale.com), [Arvind Venkataramani](mailto:arvind@tailscale.com)  
* 🟢On track. Oct 31, 2025 | Admin experience research, phase 1  | Interviews with business tailnet admins to uncover problems and unmet needs | [Arvind Venkataramani](mailto:arvind@tailscale.com)

	**Completed UX Research**

* In-product feedback forms are being shipped to enable users to give continuous and rich feedback  
* [https://www.tailscale.com/feedback](https://www.tailscale.com/feedback) now points to a public-facing feedback page

**🎥 Demos**  
Access our demo archive

* MCP 101 | [Remy Guercio](mailto:remy@tailscale.com) | Sep 3, 2025  
* Amplitude Demo: Data Ingestion & Product Analysis | Growth Pod | Sep 9, 2025  
* 🔜MacOS Windowed UI | Client Pod | Oct 14, 2025

### **🧑‍💼 Customer Highlights** 

\[Removed\]

### **🎨 Product Design**

* Process  
  * We’re opening up a new Product Designer role. View the job posting  
  * Collaboration on the front-end library (via Storybook). Now lives in its own repo. The process to ensure Admin Console components are now linked to the repo begins\!  
* Design/UX big picture  
  * “Policy fragments” feature has spawned new discussions about how to help users understand the ACL architecture better through UI changes.  
  * Self-serve IdP switches are up next. Aiming to take a load off support.   
    

## **Resources** Still want more?

* 2025 Product Roadmap  
* All Information Jira  
* EPD Jira Plans  
* EPD Q1 FY 26 Recap   
* EPD Q2 FY 26 Recap   
* EPD Team Q3 FY26 Plan Recap   
* EPD Q3 Project Mid Quarter Check \- in

[image1]: <data:image/png;base64,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>