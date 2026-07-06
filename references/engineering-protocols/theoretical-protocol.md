# Theoretical Protocol

Use this protocol for algorithmic work, data-structure selection, complexity
analysis, and performance claims.

## Algorithm Exploration

Before implementing a non-trivial algorithm, enumerate at least two viable
candidates. For each candidate, state:

- Worst-case, average-case, and amortized time where relevant.
- Auxiliary and total space.
- Cache behavior, including sequential versus random access and working set.
- Practical constants and expected input shape.

Identify the theoretical lower bound. If the chosen algorithm does not achieve
it, document the gap and whether closing it is tractable.

Example:

```text
Problem: kth largest in unsorted array of n
A: Sort + index      -> O(n log n), O(1) aux
B: Heap of size k    -> O(n log k), O(k) aux; strong when k << n
C: Introselect       -> O(n) expected or worst-case by variant, O(1) aux
Choice: Introselect when mutation is allowed. Lower bound: Omega(n).
```

## Data Structure Selection

No significant data structure should be chosen by habit. Evaluate:

- Access pattern: read/write ratio, sequential versus random, hot/cold paths.
- Operation dominance: lookup, insert, delete, range, rank, union, iteration.
- Memory layout: locality, pointer chasing, AoS versus SoA, heap versus arena.
- Concurrency profile: read-heavy, write-heavy, contention, ownership.

Prefer cache-friendly and operation-optimal structures for the observed access
profile.

## Complexity Annotation

Annotate non-trivial or reusable algorithms where the bound affects usage.

```text
Time:  O(log n) worst-case, O(1) amortized for cache refresh.
Space: O(1) auxiliary.
Cache: O(log_B n) I/Os in the disk model with block size B.
Lower: Omega(log n) comparison-based lookup; optimal.
```

Do not clutter routine application glue with formal annotations unless the
complexity is surprising or relevant to callers.

## Proactive Efficiency

- Surface known superior algorithms or data structures.
- Flag suboptimal complexity, poor locality, missed vectorization, unnecessary
  locking, or mismatched data structures.
- Prefer iterative transformations over recursion when stack behavior matters.

## Benchmarking

Every performance claim needs measurement.

- Distinguish throughput from latency percentiles.
- Validate empirical curves against expected complexity.
- Account for JIT warm-up, cache state, branch predictors, CPU scaling, and
  NUMA effects where relevant.
- Do not claim code is fast without a number and a measurement method.
