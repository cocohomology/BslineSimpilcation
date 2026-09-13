# Arc-Length Tangential Quotient and a Local Geometric Bound

Session 0005 derivation.

## 1. Purpose

The synchronized Green error
\[
E=C-\widetilde C=G_De
\]
is exact and cheap to certify, but it is parameterization-sensitive. A large component of \(E\) parallel to the reference tangent may represent mainly a sliding of parameter points along essentially the same geometry.

This note studies one local question only:

> Can the tangential component be absorbed by a monotone reparameterization, with an explicit finite remainder and a certified geometric consequence?

The answer is yes under a smallness/monotonicity condition. The clean formulation uses the arc-length coordinate of the reference curve; this removes an artificial dependence on tangential acceleration caused by a bad parameterization.

---

## 2. Canonical sign convention

The repository uses
\[
E:=C-\widetilde C,
\qquad e:=C''-\widetilde C'',
\qquad E=G_De
\]
under the fixed-endpoint gauge.

For the reparameterization argument it is convenient to write the candidate displacement as
\[
\Delta:=\widetilde C-C=-E.
\]
This avoids the sign ambiguity that appeared informally in the previous roadmap. All final bounds are written again in terms of the canonical \(E\).

Assume
\[
E(a)=E(b)=0,
\]
so \(C\) and \(\widetilde C\) share endpoints.

---

## 3. Move to the reference arc-length coordinate

Assume the reference curve \(C:[a,b]\to\mathbb R^d\) is regular and piecewise \(C^2\) with continuous tangent, as is the case for a regular \(C^1\) cubic spline. Define
\[
v(t)=\|C'(t)\|>0,
\qquad
s(t)=\int_a^t v(\tau)\,d\tau,
\qquad
L=s(b).
\]
Because \(C\) is regular, \(s:[a,b]\to[0,L]\) is strictly increasing and has an inverse \(t=t(s)\).

Define the unit-speed reference curve
\[
\gamma(s):=C(t(s)).
\]
Then
\[
\gamma'(s)=T(s),
\qquad \|T(s)\|=1.
\]
Where the second derivative exists,
\[
\gamma''(s)=\kappa_{\rm vec}(s),
\qquad
\kappa(s)=\|\kappa_{\rm vec}(s)\|.
\]
For a regular \(C^1\) cubic with finitely many knots, \(T\) is Lipschitz and \(\kappa\) is bounded almost everywhere. Let
\[
K:=\operatorname*{ess\,sup}_{s\in[0,L]}\kappa(s).
\]

Pull the candidate displacement to the same arc-length coordinate:
\[
\Delta(s):=\widetilde C(t(s))-C(t(s))=-E(t(s)).
\]
Decompose
\[
\Delta=\Delta_\parallel+\Delta_\perp,
\qquad
\Delta_\parallel=(\Delta\cdot T)T,
\qquad
\Delta_\perp=\Delta-(\Delta\cdot T)T.
\]

---

## 4. Tangential shift in arc length

Define the signed tangential displacement
\[
\delta(s):=\Delta(s)\cdot T(s)=-E(s)\cdot T(s).
\]
The natural first-order correspondence is not a shift in the original parameter \(t\), but a shift in reference arc length:
\[
\rho(s):=s+\delta(s).
\]

The associated original-parameter correspondence is
\[
\phi(t)
:=s^{-1}\bigl(s(t)+\delta(s(t))\bigr).
\]

### Endpoint behavior

Since \(E(a)=E(b)=0\),
\[
\delta(0)=\delta(L)=0.
\]
Hence
\[
\rho(0)=0,
\qquad
\rho(L)=L.
\]

### Monotonicity

Differentiate with respect to arc length (almost everywhere):
\[
\delta'(s)
=\Delta_s\cdot T+\Delta\cdot T_s.
\]
Thus
\[
|\delta'(s)|
\le \|\Delta_s(s)\|+\kappa(s)\|\Delta(s)\|.
\]
A simple sufficient condition for strict monotonicity is
\[
\boxed{
q:=\|D_s\Delta\|_\infty+K\|\Delta\|_\infty<1.
}
\]
Since \(\Delta=-E\), equivalently
\[
\boxed{
q=\|D_sE\|_\infty+K\|E\|_\infty<1.
}
\]
Then
\[
\rho'(s)\ge1-q>0
\]
almost everywhere. Because \(\rho\) fixes both endpoints, it is an orientation-preserving bi-Lipschitz homeomorphism of \([0,L]\).

In the original spline parameter,
\[
D_sE=\frac{E'(t)}{\|C'(t)\|}.
\]
So the smallness condition is directly computable from the synchronized error curve and the regular reference curve.

---

## 5. Why arc length is better than a direct parameter shift

A first attempt in the original parameter would use
\[
\phi(t)=t+\eta(t),
\qquad
\eta\approx\frac{\Delta\cdot T}{\|C'\|}.
\]
The Taylor remainder then involves \(\|C''\|\), which contains both genuine curvature and purely tangential acceleration due to variable parameter speed.

That is undesirable for the present goal: a badly parameterized straight line can have very large \(C''\) while its geometry has zero curvature.

In arc length,
\[
\gamma''=\kappa_{\rm vec}
\]
is purely normal. Therefore the second-order remainder depends on geometric curvature rather than tangential speed variation.

This is an important modeling improvement, not merely a change of notation.

---

## 6. Finite remainder estimate

Compare the candidate point at synchronized reference arc length \(s\),
\[
\widetilde\gamma(s):=\widetilde C(t(s))
=\gamma(s)+\Delta(s),
\]
with the reference point at shifted arc length \(\rho(s)=s+\delta(s)\).

Because \(T=\gamma'\) is \(K\)-Lipschitz,
\[
\gamma(s+\delta)-\gamma(s)-T(s)\delta
=\int_0^\delta\bigl(T(s+r)-T(s)\bigr)\,dr,
\]
so
\[
\boxed{
\|R(s)\|
:=\|\gamma(s+\delta)-\gamma(s)-T(s)\delta\|
\le\frac K2\delta(s)^2.
}
\]
This bound remains valid when the interval between \(s\) and \(s+\delta\) crosses spline knots, because only global Lipschitz continuity of \(T\) is used.

Now
\[
\Delta(s)=\delta(s)T(s)+\Delta_\perp(s),
\]
therefore
\[
\widetilde\gamma(s)-\gamma(\rho(s))
=\Delta_\perp(s)-R(s).
\]
Hence the pointwise bound
\[
\boxed{
\|\widetilde\gamma(s)-\gamma(\rho(s))\|
\le
\|\Delta_\perp(s)\|+\frac K2\delta(s)^2.
}
\]

This is a finite inequality, not only an asymptotic \(O(\|E\|^2)\) statement.

---

## 7. Geometric consequence

Because \(\rho\) is an orientation-preserving homeomorphism of the complete interval, it defines a valid one-to-one order-preserving correspondence between the two parameterized curves.

Therefore the Hausdorff distance is bounded by the maximum distance under this correspondence; likewise the orientation-preserving Fréchet distance is no larger than this particular matching cost.

Define, in canonical Green-error notation,
\[
N_{G,\perp}(e)
:=\sup_t\|P_{N(t)}E(t)\|,
\]
and
\[
N_{G,\parallel}(e)
:=\sup_t|E(t)\cdot T(t)|.
\]
Recall
\[
N_G(e)=\|E\|_\infty.
\]
Since \(\Delta=-E\), the normal and tangential magnitudes are unchanged. Under
\[
\|D_sE\|_\infty+K N_G(e)<1,
\]
we obtain
\[
\boxed{
 d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)
\le d_F^+(C,\widetilde C)
\le
N_{G,\perp}(e)+\frac K2N_{G,\parallel}(e)^2.
}
\]
In particular,
\[
\boxed{
 d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)
\le
N_{G,\perp}(e)+\frac K2N_G(e)^2.
}
\]

This is the first rigorous geometry-aware bridge produced by the current D2/Green framework:

- normal synchronized error enters at first order;
- tangential synchronized error enters only quadratically through curvature;
- the estimate is certified provided the induced correspondence remains monotone.

---

## 8. First-order quotient interpretation

Scale a perturbation by \(\varepsilon\):
\[
E_\varepsilon=\varepsilon H.
\]
Then
\[
N_{G,\perp}(E_\varepsilon)=O(\varepsilon),
\qquad
\frac K2N_{G,\parallel}(E_\varepsilon)^2=O(\varepsilon^2).
\]
Thus, locally,
\[
\boxed{
\text{the first-order geometric residual is the normal component }P_NE.
}
\]
Tangential perturbation is a first-order reparameterization direction.

This justifies promoting normal projection from a heuristic to a genuine first-order quotient quantity, under explicit regularity and monotonicity assumptions.

---

## 9. Counterexample / sanity checks

### 9.1 Straight line with nonlinear parameterization

For a straight reference segment,
\[
K=0.
\]
If the candidate displacement is purely tangential and the monotonicity condition holds, then
\[
N_{G,\perp}=0
\]
and the bound gives
\[
d_H=0.
\]
This is correct: an endpoint-preserving monotone tangential redistribution along a straight segment changes only the parameterization, not the image.

This check is important because a direct original-parameter Taylor bound based on \(\|C''\|\) could be arbitrarily pessimistic for a badly parameterized straight line. The arc-length formulation removes that artifact completely.

### 9.2 Curved pure reparameterization

Suppose in reference arc length
\[
\widetilde\gamma(s)=\gamma(s+\zeta(s)),
\qquad \zeta(0)=\zeta(L)=0,
\]
with small \(\zeta\).

Then
\[
\Delta=\zeta T+O(K\zeta^2),
\]
so
\[
\Delta_\perp=O(K\zeta^2).
\]
The actual images are identical and the true Hausdorff distance is zero, while the present bound is generally only \(O(K\zeta^2)\).

Therefore the theorem removes the **first-order** parameterization artifact but is not exactly reparameterization-invariant on curved geometry. Exact invariance would require a nonlinear correspondence rather than this single linearized tangential shift.

### 9.3 High curvature

The quadratic correction contains \(K\). Hence even a small tangential shift may create a non-negligible normal chord error on a tightly curved region. This is geometrically real, not a parameter-speed artifact.

---

## 10. Correctness review

### Assumptions actually used

- regular reference curve, so arc length is a valid coordinate;
- continuous tangent with bounded curvature almost everywhere, equivalently \(T\in W^{1,\infty}\);
- shared endpoints;
- synchronized displacement \(E\) absolutely continuous in arc length;
- smallness condition ensuring the constructed correspondence is monotone.

A regular \(C^1\) cubic spline satisfies the required reference regularity as long as \(\|C'\|\) stays away from zero.

### Points checked

- canonical sign convention against \(E=G_De\);
- endpoint fixing;
- monotonicity by differentiating the signed tangential shift;
- remainder for positive and negative \(\delta\);
- knot crossing handled by Lipschitz tangent rather than pointwise \(C^2\);
- straight-line reparameterization;
- curved pure reparameterization;
- dimensional consistency: \(K\) has units \(1/\text{length}\), so \(K\delta^2\) has units of length.

### Confidence

High for the local theorem and the finite Hausdorff/Fréchet upper bound.

Novelty is **not** claimed. The result is elementary differential geometry specialized to the present Green-error setting. Its significance here is that it gives the first rigorous bridge from the synchronized D2/Green representation to a geometry-aware tolerance.

---

## 11. Limitations and the next bottleneck

The theorem does not finish the parameterization problem.

Remaining issues:

1. \(N_{G,\perp}\) is reference-curve dependent and is not a norm on \(e\) alone.
2. The monotonicity condition contains \(D_sE\); this must be cheaply certifiable in the spline setting.
3. Exact evaluation of \(N_{G,\perp}\) is no longer immediately the same quintic problem as \(N_G\), because the tangent normalization introduces rational structure.
4. The bound is only quadratically, not exactly, invariant under curved pure reparameterization.
5. High curvature can make the correction term significant.

The next research session should ask only:

> Does the geometry-aware bound remain algebraically cheap/certifiable for cubic splines, or does tangent/curvature normalization destroy the fixed-degree advantage?

Do not yet design the full simplification algorithm.
