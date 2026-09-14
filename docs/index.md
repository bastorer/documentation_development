# FlowSieve

**FlowSieve** is a C++ library for computing the Helmholtz decomposition of
geophysical flow fields — separating a vector field (e.g. ocean surface
currents, atmospheric winds) into its rotational (vorticity-driven) and
divergent (divergence-driven) components on the sphere.

<!--
TODO(Ben): Replace this paragraph with the actual motivating description from
your paper / README — e.g. what scientific questions FlowSieve is built to
answer (kinetic energy cascade analysis, coarse-graining, etc.), and a link to
Storer, Buzzicotti, Khatri, Griffies & Aluie (2023) if that's the right
citation to point readers to.
-->

FlowSieve solves this decomposition using a **mimetic finite-difference**
discretization, which preserves discrete analogues of vector calculus
identities (e.g. divergence of a curl is exactly zero) rather than only
approximately. The solver stack is built on [Eigen](https://eigen.tuxfamily.org/)
for local linear algebra and [PETSc](https://petsc.org/) for the large-scale
sparse solve, using a matrix-free (`MatShell`) formulation with LGMRES.

## Where to start

- **[Installation](installation.md)** — dependencies and build instructions
- **[Quickstart](quickstart.md)** — running your first decomposition
- **[Theory](theory/helmholtz-decomposition.md)** — the math behind the
  decomposition and FlowSieve's mimetic operator conventions
- **[Examples](examples/index.md)** — worked examples on real datasets
- **[API Reference](api/index.html)** — auto-generated from source (Doxygen)

## Key design points

- **Parallelism:** OpenMP for shared-memory parallel regions;
  <!-- TODO(Ben): confirm — is PETSc's MPI layer also used for distributed
  solves, or is FlowSieve currently single-node/OpenMP-only? This matters for
  the installation and quickstart pages. --> PETSc for the sparse solve.
- **Numerical convention:** operators are defined so that
  `div(F) = -w⁻¹ grad_T(wF)` with `w = cos(lat)`, making the sign in the
  divergence operator *definitional* rather than an arbitrary convention —
  see [Mimetic Operators](theory/mimetic-operators.md) for the derivation and
  why this keeps all operators internally consistent.
- **Solver:** a PETSc `MatShell`-based LGMRES solve (migrated from an
  earlier Eigen-based GMRES implementation) for scalability to large grids.

## Project status

<!--
TODO(Ben): A short, honest status paragraph — e.g. supported grid types
(currently polar-stereographic / lat-lon?), known limitations, and the
current open issue around NetCDF reader compatibility on HPC systems, if
that's still worth flagging to users trying to build on TACC-like systems.
-->
