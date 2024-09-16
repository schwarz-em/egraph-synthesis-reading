# E-Graph Synthesis Reading

## Papers

### E-Graphs

- [egg: Fast and Extensible Equality Saturation](https://dl.acm.org/doi/pdf/10.1145/3434304)

## Schedule

## Week 1 (9/16) - Intro to E-Graphs

- [egg: Fast and Extensible Equality Saturation](https://dl.acm.org/doi/pdf/10.1145/3434304)
- [E-graphs primer](https://www.cole-k.com/2023/07/24/e-graphs-primer)

### Notes

E-graphs
- E-graphs solve the phase ordering problem
    - Different orderings of optimizations cause different results
    - Rewrite rules can be destructive
- Apply rewrite rules to produce a simplified (optimized) solution
    - Some orderings will lead to a local minima that is not fully optimized
- Calculating all rewrite results is not optimal due to the solution set being large
- Solve this by sharing and by merging operations into equality classes (e-classes)
- E-node: an operator or a term which has a set of arguments (can be empty)
- Extraction: given an e-graph, choose a solution based on a cost function
- E-graphs can allow for 
    - Fine-grained tradeoff of optimization and runtime
    - Offline optimization, get a viable synthesis output first and improve over time

Egg
- Embedded DSL in Rust for creating egraphs w/ equality saturation
    - Extremely flexible, better than handwritten implementations
- Some features/optimizations:
    - Rebuild for congruence convergence less frequently
    - Support conditional and dynamic rewrite rules

## Week 2 - E-graph based Synthesis

- [There and Back Again: A Netlist’s Tale with Much Egraphin’](https://arxiv.org/pdf/2404.00786)
- [ESFO: Equality Saturation for FIRRTL Optimization](https://dl.acm.org/doi/abs/10.1145/3583781.3590239)
- [E-Syn: E-Graph Rewriting with Technology-Aware Cost Functions for Logic Synthesis](https://arxiv.org/html/2403.14242v1)
