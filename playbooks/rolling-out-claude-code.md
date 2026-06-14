---
last_reviewed: 2026-06-14
audience: EMs and platform leads
confidence: medium
---

# Playbook: rolling out Claude Code at a 50-200 engineer firm

The playbook covers the operating decisions for introducing Claude Code as a substrate runtime at a firm in the 50-200 engineer band. It does not cover the tool's features. The features are documented at [`docs.anthropic.com/en/docs/claude-code`](https://docs.anthropic.com/en/docs/claude-code); read those once, then come back here.

## When to use the playbook

Use it when the rollout is intended to reach more than two squads and there is at least one regulated workload involved. Single-squad pilots can ignore most of the structure below; the structure is what holds the rollout together when it grows past the original pilot.

## What you need before you start

- A named executive sponsor. The rollout will hit two or three contested decisions; the sponsor's job is to resolve them quickly. Without one, the rollout stalls in the second month.
- A platform-engineering point of contact. Claude Code's value rises sharply when CLAUDE.md files are authored, MCP servers are wired in, and the firm's tooling integrates cleanly. The platform engineer is the one who does that work.
- A risk-and-compliance partner. The rollout produces a lot of audit-shaped questions; having the partner involved from week one is cheaper than introducing them in month three.
- A measurement plan. Section §5 of [`AIDLC.md`](../AIDLC.md) covers the metrics. Decide before week one which numbers you will report and to whom.

## The phases of the rollout

The rollout is four phases: pilot, expansion, steady state, and review. Each has a duration, a success criterion, and a refusal list. The refusal list matters as much as the success criterion; what you decline to do is what protects the rollout.

### Phase 1: Pilot (weeks 1-4)

**Goal.** One squad uses Claude Code on a non-regulated workload. The squad reports per-squad uplift numbers at week four using the methodology in §5. The reported numbers are honest, not impressive.

**Investment.** One CLAUDE.md authored for the squad's primary repository. One MCP server for the firm's internal documentation, if one exists. One pre-commit hook that runs the firm's existing checks against agent-generated code without exceptions. One quarterly retro slot to discuss what is and is not working.

**Refusal list.** Do not roll out across more than one squad. Do not measure anything that requires more than two weeks of data. Do not promise productivity numbers to the sponsor. Do not exempt the squad from the firm's existing code-review standards.

**Decision at the end of the phase.** Go, no-go, or extend. Going means the next phase starts on week five with a second squad joining. No-going means the pilot stops and the firm waits six months before trying again with different inputs. Extending means another four weeks of pilot with the same squad and the same measurement; extending more than once is a no-go.

### Phase 2: Expansion (weeks 5-12)

**Goal.** Three to five squads, including at least one regulated workload, run Claude Code under the same operating model. The per-squad uplift numbers stabilise enough to be reported quarterly. The governance overlay from §4 is wired in for the regulated workload.

**Investment.** A CLAUDE.md per repository. Two or three MCP servers for the firm's internal systems (issue tracking, internal docs, the canonical metrics dashboard). The `agentic-harness` primitives wired in for the regulated workload, with a hash-chained audit log feeding into the firm's existing observability stack. A small ADR library that records the contested decisions and their resolutions.

**Refusal list.** Do not expand to more than five squads. Do not allow squads to opt out of the harness on regulated workloads. Do not let the sponsor's enthusiasm push the rollout past the squads that have asked to be in it. Do not consolidate the rollout to a single CLAUDE.md template at this stage; the variation is the data.

**Decision at the end of the phase.** Go to steady state, contract back to pilot, or pause. Going means the rollout becomes a default option for new squads. Contracting means one or two squads identified specific issues that need addressing before further expansion; the right move is to address them and re-expand in a quarter. Pausing means the measurement is ambiguous; honest pausing is a sign of operator discipline, not failure.

### Phase 3: Steady state (months 4-12)

**Goal.** Claude Code is one of two default substrates for new squads. The squads that opted in during expansion continue to use it. The measurement is quarterly. The governance overlay is part of the firm's audit cycle.

**Investment.** A platform-engineering on-call for the rollout: someone who answers the questions squads have, maintains the CLAUDE.md templates, and updates the MCP servers as the firm's internal systems change. A quarterly cost-and-uplift report to the executive sponsor.

**Refusal list.** Do not promote the rollout as a productivity miracle in internal communications. The squads producing the data will know if the framing is inflated, and the trust loss is expensive. Do not make Claude Code a hiring requirement. Do not push squads that explicitly decline to adopt it.

**Decision points.** Quarterly review of the per-squad uplift numbers, the cost trajectory, and the audit-trail completeness. Substrate substitution (e.g. switching a squad from Claude Code to Cursor) should be reported as a normal operational decision, not as a failure. The substrate-agnostic stance from §3 is the policy.

### Phase 4: Review (annually)

**Goal.** A written assessment of the rollout's first year, with a recommendation to continue, expand, or replace. The assessment is honest about the costs and the gains.

**Investment.** Two weeks of platform-engineering time and one week of risk-partner time. A retrospective with the participating squads.

**Refusal list.** Do not write the assessment in a way that pre-decides the recommendation. Do not let vendor account managers contribute to the writing. Do not let the executive sponsor read the draft before the platform team and the risk partner have signed off.

## Common pitfalls

- **The over-CLAUDE.md problem.** Squads add rules to their CLAUDE.md files faster than they remove obsolete ones. By month six the file is three thousand lines and nobody reads it. The mitigation is a quarterly audit with a remove-first bias; rules that no longer fire on any run are removed.
- **The MCP-server-rot problem.** MCP servers get added during enthusiasm phases and atrophy after. The mitigation is a named owner per MCP server; servers without owners get removed.
- **The audit-trail-as-afterthought problem.** Squads instrument the audit trail late, then discover that important events were not recorded. The mitigation is to wire `agentic-harness` in at phase 2, before the workload depends on the audit data.
- **The single-CLAUDE.md-for-the-firm problem.** Centralised template authoring kills the variation that makes the operating model honest. The mitigation is per-squad ownership of the file, with a small shared subset for cross-cutting concerns.

## What success looks like at year one

The firm is using Claude Code on five to fifteen squads under stable operating-model practice. Per-squad uplift is reported quarterly with confidence ranges. The audit chain for regulated workloads is complete and inspectable. The squads that declined to adopt remain on whichever substrate suits their workload. The executive sponsor can describe the rollout's costs and benefits without using the word "transformative".

The rollout has not produced a productivity miracle. It has produced a measurable shift in the engineering organisation's working shape, the cost of which the firm can defend to its finance partner and the audit trail of which the firm can defend to its regulator. That is what success looks like at this scale.
