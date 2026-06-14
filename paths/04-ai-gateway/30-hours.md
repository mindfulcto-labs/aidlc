---
last_reviewed: 2026-06-14
tier: 30-hours
---

# Path 4, 30-hour tier: AI gateway architecture

The project is the curriculum. No published book covers the category end-to-end yet.

## 1. Build a small AI gateway on `apiloom`

[`github.com/mindfulcto-labs/apiloom`](https://github.com/mindfulcto-labs/apiloom)

Stand up `apiloom` (Go-based open-source API platform) as the underlying gateway. Bolt on AI-specific concerns: multi-provider routing, PII redaction, prompt-injection scanning, audit-trail emission, per-team cost attribution. Use the `compliance-as-code` schema for the audit-trail shape. Use the `agentic-harness` audit log format for the chain.

You produce a working gateway that handles real traffic and a written architecture decision record explaining the trade-offs you took. The ADR is the artefact you show a hiring panel; the gateway is the artefact your team uses.

Why this slot: no current book covers the AI-gateway category end-to-end. The exercise is the only way to internalise the trade-offs.

## 2. Read the Apiloom community edition source

[`github.com/mindfulcto-labs/apiloom-ce`](https://github.com/mindfulcto-labs/apiloom-ce)

The community edition is the smaller, focused Go implementation. Reading the source teaches the gateway shape from the inside. Pay particular attention to the policy engine, the routing layer, and the observability hooks.

Why this slot: reading one mature gateway implementation in source is the cheapest way to understand what every other gateway in the category is doing. The community edition is small enough that the exercise fits in the 30-hour window.
