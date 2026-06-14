---
last_reviewed: 2026-06-14
---

# Path 4: AI gateway architecture

The reading order for a platform or staff-plus engineer who has been asked to put a gateway in front of the firm's AI traffic. Routing, rate limiting, key management, observability, PII redaction, prompt-injection defence, audit emission.

## Audience

Platform engineers, staff engineers, Heads of Platform. Anyone whose remit includes "all calls to a large language model from inside the firm should go through this one thing".

## Tiers

- **[30 minutes](./30-minutes.md)**: Cloudflare AI Gateway docs intro + Kong AI Gateway pages.
- **[3 hours](./3-hours.md)**: Portkey + Helicone + TensorZero architecture posts + read the LiteLLM source.
- **[30 hours](./30-hours.md)**: Build a gateway on `apiloom` + read `apiloom-ce` source.
- **[Notes](./notes.md)**: why the path looks the way it does, vendor inclusion rationale, open questions.

## What this path is not

A vendor product comparison. The category consolidates and re-shuffles faster than any path can stay current. The substrate-shape framing (what a gateway needs to do) lasts longer than which product currently does it best.

A single-language tutorial. The Python and Go implementations both have lessons. The Rust counterpart is part of the wider portfolio; see `sentinel-rs` when it ships.
