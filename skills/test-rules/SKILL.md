---
name: test-rules
description: Apply when deciding whether to add, change, remove or review automated tests or other committed checks, including runtime, integration, type-level and compile-time tests.
---

# Test rules

Tests protect agreed behaviour while leaving implementation choices replaceable. Optimise for confidence per maintained line. Apply these rules when choosing, writing and reviewing tests; they do not prescribe whether tests or code come first.

## A test must add knowledge the code does not hold

- A test earns its place by recording a decision the code cannot show on its own: a requirement, a spec, a chosen edge-case outcome, a promised failure behaviour, a bug that must not return.
- Someone reading only the test should learn what the module must guarantee and why. A reader who could predict every assertion from the source alone has learned nothing.
- How existing callers happen to use a function is not a contract. Test what was agreed, not what the code currently does.
- The implementation is evidence of how something works, not authority for how it should work. Derive consequences of the agreed contract; do not invent new guarantees. Raise material ambiguity instead of pinning a guess in a test.
- Decide the expected result from an independent source before running the code: a requirement, spec, worked example, real captured input or reference result.

## Never write these

- Tests of the language, type system, compiler, runtime, standard library or a dependency. This includes types or values asserted to match the declaration they were derived from.
- Tests that restate source: constants, enums, defaults, literals, mappings, registries, that an export or file exists, that a declaration compiles. Arithmetic on a constant is still a restatement: `5 * MINUTES_TO_SECONDS == 300` is as worthless as `MINUTES_PER_HOUR == 60`.
- Tests whose expected value comes from the code under test: comparing a result with itself or with the same logic, pasting the code's output into the assertion, accepting an unchecked snapshot.
- Tests that check no behaviour: no meaningful assertion, only fixtures or mocks, only that internal calls happened, never reaching the path they claim.

None of the usual justifications make one of these acceptable:

- "it guards against someone accidentally changing the value";
- "it documents the contract" or "makes the intent explicit";
- "it is cheap" or "only one line";
- "it pins the public API" or "catches a breaking change";
- "it increases coverage";
- "it is a type-level test, so it costs nothing at runtime".

If you find yourself arguing that one is warranted here, delete it. Do not imitate such tests where they already exist; flag them for removal.

## Prove each test detects a real failure

For every new or materially changed scenario:

- Name the contract it protects, a specific plausible violation, the assertion that catches it, and why existing coverage misses it.
- Break production behaviour in a way a consumer would notice, run the test, confirm it fails for that reason, then restore and confirm it passes. For a bug fix, run against the defect and the fix.
- Editing the value, type or declaration the test restates is not a violation. If that is the only edit that fails the test, delete it.
- A failure because a symbol, fixture or implementation does not exist yet proves nothing.
- If no plausible production bug fails it, or existing coverage already catches the same bug, delete it.
- If you could not run the check, say so in the handoff; do not claim it.

## Test through the consumer's boundary

- Call the interfaces consumers use, as they would, with real internal components working together. Prefer end-to-end and integration tests.
- A boundary is a capability and its consumers, not a file, class or export. Exporting a helper does not make it worth its own tests.
- Test a smaller component on its own only when the user specified its behaviour, or its failures cannot be reached or diagnosed through the boundary. Then list how it can fail first, and test those failures.
- Cover each guarantee once, at its owning layer.
- A test that breaks under a behaviour-preserving refactor asserts implementation. Do not add it.

## Choose scenarios that matter

- Each scenario needs a plausible consumer, an agreed expectation and a real consequence if it fails: normal use, lifecycle transitions, documented limits, credible failures.
- Prefer a few scenarios that walk the capability through its lifecycle, including promised failure, cancellation and recovery, over many single-operation tests. Assert effects throughout.
- Use distinguishable inputs that would expose a mix-up; keep variants on independent state; keep failures diagnosable.
- Exact bytes, ordering and counts are valid expectations when consumers can observe and rely on them.
- Round trips and agreement between implementations prove only that relationship, not correctness.
- If awkward combinations reveal an over-permissive interface, fix the interface instead of testing behaviour nobody needs.

## Use real collaborators

- Use real project-owned code; contain effects with isolated files, stores and transports.
- Substitute external dependencies only for isolation, determinism or cost, and never let the substitute supply the behaviour under test.
- Do not add production exports, flags, wrappers or injection hooks just to reach internals.
- Heavy mocking, complex setup and repeated exceptions are signs the boundary or design is wrong. Rethink it before adding more test machinery.

## Evolve coverage with the code

- New behaviour: extend the owning scenario if it is the same coherent use; otherwise add an independent one.
- Bug fix: the smallest test change that distinguishes the defect from the fix.
- Refactor: setup may change; assertions and expected results may not.
- Intentional behaviour change: update the expectations. Removed behaviour: remove its tests and test-only support.
- Before deleting redundant coverage, confirm the remaining tests protect the same behaviour.
- Never delete, skip or weaken a failing test to make the suite pass. Find out whether it exposes a bug, a wrong expectation or a contract change. Fix the code, or ask.

## Keep tests proportionate

- Weigh test code, fixtures and helpers against the production change; trim duplication and unneeded setup.
- For a large input matrix, consider one property test of an independently justified invariant.
- Coverage percentages and test counts are diagnostics, not targets.
