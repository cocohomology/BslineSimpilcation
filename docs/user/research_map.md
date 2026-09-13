# Research Map — User-Facing

This document is a high-level map, not a fixed plan. Sections may be reordered, merged, expanded, or abandoned as the research evolves.

## A. Core reduction — FOUNDATION ESTABLISHED

Study the map

\[
C\mapsto C''
\]

for \(C^1\) cubic splines.

Session 0002 established the exact algebraic structure:

\[
S^1_3/\mathcal P_1\cong PL_{\rm disc}.
\]

The second derivative is a piecewise-linear object with possible jumps, and every such object integrates back to a \(C^1\) cubic after fixing two vector integration constants.

The singularity type of \(C''\) records minimal cubic knot multiplicity:
- continuous kink -> simple knot;
- jump -> double knot;
- no kink/jump -> redundant breakpoint.

With \(K\) continuous kinks and \(J\) jumps,
\[
\kappa=K+2J,
\qquad
N_{\rm ctrl}=4+\kappa
\]
for a minimal open/clamped cubic representation.

This means the D2-domain is not merely a convenient visualization: it carries the fixed-degree representation complexity exactly.

Remaining issue inside this block: reconstruction requires a choice of affine gauge (e.g. fixed endpoints).

## B. Error transport through integration — CURRENT FOCUS

Let
\[
e=C''-\widetilde C''.
\]

After fixing the affine reconstruction mode, study the operator mapping \(e\) to the synchronized positional error \(E=C-\widetilde C\).

The next narrow target is only the two-endpoint gauge
\[
E(a)=E(b)=0,
\]
and its exact Green kernel.

Later targets, only if the kernel viewpoint remains useful:
- sharp operator bounds for relevant \(L^p\) norms;
- exact/certified evaluation for piecewise-linear \(e\);
- examples where \(L^p\) is provably over-conservative because of cancellation.

## C. Geometry-aware error

Investigate how to reduce sensitivity to parametrization while preserving computability.

Candidate directions remain deliberately open:
- normal projection of integrated error;
- normal graph / tubular-neighborhood representation;
- Degen-style normal correspondence;
- order-preserving reparametrization (Fréchet-type viewpoint);
- other gauges or quotient constructions if the current candidates fail.

Primary question:

> Can one obtain a computable quantity that is closer to geometric error than synchronized parameter error, yet remains structured enough for optimization in the piecewise-linear \(C''\)-domain?

This block is postponed until the synchronized baseline is understood.

## D. Counterexample program

Every candidate metric should eventually be attacked by:
- pure reparametrization of a geometrically unchanged curve;
- very short knot spans with large second derivative;
- cancellation between neighboring second-derivative errors;
- nearly straight segments;
- high curvature with small positional deviation;
- local backtracking / correspondence ambiguity;
- near self-approach of the curve;
- discontinuous \(C''\) caused by double knots.

The exact list is not sacred; add new counterexamples whenever a proof exposes a new weakness.

## E. Low-complexity approximation of C''

Only after the error metric is sufficiently understood:
- formulate the reduced approximation problem for PL vector functions;
- respect the weighted complexity \(\kappa=K+2J\), not merely unique breakpoint count;
- compare breakpoint deletion, merge, movement, and free-breakpoint fitting;
- derive pseudocode before any code test.

No source-code implementation is planned at this stage.

## F. Certification against geometry

The ultimate CAD requirement remains geometric tolerance.

Possible end-state (not a commitment):

1. optimize a tractable intermediate quantity in the \(C''\)-domain;
2. reconstruct the cubic candidate;
3. certify final geometric error with Hausdorff or a rigorous surrogate;
4. refine only where certification fails.

If research shows a better architecture, replace this plan.

## G. Stage-level note criterion

A full TeX note should be created only when at least one of the following occurs:
- a new useful theorem is proved with a coherent chain of lemmas;
- a candidate metric is characterized sufficiently well to justify a new algorithmic framework;
- a major negative theorem rules out a broad class of approaches;
- theory plus pseudocode forms a self-contained method worth presenting to the user.

The Session 0002 D2 theorem is important but currently treated as foundational rather than a stage-level TeX breakthrough.
