# ADR 0001: Migrate by product slices with a dual-run gate

- **Status:** Accepted
- **Date:** 2026-11-12
- **Context:** AWS data platform migration (reference architecture)

## Context

A legacy warehouse can be migrated in a single cutover, by freezing change and rebuilding everything, or in slices (a mart, a report family, or a source system) with a period of dual-run and reconciliation. A single cutover looks shorter on a plan and concentrates risk into one weekend.

## Decision

Migrate in product slices. For each slice:

1. Ingest the required sources into S3 and build silver/gold products on AWS.
2. Run the legacy and AWS outputs in parallel for an agreed window.
3. Reconcile grain, totals, and a defined set of control queries against documented tolerances.
4. Cut consumers over only when the gate is met, then retire the legacy jobs for that slice.

A programme-level big-bang is rejected unless a slice is genuinely inseparable.

## Consequences

- The programme takes longer but each cutover is reversible and evidenced.
- Reconciliation tooling and a control board are mandatory, not optional.
- Some shared dimensions must be migrated early because many slices depend on them.
