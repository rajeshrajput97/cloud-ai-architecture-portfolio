# Cloud and AI Architecture Portfolio

Reference architectures and architecture decision records (ADRs) for enterprise cloud and AI platforms. The material is **illustrative**. It describes patterns I use when designing Azure, Databricks, Microsoft Fabric, AWS, and GenAI estates. It is not a record of named client engagements, and it does not claim production metrics.

The five case studies below can be read independently. Together they cover platform landing zones, multi-cloud data, GenAI governance, agentic AI, and data-platform migration.

[![Markdown Lint](https://github.com/rajeshrajput97/cloud-ai-architecture-portfolio/actions/workflows/lint.yml/badge.svg)](https://github.com/rajeshrajput97/cloud-ai-architecture-portfolio/actions/workflows/lint.yml)

## Case studies

| # | Case study | What it covers |
| --- | --- | --- |
| 1 | [Azure enterprise landing zone for AI](case-studies/01-azure-enterprise-landing-zone-for-ai/README.md) | Hub-and-spoke foundation for Azure OpenAI, AI Foundry, Databricks, and ADLS, with policy, identity, and private networking |
| 2 | [Multi-cloud lakehouse with Databricks and Fabric](case-studies/02-multicloud-lakehouse-databricks-fabric/README.md) | A shared lakehouse across Azure and another cloud, with Unity Catalog, OneLake, and a single governance plane |
| 3 | [Enterprise GenAI platform with governance and LLMOps](case-studies/03-enterprise-genai-platform-governance/README.md) | Model gateway, RAG, content safety, prompt and evaluation lifecycle, and cost controls |
| 4 | [Agentic AI on Azure AI Foundry](case-studies/04-agentic-ai-azure-ai-foundry/README.md) | Planner/executor agents, tool hosting, identity, observability, and human approval paths |
| 5 | [AWS data platform migration](case-studies/05-aws-data-platform-migration/README.md) | Phased move from a legacy warehouse or Hadoop estate to a governed AWS data platform |

Each case study follows the same structure: problem statement, requirements, a mermaid architecture diagram, component choices, ADRs, and security, cost, and NFR notes.

## How to use this repository

- Start with the landing zone if you need the platform foundation, then read the GenAI or agentic studies for workload patterns.
- Treat every ADR as a starting point for a design review, not as a mandatory standard.
- Pair this portfolio with the runnable samples in [enterprise-rag-azure](https://github.com/rajeshrajput97/enterprise-rag-azure), [databricks-medallion-lakehouse](https://github.com/rajeshrajput97/databricks-medallion-lakehouse), [agentic-ai-orchestrator](https://github.com/rajeshrajput97/agentic-ai-orchestrator), and the Terraform modules in [terraform-azure-ai-platform](https://github.com/rajeshrajput97/terraform-azure-ai-platform).

## Quality checks

Markdown is linted with `markdownlint` in GitHub Actions on every push and pull request:

```bash
npm install -g markdownlint-cli
markdownlint "**/*.md"
```

## License

MIT © 2026 Rajesh Kumar Rajput
