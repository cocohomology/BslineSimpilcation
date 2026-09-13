# Research Map — User-Facing

This document is a high-level map, not a fixed plan. Sections may be reordered, merged, or abandoned as the research evolves.

## A. Core reduction

Study the map from cubic splines to piecewise-linear second derivatives:

\[
C \mapsto C''.
\]

Questions:
- exact correspondence between spline knots/multiplicities and breakpoints/jumps of \(C''\);
- boundary data required to reconstruct \(C\) uniquely from \(C''\);
- which simplifications of \(C''\) correspond to meaningful simplifications of \(C\).

## B. Error transport through integration

Let \(e=C''-\widetilde C''\). Study the operator that maps \(e\) to \(E=C-\widetilde C\).

Targets:
- exact Green representation;
- sharp operator bounds for relevant endpoint conditions;
- comparison with \(L^1,L^2,L^\infty\);
- examples where \(L^p\) is provably over-conservative because of cancellation.

## C. Geometry-aware error

Investigate how to reduce sensitivity to parametrization while preserving computability.

Candidate directions:
- normal projection of \(Ge\);
- normal graph / tubular-neighborhood representation;
- Degen-style normal correspondence;
- order-preserving reparametrization (Fréchet-type viewpoint);
- decomposition into tangential and normal errors.

Primary question:

> Can one obtain a computable quantity that is closer to geometric error than synchronized parameter error, yet remains structured enough for optimization in the piecewise-linear \(C''\)-domain?

## D. Counterexample program

Every candidate metric must be tested against:
- pure reparametrization of a geometrically unchanged curve;
- very short knot spans with large second derivative;
- cancellation between neighboring second-derivative errors;
- nearly straight segments;
- high curvature with small positional deviation;
- local backtracking / correspondence ambiguity;
- near self-approach of the curve;
- discontinuous \(C''\) caused by double knots.

## E. Low-complexity approximation of \(C''\)

Only after the error metric is sufficiently understood:
- formulate the reduced approximation problem for piecewise-linear vector functions;
- compare fixed-breakpoint deletion, free-breakpoint fitting, and merge operations;
- identify whether the optimization is local, global, convex, or combinatorial;
- derive pseudocode for candidate generation and certification.

No source-code implementation is planned at this stage.

## F. Certification against geometry

The ultimate CAD requirement remains a geometric tolerance.

Potential end-state:

1. optimize a tractable intermediate quantity in the \(C''\)-domain;
2. reconstruct the cubic spline candidate;
3. certify final geometric error, potentially with Hausdorff or a rigorous surrogate;
4. refine only where certification fails.

## G. Stage-level note criterion

A full TeX note should be created only when at least one of the following occurs:
- a new useful theorem is proved with a coherent chain of lemmas;
- a candidate metric is characterized sufficiently well to justify a new algorithmic framework;
- a major negative theorem rules out a broad class of approaches;
- theory plus pseudocode forms a self-contained method worth presenting to the user.
