---
last_reviewed: 2026-06-14
audience: EMs and engineering directors
confidence: medium
---

# Playbook: per-squad uplift metrics under AI augmentation

The playbook tells you how to measure the productivity effects of introducing AI tooling into a squad, honestly enough that the squad recognises the report and a Finance partner can defend it.

## Why this is hard

DORA's Four Keys are the canonical engineering productivity metrics, and they bend in misleading ways under AI augmentation. Deployment frequency rises sharply; lead time falls sharply; change failure rate moves in either direction depending on the workload; mean time to restore depends on whether the responder used the agent or not. The aggregate picture often reads as a win, but the win is overstated when the metrics are presented without their context.

The right measurement model accepts the complexity instead of compressing it. Section §5 of [`AIDLC.md`](../AIDLC.md) sets the principles; this playbook is the operational version.

## The five metrics

The squad reports five numbers per quarter. Each one is reported as a range, not as a point estimate.

### 1. AI-code-share

The fraction of merged code authored substantially by an agent. "Substantially" is the load-bearing word: the agent rarely writes a complete commit alone, and counting raw lines or raw commits under-counts the squad's real leverage. The working definition is "the reviewer marked the commit as agent-substantial during review". The reviewer's mark is the data; the mark is recorded in the commit footer or in the firm's PR metadata.

Report as a percentage range, with the confidence band wider for smaller squads.

The number rises over the first six months of a rollout, then stabilises. A squad that reports 90% AI-code-share has either an unusual workload or a measurement problem; investigate both. A squad that reports 5% AI-code-share has either an unusual workload or an adoption problem; investigate both.

### 2. Complexity-adjusted velocity

Story points or shippable units delivered, weighted by the cognitive complexity of the change. The simplest workable adjustment is a 1-to-5 complexity weight per change, applied at review time. The EM owns the weighting consistency across the squad.

Report as a quarter-over-quarter ratio, with the methodology disclosed.

The metric is useful because raw velocity over-reports the gain from AI augmentation: agents shorten the time on simple changes more than on complex ones, so a squad doing more simple work looks more productive than a squad doing more complex work. Weighting corrects for this.

### 3. Escaped-defect rate

Defects discovered in production within thirty days of release, normalised by the volume of changes that shipped in the same window.

Report as a count per week, with the previous quarter's number for comparison.

The metric catches the failure mode where the squad ships faster but ships more bugs. The two numbers (deployment frequency and escaped defects) should be reported together, not separately; presenting them apart invites the wrong conversation.

### 4. Cost per merged pull request

The total tool spend for the squad in the quarter, divided by the count of merged PRs in the quarter.

Report as a currency amount, with the cost trajectory over the previous three quarters for context.

The metric is the Finance partner's reasonable question made tractable. It is not the only relevant cost number; the squad's payroll, infrastructure, and overhead matter too, and the report should include them as context. The cost-per-PR figure on its own is misleading.

### 5. Review-load delta

The change in the median time a reviewer spends per pull request, compared to a non-AI-augmented baseline (e.g. the squad's numbers from two quarters before AI introduction).

Report as a percentage change with directionality.

The metric matters because AI-generated code shifts the workload from authoring to reviewing. The reviewer ends up working harder per commit, even as the author works less. A squad whose review-load delta is rising sharply has a sustainability problem the deployment-frequency number is hiding.

## How to report

The report is a single page per quarter. The five numbers, each with a range, each with a methodology footnote. Two paragraphs of operator context explaining what the numbers mean and what they do not mean. A third paragraph that is honest about the things the report cannot measure.

Bad reports compress the five numbers into a "productivity index". The index is meaningless once you know how it was computed, and reporting it invites unhelpful comparison between squads. Do not produce the index.

Good reports include the squad's own assessment of the gain or loss, written by the EM in plain English. The qualitative assessment often disagrees with the quantitative numbers; the disagreement is the most interesting data in the report.

## What not to do

- **Do not benchmark squads against each other.** The comparison invites optimisation on the metric rather than on the underlying work. Squads benchmark themselves against their own prior quarters.
- **Do not present a single composite number to the executive sponsor.** The sponsor's instinct will be to compare it across teams; the comparison is misleading.
- **Do not extrapolate the numbers across firms.** The methodology transfers; the numbers do not. Report the methodology in any cross-firm conversation; refuse to report the numbers.
- **Do not let vendors contribute to the methodology.** Vendor framing of productivity metrics is uniformly more optimistic than what the data supports.
- **Do not measure for one quarter and stop.** A single quarter's numbers are noise. The discipline starts paying off at the four-quarter mark, when seasonal patterns and one-off effects become visible.

## What the numbers will probably show

Anonymised range examples from operator practice, reported with the confidence-band that §5 of [`AIDLC.md`](../AIDLC.md) requires:

- AI-code-share: rises from 0% to between 30% and 60% over the first three quarters of adoption.
- Complexity-adjusted velocity: rises by 20% to 40% over the same window for squads working on greenfield product; rises by 10% to 20% for squads working on brownfield platforms.
- Escaped-defect rate: moves between -10% and +30% in the first three quarters, with high variance; stabilises in the second year.
- Cost per merged PR: rises in the first two quarters as the spend grows ahead of the merged count; falls below baseline in the third or fourth quarter for most squads; remains above baseline for squads with low-volume complex work.
- Review-load delta: rises by 10% to 40% in the first six months; stable thereafter if the squad has invested in CLAUDE.md and reviewer training.

The numbers do not transfer between firms with materially different review cultures, codebase shapes, or domain-risk profiles. Read them as planning anchors, not as targets.

## What this playbook is not

It is not a method for proving the AI investment paid off. It is a method for honestly measuring the change. Whether the change was worth the spend is a finance and strategy decision that the metrics inform but do not make.
