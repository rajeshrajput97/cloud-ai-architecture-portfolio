# ADR 0003: Enforce access in Unity Catalog and publish into Purview

- **Status:** Accepted
- **Date:** 2026-11-12
- **Context:** Multi-cloud lakehouse with Databricks and Microsoft Fabric (reference architecture)

## Context

Access can be enforced in storage IAM, in Databricks legacy table ACLs, in Unity Catalog, in Fabric workspaces, or only documented in an enterprise catalogue. Multiple enforcement points drift. A catalogue without enforcement becomes a brochure.

## Decision

- Unity Catalog is the enforcement point for Databricks tables, views, volumes, and external locations.
- Grants are issued to Entra ID groups, not to individuals, except for break-glass accounts.
- Microsoft Purview is the enterprise catalogue and glossary. It receives lineage and classification from Unity Catalog and Fabric; it does not replace Unity Catalog grants.
- Fabric workspace roles are aligned with the same groups, but they must not be the only control on a sensitive gold product.

## Consequences

- Engineers have one place to request table access.
- Integration work is required to keep Purview in step with Unity Catalog.
- Products consumed only inside Fabric still need a classification and an owner in Purview.
