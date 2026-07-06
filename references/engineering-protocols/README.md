# Engineering Protocols Reference

These protocols are advisory reference material for high-rigor software work.
They are not unconditional instructions for every task. Apply them
proportionally to task risk, complexity, and performance sensitivity.

Use this reference for:

- Non-trivial implementation or refactoring.
- Algorithm and data-structure selection.
- Architecture and distributed-system design.
- Performance-sensitive or memory-sensitive code.
- Correctness, security, resilience, and code review.
- Computational intelligence or superoptimization work.

Escalation model:

- Routine edits: preserve safety, correctness, minimality, and tests.
- Non-trivial code: compare viable approaches and document trade-offs.
- Architecture: identify bottlenecks, consistency model, and lifecycle risks.
- Performance work: profile first, measure after, and state the target machine.
- Research-grade optimization: require proof, benchmarks, and reproducibility.

Files:

- `core-engineering.md`: engineering laws, correctness, simplicity, security.
- `theoretical-protocol.md`: algorithms, data structures, complexity, benchmarks.
- `architecture-protocol.md`: system design, bottlenecks, consistency, resilience.
- `paradigm-protocol.md`: paradigm selection, FP, OOP, ECS/DoD, hybrid composition.
- `computational-intelligence.md`: EC/ML/search representations and validation.
- `superoptimization.md`: hot paths, equivalence, machine validation.
