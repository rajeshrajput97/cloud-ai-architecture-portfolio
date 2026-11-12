# ADR 0002: Require grounding and citations for enterprise question answering

- **Status:** Accepted
- **Date:** 2026-11-12
- **Context:** Enterprise GenAI platform with governance and LLMOps (reference architecture)

## Context

A chat model can answer from its training data, from a retrieved enterprise corpus, or from both. Ungrounded answers are fluent and hard to audit. For policy, handbook, or operational questions, that risk is usually unacceptable.

## Decision

Enterprise question-answering use cases must use a retrieval path and must ask the model to answer only from provided sources, returning citations. If retrieval returns nothing relevant, the application returns a "not found" style response rather than an ungrounded guess.

Open-ended writing or brainstorming use cases may opt out, but that choice is recorded at onboarding and is not the default.

## Consequences

- Index quality and access control become part of the product, not an optional extra.
- Some questions will correctly receive a refusal or a "not in corpus" answer.
- Evaluation must include groundedness and citation accuracy, not only fluency.
