---
last_reviewed: 2026-06-14
---

# Path 4: notes

## Why the path looks the way it does

The AI-gateway category is younger than the others and moves faster. The 30-hour project tier is the most stable element; vendor docs and product framings at the 30-minute and 3-hour tiers will revise as the category consolidates.

The path deliberately under-indexes on vendor product comparisons. The substrate-shape framing (what the gateway needs to do: routing, redaction, scanning, audit) lasts longer than which product currently does it best.

## Resources considered but not included

- The Bifrost (Datadog) AI gateway documentation. Too new at time of writing; revisited later.
- The vLLM Router documentation. Inference-server routing is a different category from cross-vendor gateway routing; conflating them confuses operators.
- Kong AI Gateway's deeper plugin-authoring docs. More useful at the 30-hour tier than at the 3-hour tier.

## Open questions

- Whether to add an entry on edge gateways (Fastly Compute, Cloudflare Workers) at the 3-hour tier. The deploy shape matters; the question is whether it belongs in this path or in a future path on edge AI.
- Whether the path should split between application-side (developer-facing) gateways and platform-side (infrastructure-facing) gateways. Current leaning: keep them together until the difference matters enough to readers to merit two paths.
