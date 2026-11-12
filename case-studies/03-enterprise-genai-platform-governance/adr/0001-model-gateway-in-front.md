# ADR 0001: Place a model gateway in front of every production caller

- **Status:** Accepted
- **Date:** 2026-11-12
- **Context:** Enterprise GenAI platform with governance and LLMOps (reference architecture)

## Context

Applications can call Azure OpenAI (or another model host) directly with a resource key or managed identity, or they can call a shared gateway. Direct access is simpler. It also spreads keys, makes quota and safety policy inconsistent, and blocks a later model swap.

## Decision

Production and official internal copilots call a platform gateway only. The gateway is responsible for authentication, authorisation, per-use-case quota, content safety, model routing, and usage traces. Direct access to model resources is limited to the platform team and to tightly controlled break-glass procedures.

## Consequences

- Application teams take a stable HTTP contract rather than a vendor SDK as their production dependency.
- The gateway becomes a critical path and must be designed for availability and low added latency.
- Local development can use a stub or a development key with a non-production model, as in the companion RAG sample.
