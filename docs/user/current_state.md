# Current State — User-Facing Summary

## Scope

The research still targets regular \(C^1\), cubic, non-rational spline curves. The structural reduction remains
\[
C\xrightarrow{D^2}q=C'',
\]
with \(q\) piecewise linear and possibly discontinuous at double knots.

The objective is unchanged: simplify representation complexity under a geometric tolerance, using a structure tighter than global \(L^p\) surrogates but cheaper and more controllable than a full Hausdorff optimization.

---

## Stable foundation

### 1. Complexity is exact in the \(C''\) domain

For \(C^1\) piecewise cubics,
\[
D^2:S_3^1\to PL_{\rm disc}
\]
is onto with affine kernel. Jumps and continuous kinks of \(C''\) encode double and simple cubic knots, so fixed-degree representation complexity is carried exactly by the second derivative.

### 2. Fixed-endpoint synchronized error is exact and cheap

With
\[
E=C-\widetilde C,
\qquad e=C''-\widetilde C'',
\qquad E(a)=E(b)=0,
\]
we have
\[
E=G_De.
\]
The synchronized max error \(\|E\|_\infty\) is a rigorous Hausdorff upper bound and, for cubic splines, is directly certifiable by fixed-degree one-variable calculations or Bézier subdivision.

### 3. The first-order tangent/normal analysis remains valid

Tangential synchronized displacement is a first-order reparameterization direction; normal displacement is the first-order geometric residual. The previous global curvature closure was rejected because it can be extremely conservative when large curvature is remote from the tangential error, but this does not invalidate the local first-order decomposition.

---

## New lesson from Degen: the norm should come after the correspondence

The latest session returned to Degen's 1992 paper, but not to copy his normal distance mechanically.

The important structure in Degen's argument is:
\[
\boxed{
\text{build a normal neighbourhood}
\to
\text{restrict to admissible candidates}
\to
\text{obtain a unique correspondence}
\to
\text{derive a deviation function}
\to
\text{take its max norm}.
}
\]

In other words, the difficult part is not choosing \(L^\infty\); the difficult part is creating a geometric coordinate chart in which the deviation has the right meaning.

This changes our own strategy. We no longer treat the final error as “some improved norm of synchronized Green error.” Instead, the Green error becomes a cheap predictor and certificate for a more geometric nonlinear correspondence.

---

## Nonlinear normal correspondence

For a candidate point \(\widetilde C(t)\), seek a nearby reference parameter \(u=\sigma(t)\) satisfying
\[
\boxed{
(\widetilde C(t)-C(u))\cdot C'(u)=0.
}
\]
This says that the displacement from the reference to the candidate is normal to the reference curve.

For fixed \(t\) and a cubic reference span, this is a polynomial equation of degree at most five in \(u\).

At a normal root, define
\[
r=\widetilde C(t)-C(u).
\]
The implicit-function denominator is
\[
\boxed{
\|C'(u)\|^2-r\cdot C''(u).
}
\]
In reference arc length it becomes
\[
1-r\cdot\kappa_{\rm vec}.
\]
Thus the usual “distance smaller than local radius of curvature” intuition appears naturally as the condition that normal coordinates do not degenerate.

The branch derivative is
\[
\boxed{
\sigma'(t)=
\frac{\widetilde C'(t)\cdot C'(\sigma(t))}
{\|C'(\sigma(t))\|^2-r\cdot C''(\sigma(t))}.
}
\]
So branch orientation and normal-coordinate degeneracy can be inspected separately.

---

## A useful synthesis with our previous work

The previous first-order tangential correction now has a clearer interpretation.

Starting from the synchronized guess \(u=t\), one Newton/implicit-function step gives
\[
\boxed{
\sigma(t)-t
\approx
-\frac{E(t)\cdot C'(t)}{\|C'(t)\|^2}.
}
\]
This is exactly the shift derived earlier from the arc-length tangent decomposition.

So the first-order theory was not a discarded detour. It is the linearization of the full nonlinear normal projection.

---

## Why the nonlinear normal deviation is attractive

Suppose the candidate forms a one-to-one normal graph over the reference:
\[
\widetilde C(\tau(u))=C(u)+r(u),
\qquad r(u)\perp C'(u),
\]
and every matched reference point is the unique nearest point on the reference curve.

Then
\[
\boxed{d_H(C,\widetilde C)=\|r\|_\infty.}
\]

So inside a genuine non-overlapping tubular neighbourhood, the normal deviation max is not merely an upper bound; it is the Hausdorff distance itself.

This is the regime we would like to certify, rather than approximating it by one global curvature constant.

---

## Revised role of the \(D^2\)/Green framework

The project now has three layers:

1. **representation layer:** \(C''\) carries cubic complexity exactly;
2. **synchronized layer:** \(E=G_De\) is exact, cheap, and easy to certify;
3. **geometric layer:** use \(E\) to predict and certify a nearby nonlinear normal branch.

The first normal-branch predictor is
\[
\sigma_0(t)=t-rac{E\cdot C'}{\|C'\|^2}.
\]

This may let us avoid a global nearest-point search if the candidate is already known to be close.

---

## Current unresolved problem

A quintic equation for each fixed \(t\) is not by itself difficult. The real issue is selecting and certifying the **correct continuous root branch**:

- several normal roots may exist;
- roots can compete near self-approach or small reach;
- the intended root must remain continuous and orientation preserving;
- maximizing the nonlinear normal deviation may be more complicated than the synchronized Green max.

Therefore we have **not** yet shown that the nonlinear normal metric is as cheap as the Green metric.

The next session will focus only on a sufficient admissibility certificate: can the Green predictor, local curvature/tube bounds, and tangent-angle information certify one nearby root branch without solving the full curve-to-curve nearest-point problem?

No TeX stage note yet; no source-code test is currently needed.
