# Current State — User-Facing Summary

## Scope

The current branch studies regular \(C^1\), cubic, non-rational spline curves. The basic reduction is
\[
C\xrightarrow{D^2}q=C'',
\]
where \(q\) is piecewise linear and may jump at double knots.

The long-term goal remains tolerance-constrained spline simplification: reduce representation complexity while controlling geometric error more tightly than classical global \(L^p\)-type surrogates, without paying the full cost of direct Hausdorff optimization.

---

## 1. Representation complexity is exact in the \(C''\) domain

For \(C^1\) piecewise cubics,
\[
D^2:S_3^1\to PL_{\rm disc}
\]
is onto with affine kernel.

For \(q=C''\):
- a jump corresponds to a double cubic knot;
- a continuous kink corresponds to a simple knot;
- no jump/kink means the breakpoint is redundant.

If \(K_0\) is the number of continuous kinks and \(J\) the number of jumps,
\[
\kappa(q)=K_0+2J,
\qquad
N_{\rm ctrl}=4+\kappa(q)
\]
for a minimal open/clamped cubic representation.

So the second-derivative domain carries the fixed-degree representation complexity exactly.

---

## 2. Fixed-endpoint synchronized error is exact and directly certifiable

Let
\[
E=C-\widetilde C,
\qquad e=C''-\widetilde C'',
\qquad E(a)=E(b)=0.
\]
Then
\[
E=G_De
\]
through the fixed-endpoint Green operator, and
\[
N_G(e)=\|E\|_\infty
\]
is exactly the synchronized positional error. Hence
\[
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)\le N_G.
\]

For PL \(e\), the error curve \(E\) is piecewise cubic. Its exact Euclidean maximum reduces to fixed-degree one-variable polynomial problems (degree at most five for the basic synchronized max), or alternatively to certified cubic Bézier subdivision.

Thus ordinary \(L^p\) norms are no longer needed as the primary synchronized error measure merely for computational convenience.

A short Green-function refresher is stored in `docs/user/background/green_functions.md` and should be included in any later self-contained TeX note.

---

## 3. First-order parameterization correction

The main weakness of synchronized error is that tangential displacement can be mostly a parameterization artifact.

Using the arc length of the reference curve, let \(T\) be the unit tangent and \(K\) a curvature bound. Decompose the synchronized error into normal and tangential parts and define
\[
N_{G,\perp}=\sup\|P_NE\|,
\qquad
N_{G,\parallel}=\sup|E\cdot T|.
\]

The arc-length shift
\[
\rho(s)=s-E(s)\cdot T(s)
\]
removes the tangential component to first order. When this shift is orientation preserving,
\[
\boxed{
d_H\le N_{G,\perp}+\frac K2N_{G,\parallel}^2.
}
\]

Interpretation:
- normal synchronized error is the first-order geometric residual;
- tangential synchronized error contributes only quadratically through geometric curvature.

For a straight reference line, pure monotone tangential redistribution is recognized exactly as zero geometric error. For a curved pure reparameterization, the current bound is generally only second-order small rather than exactly zero.

---

## 4. The geometry-aware bound is still fixed-degree certifiable

This was the main question of Session 0006.

On one cubic span, set
\[
v=C',\quad a=C'',\quad S=v\cdot v,\quad A=E\cdot E,\quad B=E\cdot v,\quad U=E'\cdot E'.
\]
Then
\[
\|P_NE\|^2=\frac{AS-B^2}{S},
\qquad
|E\cdot T|^2=\frac{B^2}{S},
\qquad
\|D_sE\|^2=\frac{U}{S}.
\]
Curvature is
\[
\kappa^2=rac{W}{S^3},
\qquad
W=S(a\cdot a)-(v\cdot a)^2,
\]
with \(\deg W\le4\) for a cubic span.

The exact spanwise maxima reduce to fixed-degree univariate stationary equations:
- normal error: degree at most 13;
- tangential error: degree at most 8 after removing the zero factor;
- curvature: degree at most 7;
- \(\|D_sE\|\): degree at most 6.

For a simple tolerance decision, direct polynomial inequalities often have lower degree than these exact-max calculations.

### Direct monotonicity certification

A particularly useful improvement is that the correspondence monotonicity need not be certified through a conservative global norm estimate.

With
\[
\delta=-E\cdot T=-\frac{B}{\sqrt S},
\]
we obtain
\[
\rho'(s)=\frac{H}{2S^2},
\qquad
\boxed{H=2S^2-2B'S+BS'.}
\]
Therefore, under regularity \(S>0\),
\[
\boxed{\rho'>0\iff H>0,}
\]
and \(H\) has degree at most eight.

So the first geometry-aware correction still requires only local fixed-degree one-variable certification, not a coupled curve-curve nearest-point search.

Another useful fact is that the arc-length proof does **not** force an implementation to compute or invert arc length: all certification formulas can be evaluated in the original spline parameter using \(E,C',C''\).

---

## Current assessment

The current chain is now coherent:

\[
\boxed{
\text{exact representation complexity}
\to
\text{exact synchronized error}
\to
\text{low-degree certification}
\to
\text{first-order parameterization quotient}
\to
\text{certified geometric upper bound}
}
\]

and the last step still preserves the one-variable fixed-degree algebraic structure.

This is the first point where the framework looks like a plausible simplification architecture rather than only an interesting reformulation.

However, it is **not yet accepted as a stage breakthrough**. The next session is an adversarial review rather than another forward derivation.

The main risks are:
- near-zero speed and numerical conditioning;
- high curvature making the quadratic tangential term too large;
- curved pure reparameterization, where the true distance is zero but the current bound remains second-order positive;
- near self-approach, where the chosen order-preserving correspondence may be far from optimal;
- conservatism from multiplying separate global maxima that may occur at different locations;
- short knot spans and double-knot one-sided curvature.

If the framework survives that review and a targeted prior-art check, the next milestone will be the first self-contained TeX note.
