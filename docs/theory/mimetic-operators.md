# Mimetic Operator Conventions

FlowSieve's discrete operators (divergence, gradient, vorticity/curl) are
built to satisfy discrete vector calculus identities *exactly*, not just
approximately — this is what "mimetic" refers to. Getting the relationship
between operators right, especially on a spherical grid with metric factors,
is what makes the discrete Helmholtz decomposition well-posed and
consistent with the continuous theory in [Helmholtz
Decomposition](helmholtz-decomposition.md).

## The sign convention

On the sphere, with $w = \cos(\text{lat})$ as the metric weighting factor,
FlowSieve's divergence operator is defined as the (weighted) transpose of
the gradient operator:

$$
\operatorname{div}(\mathbf{F}) = -w^{-1}\, \operatorname{grad}_T(w\mathbf{F})
$$

The important point here is that **the minus sign is definitional, not a
convention to be second-guessed operator-by-operator**: because divergence
is *defined* as this weighted transpose of the gradient, the sign falls out
of the definition rather than being an independent choice. This is what
keeps the full operator set — gradient, divergence, and the vorticity/curl
operator built from them — internally consistent with one another: as long
as $\operatorname{grad}_T$ is implemented correctly, $\operatorname{div}$
inherits correctness by construction.

<!--
TODO(Ben): This is the highest-value page to expand with the actual
derivation detail from your review — e.g.:
  - What grid staging (Arakawa C-grid? co-located?) the operators are
    defined on, and why that staging was chosen
  - The discrete stencils themselves (even just for grad and div — vorticity
    typically follows the same pattern)
  - Why this matters concretely: e.g. tie it back to the deflation subspace
    contamination / grid-scale oscillation bug you diagnosed, as a worked
    example of what breaks when the transpose relationship isn't respected
  - Whether this convention is unique to the polar-stereographic grid used
    elsewhere (ArcticButterflies/PhiSolver-PsiSolver) or specific to
    FlowSieve's lat-lon grid handling
-->

## Solver implications

Because the divergence operator is implemented as a transpose of the
gradient operator (rather than as an independently-discretized stencil), the
two must be kept in lockstep under any future changes — a bug in one
propagates a sign or scaling error into the other. This is a common failure
mode worth calling out explicitly for future contributors.

FlowSieve's sparse solve uses PETSc's matrix-free `MatShell` interface with
LGMRES rather than forming the full operator matrix explicitly.

<!--
TODO(Ben): Worth a short paragraph here on why MatShell/matrix-free was
chosen over assembling the matrix (memory footprint at scale? matches the
migration you did from the earlier Eigen-based GMRES solver?), and any
solver-tuning notes (deflation subspace settings, convergence tolerances)
that would help someone debugging solver behavior in the future — this is
exactly the kind of thing that's easy to forget once it's working.
-->

## Related solvers

The same mimetic conventions are shared conceptually with FlowSieve's
Python counterparts (`PhiSolver.py` / `PsiSolver.py`), which solve an
analogous decomposition on a polar-stereographic grid using a
coarse-to-fine multigrid-style approach. If the two codebases share
derivations or stencil logic, it may be worth cross-linking rather than
duplicating the explanation.
