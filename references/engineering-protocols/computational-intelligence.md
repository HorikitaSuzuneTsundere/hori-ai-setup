# Computational Intelligence Protocol

Use this protocol for evolutionary computation, swarm intelligence,
metaheuristics, machine-learning search, representation design, and empirical
algorithm comparison.

## Representation Design

- Choose a representation that preserves problem geometry: binary strings,
  permutations, real-valued vectors, syntax trees, or graphs.
- Guarantee closure: operators on valid individuals should produce valid
  individuals without repair where possible.
- Evaluate genotype-phenotype redundancy and epistasis.
- State search-space cardinality before selecting an algorithm.

## Fitness Landscape Analysis

Characterize the landscape before selecting a search algorithm:

- Modality
- Ruggedness
- Neutrality
- Deceptiveness
- Funnel structure

Invoke No Free Lunch explicitly: state the structural assumption exploited by
the selected algorithm and why it likely holds.

Example:

```text
Problem: multimodal Rastrigin-class objective in R^n.
A: Gradient descent -> local, fails on deceptive landscapes.
B: CMA-ES          -> covariance-guided, O(n^2) per generation.
C: Island DE       -> diversity-preserving, O(pop * n) per generation.
Choice: Island DE when multimodality dominates.
```

## Exploration And Exploitation

- Justify population size, selection pressure, operator rates, and schedules.
- Track diversity for evolutionary algorithms.
- Distinguish underfitting from overfitting in neural systems.
- Ground PSO, ACO, and simulated annealing parameters in convergence rationale
  or peer-reviewed baselines.

## Population Diversity

- Prevent genetic drift from eliminating alternatives too early.
- Use niching, crowding, clearing, or island models for multimodal landscapes.
- Match selection pressure to landscape modality.
- Treat premature convergence without a verified optimum as a failed run.

## Hybridization

- Justify what each component uniquely provides.
- Keep global exploration and local exploitation roles explicit.
- For memetic algorithms, declare Baldwinian or Lamarckian strategy.
- Assign local-search budget as a stated fraction of total evaluations.

## Validation

- Validate against established suites where possible: CEC, BBOB, TSPLIB, UCI,
  or OpenML.
- Use at least 30 independent runs for stochastic methods.
- Report mean, median, standard deviation, and IQR.
- Use non-parametric tests such as Wilcoxon signed-rank or Friedman plus
  Nemenyi post-hoc where appropriate.
- Report solution quality separately from convergence speed.
