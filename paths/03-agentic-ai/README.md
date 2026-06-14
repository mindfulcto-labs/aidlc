---
last_reviewed: 2026-06-14
---

# Path 3: agentic AI engineering

The reading order for an engineer building agentic systems that survive contact with production and regulators. Harness design, autonomy bounding, audit-trail patterns, orchestration choices.

## Audience

Engineers and senior engineers building or maintaining AI agents in production. Platform engineers wrapping agent frameworks in firm-specific harnesses. Anyone whose responsibilities include "the agent did the wrong thing" incidents.

## Tiers

- **[30 minutes](./30-minutes.md)**: Anthropic "Building effective agents" + LangGraph quickstart.
- **[3 hours](./3-hours.md)**: Lilian Weng's "LLM-powered autonomous agents" + LangGraph multi-agent examples.
- **[30 hours](./30-hours.md)**: Chip Huyen *AI Engineering* agents chapters + build one agent on `agentic-harness`.
- **[Notes](./notes.md)**: why the path looks the way it does, framework-comparison rationale, open questions.

## What this path is not

A framework-comparison guide (LangGraph vs CrewAI vs AutoGen vs DSPy). Those comparisons revise every quarter. The harness exercise is framework-agnostic by construction.

A research catalogue. The taxonomy in Weng's piece covers the underlying shapes; chasing the latest paper rarely improves the operator's mental model faster than building the agent does.
