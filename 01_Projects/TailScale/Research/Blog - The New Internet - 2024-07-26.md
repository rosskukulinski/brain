---
created: 2025-10-24
source: https://tailscale.com/blog/new-internet
author: Avery Pennarun
published: 2024-07-26
tags: [tailscale, networking, distributed-systems, infrastructure, vision]
status: complete
project: TailScale
---

# Summary

Tailscale CEO Avery Pennarun presents a compelling vision for decentralizing the internet by removing the connectivity barriers that force reliance on cloud providers. The core argument: modern development complexity stems not from computational challenges but from networking limitations—firewalls, NATs, and dynamic IPs prevent devices from being true peers. Tailscale aims to give every device static addresses, certificates, and peer status, enabling direct device-to-device communication. This shift could eliminate unnecessary cloud intermediaries (like using AWS to transfer files between devices in the same room), reduce infrastructure overhead, and enable new application architectures. Success requires near-universal adoption, which they're pursuing through free consumer plans coupled with enterprise revenue. Pennarun positions this as part of a historical pendulum swing from mainframes to PCs to cloud, now back to distributed computing—but with the connectivity guarantees that were previously exclusive to centralized providers.

---

# The New Internet: Tailscale's Vision for the Future of Connectivity

**Author:** Avery Pennarun (CEO and Co-founder)
**Published:** July 26, 2024
**Category:** Insights

---

## Overview

Pennarun explores how Tailscale aims to reshape internet connectivity by addressing fundamental problems in modern software development. He argues that excessive complexity in today's tech stack stems from architectural decisions made decades ago.

## Key Sections

### The Problem with Scaling

Developers routinely over-engineer for scale before it's needed. As Pennarun notes, many teams use sophisticated tools like Kubernetes for workloads requiring "0.2 requests per second"—work a smartphone could handle. This obsession with scalability creates unnecessary overhead through lengthy build processes, container orchestration, and deployment delays.

### The Internet's Core Issue

The real bottleneck isn't computation—it's connectivity. Firewalls, NATs, and dynamic IP addresses force developers toward centralized cloud providers. Individual devices cannot reliably serve as peers, necessitating intermediaries like AWS.

### Why AWS Dominates

Cloud providers control the economic rent in tech because they possess what individual machines lack: static IP addresses, DNS names, TLS certificates, and open ports. Home computers remain locked behind network barriers despite superior hardware capabilities.

### The New Internet

Tailscale's solution grants every device certificates, addresses, and peer status while maintaining security. This enables direct device-to-device communication, eliminating unnecessary cloud intermediaries for many applications.

### Taildrop Example

Their file-sharing feature demonstrates this principle. Before Tailscale, transferring files between nearby devices required uploading to cloud storage, paying egress fees, and managing encryption keys. With Tailscale's peer-to-peer model, it becomes a simple HTTP operation.

### Universal Adoption Imperative

The technology requires near-universal adoption to fulfill its potential. Currently, roughly 1 in 20,000 people globally use Tailscale. Their business strategy—offering free plans while pushing enterprise adoption—addresses this chicken-and-egg problem.

### Historical Parallels

Pennarun draws parallels to previous technological shifts: IBM mainframes gave way to Microsoft's distributed PCs, which were replaced by cloud's recentralization. He argues we're now positioned for another pendulum swing toward distributed computing.

---

## Core Vision

Removing networking complexity enables developers to focus on actual problems rather than infrastructure overhead. When connectivity becomes seamless and peer-based, entirely new applications become feasible—ones impossible in centralized architectures.