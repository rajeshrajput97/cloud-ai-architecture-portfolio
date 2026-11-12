# ADR 0003: Prefer CDC for rapidly changing operational sources

- **Status:** Accepted
- **Date:** 2026-11-12
- **Context:** AWS data platform migration (reference architecture)

## Context

Operational databases can be extracted with nightly full dumps, with incremental watermark queries, or with log-based change data capture (CDC). Full dumps are simple and stress source systems. Watermarks miss updates and deletes unless they are carefully designed.

## Decision

Use log-based CDC (for example AWS DMS or an equivalent) for operational sources that change frequently or that need nearer-to-real-time silver tables. Use batch extracts for static or slowly changing reference data, and for sources that cannot offer a safe CDC endpoint.

## Consequences

- The platform can keep silver tables current without nightly full-load windows.
- CDC requires source-system permissions, monitoring for delayed slots or tasks, and a plan for schema change.
- Replay and late-arriving data must be handled in silver merge logic.
