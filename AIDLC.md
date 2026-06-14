# AIDLC

The operator's manual for AI-supported software development. Tool-agnostic. Governance-first. Measured per squad.

*Author: Venkat Ramachandran. Last revised: 14 June 2026. Confidence: medium on §§1-3 (operator-tested), exploratory on §§4-5 (drafts pending v0.2).*

---

## 1. Why this exists, and what Amazon left out

In April 2025 a group at Amazon Web Services published `awslabs/aidlc-workflows` and named a thing the rest of the industry had been doing without a name. The repo gathered the shape of AI-supported software work into three phases: Inception, Construction, Operations. The Builder's Library followed with the longer essay. Both deserved the attention they got. AWS pulled the term forward and the vocabulary stuck.

This repo is not a replacement for that work. It extends it.

The Amazon framing is a toolchain framing. It is written from the position of the company that sells the tools, and it is honest about that. The framing is generous about what the tools can do, and it is mostly silent on the questions a Director or VP has to answer the morning a regulator asks how the AI is making decisions, who is accountable for them, and what the evidence chain looks like. The toolchain is necessary. It is not sufficient.

What I want to add is the operating-model layer. The substrate that makes the toolchain work inside a real engineering org under regulatory pressure. The measurement model that survives contact with a CFO who already paid for the licences and wants the productivity numbers. The governance overlay that lines up the squad's daily practice with the ISO 42001 audit trail. The failure modes that no vendor blog will tell you about because telling you would cost the vendor the next renewal.

The short version: Amazon ships the toolchain. This document is the operating model. They are two halves of the same conversation.

Two notes on how to read what follows. First, every claim is something I have either done, seen done, or governed. Where I am speaking from one operator's vantage point and the next operator's would differ, I say so. Second, the document is written to be acted on. There are no architecture diagrams in v0.1. There is a substrate table in §3 that you can copy into a planning doc tomorrow morning, and there is a measurement model in §5 you can hand to a sceptical finance partner. If you want diagrams, v0.2 will add them.

## 2. The three phases, restated for operators

I keep Amazon's three phases. The vocabulary is too good to throw away and there is nothing in the operator perspective that requires breaking the names. What I want to do is re-anchor each phase on the decision the engineering manager actually has to make, not on the tool that helps them make it.

**Inception.** This is the phase where you decide what the squad is building and how it intends to know whether the build worked. The Amazon framing focuses on spec authoring, often with a Claude or Q-Developer assistant, generating user stories and test scaffolding. That is correct and useful. The decision the EM is making, though, is older and harder: which problems does this squad take on, and which problems does it explicitly decline. The right Inception output is not a spec. The right Inception output is a refusal list. A spec follows easily when the team is clear on what it is not doing. Vendor tools help write the spec; they do not help write the refusal list, and that is where most squads lose their first six months on AI-augmented work.

The question Inception forces the EM to answer: *what does this squad refuse to do, and why?*

**Construction.** This is the phase where code is written. The Amazon framing leans heavily on tool selection, autonomy ceiling, and review cadence. I agree on every count. What I want to add is that the squad's Construction phase needs a steady-state honest answer to one question that Amazon does not press hard on: *who owns the artefact when the AI substantially generated it?* The answer is almost always the human reviewer, but it has to be said out loud and the squad has to have practised saying it. The first time the question gets asked in an incident review is the wrong time.

Construction also includes the second-order work the toolchain quietly creates: hook authoring, agent prompt maintenance, eval suite upkeep, configuration drift. These are not free. A squad that does AI-supported Construction at scale will spend ten to twenty percent of its capacity on the meta-work of keeping the tools usable, and that capacity has to come from somewhere. Pretending it does not exist is the most common Year One mistake.

The question Construction forces the EM to answer: *what fraction of the squad's capacity is going into the meta-work of the tools, and is it dropping or rising?*

**Operations.** This is the phase where the system runs in production. The Amazon framing here is the thinnest of the three, partly because AWS sells production tooling separately and partly because most of what is interesting in AI Operations is not toolchain. It is incident response shape, model drift detection, rollback semantics, evals-as-production-checks, and the audit trail you generate as a by-product of running the system at all.

I want to push hard on the last item. The audit trail is not extra work. It is the by-product of a system that records what it did, in what order, on whose instructions, with what blast radius. If you instrument the system right at Construction time, Operations produces the audit trail for free. If you wait until your first regulator visit to start instrumenting, you will pay for the audit trail twice: once in retroactive instrumentation, once in regulator goodwill burned.

The question Operations forces the EM to answer: *if a regulator walked in tomorrow, what would I show them, and how long would it take to put my hands on it?*

## 3. The tool-agnostic substrate

Amazon's framing has a quiet selection bias toward Q Developer and Bedrock. This is reasonable; AWS pays the bill. The operating model has to work across the five substrate runtimes a real UK or EU engineering org will actually use over the next three years. The table below sketches the differences at a level that fits in a planning meeting. It is not a vendor comparison. It is a workload-shape comparison.

| Substrate | Workload shape it suits | Autonomy ceiling | Audit posture | Cost profile | Squad archetype |
|---|---|---|---|---|---|
| Claude Code | Long-context refactors, agentic loops over a known codebase, IDE-adjacent work | High when the squad has invested in CLAUDE.md and per-repo rules; low when it has not | Strong: full session logs available; integrates cleanly with corporate observability | Token-priced, predictable on plans, less predictable on agent loops | Greenfield product squads; brownfield platform squads with strong code-base hygiene |
| Cursor | Inline completion + chat + composer over an open IDE, fast feedback | Medium; the IDE-bound shape limits how far the model can drift unsupervised | Moderate: edits are reviewable in the IDE, but the prompt history is harder to lift | Subscription-priced, predictable | Application squads; squads with junior majorities; squads valuing speed-of-iteration |
| Windsurf | Cascade flows, multi-file edits, longer-horizon agentic work in an IDE | High in Cascade mode; medium otherwise | Moderate; Cascade traces are better than the inline equivalents | Subscription, sometimes ambiguous on heavy use | Squads where the EM wants more agentic work than Cursor encourages |
| GitHub Copilot | Inline completion, PR summaries, deep GitHub integration | Low to medium; the design is intentionally cautious | Strong on the GitHub-integrated paths; weaker on out-of-band uses | Subscription, often pre-paid by the firm | Every squad that already lives on GitHub; the low-friction default |
| Codex (OpenAI) | Cloud-side agentic work, parallel runs, long horizons | High in cloud agents; the runtime hides the actual call shape | Mixed; depends on the integration the squad ships | Token-priced; cloud agents add per-run overhead | Squads with strong eng-platform support that can wrap Codex behind their own observability |

Two things to read from the table. First, none of the five is the right answer for every squad. The honest planning move is to pick two as the default substrate and let squads opt into the others with a stated reason. The opt-in record becomes its own evidence trail for the governance overlay in §4.

Second, the autonomy ceiling column matters more than the cost column. Cost differences between the five substrates are real but small at firm scale. Autonomy ceiling differences are the difference between a squad that can ship a fully agentic deployment workflow and one that is still doing line-by-line review. Plan around the ceiling, not the bill.

A selection heuristic that works in practice:

- **Greenfield product** with a small senior team: Claude Code as primary, Cursor for the IDE shortcuts when needed.
- **Brownfield platform** with strong code hygiene: Claude Code as primary, GitHub Copilot for the GitHub-native paths.
- **Regulated data** workloads: GitHub Copilot for the conservatism, plus a sandbox copy of Claude Code for exploratory work that does not touch production data.
- **Infra and SRE** squads: Codex cloud agents for the multi-step ops work, plus the squad's preferred IDE assistant for everyday tasks.

These are heuristics, not rules. A good EM will revise them quarterly as the substrate runtimes themselves evolve.

What the operating model deliberately refuses to do is pick a winner. The vendor landscape is moving fast enough that any winner-pick in v0.1 of this document will look quaint by v0.2. The substrate-agnostic stance is the whole point of the operating model: the EM is investing in a way of working that survives the next vendor reshuffle.

---

*Sections 4-9 in progress. v0.2 ships §§4-5 (Governance overlay, Measurement model). v0.3 ships §6 (Cognitive debt). Failure modes (§7) and "what I am not claiming" (§8) anchor the v0.2 release.*
