---
last_reviewed: 2026-06-14
tier: 30-hours
---

# Path 3, 30-hour tier: agentic AI engineering

The book and the project.

## 1. Chip Huyen, *AI Engineering* (O'Reilly, 2025), agents chapters

The most rigorous published treatment of the production-AI shape as of 2026. Read the agents-and-tools chapters specifically. Huyen's framing of agentic systems as multi-component pipelines with explicit failure-mode budgets is the closest published view to the operating model in `AIDLC.md`.

If you only buy one AI engineering book this year, this is the one. The agents chapters alone justify the price.

Why this slot: the book threads eval, observability, and agentic patterns at the depth a production operator needs. Earlier and concurrent books cover pieces; this one threads them.

## 2. Build one agent against `agentic-harness`

[`github.com/mindfulcto-labs/agentic-harness`](https://github.com/mindfulcto-labs/agentic-harness)

Pick a workflow your team does manually (procurement triage, ticket classification, contract clause extraction, on-call runbook triage). Build a small agent on `agentic-harness` that does the work under autonomy budgets, blast-radius classification, and hash-chained audit trails.

The harness ships a procurement-triage example as a starting point. The 30-hour exercise is to replace it with your own domain. The replacement work teaches you four things the reading list cannot: where the budgets bite, where the policy gate refuses your good intentions, what the audit chain looks like in production, and how much trust you actually want to extend to the agent on day one.

Why this slot: the artefact is also the natural credential when you are explaining the work to a hiring panel.
