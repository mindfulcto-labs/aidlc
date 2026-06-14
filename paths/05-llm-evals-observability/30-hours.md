---
last_reviewed: 2026-06-14
tier: 30-hours
---

# Path 5, 30-hour tier: LLM evals and observability

The book and the production-grade instrumentation exercise.

## 1. Chip Huyen, *AI Engineering* (O'Reilly, 2025), eval chapters

The same book referenced in Path 3, different chapters. Huyen's treatment of evaluation is the most rigorous published account of the discipline as of 2026. Read the eval chapters with a notebook open; the exercises in the margins are worth doing.

Why this slot: the book threads evaluation, observability, and lifecycle in one narrative. No other published treatment covers all three at the operator depth.

## 2. Instrument one production agent with Langfuse plus Ragas plus MLflow

[`github.com/langfuse/langfuse`](https://github.com/langfuse/langfuse), [`github.com/explodinggradients/ragas`](https://github.com/explodinggradients/ragas), [`github.com/mlflow/mlflow`](https://github.com/mlflow/mlflow)

Pick one agent or LLM-powered service in your firm. Wire Langfuse for traces, Ragas for periodic quality evals on the trace data, and MLflow for lifecycle tracking of the prompt-and-model versions. Tie the eval results into the audit trail at `compliance-as-code` so the evidence chain is intact.

The integration point is the bridge to Path 2. Evals run in CI become evidence; the evidence chains via the harness; the chain satisfies ISO/IEC 42001 A.6.2.5 and EU AI Act Article 15. The 30-hour run is where the conceptual link becomes operational.

Why this slot: instrumenting one real service teaches more than reading three books on observability. The exercise produces an artefact you can show a regulator.
