# ADR 0003: Enforce guardrails with Azure Policy before workload deployment

- **Status:** Accepted
- **Date:** 2026-11-12
- **Context:** Azure enterprise landing zone for AI (reference architecture)

## Context

Landing-zone standards can be published as documentation, as Terraform or Bicep reviews, or as Azure Policy. Documentation alone is not enforced. Code review catches some drift but not resources created in the portal.

## Decision

Encode the following as Azure Policy initiatives assigned at the landing-zone management group, with a deny or deploy-if-not-exists effect where the built-in definition supports it:

- Allowed regions.
- Public network access disabled on OpenAI, storage, and Key Vault.
- Required diagnostic settings to the central Log Analytics workspace.
- Required tags: `env`, `cost-center`, `workload`.
- Allowed SKUs for firewall, Databricks, and storage.

Sandbox subscriptions use audit-only effects so experimentation is not blocked, but reports still surface violations.

## Consequences

- Non-compliant resources fail early, before data is loaded.
- Policy exceptions need a named owner and a review date.
- Platform engineers must test policy changes in a canary subscription to avoid blocking legitimate deployments.
