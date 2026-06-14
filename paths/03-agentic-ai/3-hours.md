---
last_reviewed: 2026-06-14
tier: 3-hours
---

# Path 3, 3-hour tier: agentic AI engineering

Theory paired with reading-the-source practice.

## 1. Lilian Weng, "LLM-powered autonomous agents"

[`lilianweng.github.io/posts/2023-06-23-agent`](https://lilianweng.github.io/posts/2023-06-23-agent/)

Published mid-2023 and still the cleanest taxonomy of agentic architectures. Surface vocabulary has moved on; the underlying decomposition (planning, memory, tools, reflection) has held up. Read it against the Anthropic essay and the difference between research-shape framings and operator-shape framings becomes obvious.

Why this slot: the taxonomy is the vocabulary other people will use in design reviews. Knowing it cold is operator table stakes.

## 2. Read the LangGraph multi-agent examples

[`github.com/langchain-ai/langgraph/tree/main/examples`](https://github.com/langchain-ai/langgraph/tree/main/examples)

Specifically the multi-agent example notebooks. They illustrate what the framework is honest about (state machines, checkpoints, interrupts) and what it abstracts away (the control flow when several agents interact). Both matter for choosing where your firm-specific harness sits.

Why this slot: any framework you eventually pick will require you to write similar example code. Reading the canonical examples first means yours look like work, not like first attempts.
