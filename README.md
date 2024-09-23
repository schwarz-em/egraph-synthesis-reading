# E-Graph Synthesis Reading

## Papers

### E-Graphs

- [egg: Fast and Extensible Equality Saturation](https://dl.acm.org/doi/pdf/10.1145/3434304)

### E-Graph-based synthesis

- [ESFO: Equality Saturation for FIRRTL Optimization](https://dl.acm.org/doi/abs/10.1145/3583781.3590239)
- [E-Syn: E-Graph Rewriting with Technology-Aware Cost Functions for Logic Synthesis](https://arxiv.org/html/2403.14242v1)

### E-Graphs for EDA

- [There and Back Again: A Netlist’s Tale with Much Egraphin’](https://arxiv.org/pdf/2404.00786)

### E-Graphs for RTL Optimization

- [ROVER: RTL Optimization via Verified E-Graph Rewriting](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10549954)
- [Automatic Datapath Optimization using E-Graphs](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9974492)

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

### Notes

ESFO:
- How much optimization happens between high FIRRTL and LoFIRRTL?
- This work is quite simple, just do egraph optimization on LoFIRRTL and then pass back to Yosys 
- Rewrite examples are trivial
- Greedy extraction is sometimes better than ILP, but that doesn’t make sense
- Seems to not support SRAMs, all test circuits are small

E-syn:
- Lower level Boolean optimization 
- Technology aware mapping
- Uses pooled extraction + XGBoost
- Improvement over ABC, even on small circuits
- Runtime seems high, 6 min for an adder
    - Likely due to extraction and not rewrite

Balkind:
- What is the point of hardware decompilation?
    - Deduplication?
    - Loop rerolling lacks motivation
- 2: Standard library component identification
    - This is not how component mapping is done
    - Useful for complex Boolean expressions, can map to std cells
    - BUT cell mapping does lack a good algorithm for finding global optima
- 4: egraphs for deduplication
    - FIRRTL lacks efficient deduplication, must externalize differences between modules as ports (ex hartid)
- 5: retiming
    - How to create the rewrite rules for this?
    - Won’t saturate in trivial case, need to incorporate timing engine
    - Traditional retiming is better, no point in looking for global optima

## Week 3: E-Graphs for RTL Optimization

- [ROVER: RTL Optimization via Verified E-Graph Rewriting](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10549954)
- [Automatic Datapath Optimization using E-Graphs](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9974492)
