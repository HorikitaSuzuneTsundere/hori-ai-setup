---
name: ej-code-format-constraints
description: Enforce EJ Coding Standards Section IV — Code Format & Structural Constraints (Standards 26–34). Covers function size (13–15 lines), one statement per line, 80-character row limit, minimal scope declaration, no boolean arguments, no recursion in imperative code, fixed upper bound loops, self-documenting code, and explicit-over-implicit design.
license: MIT
compatibility: opencode
---

## What I do

I apply Standards 26–34 of the EJ Coding Standards when writing or reviewing source code. I enforce structural shape and formatting discipline at the line and function level.

## When to use me

Use me when:
- Writing new functions and checking their size, line structure, or scope discipline
- Reviewing code for boolean parameters, recursion in imperative paths, or unbounded loops
- Enforcing the 80-character line limit or single-statement-per-line rule
- Evaluating whether intent is communicated by structure and naming rather than comments
- Checking for implicit behavior, hidden hooks, or undocumented defaults

---

## Standards

### Standard 26 — Function Size Constraint
Functions must contain **13 to 15 lines of code**. No function may span more than a single visible page. This is not a style preference — it is a structural discipline. A function that cannot be expressed within this limit is performing more than one responsibility, contains hidden complexity, or lacks adequate decomposition.

### Standard 27 — One Statement and One Declaration Per Line
Each line of source code must contain exactly one statement or exactly one declaration — never both, and never multiples of either. Multi-statement lines obscure intent, complicate debugging, and reduce readability at the exact points where clarity matters most. One thought per line. No exceptions.

### Standard 28 — 80-Character Row Limit
No line of source code may exceed 80 characters in width. A line that exceeds this limit signals excessive nesting, overlong expressions, chained operations that should be decomposed, or identifiers that should be renamed. The limit enforces structure; it surfaces complexity rather than constraining screen real estate.

### Standard 29 — Minimal Scope Declaration
Every variable, data object, and identifier must be declared at the smallest scope in which it is actually needed — and no broader. No variable should outlive its purpose. Scope is the first form of access control: the narrower the scope, the less anything outside it can depend on or corrupt that variable.

### Standard 30 — No Boolean Arguments
Functions must not accept boolean flags as parameters. A boolean argument always signals that the function contains at least two distinct behaviors and must be split into two separate, explicitly named functions.

❌ `process(data, true)` — communicates nothing
✅ `processWithValidation(data)` / `processRaw(data)` — communicates everything

### Standard 31 — No Recursion in Imperative Code
All control flow in imperative code must use iteration, not recursion. No function may call itself directly or indirectly within an imperative context. Recursion in imperative code makes stack depth unpredictable, violates statically bounded execution, and makes formal termination analysis impossible. Where a recursive structure is natural, convert it to an iterative one with an explicit stack.

> This standard applies strictly to imperative control flow. Standard 67 (Programming Paradigms) recognizes recursion as idiomatic within the functional paradigm — genuinely different contexts, not a contradiction.

### Standard 32 — Fixed Upper Bound Loops
Every loop must have a statically determinable upper bound — an upper limit on the number of iterations that can be established by reading the code, without executing it. Unbounded iteration admits infinite execution and cannot be formally reasoned about.

### Standard 33 — Self-Documenting Code
Code must communicate its intent through structure, naming, and design — not through comments. Minimize comments to the absolute minimum necessary. A comment that restates what the code does is evidence of a clarity failure in the code itself. When a comment seems necessary, first ask whether a better name or smaller function would eliminate the need for it.

### Standard 34 — Explicit Over Implicit
All behavior must be visible in the source. Nothing should occur through convention, hidden framework lifecycle hooks, implicit type coercions, or undocumented defaults not traceable by reading the code directly. If something happens, the reader must be able to see it happen.

---

## Enforcement Checklist

- [ ] Is the function 13–15 lines? (Std 26)
- [ ] Is there exactly one statement or declaration per line? (Std 27)
- [ ] Does every line stay within 80 characters? (Std 28)
- [ ] Is every variable declared at the narrowest possible scope? (Std 29)
- [ ] Does any function accept a boolean parameter? (Std 30 — split if yes)
- [ ] Does any imperative code use recursion? (Std 31 — convert to iteration)
- [ ] Does every loop have a statically determinable upper bound? (Std 32)
- [ ] Is intent communicated by structure and naming rather than comments? (Std 33)
- [ ] Is all behavior explicitly visible — no hidden hooks or implicit coercions? (Std 34)
