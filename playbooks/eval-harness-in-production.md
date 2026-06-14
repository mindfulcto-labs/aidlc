---
last_reviewed: 2026-06-14
audience: ML engineers and SREs
confidence: medium
---

# Playbook: running an LLM eval harness in production

The playbook tells you how to operate an evaluation harness for an LLM-powered system in production, in a way that produces the audit trail your regulator wants and the operational signals your on-call expects.

## When to use the playbook

Use it when the LLM system has live users and matters enough to the business that a regression in quality would be a real problem. Pilots and prototypes can use lighter-weight measurement; the playbook is for systems whose outputs are consumed by downstream decisions.

## What you need before you start

- An eval suite. Ragas, DeepEval, or a custom suite written against your domain. The suite has to run end-to-end in under thirty minutes; longer suites get postponed and then forgotten.
- An observability platform. Langfuse is the open-source default in 2026; vendor alternatives work. The platform needs to ingest LLM traces with token counts, latencies, and prompt/completion text.
- A model lifecycle tracker. MLflow is the open-source default; the tracker holds the prompt versions, the model versions, and the eval-suite versions, with a stable identifier per release.
- An audit-log sink. The harness in [`agentic-harness`](https://github.com/mindfulcto-labs/agentic-harness) emits one; the sink is the durable Postgres table the chain lands in.

## The shape of production evals

Production evals run on three different cadences. Each cadence has a different purpose and a different failure mode.

### Cadence 1: per-request evals (inline, optional)

Some evaluation runs inline on every LLM call. PII detection, prompt-injection scanning, output safety checks. These are not "evals" in the academic sense; they are guardrails that produce inline decisions.

The architectural choice: where the inline check lives. Three options.

1. **Inside the LLM provider's API.** Easy to set up; vendor-controlled; opaque to your audit log.
2. **In the application code.** Custom; full control; high implementation burden.
3. **In a gateway between the application and the provider.** The pattern recommended in `AIDLC.md` §3. Centralised; auditable; the inline checks live with the rest of the runtime safety stack. The pattern is what [`sentinel-rs`](https://github.com/mindfulcto-labs/sentinel-rs) is being built against; for Python-shop firms the same pattern works with [`apiloom`](https://github.com/mindfulcto-labs/apiloom) plus middleware.

The right answer for most firms is option 3. The audit trail is cleaner, the failure mode is more predictable, and the inline-check upgrade path is decoupled from the application code.

### Cadence 2: per-batch evals (scheduled, in CI)

Some evaluation runs on a schedule, against a curated test set. Faithfulness, answer relevancy, context precision, the metrics Ragas and DeepEval implement. These produce the quality signal that catches model drift, prompt regressions, and retrieval failures.

The scheduling cadence depends on the system's release frequency and the volatility of the underlying model. A system that uses a vendor-hosted model that the vendor occasionally upgrades silently needs more frequent batch evals than a system using a pinned local model.

The recommended cadence is nightly for production-critical systems, weekly for less critical ones. Less than weekly means model regressions catch you by surprise; more than nightly costs more in compute than it saves in early detection.

The results land in the model lifecycle tracker (MLflow), linked to the prompt version and the model version that produced them. The link is what makes regression debugging tractable.

### Cadence 3: per-incident evals (on-demand)

Some evaluation runs when something is wrong. A customer complaint, an unusual error rate, a regression flagged by the batch evals. The on-demand run uses the same eval suite, applied to a narrower slice of traffic, with the results compared to the same slice from a known-good baseline.

The harness for on-demand evals is the batch eval suite re-pointed at production traces from a specific time window. The observability platform's trace export is the source data.

## The audit trail

Every eval run produces evidence. The evidence is the link between the runtime LLM system and the controls in the firm's governance posture. Three records per eval run:

1. **The eval run itself.** Recorded in MLflow with a run-id, a timestamp, the prompt version, the model version, the eval-suite version, and the result scores. MLflow is the source of truth for the eval-run metadata.
2. **The audit-log entry.** Recorded in the harness's hash-chained Postgres table. The entry carries the run-id from MLflow as a cross-reference and the result scores as a payload. The entry is the regulator-legible artefact.
3. **The evidence record.** Recorded in [`compliance-as-code`](https://github.com/mindfulcto-labs/compliance-as-code). The record points at the audit-log entry by hash and tags the controls the run satisfies. The record is the audit-time artefact.

The chain ties one eval run to three durable records, each with a different reader audience (engineer, regulator, auditor). The chain is the thing an internal audit will follow during a review.

The chain also satisfies several specific controls:

- ISO/IEC 42001 A.6.2.3 (verification and validation): the eval suite is the verification.
- ISO/IEC 42001 A.6.2.5 (operation and monitoring): the per-batch cadence is the monitoring.
- ISO/IEC 42001 A.6.2.7 (event logs): the audit-log entry is the event.
- EU AI Act Article 15 (accuracy, robustness, cybersecurity): the eval scores are the quantitative robustness evidence.

## Operational signals

The eval harness produces signals the on-call needs. The two signals worth wiring into the firm's existing alerting:

1. **Score drift alert.** When a batch eval produces a score more than one standard deviation below the rolling 30-day average for the same suite and the same system, page the on-call. The signal catches silent regressions in vendor-hosted models faster than user complaints do.
2. **Suite execution failure alert.** When the scheduled eval suite fails to run (transient error, dependency change, infrastructure problem), page the on-call. The signal catches the failure mode where the evals stop running silently and the firm loses its quality signal without knowing.

Do not alert on individual eval-result thresholds without the drift detection. Static thresholds produce noisy alerts in the first month and ignored alerts in the second.

## What this playbook is not

It is not a substitute for a quality bar on the LLM system itself. Evals catch regressions; they do not produce quality from nothing. A system whose batch evals show 60% faithfulness scores does not have a measurement problem; it has a quality problem the measurement happens to be reporting.

It is not a substitute for human review of high-stakes outputs. Article 14 of the EU AI Act, for high-risk systems, requires human oversight in the loop. Evals support that oversight; they do not replace it.

It is not a quarterly exercise. The cadences are continuous. A system whose evals run "occasionally" is a system without an honest quality signal.

## What success looks like at month six

The eval suite runs nightly on every production-critical LLM system. The results land in MLflow, the audit log, and the evidence store with a stable cross-reference chain. The on-call has been paged twice by score-drift alerts in the previous quarter, and both times the alert was useful. The internal audit team has traced one regulator-asked question from the posture statement to the audit-log evidence in under fifteen minutes. The harness's compute cost is a small line item in the system's monthly bill, not a budget conversation.

That is what a working production eval discipline looks like at this scale.
