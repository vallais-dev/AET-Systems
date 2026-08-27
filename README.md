About
aet is a single executable that runs several tests to compute function values and derivatives (up to 3rd order) on a given interval. All settings are controlled via command-line arguments.

## System Requirements

- **NVIDIA GPU** with support for **CUDA Compute Capability 6.1** or higher (Pascal, Volta, Turing, Ampere, Ada Lovelace, and newer).
- **NVIDIA driver** with CUDA support (version 10.0 or higher).
- **OS**: Linux (tested on Ubuntu 22.04).

Usage

./aet --mode <mode> [options]
If --mode is omitted, main is used by default.

Modes and their options
1. Mode main (primary)

Option	Default	Description
--func	sin	    Function name: sin, cos, exp, runge, poly, stiff_gaussian
--N	    32	    Approximation order (higher = more accurate)
--nodes	1024	  Number of evaluation points
--a	   -1.0	    Left boundary
--b	    1.0	    Right boundary

2. Mode runge (Runge test)

Option	Default	Description
--N	    256	    Approximation order
--nodes	2048	  Number of evaluation points

3. Mode lorenz (Lorenz test)

Option	Default	Description
--N	    256	    Approximation order
--nodes	2048	  (reserved, can be ignored)

4. Mode stiff (stiff Gaussian layer)

Option	Default	Description
--sigma	0.05	  Gaussian width parameter
--N	    256	    Approximation order
--points 1000	  Number of test points
--a	   -0.2   	Left boundary
--b	    0.2	    Right boundary


Examples:

chmod +x ./aet - first thing first

# Primary mode: Runge function, N=128, 1024 points
./aet --mode main --func runge --N 128 --nodes 1024

# Runge test with N=64
./aet --mode runge --N 64

# Lorenz test with N=512
./aet --mode lorenz --N 512

# Stiff Gaussian with modified sigma and boundaries
./aet --mode stiff --sigma 0.1 --N 128 --points 500 --a -0.5 --b 0.5


The results presented in the article were obtained using the following parameters:

./aet --mode runge --N 256
./aet --mode lorenz --N 256
./aet --mode stiff --N 64 --sigma 0.05 --a -0.2 --b 0.2
