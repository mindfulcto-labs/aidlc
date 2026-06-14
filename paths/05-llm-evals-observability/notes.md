---
last_reviewed: 2026-06-14
---

# Path 5: notes

## Why the path looks the way it does

The eval category is mature enough that two strong opinionated voices (Hamel, Eugene) and two strong libraries (Ragas, DeepEval) carry the load at the 30-minute and 3-hour tiers. The 30-hour exercise binds eval to observability and to the audit trail, which is the operator-grade synthesis the field is converging toward.

The path is intentionally Python-first. The Rust angle for evaluation does not pay off; the workload is network-bound on LLM calls, not CPU-bound, so the Rust ecosystem's strengths do not bite. The Rust angle in the wider portfolio is the gateway and the runtime enforcer, not the eval harness. The `rag-bench-rs` repository covers the Rust angle for systems benchmarks, which is a different exercise.

## Resources considered but not included

- Promptfoo. Mature, useful, included in `awesome-ai-governance`. Excluded from the main entries to keep the slot count tight; the docs reward a quick read if you have time.
- Garak. Adversarial-evaluation tool; valuable for red-teaming but a different workload from production-quality eval. Considering a future slot.
- Vendor observability product docs (Datadog AI Observability, New Relic AI Monitoring). Excluded for the vendor-tilt drift the wider repo avoids.

## Open questions

- Whether to add an entry on AI red-teaming and adversarial evaluation. The topic is real; the question is whether it belongs in this path or in a separate one. Current leaning: stay one path until the eval-and-red-team distinction matters more to readers than the unified shape does.
- Whether to add an entry on the OpenLLMetry semantic conventions. The standard is settling; once it lands at a stable version it deserves a slot.
