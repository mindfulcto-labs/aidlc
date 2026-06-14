# AIDLC

The operator's manual for AI-supported software development. Tool-agnostic. Governance-first. Measured per squad.

*Author: Venkat Ramachandran. Last revised: 14 June 2026.*

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

## 4. The governance overlay

The substrate runs through the engineering org. The governance overlay tells you what evidence the substrate has to produce for the firm to remain in regulatory good standing. This section maps ISO/IEC 42001 Annex A controls and EU AI Act Articles onto the three phases in §2, so an EM and a Risk partner can read the same document.

The first thing to say is that most of these obligations are evidence obligations, not policy-gate obligations. The control does not refuse a request at runtime; it requires that you can show, after the fact, that the request happened, who authorised it, and what consequences it had. The hash-chained audit log in [`agentic-harness`](https://github.com/mindfulcto-labs/agentic-harness) and the evidence schema in [`compliance-as-code`](https://github.com/mindfulcto-labs/compliance-as-code) are designed against this shape. A small minority of controls do gate at runtime (notably the EU AI Act Article 14 human-oversight obligations for high-risk systems), and those gates live in the substrate or in the gateway, not in the audit log.

The second thing to say is that the standards are written for the firm, not for the engineering team. They use the language of management systems, not the language of pull requests. Part of the operating-model work is the translation. Below is the operator-grade version.

**Inception phase.** The relevant ISO/IEC 42001 controls cluster in A.5 (assessing impacts of AI systems) and A.6.1 (management guidance for AI system development). The squad's refusal list (the question Inception forces the EM to answer in §2) is the artefact that satisfies A.5.1 (AI system impact assessment process) and A.5.4 (assessing societal impacts). Capture it in the repository, version-control it, and link it from the squad's onboarding doc. The EU AI Act parallel is Article 9 (risk management system), which the firm-level documentation usually owns; the squad's contribution is the inputs.

The single highest-yield Inception artefact is the data-source declaration: which datasets does this squad use, where did they come from, what licence and what classification. ISO/IEC 42001 A.7.4 (data provenance) wants this; EU AI Act Article 10 wants this; UK Caldicott principles want this. Producing it once, at Inception time, in a machine-readable shape, lets every downstream control satisfy itself by reference.

**Construction phase.** The relevant controls cluster in A.6.2 (AI system requirements through verification through operation). For the AI-augmented Construction shape, the load-bearing ones are A.6.2.5 (operation and monitoring), A.6.2.6 (technical documentation), and A.6.2.7 (event logs). EU AI Act Article 12 (record-keeping) and Article 15 (accuracy, robustness, cybersecurity) map onto the same artefacts.

The single highest-yield Construction artefact is the event log: every tool call, every model call, every decision the agent took, with timestamps and inputs. The harness in [`agentic-harness`](https://github.com/mindfulcto-labs/agentic-harness) emits this as a hash-chained Postgres table; the chain is verifiable by anyone with read access, without trusting the database administrator. Sites that want stronger guarantees can layer signing on top.

The second highest-yield Construction artefact is the eval suite. ISO/IEC 42001 A.6.2.3 (verification and validation) wants it; EU AI Act Article 15 wants quantitative robustness evidence; the squad's own engineering hygiene wants it. The eval suite should be CI-runnable, version-controlled, and re-runnable on any commit. Tying it into the audit chain at release time makes A.6.2.5 (monitoring) free.

**Operations phase.** The relevant controls cluster in A.6.2.5 (operation), A.8 (information for interested parties), and A.10 (third-party relationships). EU AI Act Article 14 (human oversight) and Article 13 (transparency) live here for deployer obligations.

The single highest-yield Operations artefact is the incident postmortem with AI-tooling-use noted. The postmortem is for the team; the AI-tooling-use field is for the audit trail. Postmortems also satisfy A.8.3 (communication of incidents), which several jurisdictions read narrowly.

The NIST AI RMF (GOVERN, MAP, MEASURE, MANAGE) is the connective tissue between the EU and US obligation sets. Sites operating multi-jurisdictionally use AI RMF as the shared vocabulary and the per-jurisdiction maps as the local translation.

A worked example. A squad ships a procurement-triage agent. Inception produces an impact assessment naming the supplier-data source and the in-scope decision boundaries. Construction produces an agent built on [`agentic-harness`](https://github.com/mindfulcto-labs/agentic-harness), with autonomy budgets, blast-radius policy, and a hash-chained audit log; an eval suite that runs nightly; and a CHANGELOG entry on every model upgrade. Operations produces a per-incident postmortem template that records whether the responder used agentic tooling. The whole chain ties to one entry in [`compliance-as-code`](https://github.com/mindfulcto-labs/compliance-as-code) per release, which generates the SPDX 3.0 AIBOM the firm files with internal audit. Eight ISO/IEC 42001 controls and four EU AI Act Articles are evidenced by the by-products of the work, not by extra work.

## 5. The measurement model

The DORA Four Keys (deployment frequency, lead time for changes, mean time to restore, change failure rate) are the canonical engineering productivity metrics. They are useful, they are widely adopted, and they break under AI augmentation.

Deployment frequency rises sharply because the agents ship small changes constantly. Lead time falls because the agents shorten the author-to-merge cycle. Both look like wins, and they often are wins. The two metrics that decide whether the rise was actually productive are change failure rate and the mean time to restore, and those two split into something more complicated than DORA captures.

The change failure rate splits by author. A change authored by an agent and reviewed by a human has a different failure profile from a change authored by a human and reviewed by a human. So does a change authored by an agent and reviewed by an agent. The squad needs a four-way matrix, not a single rate. Tracking it requires that the CI knows who (or what) authored the change and who reviewed it. The signal lives in the commit metadata; the harness records the agent contribution in the audit trail.

Mean time to restore splits between AI-augmented and AI-unaugmented incident response. The two are not the same shape. Agent-assisted debugging accelerates incident response in some patterns (large log sweeps, structured diff analysis) and slows it down in others (novel failure modes the agent has no priors on). The squad needs both numbers; the operator decides whether to use the harness in incident response based on the gap.

Beyond DORA, the AI-augmented squad needs three new metrics:

**AI-code-share.** The fraction of merged code authored substantially by an agent. The number is rising across the industry and the right way to report it is as a percentage range per squad, with the methodology disclosed. Honest measurement of this number is harder than it looks; the agent rarely writes a complete commit alone, and counting the lines under-counts the squad's actual leverage. The pragmatic approach is to track the commits where the human reviewer flagged that the agent did most of the work, and report the share quarterly with a confidence-band.

**Complexity-adjusted velocity.** Story points or shippable units delivered, adjusted for the cognitive complexity of the change. The adjustment matters because agents shorten the time on simple changes more than on complex ones, so raw velocity over-reports the gain. The simplest workable adjustment is a complexity weight per change set on a 1-to-5 scale; the EM applies the weight at review time.

**Escaped-defect rate per squad.** Defects discovered in production within thirty days of release. This is the metric that catches "the agent helped us ship faster, and we also shipped more bugs". The number should be reported alongside the deployment frequency increase, not separately; pretending they are independent invites the wrong conversation.

Anonymised range examples, drawn from operator practice and reported as ranges to avoid the per-firm portability claim §8 explicitly disavows: squads under steady AI-augmented operation often show 1.5x to 3x deployment frequency, 30% to 50% reduction in lead time for changes under a hundred lines, and 5% to 20% rise in change failure rate when measured without the four-way author/reviewer matrix. The numbers transfer poorly across firms with different review cultures and domain-risk profiles; they are useful as planning anchors, not as targets.

Three things the measurement model deliberately refuses to do. It does not produce a single composite number; vendor dashboards do, and the number is meaningless once you know how it was computed. It does not benchmark squads against each other; the comparison invites optimisation on the metric instead of the underlying work. It does not pretend the numbers are causal; correlations are reported, the squad explores the causation in retrospectives.

The Finance partner's reasonable question is "did this AI investment pay for itself this quarter?". The honest operator-grade answer is "the deployment frequency rose by X percent, the lead time fell by Y percent, the change failure rate moved by Z percent, the cost per merged PR moved by W percent, and the squad's own assessment of the productivity gain is reported separately at quarterly retro". The answer is honest, defensible, and survives a sceptical follow-up. A single ROI number, by contrast, does not.

## 6. Cognitive debt and how to bound it

A squad operating under heavy AI augmentation accumulates cognitive debt the same way an engineering org under heavy technical debt does: a little at a time, invisibly, until the next outage finds nobody who can debug the system live without the tooling that built it.

The mechanism is not mysterious. Engineers stop carrying the design in their heads because the agent does. The next person joining the squad learns the agent's workflow rather than the system's substance. The original engineers can still debug, but they reach for the agent first, and the muscle memory atrophies. The first novel outage (one the agent's priors do not cover) finds the squad slower than they used to be.

The mitigations are mostly operational, not technical.

The first mitigation is the autonomy budget. The harness in [`agentic-harness`](https://github.com/mindfulcto-labs/agentic-harness) enforces three of them simultaneously: tool calls per run, tokens per run, wall-clock per run. The point of the budget is not to limit the agent's usefulness; the point is to force the engineer to think about what would happen if the budget ran out. Squads that work under budget pressure stay engaged with the system in ways squads that do not, do not.

The second mitigation is the blast-radius policy. Three tiers, named `READ_ONLY`, `WRITE_REVERSIBLE`, and `WRITE_IRREVERSIBLE`. The agent's right to call a tool depends on the tier. `WRITE_IRREVERSIBLE` defaults to refused unless the tool descriptor explicitly opts into two-person approval. The policy keeps the engineer in the loop on every decision that cannot be undone, and the in-the-loop participation is what preserves the design knowledge.

The third mitigation is the harness pattern. The harness wraps the agent in a layer the engineer authored. The engineer reads the harness's audit log; the engineer authors the harness's policy file; the engineer owns the harness's failure modes. The harness is the thing that makes the agent feel less like a black box, and the readability of the harness is what keeps the squad's collective knowledge load-bearing.

The fourth mitigation is the on-call exemption. On-call engineers are expected to debug production incidents without agent assistance. The expectation is written down in the on-call handbook. Postmortems explicitly note whether the responder used or did not use agentic tooling. The exemption is not a punishment; it is a deliberate maintenance of the skill that the agent quietly erodes.

The fifth mitigation is the design-review ritual. Once a quarter, the squad reviews the architecture of the system without the agents present. The engineers walk through the design verbally, name the assumptions, name the obligations. The ritual does not always discover anything; what it always does is reinforce that the design is the engineers' to know.

The research literature on cognitive load under AI augmentation is still light, and what exists has the usual sample-and-methodology problems. Microsoft's late-2024 study on critical thinking and AI is the most-cited; the operator perspective from that study reads as: AI use shifts the cognitive load from execution to oversight, and oversight skill is not free. The mitigations above are designed against the specific shape that shift takes in an engineering team.

The honest summary is that the cognitive-debt problem is real, the mitigations work but require ongoing investment, and a squad that thinks it has solved the problem is the squad most likely to be surprised by it. The operator's job is to maintain the investment.

## 7. Failure modes

Every operating model has predictable ways it goes wrong. The ones below are the ones I have either seen or read carefully-documented accounts of. Each one gets a name, a short description, and the one-line mitigation a Director can put on a planning doc.

**Spec rot.** Specs authored with AI assistance start drifting from the working code within weeks. The squad keeps shipping; the spec gets stale; the next AI-assisted change refers back to a spec that no longer matches reality and generates the wrong thing. *Mitigation: the spec is a living document with a named owner per squad. Owners review at least monthly. The CI fails when a spec file is older than its corresponding code by more than thirty days.*

**Steering drift.** The CLAUDE.md, the Cursor rules file, the system prompt, the agent's tool list. All four drift independently. The squad ends up with five subtly different sets of guard-rails and no clean way to ask "what is the agent allowed to do today?". *Mitigation: one canonical steering file per repo, named consistently, version-controlled, and reviewed in PR.*

**Hook explosion.** Pre-commit hooks, agent-side hooks, MCP-server hooks, CI hooks. Each one was a good idea at the time. The cumulative cognitive load is the squad's actual development friction. *Mitigation: hook audit every quarter. Default move is to remove, not to add. Each hook owner has to defend the keep at audit time.*

**Agent-fleet cost runaway.** Cloud agents, parallel runs, multi-step Codex jobs. The bill arrives on the wrong side of the budget. The CFO has questions. *Mitigation: per-team daily cost limit at the runtime layer, not on the dashboard. Hard cap that pages an owner when crossed.*

**IP attribution disputes.** A code change is largely agent-generated, the human reviewer signs the commit, an external party disputes authorship. The firm has no documented position. *Mitigation: explicit authorship policy in the firm's engineering handbook. The reviewer is the author of record. The agent contribution is recorded in the audit trail but not in the commit metadata.*

**Vendor lock-in via tool config.** The squad's productivity is real, the dependence on one vendor's tool is also real, the vendor changes pricing or terms. *Mitigation: the operating model treats the substrate as substitutable from day one. The substrate-agnostic stance in §3 is the policy, not the aspiration.*

**Cognitive-debt accumulation.** Engineers stop carrying the design in their heads because the agent does. The next outage finds nobody who can debug the system live. *Mitigation: on-call engineers are still expected to debug without agent assistance. The expectation is written down. Postmortems explicitly note when the responder used or did not use AI tooling.*

## 8. What I am not claiming

This document is what one operator at one firm thinks works. The vantage point is real and it is also limited.

I am not claiming that the operating model is the right one for every firm size. The patterns are written for the 50-500 engineer band; smaller orgs face different trade-offs, and larger orgs hit coordination costs the patterns do not address.

I am not claiming that the per-squad uplift numbers will transfer. The measurement model in §5 (forthcoming) is reproducible; the numbers it produces are not portable across firms with materially different codebases, review cultures, or domain-risk profiles. Read the ranges; replicate the methodology.

I am not claiming that the governance overlay in §4 (forthcoming) is a substitute for legal counsel. The mappings are operator-grade. An external auditor or regulator reviewing for compliance will want more than this document offers.

I am not claiming that the substrate runtimes named in §3 will still be the right list in twelve months. The list will need refresh. The principle (pick two as the default, opt-in records form their own evidence) is more durable than the specific names.

I am not claiming that the failure modes in §7 are complete. They are the seven I have either seen or read careful accounts of. The eighth one is the one that will surprise you, and the operating model's job is to make it surprise you with the smallest blast radius possible.

## 9. References

Linked inline rather than footnoted, so the reader does not need to scroll.

- Amazon Web Services. [`awslabs/aidlc-workflows`](https://github.com/awslabs/aidlc-workflows). The canonical three-phase framing this document extends.
- ISO/IEC. [ISO/IEC 42001:2023, Information technology — Artificial intelligence — Management system](https://www.iso.org/standard/81230.html). Annex A controls referenced throughout §4.
- European Parliament. [Regulation (EU) 2024/1689 (the AI Act)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj). Article 12 (record-keeping), Article 15 (accuracy, robustness, cybersecurity) referenced throughout §§4-5.
- National Institute of Standards and Technology. [AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework).
- UK Department for Science, Innovation and Technology. [AI Cyber Security Code of Practice](https://www.gov.uk/government/publications/ai-cyber-security-code-of-practice).
- Anthropic. [Building effective agents](https://www.anthropic.com/research/building-effective-agents). The December 2024 essay referenced in §2.
- DORA Industry Report. Annual DevOps performance reports. The measurement model in §5 references DORA's four key metrics and explains where they break under AI augmentation.

Sibling repositories: [`agentic-harness`](https://github.com/mindfulcto-labs/agentic-harness) (the runtime primitives), [`compliance-as-code`](https://github.com/mindfulcto-labs/compliance-as-code) (the schema and AIBOM emitter), [`awesome-ai-governance`](https://github.com/mindfulcto-labs/awesome-ai-governance) (the broader tool registry), [`engineering-standards`](https://github.com/mindfulcto-labs/engineering-standards) (phase-by-phase standards and checklists, when shipped).

---

*All nine sections published. Revisions land via `CHANGELOG.md`.*
