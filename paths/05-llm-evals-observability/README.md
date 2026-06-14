---
last_reviewed: 2026-06-14
confidence: medium
---

# Path 5: LLM evals and observability

The reading order for a Machine Learning engineer or SRE who needs to evaluate LLM-powered systems honestly and observe them in production. Covers the shape of evaluation that survives a regulator, the shape of observability that does not bankrupt the budget, and the audit-trail pattern that ties both back to the governance overlay in `AIDLC.md` §4.

## Audience

ML engineers running LLM systems in production. SREs supporting LLM-powered services. Platform engineers building eval suites that will eventually become part of CI. Engineering managers responsible for the productivity case that justified the spend.

## 30 minutes

- *(in progress)* Hamel Husain's "Your AI product needs evals". The post is short, opinionated, and works as a brief for anyone who has not internalised that LLM systems require their own evaluation discipline.
- *(in progress)* Eugene Yan's "LLM evaluation patterns". The Yan piece is the closest the field has to a vocabulary reference; reading it alongside Husain gives you both the why and the how.

## 3 hours

- *(in progress)* The Ragas documentation, cover to cover. Ragas is the most mature open-source RAG evaluation library, and reading its docs end-to-end teaches you what evaluating a retrieval system actually looks like.
- *(in progress)* The DeepEval documentation, same treatment. DeepEval and Ragas overlap; the differences in framing are themselves instructive.

## 30 hours

- *(in progress)* Chip Huyen's *AI Engineering* (O'Reilly 2025), the evaluation chapters. The book is the most rigorous published treatment of the production-AI shape.
- *(in progress)* Instrument one production agent with Langfuse and a custom Ragas suite, tied to MLflow for lifecycle tracking. The 30-hour run is: pick one agent or LLM-powered service, wire it up, run the evals on a schedule, and feed the results into the audit trail. The integration point with the audit chain is documented in `compliance-as-code` and `agentic-harness`.

## Notes

Evals are network-bound, not CPU-bound. That is why the field stayed Python and why the path's tooling recommendations are Python-first. The Rust angle in the broader portfolio is the gateway and the runtime enforcer, not the eval harness.

The audit-trail link is the bridge between this path and Path 2. Evals run in CI become evidence; the evidence chains via the harness; the chain satisfies ISO 42001 A.6.2.5 and EU AI Act Article 15. The path's 30-hour exercise is the place where the conceptual link becomes operational.
