# ADR 0002: Make S3 the system of record and treat the warehouse as a serving layer

- **Status:** Accepted
- **Date:** 2026-11-12
- **Context:** AWS data platform migration (reference architecture)

## Context

Teams sometimes load sources straight into Amazon Redshift (or another warehouse) and treat that warehouse as the only copy of the data. That repeats the legacy pattern: expensive storage for raw history, and no independent lake for science or reprocessing.

## Decision

Amazon S3 is the system of record for raw, cleaned, and product datasets. Redshift, Athena, or another engine is a serving layer on top of those datasets (via copy, Spectrum, or federation). History is not kept only inside the warehouse.

## Consequences

- Reprocessing and machine-learning access do not depend on warehouse CPU.
- Engineers must design table formats, partitions, and a catalogue on S3, not only warehouse DDL.
- Serving layers can be resized or even replaced without another source-system extraction.
