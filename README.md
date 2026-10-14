<!-- solve-problem:5bdc905b-0e46-4828-bc40-95bd4df4219f -->
# An FPRAS for #BIS

A [Tangle Solve problem](https://solve.tangle.tools/problems/5bdc905b-0e46-4828-bc40-95bd4df4219f).

## What is the problem?

**#BIS** is the problem of counting independent sets in a **bipartite** graph. Input: a bipartite graph G = (V₁, V₂, E). Output: |I(G)|, the number of subsets S ⊆ V₁ ∪ V₂ containing no edge of E. Equivalently, the hard-core partition function Z_G(λ) at fugacity λ = 1.

The question: does #BIS admit an **FPRAS** — a randomized algorithm that, given G and ε > 0, outputs Ź with Pr[(1−ε)Z ≤ Ź ≤ (1+ε)Z] ≥ 3/4, running in time poly(|G|, 1/ε)?

Precise interpretation of "solving": either (a) construct such an algorithm, or (b) prove none exists under a standard complexity assumption (most naturally: #BIS is #SAT-hard to approximate, i.e., no FPRAS unless NP = RP or the RHGP/randomized hierarchy collapses). The problem sits strictly between the known classes in the approximate-counting trichotomy of Dyer–Goldberg–Greenhill–Jerrum: it is not known to have an FPRAS (unlike #Matchings-type problems) and not known to be #SAT-hard to approximate (unlike counting independent sets in general graphs).

## Why does it matter?

#BIS is the canonical "intermediate" problem in approximate counting: dozens of problems (counting proper q-colorings on bipartite graphs, counting downsets, certain spin systems, truth assignments of CNFs of monotone 2-SAT variants) are known either interreducible with it under approximation-preserving (AP) reductions or caught in the same gap. Resolving it would collapse or populate the entire class #RHΠ₁ (a.k.a. #BIS-equivalent class), the main unclassified region of the approximate counting landscape, and would settle the approximability of hard-core partition functions on bipartite graphs at λ = 1, a benchmark case in statistical mechanics and sampling algorithm design (Glauber dynamics, etc.).

## What's already known?

- Dyer, Goldberg, Greenhill, Jerrum (2004) set up the AP-reduction framework, showed counting independent sets in **general** (degree ≥ 6) graphs is #SAT-hard to approximate, that #BIS is in the intermediate class #RHΠ₁, and initiated the study of its status. No FPRAS and no hardness for #BIS was found.
- AP-interreducibility: many natural problems are #BIS-equivalent — counting downsets in posets, counting 2-spin configurations related to "ferromagnetic-ish" systems on bipartite inputs, counting q-colorings of bipartite graphs for certain regimes (Cevallos, Vigoda et al., partial results — verify exact statements), vertex covers (trivially, via complement, #BIS is the same problem).
- MCMC/sampling: Glauber dynamics for the hard-core model on bipartite graphs at λ = 1 has no known rapid mixing proof in general (and the tree-hardness threshold λ_c does not separate bipartite from general); on general graphs the dynamics fails at strong spatial mixing thresholds (Sly, 2010: hardness above threshold). For **bipartite** graphs λ = 1 is far below any known hardness threshold, yet no polynomial mixing bound is known — this is the main algorithmic gap.
- Spectral independence (Anari, Oveis Gharan, Rezaei; Chen, Liu, Vigoda) gives rapid mixing when the tree recurrence is contractive; at λ = 1 on arbitrary-degree bipartite graphs it does not apply.
- Curticapean et al. (arXiv:1702.05543): complexity-theoretic classification of counting (Holant problems, subgraph counting), sharpening the landscape around #BIS but leaving it open.
- Combinatorial/parametrized approaches, deterministic approximation via correlation decay on bounded-degree graphs succeed, but unbounded bipartite graphs remain open.

## What would count as solving it?

1. **Positive:** an algorithm A(G, ε) with the FPRAS guarantee above, poly-time in |V|+|E| and 1/ε, for all bipartite G. A referee accepts a proof of correctness and polynomial running time (e.g., a proof that a Markov chain on independent sets of bipartite graphs mixes in poly time, plus standard reduction from counting to sampling via simulated annealing/self-reducibility).
2. **Negative:** an AP-reduction from a #SAT-hard-to-approximate problem (e.g., #IndependentSets on general graphs) to #BIS — equivalently, showing #BIS is #SAT-hard under AP-reductions. A referee accepts a correct construction; the conclusion "no FPRAS unless NP = RP" then follows from known results.
3. **Partial credit variants:** FPRAS restricted to a subclass (e.g., λ < 1 general; bounded degree; λ = 1 with separator structure) or a proof that #BIS does/doesn't lie in a natural subclass like #RHΠ₁ ∩ something. These are publishable but do not close ALGO-000139.

## How to start

1. Read Dyer–Goldberg–Greenhill–Jerrum (2004) fully — Sections on AP-reductions and #RHΠ₁ define exactly what counts as an answer and catalogue #BIS-equivalent problems.
2. Master the sampling side: Chen–Liu–Vigoda's spectral independence survey/framework. The obvious attack is: try to prove spectral independence or some block-dynamics contraction for hard-core at λ = 1 on bipartite graphs. Main obstacle: bipartiteness gives no known leverage — the mixing witnesses (high-degree hubs) that break spectral independence exist in bipartite graphs too; the conjecture is that bipartiteness alone should help, but no mechanism is known. Understanding *why* it might not help (potential counterexample structures, near-extremal bipartite graphs) is valuable.
3. On the hardness side, understand why naive AP-reductions fail: converting a general graph to bipartite while approximately preserving independent-set counts is exactly what's failed for 20 years. Look at Holant-theoretic classifications (Curticapean et al., arXiv:1702.05543) for obstructions.
4. Consider intermediate questions: FPRAS for #BIS on graphs of max degree Δ for larger and larger Δ (currently only small Δ via correlation decay), or derandomization connections.

## Key references

- Dyer, Goldberg, Greenhill, Jerrum, "The Relative Complexity of Approximate Counting Problems," *Algorithmica* (2004), DOI: 10.1007/s00453-003-1073-y. Defines AP-reductions, classifies counting problems into #SAT-hard, FPRAS-solvable, and #RHΠ₁ (where #BIS is the canonical complete problem); proves the general-graph hardness results.
- Curticapean, Dell, Fomin, Goldberg, Lapinskas, "A Fixed-Parameter Perspective on #BIS," arXiv:1702.05543 (verify author list/venue; this may be the "Complexity of counting subgraphs" line — check whether the cited arXiv ID is the FPT-for-#BIS paper or a subgraph-counting dichotomy paper). Studies #BIS through fixed-parameter and Holant lenses; relevant classification machinery.
- Chen, Liu, Vigoda, "Optimal mixing of Glauber dynamics: entropy factorization via high-dimensional expansion," *Annals of Mathematics* (2021). The state of the art for proving rapid mixing of hard-core dynamics; explains the exact barrier at λ = 1 for general graphs.
- Sly, "Computational transition at the uniqueness threshold," FOCS 2010. Shows hardness of approximating the hard-core partition function above the tree uniqueness threshold — the reference point for why no hardness is expected/plausible at λ = 1.

## Warnings

- "Bipartite" is essential: general graphs are hard at degree ≥ 6 (DGGJ) and at large λ (Sly); do not cite those as resolving the bipartite case.
- #BIS = #VertexCover on bipartite graphs by complementing independent sets — the same open problem, often restated.
- Beware of "obvious" FPRAS attempts: Glauber dynamics mixing on bipartite graphs at λ = 1 is itself open, so sampling-based attacks require genuinely new mixing ideas.
- Partial results on bounded degree or λ < 1 do not solve the problem; the census question is unrestricted bipartite graphs, λ = 1.
- Verify the exact content and authorship of arXiv:1702.05543 before relying on it (see above).

---
*`ALGO-000139` · unverified*

## Acceptance guidance

1. **Positive:** an algorithm A(G, ε) with the FPRAS guarantee above, poly-time in |V|+|E| and 1/ε, for all bipartite G. A referee accepts a proof of correctness and polynomial running time (e.g., a proof that a Markov chain on independent sets of bipartite graphs mixes in poly time, plus standard reduction from counting to sampling via simulated annealing/self-reducibility).
2. **Negative:** an AP-reduction from a #SAT-hard-to-approximate problem (e.g., #IndependentSets on general graphs) to #BIS — equivalently, showing #BIS is #SAT-hard under AP-reductions. A referee accepts a correct construction; the conclusion "no FPRAS unless NP = RP" then follows from known results.
3. **Partial credit variants:** FPRAS restricted to a subclass (e.g., λ < 1 general; bounded degree; λ = 1 with separator structure) or a proof that #BIS does/doesn't lie in a natural subclass like #RHΠ₁ ∩ something. These are publishable but do not close ALGO-000139.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/5bdc905b-0e46-4828-bc40-95bd4df4219f?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000139.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000139)
