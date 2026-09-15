# pCHA — p-adic Categorical Hyperchaos Approximation

A deterministic forecasting engine for chaotic dynamical systems in the 
extreme-data-starvation regime. pCHA reconstructs long-horizon trajectories 
(up to T = 50 Lyapunov time units) from as few as 15 observed points, 
without access to the governing equations (zero RHS). It is formulated in 
the p-adic ultrametric state space Q_p³ and organized categorically through 
local charts and their transitions. The method is proprietary; 
reproducibility is provided through a public blind-test protocol.

---

## Key Results

### The Wall of Chaos

Across 117 systems from the dysts benchmark, pCHA maintains > 97% PASS 
rate at ε = 0.01 and > 70% at ε = 0.001. Among global and neural baselines 
(ESN, MLP, NVAR, Transformer, SINDy, EDMD, LinearStateMap), all collapse 
below 10% at ε = 0.01 and to zero at ε = 0.001. Persistence and NeuralODE — 
the two strongest non-pCHA methods — reach 33% at ε = 0.01 and drop below 
10% at ε = 0.001. Full table in 
`results/dysts_summary_multi_threshold.csv`.

*Figure 1: PASS rate vs. accuracy threshold ε.*

### Data-Volume Invariance

On a 20-system synthetic benchmark, pCHA holds 100% PASS rate and median 
max-error below 6 × 10⁻⁴ from n_train = 200 down to n_train = 15. 
Persistence drops to 90% at n_train = 15; all ML baselines remain at 0% 
across the entire range.

A separate threshold study extends the range further: at n_train ∈ {5, 10, 
15}, pCHA remains at 100% PASS rate with bounded error and without 
divergence, NaN, or blow-up. This study was conducted for pCHA only; no 
baseline comparison was performed at these training sizes.

*Figure 6: Median max-error vs. n_train, log scale. Full data in 
`results/synthetic_n_train_summary.csv`.*

### Real-World Data

Seven datasets: SantaFe laser, OMNI (space weather), AAPL, MSFT, GOOGL, 
SPY, ECG. At ε = 0.1σ, pCHA passes all seven. At ε = 0.01σ, it passes 
six of seven; the single failure is MSFT. All ML baselines fail 
universally. Full data in `results/real_world_benchmarks.csv`.

---

## Declared Scope

pCHA is applicable to:

- deterministic, bounded, continuous-time dynamical systems;
- smooth or piecewise-smooth flow (locally Lipschitz);
- scalar or low-dimensional series (1D–3D directly, or higher through a 
  standard delay embedding);
- stationary or quasi-stationary dynamics.

Outside this scope (discontinuous systems, stochastic systems, 
non-stationary data, dimension > 3 without an established embedding), 
no claims are made.

**pCHA does not solve chaos forecasting in general.** It demonstrates 
strong empirical performance within the declared scope. Results outside 
the scope are neither claimed nor implied.

A documented in-scope failure exists: ScrollDelay (delay-differential 
system with discontinuous nonlinearity) is not predicted (median 
max-error 0.52 at n_train = 200). This is reported without modification 
because it delimits the method's applicability.

---

## Verification

pCHA accepts independent verification under the terms of 
[`blind_test_protocol.md`](./blind_test_protocol.md):

- verifiers are selected by the community, not by the author;
- the author has no veto over nominations;
- submissions are accepted first-come, first-served within the declared 
  scope;
- a public registry records every submission;
- all results — including failures — are published;
- the metric, thresholds, scope, and filter are fixed in advance and are 
  not modified after test data is received.

The protocol is the single authoritative statement of verification terms. 
It is not summarized, extended, or modified by this README.

A separate commercial channel exists for organizations seeking private 
evaluation under NDA, and does not affect access to the public protocol. 
Contact below.

---

## What Is Open, What Is Closed

**Open:**

- the mathematical framework (`theory.md`);
- the verification protocol (`blind_test_protocol.md`);
- all benchmark data as aggregated CSVs (`results/`);
- all figures as PNG and PDF (`results/figures/`).

**Closed (proprietary):**

- the choice of prime p and its precision;
- the p-adic embedding;
- the construction of the categorical structure C_p;
- the morphism-extension algorithm;
- the numerical realization.

The boundary between open and closed is deliberate and is not negotiable. 
A method that performs as documented does not require source-level release 
to be scientifically valuable; it requires reproducibility of its claims, 
which the blind-test protocol provides.

---

## Repository Map

```text
pCHA/
├── README.md                     # this file
├── theory.md                     # mathematical framework (4–5 pages)
├── blind_test_protocol.md        # verification terms
└── results/
    ├── dysts_summary_multi_threshold.csv
    ├── real_world_benchmarks.csv
    ├── synthetic_n_train_summary.csv
    ├── real_world_n_train_summary.csv
    └── figures/
        ├── fig1_wall_of_chaos.png / .pdf
        ├── fig2_ecg_precision.png / .pdf
        ├── fig3_domain_coverage.png / .pdf
        ├── fig4_all_datasets_precision.png / .pdf
        ├── fig5_pass_vs_ntrain.png / .pdf
        └── fig6_error_vs_ntrain.png / .pdf
```

Source code, binaries, and raw `.npy` data are not distributed.

---

## Benchmark Conditions

All experiments use the same conditions for all methods:

- state dimension: 3D (or 1D–3D via standard embedding);
- train sizes for comparison with baselines: n_train ∈ {15, 50, 100, 200};
- threshold study (pCHA only): n_train ∈ {5, 10, 15};
- horizon: T = 50 Lyapunov time units (50,000 native interpolation 
  steps at dt = 0.001);
- strict out-of-sample hold-out;
- zero RHS (no governing equations provided);
- no future leakage at any stage;
- metric: max L2 error;
- thresholds: ε ∈ {0.1σ, 0.01σ, 0.001σ}, with σ from the test portion.

Baseline hyperparameters are taken from the original publications without 
tuning on test data. Where a pre-registered validation split is provided, 
baselines may be tuned on validation and frozen before evaluation; the 
test portion remains untouched throughout. See `blind_test_protocol.md` §10.

---

## Contact

Verification enquiries, community nominations, and commercial evaluation 
requests: **[your_secure_email@proton.me]**

Public discussion of the method, the data, and the protocol is welcome. 
Nominations and submissions are governed exclusively by 
`blind_test_protocol.md`.

---

*This README is a summary. Where it and the protocol disagree, the 
protocol governs.*