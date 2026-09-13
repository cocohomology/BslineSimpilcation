# Research Frontier — Internal

## Current narrow problem

Work only with regular \(C^1\), cubic, non-rational spline curves \(C:[a,b]\to\mathbb R^d\), initially with fixed parameter interval and fixed endpoint positions.

Let
\[
q=C'',\qquad \widetilde q=\widetilde C'',\qquad e=q-\widetilde q.
\]

Because \(q\) is piecewise linear, the simplification problem is potentially reduced to low-complexity approximation of a PL vector function.

The immediate theoretical target is **not** the approximation algorithm. It is the error geometry.

## Candidate objects under study

### 1. Green-induced synchronized error

For chosen boundary conditions, define
\[
E=Ge,
\]
where \(G\) is the inverse of the second derivative operator subject to those boundary conditions.

Primary quantity:
\[
N_G(e)=\|Ge\|_\infty.
\]

Questions:
- exact Green kernel for different reconstruction constraints;
- sharp constants relating \(N_G\) to \(L^p\) norms of \(e\);
- whether these constants are materially tighter than coefficient/discrete norm bounds used in classical spline reduction;
- efficient exact or certified evaluation when \(e\) is PL.

### 2. Normal-projected Green error

For a regular reference curve \(C\) with unit tangent \(T\), define heuristically
\[
N_{G,\perp}(e)=\sup_t\|P_{N(t)}Ge(t)\|.
\]

Interpretation: suppress the first-order tangential component, which may primarily represent reparametrization.

Status: candidate **semi-norm-like** quantity only. Do not call it a norm until null-space and dependence on the reference curve are understood.

Questions:
- exact null directions;
- behavior under pure reparametrization;
- local relation to normal-graph distance / Degen normal distance;
- whether Hausdorff admits a bound of the form
  \[
  d_H\le N_{G,\perp}+R,
  \]
  with a controlled higher-order remainder;
- conditions needed for unique normal correspondence.

### 3. Nonlinear normal correspondence

Seek a monotone map \(\sigma\) such that
\[
\widetilde C(\sigma(t))-C(t)\perp T(t).
\]

Potential quantity:
\[
D_N(C,\widetilde C)=\sup_t\|\widetilde C(\sigma(t))-C(t)\|.
\]

This is closer to geometry and Degen's construction, but more nonlinear.

Questions:
- existence/uniqueness conditions in space curves;
- whether the required assumptions can be expressed through reach/tubular-neighborhood bounds;
- whether a local linearization recovers \(N_{G,\perp}\).

## High-priority possible theorems

### T1. Exact reconstruction theorem

Characterize the correspondence between:
- \(C^1\) cubic splines with prescribed boundary data, and
- piecewise-linear second derivatives with allowed jump structure.

This should be elementary but must be written cleanly because it is the foundation.

### T2. Green operator formulas and sharp \(L^p\to L^\infty\) constants

Do this for at least:
- fixed \(E(a)=E'(a)=0\);
- fixed \(E(a)=E(b)=0\).

This is not necessarily novel, but provides exact baseline bounds and reveals the amount of slack in classical norms.

### T3. First-order quotient by tangential reparametrization

For a small perturbation \(\widetilde C=C+E\), determine precisely when the tangential part of \(E\) can be absorbed by a small reparametrization and identify the first-order geometric residual.

Expected form:
\[
E=\alpha T+E_\perp
\]
with a reparametrization correction cancelling \(\alpha T\) to first order.

Need explicit assumptions and remainder.

### T4. Local comparison with geometric distance

Under tubular-neighborhood and regularity assumptions, derive a certified or asymptotic relation between normal residual and Hausdorff/normal distance.

This is the first point where a genuine new framework may emerge.

## Counterexamples to actively construct

1. **Straight-line bad parametrization**: same geometric line, nontrivial \(C''\).
2. **Tiny-span spike**: huge \(e\) on interval length \(h\ll1\), small integrated displacement.
3. **Cancellation pair**: adjacent opposite-sign PL errors with small \(Ge\).
4. **Near self-approach**: normal correspondence non-unique though Hausdorff is small.
5. **High curvature tube failure**: perturbation crosses the reach threshold.
6. **Double-knot jump**: determine how a jump in \(C''\) contributes after two integrations and whether common norms mis-rank it.

## Literature hooks

Already available in project materials:
- Lyche--Mørken discrete norms and knot removal;
- Degen normal distance / admissible curves;
- DeVore nonlinear approximation;
- Jupp free-knot splines;
- Schumaker spline fundamentals.

Likely future literature categories if needed:
- Green operators / negative Sobolev norms;
- Fréchet distance and curve correspondence;
- tubular neighborhoods, reach, normal graphs;
- elastic metrics / shape spaces (only if directly relevant; avoid scope explosion);
- approximation of PL/vector functions with free breakpoints.

## Stop conditions

Pause this direction and report to the user if any of the following becomes convincing:
- every geometry-aware metric considered becomes as hard as Hausdorff/Fréchet optimization;
- parameterization effects cannot be suppressed without destroying the linear/PL advantage;
- certified constants are so loose that the method loses engineering value;
- simplification of \(C''\) systematically fails to correlate with spline representation complexity.

Likewise report immediately if a theorem materially stronger than the current baseline is established.
