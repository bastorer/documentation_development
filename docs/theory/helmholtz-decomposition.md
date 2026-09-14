# Helmholtz Decomposition

## The decomposition

For a sufficiently well-behaved vector field $\mathbf{F}$ on a domain, the
Helmholtz decomposition writes $\mathbf{F}$ as the sum of a **divergent**
(curl-free) part and a **rotational** (divergence-free) part:

$$
\mathbf{F} = \nabla \phi + \mathbf{k} \times \nabla \psi
$$

where:

- $\phi$ is the **velocity potential**, whose gradient gives the divergent
  component,
- $\psi$ is the **streamfunction**, whose rotated gradient
  ($\mathbf{k} \times \nabla \psi$) gives the rotational component,
- $\mathbf{k}$ is the local vertical unit vector.

By construction, $\nabla \times (\nabla \phi) = 0$ (the divergent part is
curl-free) and $\nabla \cdot (\mathbf{k} \times \nabla \psi) = 0$ (the
rotational part is divergence-free) — the two components carry independent
information about the field's structure.

## Why this decomposition, for geophysical flows

<!--
TODO(Ben): This is the place to bring in the physical motivation from your
Science Advances paper — e.g. why separating rotational and divergent
kinetic energy matters for understanding the ocean/atmosphere energy
cascade, and what "cascade" means in this context for a reader unfamiliar
with the paper. A couple of paragraphs summarizing the physical picture
(without reproducing figures/text verbatim) would anchor this page well.
-->

## Recovering $\phi$ and $\psi$

Taking the divergence and curl of $\mathbf{F} = \nabla \phi + \mathbf{k}
\times \nabla \psi$ gives two decoupled Poisson problems:

$$
\nabla^2 \phi = \nabla \cdot \mathbf{F}, \qquad
\nabla^2 \psi = -\hat{k} \cdot (\nabla \times \mathbf{F})
$$

Solving these (subject to appropriate boundary conditions) recovers $\phi$
and $\psi$, and hence the two components of $\mathbf{F}$. This is the
computation FlowSieve performs, discretely, on the sphere.

## From continuous to discrete

Going from the continuous identities above to a discrete solve that actually
*preserves* them exactly (rather than only approximately, as would happen
with a naive finite-difference discretization) requires care in how the
gradient, divergence, and curl operators are defined relative to one
another. FlowSieve uses a **mimetic finite-difference** discretization for
this reason — see [Mimetic Operators](mimetic-operators.md) for the
discrete operator definitions and the specific sign convention FlowSieve
uses on the sphere.

<!--
TODO(Ben): If there's a citation list / further reading you point students
or new collaborators to when introducing this topic, list it here.
-->
