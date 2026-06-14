---
last_reviewed: 2026-06-14
confidence: medium
---

# Path 3: Agentic AI engineering

The reading order for an engineer building agentic systems that survive contact with production and regulators. Covers harness design, autonomy bounding, audit-trail patterns, and the orchestration choices that pay off for the next two years.

## Audience

Engineers and senior engineers who are building or maintaining AI agents in production. Platform engineers wrapping agent frameworks in firm-specific harnesses. Anyone whose responsibilities include "the agent did the wrong thing" incidents.

## 30 minutes

- *(in progress)* Anthropic's "Building effective agents" (December 2024). Short, opinionated, and grounded in what production patterns actually look like. The piece is the right anchor because it refuses the agent-framework hype while still being practical.
- *(in progress)* The LangGraph quickstart, end to end. Pick LangGraph over LangChain for this introduction because the state-machine framing is closer to what production work demands than the chain-and-callback shape.

## 3 hours

- *(in progress)* Lilian Weng's "LLM-powered autonomous agents". The piece is from mid-2023 and the surface vocabulary has moved on, but the taxonomy underneath has held up better than most newer attempts.
- *(in progress)* Read the multi-agent examples in the LangGraph repository. The examples illustrate what the framework is honest about and what it abstracts away, both of which matter for choosing where the firm-specific harness sits.

## 30 hours

- *(in progress)* Chip Huyen's *AI Engineering* (O'Reilly, 2025), specifically the chapters on agents and evaluation. The book is the most rigorous treatment of the production-AI shape published to date.
- *(in progress)* Build one agent against [`agentic-harness`](https://github.com/mindfulcto-labs/agentic-harness), wiring autonomy budgets, blast-radius classification, and the hash-chained audit log into a real workflow. The harness ships a procurement-triage example as a starting point. The 30-hour exercise is to replace the example with your own domain.

## Notes

Agent work has two failure modes the path explicitly addresses: agents that are too cautious to do anything useful, and agents that take destructive actions the team did not anticipate. The harness primitives in the linked repo are designed against the second; the orchestration choices in this path are designed against the first.

The path deliberately avoids vendor-specific agent platforms (vendor-X-agents, vendor-Y-agents). The frameworks change too fast for a long-form learning path to keep up; the primitives do not.
