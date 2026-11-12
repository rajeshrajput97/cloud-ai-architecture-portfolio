# ADR 0001: Adopt a hub-and-spoke network rather than a single shared VNet

- **Status:** Accepted
- **Date:** 2026-11-12
- **Context:** Azure enterprise landing zone for AI (reference architecture)

## Context

AI, data, and connectivity services can be placed in one large Virtual Network or separated into a hub and workload spokes. A single network is simpler to start. It also makes it hard to isolate production from experimentation, to inspect egress in one place, and to give different teams ownership of their address space.

## Decision

Use a hub-and-spoke topology:

- The hub holds Azure Firewall, Private DNS zone links, optional ExpressRoute or VPN gateways, and Azure Bastion.
- An AI spoke holds Azure OpenAI, AI Foundry, and Key Vault private endpoints.
- A data spoke holds Databricks (VNet injection), ADLS Gen2, and Purview endpoints.
- Spokes peer only with the hub unless a specific east-west path is approved.

Virtual WAN is deferred until there are several regions or many spokes that justify a managed global backbone.

## Consequences

- Platform and workload teams can change their spokes without sharing a single route table.
- Egress and hybrid connectivity are centralised, which adds a hop and a firewall cost.
- Address space must be planned early so Databricks delegations and private-endpoint subnets fit without overlap.
