# ADR 0001: Use Delta Lake as the shared table format

- **Status:** Accepted
- **Date:** 2026-11-12
- **Context:** Multi-cloud lakehouse with Databricks and Microsoft Fabric (reference architecture)

## Context

The lakehouse can store data as CSV or Parquet files, as Apache Iceberg or Apache Hudi tables, or as Delta Lake tables. Fabric and Databricks both have their preferred defaults. A mixed format estate makes time travel, schema enforcement, and interoperability harder.

## Decision

Use Delta Lake as the default table format for bronze, silver, and gold products that Databricks writes. Where a Fabric warehouse or an AWS service requires a different format, publish a derived product rather than changing the system of record.

Iceberg may be introduced later for a specific interchange, but it is not the default in this reference.

## Consequences

- ACID writes, schema evolution, and time travel are consistent for platform pipelines.
- Some non-Databricks engines will need a shortcut, a copy, or a connector.
- The platform team must version Delta features carefully so readers in Fabric and in the second cloud stay compatible.
