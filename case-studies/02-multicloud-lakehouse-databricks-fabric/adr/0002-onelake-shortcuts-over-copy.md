# ADR 0002: Prefer OneLake shortcuts over default cross-cloud copy

- **Status:** Accepted
- **Date:** 2026-11-12
- **Context:** Multi-cloud lakehouse with Databricks and Microsoft Fabric (reference architecture)

## Context

Gold data can be copied into OneLake, or Fabric can reach ADLS or a supported external location through shortcuts. Copying simplifies performance and isolation. It also doubles storage and adds another pipeline that can drift.

## Decision

Default to OneLake shortcuts (or Databricks external locations) for gold products that Microsoft analysts need. Approve a physical copy only when at least one of the following is true:

- Query latency over the shortcut is unacceptable.
- Egress cost of repeated remote reads exceeds the cost of storage and a controlled refresh.
- A residency or contractual rule requires a copy in the Microsoft tenant.

## Consequences

- Most gold products have a single system of record.
- The platform team must observe shortcut performance and egress and be ready to promote a product to a copied pattern.
- Disaster-recovery plans must state whether a shortcut target is in the same failure domain as Fabric capacity.
