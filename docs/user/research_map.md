# Research Map — User-Facing

This is a high-level map, not a fixed plan. Sections may be reordered, merged, expanded, or abandoned as the research evolves.

## A. Core reduction — FOUNDATION ESTABLISHED

For \(C^1\) cubic splines,
\[
C\mapsto C''
\]
turns the curve into a possibly discontinuous piecewise-linear vector function. After quotienting the affine kernel,
\[
S^1_3/\mathcal P_1\cong PL_{\rm disc}.
\]

The singularity type of \(C''\) records minimal cubic knot multiplicity exactly:
- continuous kink -> simple knot;
- jump -> double knot;
- neither -> redundant breakpoint.

This makes the second-derivative domain an exact representation-complexity model rather than a visual analogy.

## B. Synchronized error transport — BASELINE ESTABLISHED

Under endpoint preservation,
\[
E=C-\widetilde C=G_De,
\qquad e=C''-\widetilde C''.
\]
The Green-induced quantity
\[
N_G=\|E\|_\infty
\]
is exact synchronized positional error and a Hausdorff upper bound.

For PL \(e\), \(E\) is piecewise cubic and \(N_G\) is directly certifiable by fixed-degree univariate root isolation or Bézier subdivision. Therefore \(L^p\) surrogates are no longer central merely for computational convenience.

A compact Green-function refresher is stored in `docs/user/background/green_functions.md`.

## C. Geometry-aware correction — FIRST LOCAL THEOREM ESTABLISHED

The dominant weakness of synchronized error is tangential parameter sliding.

Session 0005 moves to the reference arc-length coordinate. If \(T\) is the unit tangent and
\[
K=\operatorname*{ess\,sup}\kappa
\]
is the curvature bound, then the signed tangential candidate displacement defines an arc-length matching. Under the explicit smallness condition
\[
\|D_sE\|_\infty+K\|E\|_\infty<1,
\]
the matching is monotone and yields
\[
 d_H
\le
N_{G,\perp}(e)+\frac K2N_{G,\parallel}(e)^2
\le
N_{G,\perp}(e)+\frac K2N_G(e)^2.
\]

Thus:
- the normal component is the first-order geometric residual;
- tangential error is removed to first order;
- the remaining tangential contribution is quadratic in size and weighted by geometric curvature.

The use of arc length is important: it avoids contaminating the remainder with tangential acceleration caused by poor parameter speed.

This is still only a local theorem. It is not exactly reparameterization-invariant for curved pure reparameterizations.

## D. Current frontier — CAN THE GEOMETRIC BOUND STAY CHEAP?

The next question is computational/algebraic rather than conceptual:

> For cubic splines, are the terms in the new geometry-aware bound still certifiable by fixed-degree local univariate algebra?

The next session will study:
- \(N_{G,\perp}\);
- \(\|D_sE\|\);
- curvature maximum \(K\);
- the monotonicity condition.

If these remain low-degree and local, the D2/Green route will retain the main advantage that motivated it: more geometric information without a full curve-to-curve nearest-point search.

## E. Counterexample program

The main geometry-aware candidates must face:
- identical straight geometry with nonlinear parameterization;
- identical curved geometry with nonlinear parameterization;
- high curvature;
- near-zero speed while remaining formally regular;
- short knot spans and derivative spikes;
- near self-approach / correspondence ambiguity;
- double-knot jumps;
- cancellation patterns in second-derivative error.

## F. Low-complexity approximation algorithm — POSTPONED

Only after the geometry-aware certification route survives:
- formulate weighted PL simplification using kink/jump complexity;
- compare deletion, merge, breakpoint movement, and free-breakpoint fitting;
- use pseudocode before implementation;
- use numerical work to attack assumptions and measure conservatism.

## G. Stage-level note criterion

The first full TeX note is now close but intentionally deferred.

Write it if the Session 0005 geometry-aware theorem survives the next computability/adversarial review. Such a note should include:
- the D2 representation theorem;
- a self-contained Green-function/kernel introduction;
- exact synchronized Green error and its certification;
- arc-length tangential quotient theorem;
- limitations/counterexamples;
- the resulting pseudocode architecture if justified.

No novelty claim should be made without a focused literature check.
