# ADR 0003: Make evaluation a blocking release gate

- **Status:** Accepted
- **Date:** 2026-11-12
- **Context:** Enterprise GenAI platform with governance and LLMOps (reference architecture)

## Context

Prompt and model changes are often released after a manual demo. Demos do not catch regressions in groundedness, toxicity, or cost, and they do not scale to several use cases.

## Decision

A production promotion of a prompt, retrieval configuration, or model deployment requires an evaluation report on a versioned golden set. The report includes at least groundedness or task accuracy (as appropriate), safety failures, and token cost versus the current production version. The promotion is blocked if agreed thresholds are missed, unless a named owner accepts a time-limited exception.

Online sampling continues after release so drift can be detected.

## Consequences

- Use-case teams must maintain a golden set, which is itself a reviewable artefact.
- Evaluation adds token cost and pipeline time to every release.
- Thresholds need periodic review so the gate stays strict without becoming immovable.
