# Paradigm Protocol

Use this protocol when selecting a programming paradigm for a module or
system, composing paradigms at module boundaries, or reviewing code for
paradigm-specific correctness.

The protocol covers three paradigms: Functional Programming (FP),
Object-Oriented Programming (OOP), and Entity Component Systems backed by
Data-Oriented Design (ECS/DoD). Generic programming and metaprogramming
discipline are governed by the EJ skills referenced below.

## Paradigm Selection Guide

Choose a paradigm by evaluating the problem across these dimensions:

| Dimension | Favors FP | Favors OOP | Favors ECS/DoD |
|---|---|---|---|
| Data shape | Uniform streams, transforms | Heterogeneous, identity-rich | Homogeneous bulk records |
| Mutation profile | Immutable by default | Encapsulated mutation | Mutation is normal and explicit |
| Access pattern | Sequential pipeline | Method dispatch, navigation | Sequential scan, random by ID |
| Entity count | Small or variable | Small to moderate | Large (thousands+) |
| Concurrency model | Message passing, shared-nothing | Lock-based, actor | Parallel system iteration |
| Hot path sensitivity | Low to moderate | Low | High (cache pressure) |

When dimensions conflict, prefer the paradigm that matches the dominant
constraint. For mixed workloads, use Hybrid Composition Rules.

## Functional Programming

### When to use

- Transformation pipelines (filter, map, reduce, fold over streams).
- Concurrency-safe cores where shared mutable state would create
  contention or correctness risk.
- Correctness-critical logic where referential transparency makes
  testing and verification tractable.
- Configuration, parsing, validation, and data-conversion layers.
- Any module where the natural expression is a sequence of
  pure transformations.

### Core discipline

1. **Immutable data structures** — values do not change after
   construction. Mutation is replaced by creating new values.
2. **Pure functions** — same input always yields same output; no
   observable side effects.
3. **Referential transparency** — any expression can be replaced by
   its value without changing program behavior.
4. **Algebraic types** — exhaustively matched sum and product types
   (Option, Result, sealed classes/tagged unions).
5. **Explicit effects** — I/O, state, and randomness are surfaced
   in the type system or confined to a known effect boundary.

### When NOT to use

- The hot path requires in-place mutation for O(1) space or
  cache efficiency that copying defeats.
- The working set under FP allocation patterns exceeds cache
  capacity and a corresponding OOP or DoD layout would fit.
- The algorithm is inherently imperative (e.g., in-place sort,
  state-space search with large visited sets).

### Pseudocode example

```text
-- Pipeline over immutable data
process(inputs):
  inputs
    |> filter(is_valid)
    |> map(transform)
    |> reduce(accumulate, initial)

-- No loop-carried mutation; each step returns a new value
```

### Cross-reference

- ej-correctness-contracts: Stds 6-9 (CQS, pure functions,
  determinism, null prohibition)
- ej-programming-paradigms: Std 67 (functional techniques)

## Object-Oriented Programming

### When to use

- Systems with identity and lifecycle (an entity is born, changes
  state over time, and may die).
- Plugin architectures, strategy patterns, or any extension point
  where callers should not depend on concrete implementations.
- GUI widget trees, layered abstractions, and frameworks that
  demand OOP structure.
- Modules where Liskov substitutability is the right contract
  (every subtype behaves like its supertype).

### Core discipline

1. **Encapsulation** — bundle data with behavior; shield internal
   state behind a stable interface.
2. **Polymorphism via interfaces** — callers depend on abstractions,
   not concrete types (Dependency Inversion Principle).
3. **Liskov Substitution** — every subtype must satisfy the
   preconditions, postconditions, and invariants of its supertype
   without surprising callers.
4. **Single Responsibility** — one reason to change per class.
5. **Composition over inheritance** — prefer has-a over is-a;
   reserve inheritance for genuine substitutability.

### When NOT to use

- The behavior is a pure data transformation with no identity or
  lifecycle — a function is simpler.
- Bulk homogeneous entities would create per-object overhead that
  defeats cache locality or allocation efficiency.
- The system has thousands of entities with no polymorphism
  (uniform behavior across all instances).
- The module boundary is a data-format boundary (serialization,
  protocol buffers, JSON) — FP or DoD often fits better.

### Pseudocode example

```text
interface Sorter:
  sort(list: List[T]) -> List[T]

class QuickSorter implements Sorter:
  sort(list): ...

class MergeSorter implements Sorter:
  sort(list): ...

-- Clients depend on Sorter, not on QuickSorter or MergeSorter
```

### Cross-reference

- ej-structure-responsibility: Stds 13-23 (SRP, OCP, LSP, ISP,
  DIP, composition, Demeter, information hiding)
- ej-programming-paradigms: Std 68 (OOP mechanisms)

## Entity Component Systems / Data-Oriented Design

### When to use

- Bulk processing of many entities with shared component types
  (game engines, simulations, ETL pipelines).
- Cache-sensitive hot paths where memory layout determines
  throughput (what is processed together must be stored together).
- Problems where entities are opaque IDs with no behavior — all
  behavior lives in systems.
- Access patterns are dominated by sequential scans over
  homogeneous component arrays.

### Core discipline

1. **Data separate from behavior** — components are plain data;
   systems contain logic. No methods on component data.
2. **SoA / archetype storage** — components of the same type are
   stored contiguously; entities with the same component set
   share an archetype.
3. **Entity as opaque ID** — an entity is an integer or GUID with
   no embedded data. Components are looked up by (entity, type).
4. **System scheduling** — systems declare their read/write sets
   and are ordered by dependency or phase to maximize cache reuse
   and eliminate data hazards.

### When NOT to use

- Entity count is small (below a cache-line or page threshold
  where per-entity overhead dominates).
- Relationships are deeply hierarchical or tree-shaped with
  heterogeneous per-node data.
- Individual entities have complex, divergent lifecycles that
  share no common component access patterns.
- Query flexibility (ad-hoc joins across component types) matters
  more than raw iteration throughput.

### Pseudocode example

```text
-- Archetype stores Position and Velocity contiguously
foreach entity in archetype(Position, Velocity):
  entity.position += entity.velocity * dt

-- System declares no knowledge of Renderable, AI, or other
-- components that entities in the same archetype may also hold
```

### Cross-reference

- ej-performance-memory: Stds 39-40 (data locality,
  data-oriented design)

## Hybrid Composition Rules

### Permitted boundary patterns

- **Pure FP core with OOP shell** — business logic is pure
  functions; OOP layer manages identity, lifecycle, and
  framework integration.
- **ECS system with FP internals** — a system iterates over
  components in DoD style, but each entity's update calls
  into pure transformation functions.
- **OOP owning ECS worlds** — a manager object encapsulates an
  ECS world and exposes high-level operations; internal storage
  follows DoD layout.

### Prohibited patterns

- Paradigm mixing inside a single function (one function must
  be either pure, OOP-method, or ECS-system — never two).
- Mutable state captured in closures passed as pure functions
  (violates referential transparency at the call site).
- OOP objects with SoA storage pretending to be ECS components
  (methods on data defeat the purpose of DoD layout).
- ECS components holding polymorphic interfaces (component data
  must be plain, not abstract).

### Rule of thumb

At every module boundary, declare the paradigm explicitly. The
boundary is the contract: a caller should not need to know whether
the callee uses FP, OOP, or ECS internally.
