# A Numerical Framework for Solving Hyperbolic PDEs in an HPC Environment

BSc thesis in Computer Science, University of Naples "Parthenope", academic year 2024/2025.

- **Supervisor:** Prof. Livia Marcellino
- **Co-supervisor:** Prof. Pasquale De Luca
- **Language:** Italian, with an abstract in Italian and English

## Overview

A numerical framework written in C for solving the 2D wave equation, first implemented sequentially and then parallelized with OpenMP for multicore architectures.

## Method

- Finite difference discretization on a uniform grid
- Explicit second-order Leap-Frog time integration
- Time step set to 90% of the CFL stability limit
- Homogeneous Dirichlet boundary conditions
- Validation against the analytical solution using the L2 error

## Parallelization

OpenMP `parallel for` directives with `schedule(static)` were applied to the initial condition, the first time step, the Leap-Frog loop, and the L2 error calculation, which also uses `reduction(+:err)`.

## Results

### Convergence

| Grid | Time steps | L2 error | Order |
|---|---|---|---|
| 11 × 11 | 32 | 1.8916e-03 | - |
| 21 × 21 | 63 | 4.3410e-04 | 2.12 |
| 41 × 41 | 126 | 1.0888e-04 | 1.97 |
| 81 × 81 | 252 | 2.8046e-05 | 1.98 |

The measured order is close to 2, as expected for this scheme. The L2 error does not change with the number of threads.

### Performance

Average Leap-Frog time on the 81 × 81 grid:

| Threads | Time (ms) | Speedup |
|---|---|---|
| 1 | 71.2 | 1.00 |
| 2 | 47.4 | 1.50 |
| 4 | 34.7 | 2.05 |

Test system: AMD Ryzen 5 3500U (4 cores, 8 threads), 16 GB RAM, Linux Mint 22.1, GCC 13.3.0.

## Stack

C, OpenMP, GCC, Linux

## Repository contents

- `TesiUniPa.pdf`: full thesis
- `Presentazione.pptx`: thesis defense presentation
