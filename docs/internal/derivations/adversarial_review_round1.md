# Adversarial Review Round 1 — Where the First Geometry-Aware Bound Breaks

Session 0007.

## 1. Purpose

This session deliberately stops forward theorem-building and attacks the current geometry-aware certification layer.

The framework before this review was:
\[
E=C-\widetilde C=G_De,
\]
with a first-order arc-length correspondence
\[
\rho(s)=s-E(s)\cdot T(s),
\]
and, when \(\rho\) is orientation preserving,
\[
 d_H\le N_{G,\perp}+\frac K2N_{G,\parallel}^2.
\]
Here
\[
N_{G,\perp}=\sup\|P_NE\|,
\qquad
N_{G,\parallel}=\sup|E\cdot T|,
\qquad
K=\operatorname*{ess\,sup}\kappa.
\]

The questions are not whether the inequality is correct—it is—but whether it is sufficiently tight and robust to serve the intended CAD simplification problem.

---

## 2. Attack A — near-zero speed is not a theoretical failure

A bad parameterization can make \(\min\|C'\|\) arbitrarily small even for a perfectly ordinary straight segment.

Take
\[
f_\varepsilon(t)=\left(t-\frac12\right)^3+\varepsilon t,
\qquad 0\le t\le1,
\qquad \varepsilon>0,
\]
and define the reference straight curve
\[
C_\varepsilon(t)=(f_\varepsilon(t),0).
\]
Then
\[
f_\varepsilon'(t)=3\left(t-\frac12\right)^2+\varepsilon>0,
\]
so the curve is regular, but
\[
\min|C_\varepsilon'|=\varepsilon\to0.
\]

Let \(g_\varepsilon\) be the affine map with the same endpoint values as \(f_\varepsilon\):
\[
g_\varepsilon(t)=f_\varepsilon(0)+\bigl(f_\varepsilon(1)-f_\varepsilon(0)\bigr)t.
\]
Set
\[
\widetilde C_\varepsilon(t)=(g_\varepsilon(t),0).
\]
Both curves traverse exactly the same geometric line segment monotonically, hence
\[
d_H=0.
\]

Because the reference curvature is zero,
\[
K=0,
\qquad N_{G,\perp}=0,
\]
so the geometry-aware bound also gives zero exactly.

More strongly, the direct monotonicity polynomial from Session 0006 simplifies to
\[
H=2(f_\varepsilon')^3g_\varepsilon'>0.
\]
Thus the correspondence is certified exactly even though \(\min f_\varepsilon'=\varepsilon\) is arbitrarily small.

### Verdict

Near-zero speed does **not** break the mathematics. Arc-length normalization successfully removes the fake geometric blow-up.

However, it does create a numerical-conditioning problem: near the slow point, \(H\) scales like \(\varepsilon^3\). A floating-point sign test can therefore become fragile even though the exact sign is positive.

This is an engineering guardrail, not a theoretical rejection. A later implementation should detect a small certified lower bound for \(S=\|C'\|^2\), normalize spans, use Bernstein/interval sign tests, and provide a fallback for nearly singular parameterizations.

---

## 3. Attack B — the global curvature constant creates a genuine in-class counterexample

This is the decisive negative result of the session.

Construct a regular \(C^1\) piecewise-cubic reference curve on \([0,2]\). On \([0,1]\), let
\[
C(t)=(t,0),
\]
a straight segment. On \([1,2]\), with \(u=t-1\), take for example
\[
C(t)=(1+u,Mu^2),
\qquad M>0.
\]
The curve is regular and \(C^1\) at \(t=1\). Its curvature on the second span is
\[
\kappa(u)=\frac{2M}{(1+4M^2u^2)^{3/2}},
\]
so
\[
K=2M.
\]

Now alter only the parameterization of the straight part. Define a \(C^1\) piecewise-cubic bump \(h\) supported on \([0,1]\):
\[
h(t)=A\,p(2t),\qquad 0\le t\le\frac12,
\]
\[
h(t)=A\,p(2-2t),\qquad \frac12\le t\le1,
\]
where
\[
p(x)=3x^2-2x^3.
\]
Then
\[
h(0)=h(1)=0,
\qquad h'(0)=h'(1)=0,
\qquad \max|h|=A,
\]
and
\[
\max|h'|=3A.
\]
Choose
\[
0<A<\frac13.
\]
Define the candidate
\[
\widetilde C(t)=(t-h(t),0),\qquad 0\le t\le1,
\]
and
\[
\widetilde C(t)=C(t),\qquad 1\le t\le2.
\]
Because \(1-h'(t)>0\), the candidate traverses the same straight segment monotonically. It is unchanged on the curved part. Therefore
\[
\operatorname{Im}\widetilde C=\operatorname{Im}C
\]
exactly, and
\[
\boxed{d_H=0.}
\]

On the support of the error, the reference tangent is constant and the error is purely tangential. Hence
\[
N_{G,\perp}=0,
\qquad N_{G,\parallel}=A.
\]
But the global-curvature bound gives
\[
 d_H\le \frac K2A^2=MA^2.
\]
For fixed nonzero \(A\), this upper bound tends to infinity as \(M\to\infty\), while the true distance remains exactly zero.

### Verdict

The theorem is correct, but the **global product**
\[
\frac K2N_{G,\parallel}^2
\]
is not an acceptable final engineering error metric. Curvature can be large in a region where the tangential displacement is identically zero.

This is not a pathology outside the model class: both curves are regular \(C^1\) non-rational piecewise cubics and share the same image.

The failure is specifically a loss of locality caused by replacing the pointwise Taylor remainder by one global curvature supremum.

---

## 4. Why simply combining maxima more carefully does not solve Attack B

There are two distinct sources of conservatism.

If \(K\) were fixed, replacing
\[
\sup n+\sup q
\]
by
\[
\sup(n+q)
\]
can improve the result, but only by at most a factor two for nonnegative \(n,q\):
\[
\sup n+\sup q\le2\sup(n+q).
\]
So separating the maxima of normal and tangential terms is not the main problem.

The fatal loss is taking
\[
K=\sup\kappa
\]
independently of the location where the tangential shift occurs. In the counterexample, \(\kappa=0\) wherever \(E\neq0\), but the global \(K\) is arbitrarily large elsewhere.

Any successful refinement must restore locality between curvature and the parameter shift.

---

## 5. Attack C — high curvature at the same location is real, not an artifact

The previous counterexample does **not** imply that the quadratic curvature term itself can be removed.

For a unit-speed reference curve,
\[
\gamma(s+\delta)
=\gamma(s)+T(s)\delta+\frac12\kappa_{\rm vec}(s)\delta^2+o(\delta^2).
\]
Thus if a displacement is purely tangential to first order,
\[
\Delta=\delta T,
\]
then the mismatch to the shifted reference point is generically
\[
-\frac12\kappa_{\rm vec}\delta^2+o(\delta^2).
\]
Therefore the coefficient
\[
\frac12\kappa\delta^2
\]
is asymptotically sharp when curvature and tangential shift occur at the same location.

### Verdict

The next theory should **localize** curvature rather than delete curvature.

---

## 6. Attack D — curved pure reparameterization confirms only first-order invariance

For an abstract smooth unit-speed curve, let
\[
\widetilde\gamma(s)=\gamma(s+\zeta(s)),
\qquad \zeta(0)=\zeta(L)=0.
\]
The two images are identical, hence \(d_H=0\). Expanding,
\[
\widetilde\gamma-\gamma
=\zeta T+\frac12\kappa_{\rm vec}\zeta^2+O(\zeta^3).
\]
So the synchronized normal component is itself generally \(O(\kappa\zeta^2)\), and the current linearized correspondence does not recover exact zero on curved geometry.

This is a genuine limitation of a first-order quotient.

However, one should not overstate this as an immediate in-class counterexample: a generic nonlinear reparameterization of a non-linear polynomial cubic is no longer cubic. The direct in-class failure is Attack B above, which is sufficient on its own.

### Verdict

Exact reparameterization invariance requires a nonlinear correspondence, not merely first-order tangent removal.

---

## 7. Attack E — near self-approach exposes a target-metric issue

The constructed \(\rho\) is an orientation-preserving correspondence. Therefore the current proof actually produces a Fréchet-like matching cost and only then uses
\[
d_H\le d_F^+.
\]

This is safe, but near self-intersections or strong self-approach the gap between Hausdorff and any order-preserving matching can be large. A curve can visit two spatially separated lobes in one order while another parameterized curve visits essentially the same image in a different order; Hausdorff can be zero or tiny while an order-preserving leash distance remains large.

### Verdict

No logical failure occurs: an explicit correspondence always gives a valid Hausdorff upper bound. But if the final engineering objective is *only* Hausdorff distance, no order-preserving method can be uniformly tight on curves with ambiguous self-correspondence.

This forces a modeling decision later:
- if CAD simplification should preserve traversal/order/topological meaning, the stronger correspondence is a feature;
- if only the point-set image matters, a tubular/reach assumption or a more flexible correspondence is necessary for tightness.

---

## 8. Attack F — short spans and double knots survive mathematically

A double knot makes \(C''\), and hence curvature, jump one-sidedly. The proof only needs continuous tangent and bounded one-sided curvature, so this does not invalidate the theorem.

Very short knot spans also do not increase algebraic degree. They can, however, create badly scaled polynomial coefficients. Normalizing every span to \([0,1]\), using Bernstein form, and employing interval/root-isolation methods is the natural numerical defense.

### Verdict

These are engineering-conditioning issues, not structural failures.

---

## 9. Overall stage verdict

The attack did **not** destroy the core \(D^2\)/Green program:

- exact representation complexity survives;
- exact synchronized Green error survives;
- fixed-degree certification survives;
- the normal component remains the correct first-order geometric residual;
- low-speed and double-knot attacks do not produce theoretical contradictions.

But the attack **did break the current proposed global geometry-aware bound as a practical metric**. The counterexample in Section 3 shows arbitrarily bad overestimation even when the candidate and reference have identical images.

Therefore Session 0006 was premature to regard
\[
N_{G,\perp}+\frac K2N_{G,\parallel}^2
\]
as a plausible final certification quantity.

This is a useful failure: it identifies the exact place where information is being lost—globalization of curvature.

No stage-level TeX note should be written yet.

---

## 10. Next theoretical fork

Two repair routes are now visible.

### Route A — localize the curvature remainder

The exact remainder satisfies schematically
\[
R(s)=\int_0^{\delta(s)}\bigl(T(s+r)-T(s)\bigr)\,dr,
\]
so one may use curvature only along the arc actually traversed by the shift. This fixes the Section 3 counterexample in principle.

The difficulty is computational: a moving arc-length interval may reintroduce arc-length inversion or a nonlocal envelope. The next step should determine whether a useful local bound can remain algebraic in the native spline parameter.

### Route B — replace the linearized shift by a nonlinear local normal correspondence

Seek \(u=\sigma(t)\) near \(t\) satisfying
\[
\bigl(\widetilde C(t)-C(u)\bigr)\cdot C'(u)=0.
\]
For a cubic reference and fixed \(t\), this is a degree-at-most-five polynomial equation in \(u\). This route is naturally related to Degen's normal-distance framework.

A valid local normal branch would:
- restore locality automatically;
- be exactly zero for genuine same-image reparameterizations on the same branch;
- avoid multiplying tangential error by unrelated remote curvature.

Its risk is branch uniqueness and the cost of certifying the branch globally in \(t\).

Given the counterexample, Route B is now the more promising main line. Route A should remain as a possible cheaper certification fallback.

The next session should therefore return to Degen/normal correspondence with this failure mechanism in mind, not as a generic literature detour.
