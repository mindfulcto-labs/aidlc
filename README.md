# aidlc

The operator's manual for AI-supported software development. Tool-agnostic. Governance-first. Measured per squad.

This repository contains two things that travel together:

1. **[`AIDLC.md`](AIDLC.md)** — a manifesto. One long-form document that lays out the operating model behind AI-supported engineering at 50-500 engineer scale, written from the operator's seat rather than the vendor's. Extends, does not replace, the Amazon framing in `awslabs/aidlc-workflows`.
2. **[`paths/`](paths/)** — five opinionated reading orders for the topics the manifesto leans on. Two resources per subtopic. 30-minute, 3-hour, and 30-hour tiers. The pattern is Ozzie Smith's `TeachYourselfCS` applied to AI-supported engineering.

The two products belong in one repo because they answer the same question from two angles. The manifesto says *here is how the work is shaped*. The paths say *here is how to learn the work*. Splitting them would create the kind of cross-repo navigation tax that pretends to be a feature.

## Three reading orders

Pick whichever lines up with how you arrived:

- **You are an EM or principal engineer wondering how to roll Claude Code or Cursor out at your firm.** Start with [`AIDLC.md`](AIDLC.md) §§1-3, then [`paths/01-ai-supported-engineering`](paths/01-ai-supported-engineering/), then [`playbooks/rolling-out-claude-code.md`](playbooks/rolling-out-claude-code.md) when v0.2 ships.
- **You are a Director or VP under regulatory pressure (EU AI Act, ISO 42001, DORA, NIS2) and you need to make AI-augmented engineering audit-ready.** Read [`AIDLC.md`](AIDLC.md) §4 first when v0.2 ships, then [`paths/02-ai-governance`](paths/02-ai-governance/).
- **You are an engineer who wants to build agentic systems that survive contact with production and regulators.** Read [`paths/03-agentic-ai`](paths/03-agentic-ai/), then the sibling repo [`agentic-harness`](https://github.com/mindfulcto-labs/agentic-harness).

## What this is not

This is not vendor-comparison content. The substrate table in `AIDLC.md` §3 is workload-shape oriented, not feature-checklist oriented. Vendors change quarterly; the operating model has to outlive them.

This is not legal advice. The governance overlay in §4 maps to ISO 42001 Annex A, EU AI Act Articles 9-15, NIST AI RMF, and the UK AI Cyber Code of Practice. The mappings are written to be auditable by an internal audit team; an external auditor or counsel reviewing for actual compliance is still required.

This is not a Dunnhumby internal document. No firm-specific codenames, no proprietary metric values, no client names. Operator examples are anonymised. Where a number appears, it is given as a range and the methodology behind the range is stated.

## How this is maintained

One named maintainer (Venkat). Five paths is the hard ceiling. Adding a sixth requires removing one. Quarterly review with `last_reviewed` front-matter on every path. `CHANGELOG.md` records both additions and removals. Silent rot signals abandonment; visible removals signal taste.

## License

Documentation: [Creative Commons BY-SA 4.0](LICENSE-CC-BY-SA-4.0). Code samples and scripts: [Apache License 2.0](LICENSE).

## Companion repositories

- [`agentic-harness`](https://github.com/mindfulcto-labs/agentic-harness) — runtime primitives the operating model depends on.
- [`compliance-as-code`](https://github.com/mindfulcto-labs/compliance-as-code) — the schema and AIBOM emitter referenced in `AIDLC.md` §4.
- [`awesome-ai-governance`](https://github.com/mindfulcto-labs/awesome-ai-governance) — the broader tool registry.
- [`engineering-standards`](https://github.com/mindfulcto-labs/engineering-standards) — phase-by-phase standards and checklists that operationalise the manifesto. (Ships in week 6.)

## Versioning

`AIDLC.md` carries `Last revised: YYYY-MM-DD` at the top. Substantive revisions update that date and add an entry to `CHANGELOG.md`. The repo is not a code library; it does not need semantic versioning, and pretending otherwise would invite the wrong kind of comparison.
