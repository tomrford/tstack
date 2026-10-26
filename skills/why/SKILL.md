---
name: why
description: 'Use for "why does X work this way", "why we picked Y", design rationale, regressions, postmortems, or data-backed thresholds. Investigates relevant history and evidence, then returns a cited read on decisions and tradeoffs. Use how for runtime behavior.'
---

# Why

Establish what led to the current design without inventing a tidy rationale for it.

Anchor the question in the relevant code and behaviour. Trace the substantive changes that introduced or reshaped it, following history beyond the most recent edit. Read the associated discussions and evidence where available.

Choose sources according to the question. Commits and PRs can explain implementation choices; issues, design documents, and conversations can reveal requirements and rejected alternatives; incidents and operational data can explain defensive behaviour or thresholds. Follow promising leads and widen the search when the explanation remains weak or contradictory.

Treat the user's proposed explanation as a hypothesis. Consider alternatives and look for evidence that could disprove the leading account. Seek an independent assessment when the interpretation is consequential or the record supports competing explanations.

Separate documented intent, supported inference, and unresolved uncertainty. Code establishes mechanics; it does not by itself establish author intent. A plausible benefit today is not evidence that it motivated the original decision. Surface conflicting accounts and material gaps rather than forcing agreement.

When the question informs a change, distinguish historical reasons from present requirements. Assess which constraints still hold, which have expired, and what must be preserved. Reason from the current need rather than assuming either that the existing design is justified or that a cleaner design is safe.

Answer with the best-supported explanation, its evidence, and the uncertainty that matters to the decision. Briefly identify search limits where they affect confidence. Keep recommendations distinct from historical findings, and leave implementation to the surrounding task.
