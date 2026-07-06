---
name: ej-architecture-resilience
description: Enforce EJ Coding Standards Section VI — Architecture & Resilience (Standards 45–49). Covers stateless design with explicit caching, deterministic resource lifecycle management, centralized error handling, the circuit breaker pattern for external dependencies, and concurrency isolation and safety.
license: MIT
compatibility: opencode
---

## What I do

I apply Standards 45–49 of the EJ Coding Standards when designing, building, or reviewing system architecture. I enforce stateless components, deterministic resource ownership, centralized error routing, circuit breakers, and structurally safe concurrency.

## When to use me

Use me when:
- Designing or reviewing stateless services, distributed components, or microservices
- Implementing resource acquisition/release patterns (files, connections, locks, threads)
- Designing error handling architecture — routing, logging, recovery, escalation
- Adding resilience to external dependency calls (circuit breakers, retry logic)
- Writing concurrent code involving shared state, threads, or async workers

---

## Standards

### Standard 45 — Stateless Design with Caching
Systems and components must remain stateless by default: they must not hold persistent mutable state between invocations. All required state must be passed in explicitly as input or retrieved from a dedicated, explicit caching layer. The caching layer — not the component — owns and manages system state. Stateless components are independently scalable, trivially redeployable, and free from bugs caused by hidden residual state contaminating subsequent executions.

```
Request → Stateless Component → [reads/writes] → Explicit Cache/Store
                                                        ↑ owns state
```

### Standard 46 — Resource Management
Every acquired resource must have an explicit, deterministic lifecycle: **acquire → use → release**.

Governed resources: file handles, network connections, memory allocations, database connections, locks, threads, socket descriptors.

- Resources must not be left open, leaked, or implicitly relied upon for cleanup by the runtime
- Release must be guaranteed regardless of whether the code path succeeded or failed (finally blocks, destructors, defer statements, or equivalent)
- Every resource has an explicit owner, and that owner is responsible for its complete lifecycle

### Standard 47 — Centralized Error Handling
All error control flow must be routed through a single, centralized error-handling mechanism — not scattered across every function that might fail. Error handling logic lives in one place: logging, recovery, escalation, translation, user notification. Distributed error handling produces inconsistent behavior, duplicated logic, and errors handled differently depending on which call path encountered them first.

> Standard 47 governs *where* error handling code lives architecturally.
> Standard 12 (Correctness & Contracts) governs *what the system does* at failure points — graceful degradation and fault tolerance.

### Standard 48 — Circuit Breaker Pattern
Systems that call external dependencies must implement the circuit breaker pattern explicitly.

**State machine:**
- **CLOSED** — calls pass through normally; failure count is tracked
- **OPEN** — failures exceeded threshold; calls are immediately short-circuited for a defined recovery window; no queueing, no unbounded retries
- **HALF-OPEN** — recovery window elapsed; a probe call is attempted; success → CLOSED, failure → OPEN

Circuit breakers are the primary architectural mechanism for preventing cascading failures across distributed system boundaries where a slow or failing dependency would otherwise exhaust the caller's resources entirely.

> Standard 48 is a specific named pattern for a specific failure mode: repeated dependency failures causing system-wide degradation through resource exhaustion.
> Standard 12 is general robustness — the system handles failures gracefully.

### Standard 49 — Concurrency Isolation and Safety
Each concurrent unit of execution must own its state exclusively — shared mutable state between threads or concurrent workers is prohibited wherever it can be avoided. Isolation is the primary design principle; locks are the mechanism of last resort. When shared state is unavoidable, all access must be explicitly synchronized. Code must be designed to eliminate race conditions and deadlocks by construction rather than by careful threading discipline alone. **Concurrency errors must be prevented structurally, not caught in testing.**

Preferred designs (in order):
1. No shared state (message passing, actor model)
2. Immutable shared state
3. Explicitly synchronized mutable shared state with minimal lock scope

---

## Enforcement Checklist

- [ ] Does the component hold no persistent mutable state between invocations? (Std 45)
- [ ] Is all state owned and managed by an explicit, dedicated caching layer? (Std 45)
- [ ] Does every acquired resource have an explicit acquire → use → release lifecycle? (Std 46)
- [ ] Is resource release guaranteed even on failure code paths? (Std 46)
- [ ] Is all error handling routed through a single centralized mechanism? (Std 47)
- [ ] Do all external dependency calls implement the circuit breaker pattern? (Std 48)
- [ ] Are circuit breaker thresholds and recovery windows explicitly defined? (Std 48)
- [ ] Does each concurrent unit own its state exclusively? (Std 49)
- [ ] If shared state is unavoidable, is all access explicitly synchronized? (Std 49)
- [ ] Are race conditions and deadlocks prevented structurally — not just tested for? (Std 49)
