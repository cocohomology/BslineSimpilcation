# Research Map — User-Facing

This is a high-level map, not a fixed plan. Sections may be reordered, merged, expanded, or abandoned as the research evolves.

## A. Core reduction — FOUNDATION ESTABLISHED

Study
\[
C\mapsto C''
\]
for \(C^1\) cubic splines.

Established:
\[
S^1_3/\mathcal P_1\cong PL_{\rm disc}.
\]
Every admissible piecewise-affine second derivative integrates back to a \(C^1\) cubic after fixing two vector integration constants.

The singularity type of \(C''\) records minimal cubic knot multiplicity:
- continuous kink -> simple knot;
- jump -> double knot;
- no kink/jump -> redundant breakpoint.

With \(K\) kinks and \(J\) jumps,
\[
\kappa=K+2J,
\qquad
N_{\rm ctrl}=4+\kappa.
\]

The remaining affine freedom is handled for now by preserving both curve endpoints.

## B. Error transport through integration — SYNCHRONIZED BASELINE ESTABLISHED

Let
\[
e=C''-\widetilde C''.
\]
Under fixed endpoints,
\[
E=C-\widetilde C=G_De
\]
with an explicit Dirichlet Green kernel. Therefore
\[
N_G(e)=\|G_De\|_\infty
\]
is exactly synchronized positional error and a rigorous Hausdorff upper bound.

For PL \(e\), this exact quantity is also directly certifiable:
- \(E\) is piecewise cubic;
- vector extrema reduce to roots of degree-at-most-five equations \(E\cdot E'=0\);
- alternatively, cubic Bézier convex-hull bounds plus subdivision give a robust certified tolerance test.

So the synchronized metric is both exact and algebraically simple. Global \(L^p\) bounds are now secondary rather than central.

A minimal Green-function refresher is stored in `docs/user/background/green_functions.md` for later reading and for inclusion in any future self-contained TeX note.

## C. Geometry-aware error — CURRENT FRONTIER

The dominant weakness is now parameterization.

Two curves can be geometrically very close while corresponding parameter points differ largely in the tangential direction. The next question is intentionally local:

> Can a small monotone reparameterization remove tangential synchronized error to first order, so that the normal component is the first-order geometric residual?

Only after that local statement is proved and attacked by counterexamples should the project decide whether to pursue:
- normal-projected Green error;
- normal graph/tubular-neighborhood theory;
- Degen-style normal correspondence;
- order-preserving reparameterization / Fréchet-type ideas;
- some different construction suggested by failures.

No route is privileged in advance.

## D. Counterexample program

Every geometry-aware candidate should eventually face:
- identical or nearly identical geometry with nonlinear reparameterization;
- very short knot spans with large second derivative;
- cancellation between neighboring derivative errors;
- nearly straight segments;
- high-curvature but small positional deviations;
- local backtracking/correspondence ambiguity;
- near self-approach;
- double-knot jumps;
- large tangential synchronized error with small true geometric error.

## E. Low-complexity approximation of \(C''\)

Only after the geometry-aware error question is sufficiently understood:
- formulate the PL approximation problem using weighted complexity \(\kappa=K+2J\);
- compare deletion, merge, breakpoint movement, and free-breakpoint fitting;
- exploit exact/certified synchronized Green evaluation where useful;
- write pseudocode before any implementation.

No source-code implementation is planned at this stage.

## F. Certification against geometry

The final CAD criterion remains geometric tolerance.

A possible end-state is:

1. optimize a tractable metric in the \(C''\) domain;
2. reconstruct the cubic candidate;
3. certify geometric error with a rigorous local/global mechanism;
4. refine only where certification fails.

This is not a commitment. If the parameterization research suggests a cleaner architecture, replace it.

## G. Stage-level note criterion

Write a full TeX note only when at least one of the following occurs:
- a useful theorem chain survives review and has meaningful geometric consequence;
- a geometry-aware metric/framework becomes coherent enough to justify an algorithmic route;
- a major negative theorem closes a broad family of ideas;
- theory plus pseudocode forms a self-contained method worth independent reading.

When such a note is written, it should include a short introduction to Green functions/kernels rather than assuming that background.
