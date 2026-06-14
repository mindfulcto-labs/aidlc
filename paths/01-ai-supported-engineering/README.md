---
last_reviewed: 2026-06-14
confidence: medium
---

# Path 1: AI-supported engineering

The reading order for an engineering manager or senior engineer who wants to roll AI tooling out at a real firm. The path covers selection, the operating model around the tools, and the meta-work the tools quietly create. It does not cover vendor lock-in arguments, which the operator decides separately.

## Audience

EMs running 5-15 person squads. Senior and Staff engineers asked to lead an AI-tools rollout at the squad or guild level. Directors briefing their orgs in plain English without buying any specific vendor's framing.

## 30 minutes

Two short pieces that together set the operator perspective without the vendor noise.

- *(in progress)* The Anthropic Claude Code best-practices post, plus one outside critique that pushes back. Both should be cited together because the post is honest about its position and the critique fills the gaps. Annotation will name *why this pair* rather than either piece in isolation.
- *(in progress)* Will Larson's piece on engineering metrics under AI augmentation, when published. The placeholder until then is `themindfulcto.com`'s essay on per-squad uplift, which is the same shape from a different operator's seat.

## 3 hours

- *(in progress)* Read `awslabs/aidlc-workflows` end to end. It is the canonical framing this whole repo extends. Knowing the source primary matters before reading any second-order commentary.
- *(in progress)* Read one chapter of Will Larson's *An Elegant Puzzle* on engineering org design. The chapter sets the question the AI tooling is supposed to answer; without it the rollout decisions look smaller than they are.

## 30 hours

- *(in progress)* Stand up `agentic-harness` against one squad's actual workflow. The repo is at [github.com/mindfulcto-labs/agentic-harness](https://github.com/mindfulcto-labs/agentic-harness). The 30-hour run is: read the harness, wire one Claude Code or Cursor session into it, measure for two weeks, decide what stays and what reverts.
- *(in progress)* Author the squad-level rollout doc that codifies the decisions. The harness gives you the primitives; the rollout doc gives the EM the levers. The doc usually ends up about 1500 words, and the meta-work of keeping it current is part of the practice.

## Notes

The tier sizes are deliberately small. Two resources per tier, one for theory and one for practice. The temptation to add a third resource is the same temptation that produces unmaintainable awesome-lists. The pattern is borrowed from `TeachYourselfCS`.

The 30-hour tier asks for a project, not a book. Reading without shipping is the failure mode this whole document was written to avoid.
