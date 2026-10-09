---
name: test-authoring
description: Guide the authoring, modification and review of committed automated tests during feature work, bug fixes and refactoring. Prefer deep integration coverage of agreed capabilities and module boundaries, with minimal maintained test code.
---

# Test authoring

Preserve agreed behaviour while keeping implementation choices replaceable. Optimise for confidence per maintained line.

These guidelines apply alongside implementation and review. They prescribe test contents and scope, not whether tests or production code are written first.

## Test the agreed contract

The contract is what a capability accepts, produces, guarantees and exposes to its callers. Ground expectations in the user's requirements, established public contracts, relevant specifications and consequences of those requirements.

Do not turn an agent's implementation choices into requirements by writing tests around them. The current implementation is evidence of how something works, not authority for how it should work.

An agent may derive consequences of an agreed contract. It must not silently invent additional guarantees. Surface material ambiguity rather than pinning an assumption in a test.

Internal organisation, helper behaviour and intermediate representations remain replaceable unless they implement an explicitly required contract.

## Choose the owning boundary

Prefer deep integration tests at the module boundary responsible for a capability. Invoke it as a real caller would, exercise its internal components together, and inspect observable results.

A boundary is defined by the capability and its consumers, not by a file, class or exported function. Exporting a helper does not make it worth testing separately.

Do not add isolated unit tests for private helpers, internal collaborators or individual implementation branches. A focused test belongs only where the small interface itself represents an agreed capability.

Avoid duplicating the same guarantee across layers. Additional coverage must address a distinct failure that the owning test cannot detect.

## Choose realistic scenarios

Test situations a real consumer can plausibly encounter through the capability's interface. Normal usage, realistic lifecycle transitions, documented limits and credible operating failures deserve coverage when their outcomes matter to the caller.

A scenario being representable does not make it worth testing. Do not chase arbitrary argument combinations, artificial internal states or hypothetical misuse solely because they are possible. Each scenario needs a plausible consumer, an agreed expectation and a meaningful consequence if it fails.

When awkward combinations expose an ambiguous or unnecessarily permissive interface, reconsider the interface or data model instead of adding defensive code and tests to support behaviour nobody needs.

## Exercise coherent lifecycles

Cover meaningful sequences of use, including state transitions, outputs, side effects and resource ownership where these are part of the contract.

Prefer a small number of scenarios that take the capability through its lifecycle over many tests of individual operations. Include failure, cancellation and recovery variants where the capability promises them.

Assert meaningful results throughout. Completing a sequence without checking its effects is insufficient.

Keep scenarios understandable and failures diagnosable. Use independent state for distinct variants; do not create one sprawling test whose later checks depend on unrelated earlier cases.

Choose inputs that expose consequential mistakes. Distinguishable records, values and resources are more useful than repeated placeholders.

## Use real components and independent expectations

Exercise real internal collaborators. Prefer isolated files, stores and transports over mocks of code owned by the project.

Substitute external dependencies only where isolation, determinism or cost requires it. A substitute must not provide the behaviour the test claims to verify.

Expected results must come from an independent source: an agreed requirement, specification, worked example, known fixture or established reference result.

Reject tautological tests: self-confirming assertions that compare a result with itself or derive the expected result using the same logic being tested. Also reject assertions that:

- Verify only fixture setup.
- Verify internal calls instead of observable effects.
- Restate source text, constants or configuration without testing their contractual effect.
- Pass through an unrelated guard without reaching the behaviour claimed.
- Claim more than their inputs and assertions establish.

Exact bytes, ordering and operation counts are valid expectations when they are observable contractual guarantees.

Round trips and agreement between implementations prove only the relationship being checked. They do not independently establish correctness.

## Evolve coverage with capabilities

New features extend the owning integration scenarios. Add a new test when a distinct capability requires its own scenario.

Bug fixes strengthen existing capability coverage through better inputs, lifecycle variants or assertions. Do not automatically create a standalone regression test or defect-specific test file.

A missing owning scenario is a coverage design gap. Repair coverage around the capability rather than accumulating tests around individual defects.

Behaviour-preserving refactors should preserve contractual expectations. Do not weaken assertions or rewrite expected results merely to accommodate a changed implementation.

Intentional behaviour changes update the relevant expectations. Feature removal removes its corresponding coverage.

Consolidation may remove redundant tests when the remaining coverage demonstrably protects the required behaviour.

## Make test growth earn its place

Keep setup, fixtures and helpers proportionate to the capability. Do not add production exports, flags, wrappers or injection hooks solely to test implementation internals.

Repeated exceptions, extensive mocking and complicated setup are reasons to reconsider the design or chosen boundary before adding more test machinery.

Compare added, removed and net lines separately for handwritten production code and tests, including test support and handwritten fixtures. Exclude generated outputs.

Positive test growth exceeding positive production growth requires a design check: investigate duplicated coverage, unnecessary setup, misplaced boundaries and avoidable complexity. Explain any remaining disproportionate growth.

Do not pad production code, obscure tests or delete unrelated coverage to satisfy the comparison.

Where input diversity creates a substantial example matrix, consider a compact property test: one that checks an agreed invariant across generated inputs. The invariant must have independent justification.

Coverage percentages and test counts are diagnostic information, not authoring targets.

## Judge retained value

For each new or substantially changed scenario, be able to explain:

- Which realistic consumer scenario it represents.
- Which agreed behaviour it protects.
- Which credible defect would make it fail for the intended reason.
- What it detects beyond existing coverage.
- Why its maintained code is proportionate to that value.

A useful test permits internal rewrites while rejecting violations of the contract. A test that merely preserves the current implementation has not earned its place.
