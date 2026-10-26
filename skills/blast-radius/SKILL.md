---
name: blast-radius
description: "Find what a change could break somewhere else before it ships, beyond the diff, and prove the facts its safety depends on with concrete evidence. Use for 'blast radius of X', 'what could this break', or reviewing a small diff you don't trust."
---

# Blast radius

Find the consequences a local reading of the diff would miss, and establish the evidence needed to judge whether the change is safe.

Understand the intended outcome and what actually changes, including removed behaviour and implicit guarantees. Trace affected consumers and contracts beyond direct callers. Consider shared state, lifecycle and timing, persisted data, wire formats, configuration, and dependencies where relevant.

Identify the assumptions the change's safety depends on. Challenge them against the real implementation, dependency versions, and operating conditions. Focus on plausible failure paths with meaningful consequences rather than an exhaustive list of hypothetical risks.

Assess the change from multiple angles. Seek an independent assessment when its reach, uncertainty, or consequences make blind spots costly.

Prove the consequential assumptions as directly as practical. Use existing behavioural evidence, a focused test or reproduction, or the running application. Static reasoning can establish structural guarantees; runtime claims need runtime evidence when inspection cannot settle them. A convincing explanation is not a substitute for a check that could show it is wrong.

Distinguish what was inspected, inferred, and exercised. Passing checks support only the cases and conditions they cover. If a material assumption remains unproven, say what is missing and what would resolve it.

Return a concise assessment covering:

- What changes for affected consumers, including non-obvious effects.
- The safety assumptions and evidence supporting them.
- Remaining risks, their triggering conditions, and their consequences.
- Significant concerns investigated and cleared, with reasons.
- Any verification or decision needed before shipping.

Cite the relevant code and evidence. Do not invent likelihood estimates or declare safety from an absence of findings. Keep experiments isolated and leave product changes to the surrounding task.
