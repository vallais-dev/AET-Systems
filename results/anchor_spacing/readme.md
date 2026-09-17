# Anchor spacing sweep

pCHA-only sweep across all 117 dysts systems, plus a baseline comparison 
on 5 representative systems. Not part of the main benchmark. The main 
benchmark uses M=5 for every system.

## Files

- `pcha_sweep_117.csv` — pass rate and median error vs anchor spacing M, 
  across all 117 systems
- `baselines_sweep_5.csv` — pass rate and median error for all methods, 
  across M and 5 systems (Lorenz, Chen, Rossler, HyperCai, SprottA)
- `failures_by_M.csv` — which systems fail at which M, with error and 
  step count

## Result

Pass rate stays at 116/117 from M=5 to M=20, then 115/117 at M=30. At 
M=30, that's 96.7% autonomy — 2,500 corrections instead of 10,000 — with 
zero loss in accuracy relative to M=5.

Baseline contrast on 5 systems:

- pCHA: 5/5 PASS at every M
- Persistence: 5/5 up to M=20, 3/5 at M=30
- ESN, MLP, NVAR, SINDy, EDMD, LinearStateMap: 0/5 at every M

The benchmark uses M=5 as a conservative choice. 
The method is not 
tuned to a specific anchor rate.

## Figures

- `../figures/fig7_autonomy_vs_pass.png` — pass rate vs autonomy
- `../figures/fig8_baseline_contrast.png` — pCHA vs baselines across M
