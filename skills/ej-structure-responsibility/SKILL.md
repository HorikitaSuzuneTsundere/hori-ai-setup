---
name: ej-structure-responsibility
description: Enforce EJ Coding Standards Section II — Structure & Responsibility (Standards 13–23). Covers SRP, separation of concerns, modularity, OCP, LSP, ISP, DIP, composition over inheritance, composability, Law of Demeter, and information hiding.
license: MIT
compatibility: opencode
---

## What I do

I apply Standards 13–23 of the EJ Coding Standards when designing, reviewing, or refactoring code architecture. I enforce clean boundaries between modules, classes, and interfaces.

## When to use me

Use me when:
- Designing module structure, class hierarchies, or interface boundaries
- Reviewing for SRP violations, excessive coupling, or leaking internals
- Applying SOLID principles (OCP, LSP, ISP, DIP)
- Choosing between composition and inheritance
- Enforcing the Law of Demeter or information hiding

---

## Standards

### Standard 13 — Single Responsibility Principle (SRP)
Each module, class, and function must be responsible for exactly one well-defined concern. If you need the word "and" to describe what a unit does, it must be split.

> SRP is unit-level. Standard 14 (Separation of Concerns) is system-level.

### Standard 14 — Separation of Concerns (SoC)
Logically distinct concerns must live in distinct modules, functions, or layers. Presentation, business logic, data access, and error handling must not bleed into each other.

> SoC is the *organizing principle* — what to separate. Modularity (Std 15) is the *structural mechanism* that enforces it.

### Standard 15 — Modularity
Code must be divided into independent modules that interact exclusively through well-defined, explicit interfaces. No module may reach into the internals of another.

### Standard 16 — Open/Closed Principle (OCP)
A module, class, or function must be open for extension but closed for modification. New behavior is added by extending existing structures — not by altering them. Once a unit is stable and tested, its internals are sealed.

### Standard 17 — Liskov Substitution Principle (LSP)
Any instance of a derived type must be fully substitutable for its base type without altering the correctness of the program. A subtype must honor every precondition, postcondition, and invariant established by its supertype — not just structurally, but behaviorally.

### Standard 18 — Interface Segregation Principle (ISP)
No client should be forced to depend on methods it does not use. Broad, general-purpose interfaces must be split into narrow, role-specific ones. An interface is a promise; a promise must be small enough to be kept honestly.

### Standard 19 — Dependency Inversion Principle (DIP)
High-level modules must not depend on low-level modules. Both must depend on abstractions. Abstractions must not depend on details; details must depend on abstractions. Depend on what a thing *does*, not on what a thing *is*.

### Standard 20 — Composition over Inheritance *(design-time structural preference)*
Prefer assembling behavior through composition of small, focused components over building inheritance hierarchies. Favor has-a over is-a whenever both could achieve the result. Inheritance is appropriate only when a genuine substitutability relationship exists per Standard 17.

> Standard 20 is the structural design choice at the unit level. Standard 21 is the system-level property of free combinability.

### Standard 21 — Composability *(system-level property)*
Components must be designed so they can be freely combined and recombined with other components to create new behavior, without requiring modification to either component. The test: can two components be connected by a third party who wrote neither — without either knowing the other exists?

### Standard 22 — Law of Demeter
A module may only interact with its immediate collaborators: the objects it directly owns, creates, or receives as parameters. It must not reach through those objects to interact with their internal dependencies. Long chains of method or property access are coupling to implementation details of every object in the chain.

### Standard 23 — Information Hiding
Expose only the minimum interface necessary for a module to be used correctly. Every internal detail kept private is one less surface area for bugs to propagate across module boundaries. The public interface is a contract; everything behind it is implementation free to change without breaking consumers.

> Standard 23 restricts what a module *exposes*. Standard 24 (Access & Security) restricts what a module is *permitted to access*.

---

## Enforcement Checklist

- [ ] Does this unit do exactly one thing? (Std 13)
- [ ] Are distinct concerns in distinct modules/layers? (Std 14)
- [ ] Do all modules interact only through explicit interfaces? (Std 15)
- [ ] Can new behavior be added without modifying stable code? (Std 16)
- [ ] Can derived types substitute for their base without surprise? (Std 17)
- [ ] Are interfaces narrow enough that no client depends on unused methods? (Std 18)
- [ ] Do high-level modules depend on abstractions, not concrete implementations? (Std 19)
- [ ] Is composition used instead of inheritance wherever possible? (Std 20)
- [ ] Can this component be combined with others without modification? (Std 21)
- [ ] Does this module chain through intermediaries to reach distant state? (Std 22 — fix if yes)
- [ ] Is the public interface the minimum required? (Std 23)
