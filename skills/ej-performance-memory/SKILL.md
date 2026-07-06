---
name: ej-performance-memory
description: Enforce EJ Coding Standards Section V — Performance & Memory (Standards 35–44). Covers algorithm paradigm selection, O(1) design targets, algorithmic efficiency, hot path optimization, data locality, data-oriented design, abstraction discipline, bit manipulation, memory determinism, and memory footprint reduction.
license: MIT
compatibility: opencode
---

## What I do

I apply Standards 35–44 of the EJ Coding Standards when writing, profiling, or optimizing code. I enforce performance and memory discipline from algorithm selection through memory lifecycle.

## When to use me

Use me when:
- Selecting an algorithm or data structure for a problem
- Evaluating time complexity or targeting O(1) execution
- Optimizing hot paths based on profiling data
- Designing data structures for cache efficiency or data-oriented access patterns
- Managing memory allocation lifecycles or reducing memory footprint
- Applying bit manipulation or parallelism for raw performance

---

## Standards

### Standard 35 — Algorithm Paradigm Selection
Every problem must be matched to the appropriate algorithm family before implementation begins.

| Paradigm | Mechanism | Typical Complexity |
|---|---|---|
| **Brute Force** | Exhaustive evaluation; correctness baseline | Varies |
| **Divide and Conquer** | Split → solve → merge | O(n log n) |
| **Dynamic Programming** | Memoize overlapping subproblems | Polynomial |
| **Greedy** | Locally optimal incremental choices | Fast; verify global optimality |

The chosen paradigm must be justified against the structural properties of the problem.

### Standard 36 — Constant-Time Design Target
All functions must be designed with O(1) time complexity as the explicit goal. Every function must at minimum be evaluated for the possibility of achieving constant-time execution. When O(1) is not achievable, the departure must be deliberate, documented, and minimized.

> Standard 36 is a complexity-theoretic *target* applied at every function. Standard 37 governs efficiency within whatever complexity class is chosen.

### Standard 37 — Algorithmic Efficiency
Within whatever complexity class is chosen, eliminate all redundant operations and use the most efficient data structures the problem permits:
- **Hash tables** — O(1) average-case lookup
- **Arrays** — cache-friendly sequential traversal
- **Balanced trees** — ordered operations with guaranteed O(log n) bounds

### Standard 38 — Hot Path Optimization
Optimization effort must be concentrated on hot paths — the code paths that execute most frequently. Cold paths must not be prematurely optimized. Profile first. Optimize only what profiling confirms is the actual bottleneck. **Optimization without measurement is speculation.**

### Standard 39 — Data Locality *(physical memory constraint)*
Organize data in memory so that what is processed together is stored together. Cache hit ≈ 4 cycles; main-memory access ≈ 200–300 cycles. True performance is achieved by maximizing CPU cache utilization more than by reducing theoretical algorithmic complexity. A cache miss is not a minor inconvenience; it is a performance catastrophe at frequency.

> Standard 39 is the physical hardware constraint. Standard 40 is the design philosophy that produces this outcome.

### Standard 40 — Data-Oriented Design *(design philosophy)*
Think in terms of data flow and transformation, not object hierarchies and class trees. Memory layout is the first algorithm: before writing any logic, design data structures around how they will be traversed and transformed in the critical path. The structure of data determines the structure of code — not the reverse.

### Standard 41 — Abstraction Discipline
Two inseparable rules govern all abstraction:
1. **Prefer direct implementations** over layered abstraction when those layers add depth without contributing to correctness, clarity, or genuine reuse.
2. **Abstraction must impose zero runtime overhead** — abstractions must vanish at the compilation or build stage. Any abstraction that costs measurable CPU cycles at runtime is an indirection tax, not an abstraction.

> Standard 54 (Quality & Longevity) makes the *positive case* for abstraction. Standard 41 constrains *how* it must be applied.

### Standard 42 — Bit Manipulation and Parallelism
Bit manipulation and parallelism are the two most important techniques for achieving maximum execution speed when algorithmic improvements are insufficient:
- **Bitwise operations** — replace expensive arithmetic with single-instruction equivalents
- **Parallelism** — eliminate serial bottlenecks by executing independent operations concurrently

### Standard 43 — Memory Determinism
Every memory allocation and deallocation must be knowable, predictable, and fully accounted for before the code runs. No surprise heap growth, no unbounded allocation in critical paths, no reliance on garbage collection timing for correctness. The lifecycle of every byte must be determinable by reading the code.

> Standard 43 governs *when and where* memory is allocated — lifecycle and predictability. Standard 44 governs *how much* total memory is consumed.

### Standard 44 — Memory Footprint Reduction
Actively minimize the total memory consumed by the program at runtime. Eliminate redundant allocations, remove unnecessary copies of data, apply loop unrolling to reduce loop control overhead, and avoid allocating more capacity than the problem strictly requires. Less memory consumed means more of the working set fits in the CPU cache, directly multiplying the benefits of Standard 39.

---

## Enforcement Checklist

- [ ] Has the algorithm paradigm been explicitly selected and justified? (Std 35)
- [ ] Was O(1) considered and either achieved or consciously rejected with documentation? (Std 36)
- [ ] Are the most efficient data structures used for the access pattern? (Std 37)
- [ ] Is optimization focused on profiled hot paths — not cold paths? (Std 38)
- [ ] Is data that is processed together stored together? (Std 39)
- [ ] Are data structures designed around traversal patterns, not conceptual elegance? (Std 40)
- [ ] Does any abstraction impose measurable runtime overhead? (Std 41 — eliminate it)
- [ ] Have bit manipulation or parallelism been evaluated when raw speed is the constraint? (Std 42)
- [ ] Is the lifecycle of every allocation determinable by reading the code? (Std 43)
- [ ] Have redundant allocations and unnecessary copies been eliminated? (Std 44)
