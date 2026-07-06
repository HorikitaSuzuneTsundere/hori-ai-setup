---
name: ej-programming-paradigms
description: Enforce EJ Coding Standards Section VIII — Programming Paradigms (Standards 65–69). Covers generic programming with type safety and constraints, metaprogramming discipline, functional programming with immutability and higher-order functions, OOP with encapsulation and substitutability, and deliberate design pattern selection from the full structural/behavioral/creational catalog.
license: MIT
compatibility: opencode
---

## What I do

I apply Standards 65–69 of the EJ Coding Standards when writing paradigm-specific code or selecting design patterns. I enforce disciplined application of generics, metaprogramming, functional, and OOP techniques, and deliberate pattern selection.

## When to use me

Use me when:
- Writing generic or parameterized code (templates, type parameters, constraints)
- Writing metaprogramming constructs (compile-time or runtime code generation)
- Applying functional programming techniques (immutability, higher-order functions, recursion)
- Organizing systems using OOP (encapsulation, abstraction, polymorphism, inheritance)
- Selecting or applying a design pattern from the structural, behavioral, or creational catalogs

---

## Standards

### Standard 65 — Generic Programming
When writing parameterized or generic code, enforce four requirements:

1. **Type Safety** — Incorrect type usage must be caught at the earliest possible stage (compile time preferred), never at runtime
2. **Meaningful Names** — Generic type parameters must use names that communicate their semantic role and constraints, not single-letter placeholders that require surrounding context to interpret
3. **Constraints** — Restrict which types may be used with a generic construct; enforce correctness by construction at the type level
4. **Performance Implications** — Evaluate overhead from boxing, erasure, or indirection that generic abstractions may introduce

### Standard 66 — Metaprogramming
When writing code that generates, inspects, or transforms other code at compile time or runtime:

1. **Clarity** — Write metaprogramming constructs in the clearest and most concise form possible; metaprogramming already introduces an additional layer of indirection
2. **Understandability** — Design metaprogramming solutions to be understandable and modifiable by engineers who did not write them
3. **Performance** — Optimize the metaprogramming layer itself to eliminate unnecessary overhead it introduces
4. **Testing Rigor** — Test metaprogramming code with the same rigor applied to any critical system component; its failures can corrupt the code it generates in ways that are difficult to trace

### Standard 67 — Functional Programming
When applying functional programming techniques:

1. **Immutable Data Structures** — Favor immutability to eliminate side effects and simplify reasoning; a value that cannot change cannot be corrupted by concurrent access or unexpected mutation
2. **Higher-Order Functions** — Employ functions that accept or return other functions to create flexible, composable, reusable logic
3. **Minimal Mutable State** — Minimize all use of mutable state; keep it isolated to the smallest possible region of the codebase
4. **Recursion** — Use recursion as the natural and idiomatic expression of self-referential algorithms within the functional paradigm

> Standard 31 (Code Format) prohibits recursion in imperative control flow. Standard 67 recognizes recursion as appropriate within the functional paradigm. These are genuinely distinct contexts — not a contradiction.

### Standard 68 — Object-Oriented Programming
When organizing systems using OOP techniques, apply the four mechanisms with engineering judgment:

| Mechanism | What it does | When to apply |
|---|---|---|
| **Encapsulation** | Bundle data with behavior; shield internal state | Always — default OOP discipline |
| **Abstraction** | Expose only what consumers need | When a clean interface can be defined |
| **Polymorphism** | Single interface, different underlying implementations | When behavior must vary by type without the caller knowing which type |
| **Inheritance** | Derive a type from another | Only when a genuine substitutability relationship exists per Standard 17; **never for code reuse alone** |

> OOP is a structural discipline for separating responsibility — not a default style to apply indiscriminately.

### Standard 69 — Design Pattern Selection and Application Discipline
Apply established design patterns deliberately, precisely, and only when the problem's structure matches the problem the pattern was designed to solve. A pattern applied out of habit or to signal sophistication is an antipattern.

**Before selecting any pattern, answer three questions:**
1. What specific structural or behavioral problem is being solved?
2. Does the chosen pattern address it?
3. Does a simpler solution exist? (If yes — use the simpler solution.)

Always implement patterns in their most current, modern form as supported by the target ecosystem.

**Structural patterns** — Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Private Class Data, Proxy

**Behavioral patterns** — Chain of Responsibility, Command, Interpreter, Iterator, Mediator, Memento, Null Object, Observer, State, Strategy, Template Method, Visitor

**Creational patterns** — Abstract Factory, Builder, Factory Method, Object Pool, Prototype, Singleton

> The discipline is not in knowing this list. It is in knowing when each pattern applies, when a simpler solution is correct, and when a pattern would impose more structure than the problem warrants.

---

## Enforcement Checklist

**Generics (Std 65)**
- [ ] Are type errors caught at compile time rather than runtime?
- [ ] Do generic type parameter names communicate semantic meaning — not single-letter placeholders?
- [ ] Are constraints applied to restrict valid types by construction?
- [ ] Have boxing, erasure, and indirection overhead been evaluated?

**Metaprogramming (Std 66)**
- [ ] Is the metaprogramming construct as clear and concise as possible?
- [ ] Would an engineer unfamiliar with it be able to understand and modify it?
- [ ] Is it tested with the same rigor as any critical system component?

**Functional Programming (Std 67)**
- [ ] Are data structures immutable wherever possible?
- [ ] Are higher-order functions used to enable composable, reusable logic?
- [ ] Is mutable state minimized and isolated to the smallest possible region?

**OOP (Std 68)**
- [ ] Is encapsulation applied — is internal state shielded from external mutation?
- [ ] Is inheritance used only where genuine substitutability (Std 17) exists — never for code reuse alone?

**Design Patterns (Std 69)**
- [ ] Is a specific structural or behavioral problem identified that warrants a pattern?
- [ ] Does the chosen pattern directly address that problem?
- [ ] Does a simpler solution exist? (If yes — use it.)
- [ ] Is the pattern implemented in its most current, modern form?
