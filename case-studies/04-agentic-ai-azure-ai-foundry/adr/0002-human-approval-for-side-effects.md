# ADR 0002: Require human approval for side-effecting tools

- **Status:** Accepted
- **Date:** 2026-11-12
- **Context:** Agentic AI on Azure AI Foundry (reference architecture)

## Context

Agents are most useful when they can take action, not only retrieve information. Automatic actions on business systems or outbound messages carry operational and compliance risk, especially under prompt injection.

## Decision

Every tool is classified as read-only or side-effecting. Side-effecting tools (create, update, delete, payments, messages leaving the organisation) require a human approval step before execution, unless a use-case record explicitly allows a narrow, idempotent action with documented compensating controls.

Approvals show the user the tool name, arguments, and why the planner selected the step. Rejections stop the run or force a re-plan; they do not skip to the next side-effecting call.

## Consequences

- High-impact automation is slower, which is acceptable for the risk it avoids.
- Approval user experience and timeout handling become part of the platform.
- Read-only tools can still run automatically, so many research-style goals stay interactive.
