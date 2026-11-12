# ADR 0003: Register tools with schemas, owners, and least-privilege identities

- **Status:** Accepted
- **Date:** 2026-11-12
- **Context:** Agentic AI on Azure AI Foundry (reference architecture)

## Context

Tools can be ad-hoc functions in a notebook, or they can be a versioned catalogue with a schema, an owner, and an identity. Ad-hoc tools ship faster and are difficult to audit or to reuse safely.

## Decision

A tool is production-ready only when it is registered with:

- A stable name and semantic version.
- An input schema the executor validates before dispatch.
- A named owner and a support path.
- A classification (read-only or side-effecting).
- A least-privilege identity; credentials come from Key Vault or managed identity, never from the prompt.

Unknown tool names are rejected. Catalogue changes follow the same review path as application code.

## Consequences

- Onboarding a new tool is slower than pasting a function into a notebook.
- Several use cases can share well-reviewed tools (retrieval, ticketing, knowledge lookup).
- Security reviews have a complete list of actions an agent could take.
