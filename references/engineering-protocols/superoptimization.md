# Superoptimization Protocol

Use this protocol only for hot-path, instruction-level, compiler-level,
bit-manipulation, SIMD, or micro-architectural optimization work.

## Hot Path Identification

Profile before optimizing. Identify the small region that dominates runtime.
Use tools such as hardware counters, `perf`, VTune, Cachegrind, `llvm-mca`, or
platform-specific profilers when available.

Establish baseline latency or throughput before transformation and re-profile
after each change.

## Kernel Isolation

- Extract the hot sequence into a pure function with a complete input/output
  specification.
- State the search space for equivalent sequences.
- Prune dead code, normalize commutative forms, and reduce canonical variants.
- Avoid kernels that require post-hoc output repair.

## Optimal Sequence Search

Declare the search strategy and completeness class:

- Exhaustive enumeration by increasing sequence length: complete for small k.
- Stochastic search such as STOKE-style MCMC: scalable but incomplete.
- Equality saturation with e-graphs: broad equivalence exploration plus cost
  extraction.

Example:

```text
Kernel: 32-bit popcount, x86-64
A: Loop + branch -> O(n), branchy
B: SWAR          -> O(1), portable
C: POPCNT        -> O(1), ISA-gated
Choice: POPCNT with CPUID dispatch and SWAR fallback.
```

## Equivalence Verification

- Random testing can reject candidates but does not prove equivalence.
- Formal proof via SMT can prove equivalence under a stated semantic model.
- State semantics for floating point, signed overflow, and aliasing before
  accepting a transformation.

Do not ship a speculative optimization as proven.

## Micro-Architectural Validation

- Instruction count is only a proxy.
- Model port contention, dependency chains, and vector width.
- Validate real cost on the target ISA and micro-architecture.
- Treat performance claims as machine-scoped.

## Return On Investment

Estimate yield ceiling before search: saved time per operation times frequency
times lifetime. Time-box the search and report the best result plus the known
gap to the lower bound.
