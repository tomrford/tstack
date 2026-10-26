---
name: how
description: 'Use for "how does X work", code walkthroughs before changing something, and placement / ownership / layering questions ("where should this live", "which package owns this", "is this the right layer"). Explains subsystem architecture, runtime flow, onboarding mental models. Use why for motivation.'
---

# How

Build an accurate mental model that lets the reader reason about the system and work on it confidently.

Start with the capability and its consumers. Trace a representative path through the real implementation: what triggers it, how data and control move, who owns state and resources, and what the caller observes. Follow consequential failure and lifecycle paths as well as normal operation.

Look from multiple angles where they matter. Public interfaces, internal structure, tests, and runtime behaviour may tell different parts of the story. Resolve contradictions rather than repeating the most convenient account. Use a focused experiment when static inspection leaves an important behaviour uncertain.

Explain the underlying constraints and invariants. Distinguish what the problem requires from how the current implementation happens to solve it. For placement or design questions, reason from those requirements before accepting existing boundaries.

Seek an independent assessment when competing interpretations or cross-cutting behaviour could materially change the explanation.

Lead with the mental model, then explain the important flow and decisions. Cite the code that supports the explanation, point to the few places a maintainer should start, and surface consequential gotchas or gaps. Use a diagram when it makes the relationships easier to understand.

Keep detail proportional to the question. The result should explain the system, not narrate the investigation or paraphrase every file. Investigation does not itself authorise implementation changes.
