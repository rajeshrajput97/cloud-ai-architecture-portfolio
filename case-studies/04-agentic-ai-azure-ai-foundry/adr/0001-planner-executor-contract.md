# ADR 0001: Keep a planner and executor contract even when using Foundry agents

- **Status:** Accepted
- **Date:** 2026-11-12
- **Context:** Agentic AI on Azure AI Foundry (reference architecture)

## Context

Azure AI Foundry can host managed agents that plan and call tools internally. A team could also write a fully custom orchestrator. Managed agents reduce operating work. A custom orchestrator is easier to inspect, test, and port. Hiding the plan entirely inside a vendor runtime makes evaluation and incident review harder.

## Decision

Adopt a planner/executor/tool-registry contract as the design standard, whether the runtime is Foundry-managed or self-hosted. A run must produce a stored plan, per-step observations, and a final answer. Foundry is the preferred host when it can honour that contract; a self-hosted executor is the fallback and the local test path.

## Consequences

- Use-case teams can test planning and tool dispatch offline, as in the companion orchestrator sample.
- Some managed features may be wrapped so that traces still flow to the platform observability store.
- Portability improves if a later project needs a different host, because tools stay behind a stable schema.
