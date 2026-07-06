---
name: ej-quality-longevity
description: Enforce EJ Coding Standards Section VII — Quality & Longevity (Standards 50–64). Covers DRY, YAGNI, KISS, data integrity, abstraction, clean code, refactoring, maintainability, consistency, testability, observability, scalability, complexity budgeting, adaptability, and framework currency.
license: MIT
compatibility: opencode
---

## What I do

I apply Standards 50–64 of the EJ Coding Standards when writing, reviewing, or maintaining code with focus on long-term health, codebase cleanliness, and production readiness.

## When to use me

Use me when:
- Reviewing or improving code quality, naming, or structural organization
- Eliminating duplication, unused code, or unnecessary complexity
- Assessing or improving testability, observability, or scalability
- Evaluating long-term maintainability and adaptability of a design
- Auditing dependencies for currency or checking for framework staleness

---

## Standards

### Standard 50 — DRY (Don't Repeat Yourself)
Every piece of logic must exist in exactly one place. DRY governs *logic*, not text: two blocks that look similar but represent genuinely different business rules are not a DRY violation. Two blocks that perform the same computation for the same reason, written in two places, always are.

### Standard 51 — YAGNI (You Aren't Gonna Need It)
Remove unused code, features, parameters, and abstractions without hesitation. Never write code for requirements that do not currently exist. If it is not needed now, it must not exist now.

### Standard 52 — KISS (Keep It Simple)
Code must be as simple as possible while satisfying its current requirements. Apply Occam's Razor: choose the simplest solution that is correct. When two solutions solve the same problem, the simpler one is always the better engineering choice. Complexity without a specific, present justification is a design defect.

### Standard 53 — Data Integrity and Protection
Data must be protected from corruption, invalid state, and unauthorized mutation at all times and at every layer — not only at system boundaries. Enforce immutability wherever possible. Validate data at the point of entry and reject it before it can propagate invalid state into the system's core. Maintain canonical, authoritative representations of data — never allow multiple mutable copies to diverge.

> Protecting data is not a security concern alone — it is a correctness concern.

### Standard 54 — Abstraction
Complex operations must be abstracted into understandable, reusable, and explicitly named components rather than hardcoded inline at every point of use. Abstraction is the primary tool for managing complexity — used where it genuinely reduces complexity and enables reuse, and not beyond that point.

> Standard 54 makes the *positive case* for abstraction. Standard 41 (Performance & Memory) constrains *how* it must be applied — at zero runtime cost, without excessive layering.

### Standard 55 — Clean Code *(quality of code as currently written)*
Source code must be readable, clear, and simple in the form in which it exists at any given moment. Every identifier must be named precisely and truthfully. Every function must read as a sequence of steps at a single level of abstraction. Every structure must make its intent apparent to a reader who has never seen it before.

> Standard 55 is a property of the code *as it currently exists*. Standard 56 is the *practice* of moving code toward that property over time.

### Standard 56 — Refactoring *(practice of improving structure without altering behavior)*
Continuously improve the internal structure of code — naming, organization, decomposition, coupling, cohesion — without altering its observable external behavior. Refactoring is not optional housekeeping; it is the primary mechanism by which technical debt is repaid before it becomes architectural liability. Never refactor and add features simultaneously — keep the two operations strictly separated.

### Standard 57 — Maintainability *(long-term property of being easy to change)*
Code must be designed so that future modifications can be made quickly, safely, and with confidence that nothing unintended will break. Maintainability is the emergent property of a codebase engineered with consistent discipline: clean code, refactoring, modularity, DRY, and information hiding — applied over time.

### Standard 58 — Consistency
Maintain absolute uniformity in naming conventions, code style, structural patterns, and design decisions across the entire codebase. Every choice made once must be made the same way everywhere. Inconsistency is cognitive overhead: every deviation forces the reader to determine whether it is intentional or accidental. A codebase that reads as if written by one mind — regardless of how many hands touched it — is a well-disciplined codebase.

### Standard 59 — Testability
Code must be structured so that every behavior can be verified in isolation through unit, integration, and system tests. High test coverage must be a structural design outcome, not a post-hoc measurement effort. If a function is difficult to test, its design is the problem — not the test suite. Apply TDD where possible: writing the test before the implementation forces the design to be testable by definition.

### Standard 60 — Observability
The system must emit structured logs, metrics, and traces as first-class runtime outputs — not afterthoughts.

| Signal | What it captures |
|---|---|
| **Logs** | Discrete events |
| **Metrics** | Aggregated measurements over time |
| **Traces** | Causal chains of execution across components |

A system that cannot be observed cannot be trusted, debugged, or operated reliably in production.

### Standard 61 — Scalability
Code must be designed to handle increasing load efficiently as demands grow. Use algorithms and data structures whose performance characteristics scale well with input size. Design components to be independently scalable. Scalability must be a first-class design consideration from the beginning — a system that works at small scale but collapses at production scale was never designed for production.

### Standard 62 — Complexity Budget
Complexity is a finite, depletable resource — spend it deliberately and account for every expenditure. Every line of logic must earn its place by solving a real, present problem. When code grows tangled, refactor; never rationalize complexity as unavoidable. Complexity left unjustified compounds into incomprehensibility.

### Standard 63 — Evolution and Adaptability
Code must be designed to change as requirements, technology, and understanding evolve over the life of the system. Use interface-driven design, dependency injection, and abstract types to make components adaptable without requiring rewrite. Design toward the interfaces between components, not toward their implementations.

### Standard 64 — Latest Framework Currency
Always use the most current stable versions of libraries, frameworks, and language tooling in active use within the codebase. Running on outdated dependencies is running on borrowed time: security vulnerabilities accumulate silently, performance improvements remain inaccessible, and the eventual upgrade cost compounds with every version skipped.

---

## Enforcement Checklist

- [ ] Does any logic exist in more than one place? (Std 50 — deduplicate)
- [ ] Does any unused code, feature, or parameter exist? (Std 51 — remove it)
- [ ] Is every solution the simplest one that is correct? (Std 52)
- [ ] Is data immutable where possible and validated at entry? (Std 53)
- [ ] Is complex logic abstracted into well-named, reusable components? (Std 54)
- [ ] Is every identifier named precisely and every function readable at one level of abstraction? (Std 55)
- [ ] Has the code been left structurally better than it was found? (Std 56)
- [ ] Can future changes be made quickly, safely, and with confidence? (Std 57)
- [ ] Are naming conventions and structural patterns uniform across the codebase? (Std 58)
- [ ] Is every behavior testable in isolation? (Std 59)
- [ ] Does the system emit structured logs, metrics, and traces? (Std 60)
- [ ] Are components independently scalable? (Std 61)
- [ ] Has every unit of complexity been justified? (Std 62)
- [ ] Is the design interface-driven and adaptable without rewrite? (Std 63)
- [ ] Are all dependencies at their latest stable versions? (Std 64)
