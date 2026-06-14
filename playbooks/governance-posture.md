---
last_reviewed: 2026-06-14
audience: Directors, Risk, Compliance
confidence: medium
---

# Playbook: setting an AI governance posture without a SaaS dashboard

The playbook tells you how to stand up an operator-grade AI governance posture for a firm in the 50-500 engineer band using open-source tooling and version-controlled artefacts, without buying a vendor governance product.

## When to use the playbook

Use it when the firm needs to demonstrate ISO/IEC 42001 readiness, EU AI Act conformity, or DORA-aligned AI risk management to internal audit, an external auditor, or a regulator, and the procurement cycle for a SaaS governance product is longer than the deadline allows.

Do not use it as a substitute for legal advice. The playbook produces audit-trail-ready artefacts and a control map; whether your specific facts satisfy the specific regulation is a question for counsel.

## What you need before you start

- A named governance owner. The CIO, CISO, Head of Risk, or in some firms the CDIO. The owner authorises the posture, not the implementation.
- An engineering point of contact for each AI system in scope. The contact answers the questions the posture work produces; without them, the posture stalls.
- An inventory of AI systems. The inventory does not need to be complete on day one; it needs to be honest about what you know and what you do not.
- A repository to store the posture artefacts. The artefacts are version-controlled markdown plus YAML; any private repository works.

## The four-week build

The posture is a four-week exercise. Each week produces an artefact; the artefacts compound.

### Week 1: the system inventory

**Output.** A table of AI systems in the firm, with one row per system. Columns: system name, business owner, engineering owner, risk classification (under the EU AI Act four-tier scheme: minimal, limited, high, unacceptable), data sources, output consumers, and last-reviewed date.

The inventory is the foundation. Without it, the rest of the posture work has nowhere to land. Most firms discover during the inventory that they have more AI systems than they thought; some firms discover the opposite.

Use the AI-system YAML schema in [`compliance-as-code`](https://github.com/mindfulcto-labs/compliance-as-code) (the `AISystem` model). One file per system. The schema produces an SPDX 3.0 AI Profile bill of materials with `aigov aibom emit`.

**Refusal list.** Do not classify a system at "high risk" without reading the EU AI Act Annex III definition; over-classification is a real and common error. Do not classify a system at "minimal risk" without asking the business owner whether the system makes individual-affecting decisions; under-classification is the more dangerous error.

### Week 2: the control map

**Output.** A markdown table mapping each AI system to the controls it satisfies and the controls it does not. The control set is ISO/IEC 42001 Annex A plus EU AI Act Articles 9, 10, 12, 13, 14, 15. For high-risk systems the article set extends to 16 and 17.

The control map is the document an internal auditor will use to see what the firm has and where the gaps are. The honest map names the gaps. Hidden gaps produce surprised auditors, and surprised auditors are expensive.

Use the control YAML library in [`compliance-as-code`](https://github.com/mindfulcto-labs/compliance-as-code) (the `Control` model). The mappings field on each control records the cross-references to the EU AI Act and other frameworks.

**Refusal list.** Do not claim "satisfied" for a control whose evidence does not exist yet. Do not claim "in progress" for a control that nobody is actually working on. The status field carries operational meaning; misuse breaks the trust the audit chain depends on.

### Week 3: the evidence collection

**Output.** A directory of evidence records, one per control per system, linking to the runtime source of the evidence (audit log, attestation record, model release, policy decision).

Evidence is not the same as a control. The control says "the system maintains event logs". The evidence is the audit-log run-id and hash that proves the logs exist for a specific time window.

Use the `Evidence` schema in [`compliance-as-code`](https://github.com/mindfulcto-labs/compliance-as-code). Each evidence record cross-references the audit-log entry rather than duplicating its payload (ADR 0001 in that repository explains why). For systems built on [`agentic-harness`](https://github.com/mindfulcto-labs/agentic-harness), the hash-chained audit log is the evidence source for several controls at once.

**Refusal list.** Do not generate evidence records the runtime cannot actually verify. The first time an auditor traces an evidence record back to a missing audit-log entry, the firm's evidence chain loses its trust premium.

### Week 4: the posture statement

**Output.** A one-page posture statement describing the firm's AI governance shape, signed by the named governance owner. Length: 600-800 words.

The statement covers four things: (a) the firm's AI use scope and the systems in it, (b) the standards the firm operates to (ISO/IEC 42001, EU AI Act, NIST AI RMF), (c) the firm's policy on AI-augmented engineering, (d) the firm's commitment to maintaining the control map and the evidence chain.

The statement is the document the firm publishes externally if needed. It is also the document the firm hands to an internal audit team at the start of a review. The statement is short because it points at the supporting artefacts; the artefacts carry the depth.

**Refusal list.** Do not write the statement in the marketing voice. Auditors and regulators read the statement asking "what would I be surprised by". Plain English is faster to read and harder to misinterpret.

## What happens after the four weeks

The posture is not a one-time exercise. The inventory drifts; the controls update; the evidence chain needs ongoing care. The minimum sustaining investment is:

- A quarterly inventory review. Systems get added, removed, or reclassified. The review is two hours per quarter.
- A monthly evidence-chain check. The check runs the verification routine in [`agentic-harness`](https://github.com/mindfulcto-labs/agentic-harness) on the previous month's audit log. Time: 30 minutes if scripted.
- An annual posture-statement refresh. The named owner re-signs the statement, with revisions where the firm's shape has changed.

The compound investment is roughly 15 hours per quarter for a firm with 5-15 AI systems in scope. That is one quarter of a Principal Engineer's time plus the named owner's review time.

## What you avoid by doing this

- The "we have AI somewhere, we should probably have governance" trap. The inventory tells you whether you do or do not have AI in scope.
- The "we bought a SaaS dashboard, we are covered" trap. SaaS dashboards display the data they are given; the discipline of producing the data is what the auditor cares about. The dashboard without the discipline behind it is a particularly expensive way to fail an audit.
- The "we will write the governance docs after the audit" trap. Audits move faster than governance writing. The four-week build is faster than any retroactive write-up.

## What you do not avoid

- The need for legal advice on the specific application of the regulation to the firm's specific facts.
- The need for an external audit, if the regulation requires one.
- The discomfort of telling the executive sponsor that the firm's AI inventory has more entries than they thought.
