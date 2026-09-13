# Short-Horizon Roadmap — Internal

This file is intentionally volatile. It describes only the next few research sessions. It is not a commitment to a fixed theory.

## Phase 0 — Initialization

Status: complete.

## Phase 1 — Make the D2 reduction exact

### Task 1.1 — Reconstruction structure

Status: **complete (Session 0002)**.

Established:
- \(D^2:S^1_3\to PL_{\rm disc}\) is onto with affine kernel;
- two vector constraints fix reconstruction uniquely;
- jump/kink structure of \(C''\) exactly records minimal cubic knot multiplicity;
- weighted PL complexity \(\kappa=K+2J\) gives \(N_{\rm ctrl}=4+\kappa\) for a minimal open/clamped cubic.

### Task 1.2a — Fixed-endpoint Green kernel

Status: **complete (Session 0003)**.

Established for
\[
E''=e,\qquad E(a)=E(b)=0:
\]
\[
K_D(t,s)=-\frac{(\min\{t,s\}-a)(b-\max\{t,s\})}{b-a}.
\]

Also established:
\[
N_G(e):=\|G_De\|_\infty
=\|C-\widetilde C\|_{\infty,\mathrm{sync}},
\]
and
\[
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)\le N_G(e).
\]

The kernel is one-signed and tent-shaped in the integration variable, preserving signed/vector cancellation and location information.

### Task 1.2c — PL-specific exact/certified evaluation of \(N_G\)

**Next session only.** This task is moved ahead of global \(L^p\) constants because Session 0003 suggests direct evaluation may be cheap enough to make those bounds secondary.

Goals:
- assume \(e\) is piecewise affine on the union partition of original/candidate breakpoints;
- derive the polynomial form of \(E=G_De\) on each span;
- determine the degree of the stationarity equation for scalar and vector norms;
- identify how to include span boundaries and jumps in \(e\);
- give a certified evaluation strategy in pseudocode-level mathematics only;
- estimate structural complexity in the number of spans;
- perform a goal-alignment review: is this genuinely easier than curve-to-curve Hausdorff evaluation?

Success criterion:
- a clean finite procedure for exact/certified \(N_G\) evaluation using low-degree polynomial root isolation/subdivision, with no dense sampling requirement.

Failure criterion:
- global coupling or vector norm maximization makes certification too expensive to preserve the hoped-for advantage.

Do not yet optimize breakpoint locations or design a complete simplification algorithm.

### Task 1.2b — Sharp \(L^p\to L^\infty\) bounds

Status: open but deprioritized.

Return here only if needed to:
- compare against Lyche-style norm bounds;
- obtain cheap pruning bounds;
- quantify how much direct \(N_G\) evaluation improves over global norms.

## Phase 2 — Attack ordinary Lp as a ranking metric

Status: waiting for direct \(N_G\) evaluation.

Later targets:
- cancellation pair examples;
- short-span scaling;
- ranking reversals between \(L^p\) and \(N_G\);
- decide whether an intermediate cheap surrogate is actually needed.

## Phase 3 — Parametrization

Status: postponed.

Only enter after the synchronized metric is both mathematically understood and computationally viable.

Possible directions remain open; do not assume normal projection is the only route.

## Phase 4 — Geometry-aware comparison / certification

Status: postponed.

The final CAD criterion remains geometric. Potential routes may involve normal correspondence, Fréchet-like order-preserving correspondence, reach/tubular neighborhoods, or something not yet identified.

## Phase 5 — Simplification algorithm

Status: postponed.

If the metric theory survives:
- formulate breakpoint removal/merge/move primitives;
- write pseudocode before any implementation;
- use numerical tests primarily to falsify or measure sharpness.

No source code unless explicitly requested.

## Side-branch parking lot

- optimized affine reconstruction instead of fixed endpoints;
- force continuity of \(q\) to obtain \(C^2\) candidates;
- closed/periodic curves and compatibility constraints;
- parameter normalization / alternative gauges;
- sharp global operator constants;
- potential convex formulations for fixed candidate partitions.

These are deliberately parked to keep each research session narrow.
