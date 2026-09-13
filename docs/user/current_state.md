# Current State — User-Facing Summary

## Scope

The current research branch remains restricted to regular, \(C^1\), cubic, non-rational spline curves. The basic transformation is
\[
C\xrightarrow{D^2}q=C'',
\]
where \(q\) is piecewise linear and may jump at double knots.

The long-term goal is to simplify \(q\) under a geometric tolerance using a metric/certification mechanism substantially tighter than ordinary \(L^p\) surrogates but much easier to handle than direct Hausdorff optimization.

Canonical error notation is
\[
E:=C-\widetilde C,
\qquad e:=C''-\widetilde C'',
\qquad E=G_De
\]
under the endpoint-preserving reconstruction gauge.

---

## Stable result 1 — representation complexity is exact in the \(C''\) domain

The second-derivative map from \(C^1\) piecewise cubics to possibly discontinuous piecewise-affine functions is onto with affine kernel:
\[
S^1_3/\mathcal P_1\cong PL_{\rm disc}.
\]

For \(q=C''\):
- jump -> double cubic knot;
- continuous kink -> simple knot;
- neither -> redundant breakpoint.

If \(K_0\) counts continuous kinks and \(J\) jumps,
\[
\kappa(q)=K_0+2J,
\qquad
N_{\rm ctrl}=4+\kappa(q)
\]
for a minimal open/clamped cubic representation.

Thus the fixed-degree representation complexity is encoded exactly in the PL second derivative.

---

## Stable result 2 — synchronized positional error is exact in the same domain

With shared endpoints,
\[
E''=e,
\qquad E(a)=E(b)=0.
\]
Then
\[
E=G_De
\]
with the explicit Dirichlet Green kernel derived in Session 0003. Therefore
\[
N_G(e):=\|E\|_\infty
\]
is exactly the synchronized positional error and satisfies
\[
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)\le N_G(e).
\]

A short Green-function refresher is stored in `docs/user/background/green_functions.md` and should be included in any later self-contained TeX note.

---

## Stable result 3 — the synchronized Green error is directly certifiable

When \(e\) is piecewise linear, \(E\) is piecewise cubic. On each union-partition span the Euclidean norm extrema satisfy
\[
E\cdot E'=0,
\]
a polynomial equation of degree at most five.

Hence \(N_G\) can be evaluated/certified using fixed-degree real-root isolation span by span. A second CAD-friendly route uses cubic Bézier control-vector bounds plus de Casteljau subdivision.

This removes the need to use an \(L^p\) surrogate merely because it is easier to compute.

---

## New stable result 4 — tangential synchronized error can be removed to first order

This is the first geometry-aware theorem in the project.

Let \(s\) be the arc-length coordinate of the regular reference curve \(C\), with unit tangent \(T\) and curvature
\[
\kappa(s)=\left\|\frac{dT}{ds}\right\|,
\qquad
K=\operatorname*{ess\,sup}\kappa.
\]

The candidate displacement is
\[
\Delta:=\widetilde C-C=-E.
\]
Its signed tangential displacement in arc length is
\[
\delta(s)=\Delta(s)\cdot T(s)=-E(s)\cdot T(s).
\]
Use the reference matching
\[
\rho(s)=s+\delta(s).
\]

If the curves share endpoints and
\[
\boxed{
\|D_sE\|_\infty+K\|E\|_\infty<1,
}
\]
then \(\rho\) is an orientation-preserving homeomorphism of the entire arc-length interval.

Define
\[
N_{G,\perp}(e)=\sup_t\|P_{N(t)}E(t)\|,
\]
\[
N_{G,\parallel}(e)=\sup_t|E(t)\cdot T(t)|.
\]
Then
\[
\boxed{
 d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)
\le d_F^+(C,\widetilde C)
\le
N_{G,\perp}(e)+\frac K2N_{G,\parallel}(e)^2.
}
\]
Consequently,
\[
\boxed{
 d_H\le N_{G,\perp}(e)+\frac K2N_G(e)^2.
}
\]

### Meaning

The synchronized normal error is the first-order geometric residual. Tangential synchronized error is, locally, a reparameterization direction and survives only through a quadratic curvature correction.

This is stronger than the original heuristic idea of simply projecting onto the normal space: it provides a certified finite Hausdorff upper bound under an explicit monotonicity condition.

### Why the arc-length formulation matters

A direct correction in the original spline parameter produces a remainder involving \(\|C''\|\), which is polluted by parameter-speed variation. A badly parameterized straight line may have large \(C''\) despite zero geometric curvature.

In arc length, the remainder depends on geometric curvature instead. For a straight line, \(K=0\), and a monotone endpoint-preserving purely tangential redistribution is recognized exactly as zero geometric error.

---

## Important limitation

The new theorem is only first-order invariant to reparameterization on curved geometry.

If the candidate is exactly the same curved image with a nonlinear parameterization, the true Hausdorff distance is zero, while the present bound is generally only quadratic in the parameter shift. Exact invariance would require a stronger nonlinear correspondence.

Other limitations:
- the reference curve must remain regular;
- high curvature enlarges the quadratic term;
- the monotonicity condition contains \(D_sE\);
- \(N_{G,\perp}\) is reference dependent and no longer a norm on \(e\) alone.

---

## Current assessment

The framework now has three linked exact/certified layers:

1. representation complexity in the \(C''\) domain;
2. exact synchronized positional error through the Green operator;
3. a local geometry-aware Hausdorff bound that suppresses tangential error to first order.

This is the strongest point reached so far, but the project has not yet promoted it to a full TeX stage note. One more question is critical: does the geometry-aware bound retain the fixed-degree computational advantage of the synchronized Green metric?

---

## Next research target

The next session will study only the algebraic/certification cost of:
- \(N_{G,\perp}\);
- \(\|D_sE\|\);
- the reference curvature bound \(K\);
- the monotonicity condition.

If these remain fixed-degree univariate problems on cubic spans, the framework will be ready for a stage-level adversarial review and likely a self-contained TeX note.

No source-code test is currently needed.
