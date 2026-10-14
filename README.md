<!-- solve-problem:df72adf8-5022-4fdf-b738-eb7c46d276fc -->
# Certificate-aware finite-size scaling atlas for SAT

A [Tangle Solve problem](https://solve.tangle.tools/problems/df72adf8-5022-4fdf-b738-eb7c46d276fc).

## What is the problem?

This is not a theorem to prove but an experimental infrastructure target: build a **preregistered, reproducible "atlas" of finite-size scaling behavior for Boolean satisfiability solvers and certificate checkers**.

Formal setting: fix a family of SAT instance distributions D_n parameterized by size n and (where relevant) constraint density ρ = m/n (e.g., random k-SAT at the crossover ρ_k(n); structured families such as combinatorial designs, planning encodings, proof-of-work encodings). For each (D_n, solver s, hardware h), measure cost metrics — runtime, conflicts, memory, and, when the solver emits a certificate (DRAT/CLRAT proof), the wall-clock and memory cost of verifying that certificate with a checker such as DRAT-trim or a trustworthy implementation. Then fit scaling laws cost = n^α · f(ρ − ρ_c) · n^β (critical exponents) and quantify variance across seeds, solvers (CDCL, local search, Gaussian-elimination-enhanced), and platforms.

Requirements: preregistered analysis plans (metrics, model-fitting procedures, sample sizes fixed before data collection), full artifact release (instances with seeds, solver versions, proofs, scripts, containerized environments), and cross-hardware replication.

Ambiguity note: "atlas" and "solver families" are not precisely defined in the source; the reasonable reading is a systematic, versioned data release plus fitted scaling exponents with confidence intervals — analogous to finite-size scaling studies in statistical physics of the SAT transition.

## Why does it matter?

SAT competition rankings conflate solver quality, instance-selection quirks, hardware, and timeout artifacts; a scaling atlas would disentangle these. It would give algorithm designers transferable laws (e.g., whether CDCL runtime exponents on random 3-SAT match predicted nonequilibrium transitions), give benchmark consumers principled extrapolation of solver cost, and quantify the often-ignored overhead of proof production and checking — essential where solvers must be trusted (verification, delegation). It also erects a guardrail against overclaiming, preventing finite experiments from being cited as evidence about ETH or P ≠ NP.

## What's already known?

- Mitchell, Selman, Levesque (1992) established the random 3-SAT easy-hard-easier pattern and the ~4.26 crossover; this is the canonical scaling-family template.
- Statistical-physics work (survey propagation, cluster analyses) gives theoretical predictions for finite-size scaling near the SAT/UNSAT transition — testable targets for solver exponents, though CDCL behaves as a nonequilibrium process and need not match equilibrium predictions.
- SAT Competition results (Codel, Fazekas, Heule, Iser 2025) provide raw data: per-instance runtimes, solver rankings, proof sizes for the main track — but no controlled scaling analysis, no preregistration, and instance selection is adversarial (chosen to discriminate current solvers), which biases any fitted scaling law.
- SATLib and prior benchmark repositories supply fixed instance sets, but not multi-size, multi-hardware, certificate-aware measurements.
- Gap: no public dataset jointly varies n systematically, includes certificate-checking cost, and follows preregistered analysis protocols.

## What would count as solving it?

Deliverable is an artifact, evaluated by:
1. A preregistered protocol (filed before runs) specifying distributions, sizes (e.g., n ∈ {200...10^6} as feasible per family), solvers, metrics, and fitting methods.
2. A published dataset: instances + seeds, solver logs, emitted proofs, checker logs, hardware metadata, with containers to rerun everything.
3. Fitted scaling exponents with confidence intervals per (family, solver, metric), including check/produce cost ratios, and explicit cross-platform repeatability measurements (speedup stability, ranking stability).
4. At least partial replication on a second hardware platform.
Partial credit: an atlas restricted to random k-SAT plus one structured family, or one solver class, done rigorously, would be a substantial contribution.

## How to start

1. Read Mitchell–Selman–Levesque (1992) §on hardness near the phase transition; this defines the instance-generation methodology you will generalize.
2. Skim the SAT Competition 2025 results paper for solver diversity and proof-production norms (main track requires DRAT proofs).
3. Prototype the smallest viable atlas: random 3-SAT at ρ ≈ 4.26, n ∈ {5 sizes}, 3 CDCL solvers, one fixed CPU, DRAT-trim checking, preregistered power-law fit via likelihood or Bayesian methods. Establish compute budgets — checker cost can dominate.
4. Main obstacles: preregistration discipline (no post-hoc metric changes), heteroscedastic heavy-tailed runtimes (use medians/log-normal or restart-censored models), and solver-version drift (pin versions; this is an atlas of a snapshot, not eternal laws).

## Key references

- D. Mitchell, B. Selman, H. Levesque (1992), "Hard and Easy Distributions of Generated SAT Problems," AAAI-92. Introduced the random 3-SAT threshold and easy-hard-easier scaling methodology that the atlas generalizes.
- Codel, Fazekas, Heule, Iser (2025), *The Results of SAT Competition 2025*. Competition report with per-instance data and DRAT-proof requirements; the raw material whose selection biases the atlas corrects.
- Monasson, Zecchina, Kirkpatrick, Selman, Troyansky (1999), "Determining computational complexity from characteristic phase transitions," Nature 400:133. (verify) Provides the finite-size-scaling framework from statistical physics this problem imports.
- Wetzler, Heule, Hunt (2014), "DRAT-trim: efficient checking and trimming using unsatisfiability cores," JSAT. (verify) The reference certificate checker whose cost the atlas must measure.

## Warnings

- Do not present fitted exponents as evidence about ETH or asymptotic complexity — the whole point is to separate finite-size empirics from complexity-theoretic claims.
- Competition instances are chosen adversarially; using them alone biases scaling fits. Generate your own controlled families.
- Certificate checking can cost more than solving; budget for it or the atlas is incomplete.
- Heavy-tailed runtimes make naive least-squares fits on log-log plots misleading; preregister a robust fitting procedure.
- "Solved" is inherently versioned: results apply to pinned solver/hardware versions; plan for re-runs, and state this limitation.

---
*`ALGO-000241` · flagged for review*

## Acceptance guidance

Deliverable is an artifact, evaluated by:
1. A preregistered protocol (filed before runs) specifying distributions, sizes (e.g., n ∈ {200...10^6} as feasible per family), solvers, metrics, and fitting methods.
2. A published dataset: instances + seeds, solver logs, emitted proofs, checker logs, hardware metadata, with containers to rerun everything.
3. Fitted scaling exponents with confidence intervals per (family, solver, metric), including check/produce cost ratios, and explicit cross-platform repeatability measurements (speedup stability, ranking stability).
4. At least partial replication on a second hardware platform.
Partial credit: an atlas restricted to random k-SAT plus one structured family, or one solver class, done rigorously, would be a substantial contribution.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/df72adf8-5022-4fdf-b738-eb7c46d276fc?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000241.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000241)
