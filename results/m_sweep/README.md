# Anchor spacing sweep (preliminary)

A preliminary sweep on five systems. Not a full benchmark. The point is 
simple: M=5 is a conservative choice, not the method's hard limit.

Setup:

- systems: Lorenz, Chen, Rossler, HyperCai, SprottA
- n_train = 200, T = 50 Lyapunov time units
- same rollout protocol as the main benchmark
- M ∈ {5, 10, 15, 20, 25, 30, 40, 41, 42, 43, 44, 45, 50, 100}

What happened:

- All five systems pass at M ≤ 40.
- At M=41, Lorenz fails first and the rollout doesn't finish.
- At M=43, three of five are down.
- At M=45, only SprottA is still standing.
- The bound is system-dependent, not fixed.

I don't use this sweep in the main benchmark. The benchmark runs M=5 for 
every system, so the head-to-head against baselines stays fixed and 
reproducible. The sweep is here as a supplementary check proof that 
the method isn't tuned to one specific anchor frequency.

A full sweep across all 117 dysts systems and real-data is future work. Nothing in this 
file should be read as a benchmark result.
