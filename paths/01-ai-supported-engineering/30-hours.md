---
last_reviewed: 2026-06-14
tier: 30-hours
---

# Path 1, 30-hour tier: AI-supported engineering

The exercise tier. One project plus the document that codifies the decisions.

## 1. Stand up `agentic-harness` against one squad's actual workflow

[`github.com/mindfulcto-labs/agentic-harness`](https://github.com/mindfulcto-labs/agentic-harness)

The 30-hour run is operator practice, not reading practice. Pick one squad. Wire one Claude Code or Cursor or Codex session through the harness primitives: autonomy budgets, blast-radius classification, hash-chained audit log. Measure for two weeks. Decide what stays and what reverts to the unwrapped version.

The exercise teaches you two things no reading-list entry can: which primitives actually save you a regretted action, and which primitives are friction without payoff for your specific workload.

Why this slot: the harness is the reference implementation of the operating model. Running it on real work is the cheapest way to find out where the model is right and where it needs revision.

## 2. Author the squad's rollout document

The artefact you produce alongside the harness. Roughly 1500 words. Five sections:

1. Substrate decision (one of the five in `AIDLC.md` §3, with a stated reason).
2. Autonomy ceiling for the squad (per-PR, per-week, per-quarter).
3. Audit-trail destination (where the chain lands, who reads it).
4. Refusal list (the work this squad declines under AI augmentation).
5. Review cadence (when this document gets revised).

The document is the operating layer's contract. It is also the artefact you hand a new EM the day they take over the squad.

Why this slot: the harness gives the primitives, the document gives the levers. Writing both in the same 30-hour run is how the operating model goes from manifesto to practice.
