---
name: ej-correctness-contracts
description: Enforce EJ Coding Standards Section I — Correctness & Contracts (Standards 1–12). Covers idempotency, fail-fast, design by contract, correctness verification, guard clauses, command-query separation, pure functions, determinism, null prohibition, self-checking code, defensive validation, and robustness.
license: MIT
compatibility: opencode
---

## What I do

I apply Standards 1–12 of the EJ Coding Standards when writing, reviewing, or refactoring code. I enforce correctness guarantees and behavioral contracts at the function level.

## When to use me

Use me when:
- Writing or reviewing functions that must be correct in every case, not just common cases
- Enforcing null safety, guard clauses, or fail-fast error surfacing
- Declaring preconditions, postconditions, or invariants (Design by Contract)
- Reviewing for idempotency, CQS violations, impure functions, or non-determinism
- Embedding runtime assertions and self-checking invariants

---

## Standards

### Standard 1 — Idempotency
Every operation must be safe to execute multiple times without changing the outcome beyond its first application. Repeated execution must leave the world in exactly the same state as one execution did.

### Standard 2 — Fail Fast
Code must surface errors immediately at the exact point of failure — not defer, swallow, or disguise them. A loud, early failure is always preferable to a quiet, late one. Silent failure is poison; fast failure is mercy.

### Standard 3 — Design by Contract
Every function must explicitly declare:
- **Preconditions** — what it requires from the caller
- **Postconditions** — what it guarantees upon completion
- **Invariants** — what must remain true at all times

Contracts are enforceable logic baked into the code itself, not documentation.

> Standard 3 governs *specifying* what code promises. Standard 4 governs *verifying* those promises are kept.

### Standard 4 — Correctness
Code must behave according to its specification in every case — not most cases, every case. Apply formal methods, mathematical proofs, or exhaustive verification where appropriate. Testing reveals the presence of bugs; formal verification demonstrates their absence.

### Standard 5 — Guard Clauses
Validate all necessary conditions at the entry point of a function and exit immediately if they are not met. Never nest conditional logic to express the happy path — flatten it. No else-branches, no defensive nesting, no buried precondition checks halfway through execution.

### Standard 6 — Command-Query Separation (CQS)
- Functions that **modify state** must not return values.
- Functions that **return values** must not modify state.

These two responsibilities must never coexist in a single function signature.

### Standard 7 — Pure Functions *(function-level)*
A function is pure if and only if it always produces the same output for the same input and causes no observable side effects. Pure functions must be free from hidden dependencies on external state, global variables, I/O, or system time.

> Standard 7 is function-level. Standard 8 is system-level.

### Standard 8 — Determinism *(system-level)*
The system must produce the same output given the same input, across any execution, on any machine, at any time. Code must not rely on external mutable state, system clocks, process IDs, uninitialized memory, or non-deterministic scheduling in any functional code path.

### Standard 9 — Null Prohibition
Never assign or return null. Represent absence through explicit, typed constructs: `Option` / `Maybe` types, `Result` types, or the Null Object pattern. When a function can fail or produce no result, that possibility must be visible in the return type.

### Standard 10 — Self-Checking Code
Assertions and runtime invariant checks must be embedded throughout the codebase — not only at system boundaries. If an invariant is assumed true at a point in execution, that assumption must be stated in executable form, not only in a comment.

### Standard 11 — Defensive Validation
Every calling function must inspect and handle all non-void return values — ignoring a return value is prohibited. Every called function must validate all parameters before using them.

### Standard 12 — Robustness
Code must gracefully handle unexpected situations, failures, and edge cases rather than crashing or propagating corrupt state. The system must degrade gracefully under stress, not catastrophically.

> Standard 12 governs *what happens* when things go wrong. Standard 47 (Architecture & Resilience) governs *where* error handling code lives architecturally.

---

## Enforcement Checklist

- [ ] Can the operation be called multiple times safely? (Std 1)
- [ ] Does it fail loudly at the point of failure? (Std 2)
- [ ] Are preconditions, postconditions, and invariants declared? (Std 3)
- [ ] Have all cases been verified — not just common ones? (Std 4)
- [ ] Are guard clauses at the top with no nested conditionals? (Std 5)
- [ ] Does the function either return a value OR mutate state — never both? (Std 6)
- [ ] Is it pure if it can be? (Std 7)
- [ ] Does it introduce no non-determinism? (Std 8)
- [ ] Does it return null anywhere? (Std 9 — fix if yes)
- [ ] Are runtime invariant assertions embedded? (Std 10)
- [ ] Are all return values handled and all parameters validated? (Std 11)
- [ ] Does it handle edge cases gracefully? (Std 12)
