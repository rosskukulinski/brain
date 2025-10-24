---
created: 2025-10-24
updated: 2025-10-24
source: https://tailscale.com/blog/2021-06-taildrop-was-easy
tags: [tailscale, taildrop, performance, file-transfer, peer-to-peer, benchmarks, wireguard]
status: complete
project: TailScale
---

# Taildrop Performance Analysis

## Overview

Taildrop is Tailscale's peer-to-peer file transfer feature that exemplifies their "New Internet" vision. Rather than providing raw speed benchmarks, Tailscale emphasizes architectural advantages that eliminate cloud overhead.

## File Size Capabilities

- **No file size limits** - Architecture supports unlimited file sizes
- **Verified:** User successfully transferred 3GB file from MacBook to iPhone
- No artificial constraints or quotas

## Transfer Architecture

### Point-to-Point Design
- Direct peer-to-peer transfer over encrypted Tailscale network
- Uses "your bandwidth (mostly LAN bandwidth), not ours"
- When devices are on same LAN: essentially LAN-speed transfers
- No intermediate cloud storage or relay (except when NAT traversal requires DERP)

### Performance Claims
From "The New Internet" blog post:
- "We do it all without adding any latency or overhead"
- Single HTTP PUT operation
- No multi-minute deploy times
- No log delays
- Immediate transfer initiation

## Technical Implementation

### Simplicity
- Core feature: HTTP PUT request handler
- Development time: "a few hours at most"
- Unauthenticated layer atop Tailscale's existing authentication
- No additional encryption overhead (relies on Tailscale's WireGuard encryption)
- Uses NAT traversal for peer discovery and session negotiation

### Infrastructure Efficiency
- "It costs us, effectively, nothing to run"
- Zero server infrastructure required
- No cloud egress fees
- No storage costs
- No database, message queues, or regional load balancers needed

## Comparison to Cloud-Based File Transfer

### Traditional Cloud Services (Dropbox, Google Drive, Firefox Send, etc.)
**Overhead includes:**
- Upload to cloud → storage → download from cloud
- Network egress fees
- Storage costs and retention policies
- Server CPU time
- Database management
- Message queues
- Regional load balancers
- DNS management
- TLS certificate handling
- Encryption key exchange
- Push notification systems (for multiple platforms)

### Taildrop Advantages
- Direct peer-to-peer (even when "side by side on the same wifi")
- No intermediate storage
- No cloud infrastructure overhead
- No encryption key exchange needed (Tailscale handles identity)
- No push notifications needed (devices have persistent peer status)

## Actual Performance Data from User Reports

### GitHub Issue #4949 (2022)
**Reported speeds - Windows 11, PC to PC transfers:**
- **Version 1.24.2 (optimal):** 300 Mbps - "maxing out my connection"
- **Version 1.26.1 (degraded):** 50-150 Mbps - inconsistent and fluctuating
- **Performance regression:** ~50% speed reduction in later version
- **Status:** Issue resolved as of January 2023

### Community Reports
**Positive experiences:**
- Nevada to Connecticut transfers during CES: "worked as smoothly across that distance as within the same room"
- Files sent "uncompressed" (unlike WhatsApp which compresses)

**Limitations noted:**
- No transfer speed display in UI (progress bar only)
- Occasional caching issues on Android (alpha feature quirk)
- Can only send to yourself, not to other users nearby (unlike AirDrop)

### Comparison to AirDrop
**Taildrop advantages:**
- Cross-platform: Android, iOS, macOS, Windows
- No proximity requirement
- No Bluetooth requirement
- Works over any network (same LAN or across Internet)

**AirDrop advantages:**
- Handles URLs/links elegantly (opens in browser automatically)
- Can send to anyone nearby, not just yourself
- More mature feature (not alpha)

## Underlying Tailscale/WireGuard Performance

Since Taildrop runs over Tailscale's WireGuard network, these benchmarks indicate maximum possible throughput:

### Tailscale Throughput Benchmarks (2024)

**Bare Metal Linux (i5-12400 with 25Gb/s NICs):**
- wireguard-go optimized: **13.0 Gbps**
- wireguard-go baseline: 8.36 Gbps
- In-kernel WireGuard: 11.8 Gbps

**AWS Cloud (c6i.8xlarge):**
- wireguard-go optimized: **7.32 Gbps**
- wireguard-go baseline: 5.34 Gbps
- Network limit caps performance ~7.3 Gbps

**Legacy Hardware (2012 E3-1230-V2):**
- With optimizations: **6.59 Gbps**
- Baseline: 3.36 Gbps
- Improvement: nearly 2x increase

**Gigabit Networks (Independent Testing, 2024):**
- Tailscale via Netgear hub: **817 Mbps** (vs 941 Mbps raw, 902 Mbps WireGuard)
- Netmaker: 7.88 Gbps on bare metal
- Kernel WireGuard: 7.89 Gbps on bare metal
- Tailscale bare metal: 5.25 Gbps (but frequently fell back to slower routing)

### Performance Factors

**Platform differences:**
- Linux with kernel WireGuard: Best performance
- Userspace WireGuard (most platforms): More overhead
- Linux 6.2+ with Tailscale 1.54+: UDP transport layer offloads for 4x improvement

**Optimization requirements:**
- Direct connections: "nearly always result in lower latency and higher throughput"
- UDP Generic Segmentation/Receive Offload (GSO/GRO)
- Higher CPU clock speed more important than core count
- AWS EC2: Use cluster placement groups for >5 Gbps single-flow

## What's Still Missing: Taildrop-Specific Metrics

### Not Documented (as of 2025-10-24)
- Official Taildrop throughput benchmarks from Tailscale
- Latency measurements for file transfer initiation
- Side-by-side speed comparisons with:
  - AirDrop (on same LAN)
  - Dropbox/Google Drive/OneDrive
  - WeTransfer
  - SFTP over Tailscale
- Transfer success rates and reliability statistics
- DERP relay performance impact when direct connection unavailable
- Performance by file size (small vs large files)
- Impact of concurrent transfers
- Mobile platform performance (iOS/Android) vs desktop

## Use Case: The Conceptual Win

Avery Pennarun's argument is about **eliminating unnecessary complexity** rather than raw speed:

> "Transferring files — one of the first things people did on the Internet, for no extra charge, via FTP — now has to cost money, because somebody has got to pay that rent. With Taildrop, it doesn't cost money. Not because we're generously draining our bank accounts to make file transfers free. It's because the cost overhead is gone altogether."

## Key Insight

The performance advantage isn't "X% faster" but rather:
- **Zero artificial throttling** (cloud services often rate-limit)
- **Zero metering** (no upload/download quotas)
- **LAN speeds when possible** (direct connection on same network)
- **Removes centralization penalty** (no round-trip through cloud servers)

## Questions for Further Research

1. What are actual measured transfer speeds in various scenarios?
   - Same LAN
   - Different networks (direct WireGuard connection)
   - Via DERP relay
2. How does it compare to AirDrop on same network?
3. What percentage of transfers require DERP relay vs direct connection?
4. Are there practical file size limits based on memory/disk constraints?
5. What happens when transfer is interrupted?

## Summary: Expected Taildrop Performance

Based on available data:

**Best case (optimal conditions):**
- Same LAN, modern hardware, direct connection: **Near-LAN speeds**
- Properly configured systems: **300+ Mbps to multi-Gbps** (limited by network hardware)
- Linux 6.2+ with optimizations: **Up to 13 Gbps** on high-end hardware

**Typical case (consumer use):**
- Cross-internet transfers: **50-300 Mbps** depending on configuration
- Standard consumer hardware: **100-800 Mbps range** on gigabit networks
- No artificial throttling or file size limits

**Factors that impact performance:**
- Operating system (Linux > others)
- Direct vs DERP relay connection
- Hardware capabilities (CPU, network interface)
- Tailscale version (1.54+ recommended)
- Kernel version (Linux 6.2+ optimal)
- Network configuration and firewall rules

## Sources

### Official Tailscale Documentation
- [The New Internet](https://tailscale.com/blog/new-internet) - Avery Pennarun, 2024-07-26
- [Taildrop was easy to implement](https://tailscale.com/blog/2021-06-taildrop-was-easy) - 2021-06
- [Surpassing 10Gb/s with Tailscale](https://tailscale.com/blog/more-throughput) - Performance benchmarks
- [Performance best practices](https://tailscale.com/kb/1320/performance-best-practices) - Optimization guide

### Community Reports
- [GitHub Issue #4949](https://github.com/tailscale/tailscale/issues/4949) - Taildrop speed regression (2022)
- Various user reports from blog posts and community discussions

### Independent Testing
- Netmaker VPN speed tests (2024) - Third-party WireGuard/Tailscale benchmarks
