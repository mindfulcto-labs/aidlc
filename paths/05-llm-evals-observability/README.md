---
last_reviewed: 2026-06-14
---

# Path 5: LLM evals and observability

The reading order for a Machine Learning engineer or SRE who needs to evaluate LLM-powered systems honestly and observe them in production. Evaluation that survives a regulator, observability that does not bankrupt the budget, audit-trail patterns that tie back to the governance overlay in `AIDLC.md` §4.

## Audience

ML engineers running LLM systems in production. SREs supporting LLM-powered services. Platform engineers building eval suites that will eventually become part of CI. EMs responsible for the productivity case that justified the spend.

## Tiers

- **[30 minutes](./30-minutes.md)**: Hamel Husain "Your AI product needs evals" + Eugene Yan "LLM evaluation patterns".
- **[3 hours](./3-hours.md)**: Ragas documentation cover-to-cover + DeepEval documentation.
- **[30 hours](./30-hours.md)**: Chip Huyen *AI Engineering* eval chapters + instrument one production agent with Langfuse + Ragas + MLflow.
- **[Notes](./notes.md)**: why the path looks the way it does, Rust-angle rationale, open questions.

## What this path is not

A model-comparison tutorial. Eval discipline is about your system, not about which underlying model is best. The path is model-agnostic.

A vendor observability product guide. Open-source defaults carry the path; vendor alternatives work but the operator should be able to defend the open-source baseline.
