# EJ Coding Standards — Skills Overview

A set of `opencode` skills that enforce the **EJ Coding Standards**, split
by section. Each skill covers a numbered range of standards and includes
its own enforcement checklist. Use whichever skill(s) match the task at
hand — several often apply together.

| Skill | Section | Standards | Focus |
|---|---|---|---|
| `ej-correctness-contracts` | I — Correctness & Contracts | 1–12 | Idempotency, fail-fast, design by contract, guard clauses, CQS, purity, determinism, no null, self-checking, defensive validation, robustness |
| `ej-structure-responsibility` | II — Structure & Responsibility | 13–23 | SRP, separation of concerns, modularity, OCP, LSP, ISP, DIP, composition over inheritance, composability, Law of Demeter, information hiding |
| `ej-access-security` | III — Access & Security | 24–25 | Least privilege, input sanitization, encryption at rest/in transit, layered access control, security audits |
| `ej-code-format-constraints` | IV — Code Format & Structural Constraints | 26–34 | Function size (13–15 lines), one statement per line, 80-char limit, minimal scope, no boolean args, no recursion in imperative code, bounded loops, self-documenting code, explicit over implicit |
| `ej-performance-memory` | V — Performance & Memory | 35–44 | Algorithm selection, O(1) targets, algorithmic efficiency, hot-path optimization, data locality, data-oriented design, abstraction cost, bit manipulation/parallelism, memory determinism, footprint reduction |
| `ej-architecture-resilience` | VI — Architecture & Resilience | 45–49 | Stateless design with explicit caching, resource lifecycle (acquire/use/release), centralized error handling, circuit breaker pattern, concurrency isolation |
| `ej-quality-longevity` | VII — Quality & Longevity | 50–64 | DRY, YAGNI, KISS, data integrity, abstraction, clean code, refactoring, maintainability, consistency, testability, observability, scalability, complexity budget, adaptability, framework currency |
| `ej-programming-paradigms` | VIII — Programming Paradigms | 65–69 | Generic programming, metaprogramming discipline, functional programming, OOP mechanisms, deliberate design pattern selection |

## How they work

Each skill is self-contained: a `SKILL.md` with frontmatter (`name`,
`description`, `license`, `compatibility`), a "When to use me" trigger
list, the full text of its standards, and an enforcement checklist for
review/audit use. Cross-references between related standards in
different sections (e.g. Std 23 ↔ Std 24, Std 31 ↔ Std 67) are called
out inline so the boundary between skills is clear.

## License

MIT
