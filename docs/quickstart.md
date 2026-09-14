# Quickstart

This page walks through running your first Helmholtz decomposition with
FlowSieve, end to end.

## 1. Input data

FlowSieve expects gridded vector field data (e.g. zonal/meridional velocity
components) on a <!-- TODO(Ben): lat-lon grid? polar-stereographic? which
grid types are supported today? --> grid, provided as
<!-- TODO: NetCDF? what variable naming conventions are expected? -->.

```
<!-- TODO(Ben): a minimal example of expected input file structure, e.g.
`ncdump -h` output showing the required dimensions/variables -->
```

## 2. Configuration

<!--
TODO(Ben): Is FlowSieve driven by a config file (YAML/JSON/plain text) or
command-line flags, or both? Show a minimal working config here.
-->

```
<!-- TODO: minimal config example -->
```

## 3. Running the decomposition

```bash
# TODO(Ben): actual invocation, e.g.
./flowsieve --config config.in --input velocity.nc --output decomposed.nc
```

## 4. Output

The output contains:

- The **rotational** (vorticity-associated) component of the input field
- The **divergent** (divergence-associated) component

<!--
TODO(Ben): describe the actual output variables/naming, units, and whether
the streamfunction/velocity potential themselves are also written out
(relevant given PhiSolver/PsiSolver in the related Python tooling — is there
an analogous output here, or is this strictly the vector components?).
-->

## 5. A minimal worked example

<!--
TODO(Ben): Point to (or embed) the smallest real example you have — ideally
something that runs in well under a minute, so this page functions as an
actual "does my install work" check as well as a teaching example. Consider
reusing whatever toy case you'd use for the installation smoke test above,
so you're not maintaining two separate minimal examples.
-->

## Next steps

- See [Theory](theory/helmholtz-decomposition.md) for what the decomposition
  is actually computing and why the mimetic formulation matters.
- See [Examples](examples/index.md) for more involved, realistic use cases.
