---
last_reviewed: 2026-06-14
tier: 3-hours
---

# Path 5, 3-hour tier: LLM evals and observability

The documentation read of the two mature open-source eval frameworks. Read both because the overlap and the disagreements are themselves instructive.

## 1. Ragas documentation, cover to cover

[`docs.ragas.io`](https://docs.ragas.io/)

Ragas is the most mature open-source RAG evaluation library. Reading the docs end-to-end teaches you what evaluating a retrieval system actually looks like in practice. Pay particular attention to `faithfulness`, `answer_relevancy`, and `context_precision`. The metrics are the working vocabulary of RAG quality.

Why this slot: Ragas is the de-facto reference for RAG evaluation. Even if your firm picks a different library, the Ragas vocabulary will appear in every comparison.

## 2. DeepEval documentation

[`docs.confident-ai.com`](https://docs.confident-ai.com/)

DeepEval is the pytest-shaped sibling to Ragas. The differences in framing are themselves instructive: Ragas focuses on metric definitions, DeepEval focuses on CI integration. Both are correct framings; the operator picks based on the shape of the team's existing pipeline.

Why this slot: reading both back-to-back is the cheapest way to internalise the trade-offs in the eval-tool category.
