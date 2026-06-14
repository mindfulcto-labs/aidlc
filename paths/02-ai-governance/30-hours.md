---
last_reviewed: 2026-06-14
tier: 30-hours
---

# Path 2, 30-hour tier: AI governance, operationalised

The cert-prep tier paired with a shipped artefact.

## 1. ISACA CGEIT study material, governance domain

[`isaca.org/credentialing/cgeit`](https://www.isaca.org/credentialing/cgeit)

The Certified in the Governance of Enterprise IT credential is the most concrete operational treatment of IT governance written for the leader audience. Even if you are not sitting the exam, the "evaluate, direct, monitor" framing transfers cleanly onto AI portfolio governance. CGEIT covers the governance shape; CRISC adds the risk lens; CISM adds the security lens. For this path you only need CGEIT.

Why this slot: the CGEIT framing is what an executive sponsor will use in their head, even if they have not heard the acronym. Reading the material lines your vocabulary up with theirs.

## 2. Build a posture statement using `compliance-as-code`

[`github.com/mindfulcto-labs/compliance-as-code`](https://github.com/mindfulcto-labs/compliance-as-code)

Pick one AI system inside your firm (or a synthetic one if you cannot use a real one). Run `aigov init <system-name>` to scaffold the starter pack. Fill in the AISystem YAML. Run `aigov aibom emit` to generate the SPDX 3.0 AIBOM. Wire one evidence emitter pointing at the system's audit log.

The 30-hour run produces a posture pack you can hand to internal audit. The artefact is not the goal; the discovery work along the way is the goal. You learn which controls your system already satisfies, which it does not, and which it satisfies in spirit but not in evidence.

Why this slot: the schema is operator-grade. Running it against one system teaches you both the standard and the gaps in your own implementation. No reading-only path produces the same learning.
