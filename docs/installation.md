# Installation

## Dependencies

FlowSieve requires:

| Dependency | Purpose | Notes |
|---|---|---|
| C++ compiler (C++<!-- TODO(Ben): 11/14/17? --> or later) | Core build | Tested with <!-- TODO: gcc/icc/clang versions --> |
| [Eigen](https://eigen.tuxfamily.org/) | Local/dense linear algebra | Header-only; version <!-- TODO --> |
| [PETSc](https://petsc.org/) | Sparse matrix-free solve (MatShell + LGMRES) | Build against version <!-- TODO --> |
| NetCDF-C(++) | Reading/writing gridded input and output | <!-- TODO(Ben): note the ongoing HPC NetCDF compatibility issue here if it's still relevant for users building on TACC-style systems, and any current workaround --> |
| OpenMP | Shared-memory parallel regions | Usually bundled with the compiler |
| <!-- TODO: MPI? CMake version? --> | | |

## Building from source

```bash
git clone https://github.com/<org>/FlowSieve.git
cd FlowSieve

# TODO(Ben): replace with actual build system — CMake? plain Makefiles?
# Example if CMake:
mkdir build && cd build
cmake .. -DPETSC_DIR=<path-to-petsc> -DCMAKE_BUILD_TYPE=Release
make -j<N>
```

<!--
TODO(Ben): Fill in the real build commands. Also worth documenting here:
  - Any required environment variables (PETSC_DIR, PETSC_ARCH, EIGEN_ROOT, etc.)
  - How OpenMP thread count is controlled at build vs. runtime
  - Whether there's a `make check` / test suite to validate the build
-->

## Building on HPC systems (e.g. TACC / SLURM)

<!--
TODO(Ben): This is worth its own subsection given your workflow — module
load lines for the systems you use, any quirks with linking PETSc built
against system MPI, and the current status of the NetCDF-C++ reader
compatibility issue you've been tracking. Even a "known issues" note here
saves future users (and future you) real time.
-->

```bash
module load <TODO>
```

## Verifying the install

<!--
TODO(Ben): Smallest possible smoke test — e.g. running FlowSieve on a tiny
bundled/test dataset and what output confirms a correct install.
-->

## Python / other bindings

<!--
TODO(Ben): Is FlowSieve C++-only, or is there a Python wrapper / CLI users
typically interact with? If it's invoked via config file + executable rather
than a library API, say so here — it changes how the Quickstart page should
read.
-->
