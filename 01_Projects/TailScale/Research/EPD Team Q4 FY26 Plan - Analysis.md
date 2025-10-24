---
created: 2025-10-24
updated: 2025-10-24
tags: [tailscale, analysis, planning]
status: complete
project: TailScale
source: EPD Team Q4 FY26 Plan.csv
---

# Tailscale Q4 FY26 EPD Team Plan Analysis

Analysis of the EPD Team's Q4 FY26 roadmap based on the CSV data.

## Executive Summary

- **Total Items Analyzed**: 58 items (excluding empty rows)
- **Product-Driven**: 40 items (69%)
- **Engineering-Driven**: 6 items (10%)
- **Unspecified Source**: 12 items (21%)
- **Committed Items**: 18 items with "Yes" commit status
- **High Priority (P0)**: 15 items (26%)

## 1. Product vs Engineering Source

### Distribution
- **Product**: 40 items (69% of specified items)
- **Engineering**: 6 items (10% of specified items)
- **Unspecified**: 12 items (21%)

### Analysis
The roadmap is heavily product-driven, with nearly 7x more product-sourced initiatives than engineering-sourced ones. This suggests:
- Strong product market feedback driving the roadmap
- Engineering initiatives likely focused on technical debt, scale, and reliability
- Potential gap: Engineering-driven innovation may be under-represented

### Engineering-Driven Items
1. DerpOps (ongoing) - Data plane, P0
2. Packet filter V2 - Enterprise, P0
3. Tailnet lock scalability - Enterprise, P3
4. Go client modularity - GM, P0
5. Continued work on control scalability - Platform, P0
6. Automated testing - Tooling/Clients, P0

**Notable**: All engineering items are either P0 (critical) or P3 (low priority), with nothing in between. This suggests engineering is focused on essential infrastructure OR nice-to-have improvements.

## 2. Priority Distribution

### Overall Breakdown
- **P0 (Critical)**: 15 items (26%)
- **P1 (High)**: 13 items (22%)
- **P2 (Medium)**: 20 items (34%)
- **P3 (Low)**: 6 items (10%)
- **Unspecified**: 4 items (8%)

### Observations
- Over 1/4 of the roadmap is P0 (critical priority)
- P2 dominates with 34% of items - healthy balance of important work
- Relatively few P3 items, suggesting focus on high-impact work

## 3. Commit Status Analysis

### Distribution
- **Yes (Committed)**: 18 items (31%)
- **No**: 14 items (24%)
- **Stretch**: 1 item (2%)
- **Unspecified**: 25 items (43%)

### Committed Items by Team
- **Identity**: 5 commits (28% of all commits)
- **DevEx**: 3 commits
- **Data plane**: 3 commits
- **Clients**: 2 commits
- **Enterprise**: 2 commits
- **Kubernetes**: 2 commits
- **Networking**: 1 commit

### Analysis
Identity team has an unusually high number of committed items (5), representing 28% of all commits. This suggests:
- Identity is a critical focus area for Q4
- Possible scaling/reliability issues being addressed
- Strategic priority on authentication and access control

The Data plane and DevEx teams also show strong commitment patterns with 3 items each.

## 4. Team Workload Analysis

### Items by Team
- **Networking**: 10 items (most loaded)
- **DevEx**: 9 items
- **Identity**: 8 items
- **Enterprise**: 6 items
- **Clients**: 7 items
- **Data plane**: 5 items
- **Platform**: 5 items
- **GM**: 4 items
- **Kubernetes**: 3 items
- **Billing**: 1 item
- **Security**: 3 empty rows (no details)
- **Tooling, Clients**: 1 item

### P0 Items by Team
- **DevEx**: 3 P0 items
- **Data plane**: 3 P0 items
- **GM**: 2 P0 items
- **Identity**: 2 P0 items
- **Networking**: 1 P0 item
- **Platform**: 2 P0 items
- **Tooling/Clients**: 1 P0 item
- **Enterprise**: 1 P0 item

### Red Flags
1. **DevEx team**: 3 P0 items out of 9 total (33% critical) - highest P0 concentration
2. **Data plane team**: 3 P0 items out of 5 total (60% critical) - very high-pressure quarter
3. **Networking team**: 10 items total but only 1 P0 - potentially overloaded with P2/P3 work
4. **Security team**: 3 placeholder rows with no details - planning incomplete?

## 5. Documentation Status by PM

### Documentation Completion Analysis

**Driver: Kabir Sikand** (14 items)
- Problem docs: 3 done, 8 not started, 1 in progress, 2 N/A
- 1-pagers: 2 done, 9 not started, 1 in progress, 2 N/A
- **Completion Rate**: 21% (problem docs), 14% (1-pagers)
- **Red Flag**: Managing 14 items with very low doc completion

**Driver: Megan Walsh** (11 items)
- Problem docs: 1 ready for review, 10 N/A
- 1-pagers: 1 not started, 10 N/A
- **Completion Rate**: Most items marked N/A (likely later stage work)
- **Status**: Documentation not applicable for most items

**Driver: Sam Linville** (8 items)
- Problem docs: 2 done, 4 not started, 2 N/A
- 1-pagers: 2 done, 4 not started, 2 N/A
- **Completion Rate**: 33% (problem docs), 33% (1-pagers)
- **Status**: Behind on documentation for half the portfolio

**Driver: Samuel Jinadu** (4 items)
- Problem docs: 2 not started, 2 N/A
- 1-pagers: 2 not started, 2 N/A
- **Completion Rate**: 0% (no docs completed yet)
- **Status**: Early in planning cycle

**Driver: Andrew Mitchell** (4 items)
- Problem docs: 1 in progress, 3 N/A
- 1-pagers: 1 in progress, 3 N/A
- **Completion Rate**: N/A items dominate (infrastructure work)

### PM Documentation Red Flags

1. **Kabir Sikand**: Highest workload (14 items) with lowest doc completion rate (14-21%). This PM is at risk of being overwhelmed.

2. **Samuel Jinadu**: 0% completion on documentation, though only 4 items managed. May be early in cycle or behind schedule.

3. **General Pattern**: Many items marked "coming soon" or "low priority" for project docs, suggesting documentation debt across the organization.

## 6. Stage Distribution

### Current Stage Breakdown
- **N/A**: 16 items (28%) - mostly infrastructure/KTLO work
- **Alpha**: 6 items (10%)
- **Beta**: 8 items (14%)
- **GA**: 9 items (16%)
- **POC**: 3 items (5%)
- **Design doc**: 1 item (2%)
- **Unspecified**: 15 items (26%)

### Analysis
- Healthy pipeline with work across all stages
- Large N/A category suggests significant operational/infrastructure work
- 26% unspecified stages - planning may be incomplete

## 7. Strategic Alignment Distribution

- **Core VPN**: 22 items (47% of specified)
- **Tailscale as a Platform**: 17 items (36%)
- **Scale and reliability**: 6 items (13%)
- **Personal user virality**: 2 items (4%)

### Insights
- Strong focus on Core VPN improvements (nearly half the roadmap)
- Platform strategy is significant (36% of work)
- Scale/reliability is 13% - reasonable for a growth stage company
- Personal virality is underinvested (only 2 items)

## Key Recommendations

1. **Kabir Sikand's workload**: Consider redistributing some of the 14 items or providing PM support
2. **Data plane team pressure**: 60% P0 items - monitor for burnout risk
3. **Security team planning**: Complete the 3 empty security rows
4. **Documentation debt**: Accelerate problem doc and 1-pager completion, especially for committed P0 items
5. **Engineering innovation**: Consider increasing engineering-driven initiatives beyond infrastructure
6. **Personal virality**: Only 2 items - may be underinvested if user growth is a goal

## Notable Patterns

- **Identity team momentum**: 5 committed items suggests major identity infrastructure work
- **Services architecture**: Multiple "Services" items across teams - significant new capability being built
- **Client parity work**: Ongoing Windows/macOS parity efforts (technical debt)
- **Self-serve operations**: Multiple self-serve features (domain verification, IdP changes) - reducing support burden
