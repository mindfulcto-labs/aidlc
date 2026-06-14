---
last_reviewed: 2026-06-14
---

# Path 3: notes

## Why the path looks the way it does

Agentic AI literature ranges from research papers (deep, low operator yield) to vendor product blogs (high vendor yield, no operator portability). The path threads the middle by combining one short opinionated piece (Anthropic), one durable taxonomy (Weng), one mature framework (LangGraph), and one book that handles the whole production shape (Huyen). The harness exercise grounds the theory in a real workload.

The path deliberately does not include framework-comparison content. Those comparisons are vendor-shaped and revise every quarter. The harness exercise is framework-agnostic by construction.

## Resources considered but not included

- The OpenAgents, MetaGPT, BabyAGI, AutoGPT line of repositories. Excluded because the field moves too quickly. Weng's piece covers the underlying shapes.
- Vendor "build your own agent" tutorials. The operator perspective starts where the vendor framing ends.
- A dedicated multi-agent entry. Multi-agent shapes are an extension of single-agent primitives; reading the basics first means multi-agent literature parses cleanly.

## Open questions

- Whether to add a security-flavoured entry on prompt-injection defence in agent contexts. Topic is real; current leaning is that it belongs in Path 4 (gateway), because the operator answer is to put the defence at the gateway boundary, not inside the agent.
- Whether to add a maintenance-cost entry on agent-fleet operations. The cost-runaway failure mode hints at this; operator-grade treatment has not been published yet.
