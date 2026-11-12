# ADR 0002: Make private endpoints the default for AI and data PaaS

- **Status:** Accepted
- **Date:** 2026-11-12
- **Context:** Azure enterprise landing zone for AI (reference architecture)

## Context

Azure OpenAI, storage, Key Vault, and Databricks can be reached over the public internet with firewall IP allow-lists, over service endpoints, or over Private Link. Public access is the fastest path for a prototype. It also expands the attack surface for prompts, embeddings, and lakehouse data.

## Decision

Disable public network access on Azure OpenAI, ADLS Gen2, Key Vault, and the Databricks workspace front end by default. Reach those services through private endpoints and Private DNS. Use service endpoints only as a temporary exception with an expiry date.

Databricks cluster traffic uses VNet injection (public and private delegated subnets) with no public IP on cluster nodes in production.

## Consequences

- Prompts, completions, and data-plane traffic stay on the private network.
- DNS must be designed carefully; split-horizon and on-premises resolvers need the same Private DNS zones.
- Some vendor SaaS tools that expect a public endpoint will need a documented exception or a self-hosted alternative.
