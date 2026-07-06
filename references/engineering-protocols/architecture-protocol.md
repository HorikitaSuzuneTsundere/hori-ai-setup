# Architecture Protocol

Use this protocol for system design, distributed components, resilience,
resource lifecycle, external dependencies, and concurrency boundaries.

## Bottleneck First

Identify the dominant constraint before choosing a structure:

- I/O
- CPU
- Memory
- Network
- Lock contention
- Human or operational workflow

Optimization targets the bottleneck only. Non-critical-path optimization is
premature until the bottleneck is saturated or proven irrelevant.

## Pattern Comparison

Compare at least two viable patterns before committing to system structure.
Examples:

- Monolith versus microservices.
- Event-driven versus request/response.
- CQRS versus direct CRUD.
- Actor model versus shared-nothing workers.
- Stream processing versus batch processing.

State why the chosen pattern matches bottleneck, team, deployment, and
operational constraints.

## Consistency Position

For distributed components, declare the consistency model:

- Linearizable
- Strong but not globally linearizable
- Causal
- Read-your-writes
- Eventual

Also state the CAP trade-off under partition: preserve consistency, preserve
availability, or make behavior mode-dependent.

## Resource Lifecycle

- Make ownership explicit.
- Acquire and release resources deterministically.
- Centralize error handling for cross-cutting failure modes.
- Use circuit breakers or backoff policies for unreliable dependencies.
- Avoid shared mutable state across concurrent execution contexts.

## Critical Path

For every architecture decision, identify whether it affects the critical path.
Defer elaborate machinery outside the critical path unless it reduces risk,
improves operability, or removes a known bottleneck.
