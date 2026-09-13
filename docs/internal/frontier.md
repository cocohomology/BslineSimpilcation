# Research Frontier — Internal

## Current setting

Work with regular \(C^1\), cubic, non-rational spline curves \(C:[a,b]\to\mathbb R^d\), preserving endpoints. Canonical notation:
\[
q=C'',\qquad \widetilde q=\widetilde C'',\qquad e=q-\widetilde q,
\qquad E=C-\widetilde C=G_De.
\]

## Stable foundation that survived the first attack

### F1 — exact \(D^2\) reduction
\[
D^2:S_3^1\to PL_{\rm disc}
\]
is onto with affine kernel. Jump/kink structure of \(q\) records minimal cubic knot multiplicity exactly.

### F2 — exact synchronized Green error
Under fixed endpoints,
\[
E=G_De,
\qquad N_G=\|E\|_\infty,
\]
and
\[
d_H\le N_G.
\]

### F3 — synchronized error is fixed-degree certifiable
For PL \(e\), \(E\) is piecewise cubic. \(N_G\) reduces to degree-at-most-five stationarity equations or certified cubic Bézier subdivision.

### F4 — normal displacement is the correct first-order geometric residual
Using reference arc length, the first-order shift
\[
\rho(s)=s-E\cdot T
\]
removes tangential synchronized error to first order. The local Taylor structure is sound:
\[
\gamma(s+\delta)=\gamma(s)+T\delta+\frac12\kappa_{\rm vec}\delta^2+o(\delta^2).
\]
Thus curvature-dependent quadratic tangential error is geometrically real.

### F5 — all first-order geometry-aware ingredients are fixed-degree algebraic on cubic spans
Normal/tangential projections, curvature, regularity, and the monotonicity of \(\rho\) remain fixed-degree univariate certification problems. In particular,
\[
\rho'(s)>0\iff H(t)>0,
\qquad
H=2S^2-2B'S+BS',
\]
with degree at most eight.

## Negative result N1 — the global curvature bound is not acceptable as a final metric

The previously proposed certification
\[
 d_H\le N_{G,\perp}+\frac K2N_{G,\parallel}^2,
\qquad K=\sup\kappa,
\]
is mathematically correct but can be arbitrarily conservative **inside the present cubic \(C^1\) model class**.

Explicit construction:
- the error is a purely tangential monotone reparameterization supported on a straight region;
- a disjoint region of the same curve has arbitrarily high curvature;
- candidate and reference images are exactly identical, so \(d_H=0\);
- nevertheless the global product equals \((K/2)A^2\) and can diverge as \(K\to\infty\).

Detailed counterexample: `docs/internal/derivations/adversarial_review_round1.md`.

Interpretation: the failure is the **globalization of curvature**, not the first-order tangent/normal decomposition.

## Negative/limitation N2 — order-preserving correspondence can be much stronger than Hausdorff

The current construction controls an explicit Fréchet-like correspondence and then uses
\[
d_H\le d_F^+.
\]
Near self-intersection or strong self-approach, this can be much more conservative than point-set Hausdorff distance.

This is not a logical error; it is a modeling issue. If CAD simplification should preserve traversal/order, this may be desirable. If only the image matters, a tubular/reach assumption or a more flexible correspondence is needed.

## Attack results that did not break the theory

### Low speed

A straight-line family with \(\min\|C'\|\to0\) is still treated exactly in exact arithmetic. The problem is numerical conditioning only; the monotonicity polynomial becomes small like a power of the speed.

### High curvature at the same location

The \(\kappa\delta^2/2\) scaling is asymptotically sharp. Curvature cannot simply be removed; it must be localized or handled by a nonlinear correspondence.

### Short spans / double knots

No structural failure. Use span normalization and one-sided curvature; numerical conditioning remains a future engineering issue.

## Current interpretation

The first attack changes the status of the project:

- the core \(D^2\)/Green program remains alive;
- the synchronized theory remains strong;
- the normal component remains the right first-order geometric object;
- but the simple global bound using one \(K=\sup\kappa\) is rejected as a practical final metric.

No stage-level TeX note should be written yet.

## Current main target — nonlinear local normal correspondence

The preferred next route is to seek a local branch \(u=\sigma(t)\) satisfying
\[
\boxed{
(\widetilde C(t)-C(u))\cdot C'(u)=0.
}
\]
For fixed \(t\) and cubic \(C\), this is degree at most five in \(u\).

Desired properties:
- restore locality automatically;
- exact zero on same-image reparameterizations along the same branch;
- retain a stronger-than-Hausdorff but cheaper-than-global-nearest-point structure;
- connect naturally to Degen's normal-distance framework.

Questions for the next session:
- local existence and uniqueness conditions near \(u=t\);
- relation to reach/tubular neighborhoods and Degen's admissibility assumptions;
- whether the normal branch can be certified without a full two-parameter Hausdorff search;
- how much algebraic degree grows when maximizing the resulting normal distance over \(t\).

## Secondary repair route

Localize the curvature remainder to the actual shifted arc interval. Keep this parked until the normal-correspondence route is assessed; moving arc-length intervals may destroy the clean native-parameter algebra.

## Stop / pivot conditions

Pause or pivot if nonlinear normal correspondence requires global branch search comparable to Hausdorff, or if branch uniqueness fails routinely on ordinary CAD curves.
