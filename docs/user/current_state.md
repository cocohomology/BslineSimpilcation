# Current State — User-Facing Summary

## Scope

The research still targets regular \(C^1\), cubic, non-rational spline curves. The basic reduction is
\[
C\xrightarrow{D^2}q=C'',
\]
where \(q\) is piecewise linear and may jump at double knots.

The long-term objective is unchanged: simplify representation complexity under geometric tolerance, using an error structure tighter than classical global \(L^p\)-type surrogates but cheaper and more structured than direct Hausdorff optimization.

---

## Stable foundation

### 1. Representation complexity is exact in the \(C''\) domain

For \(C^1\) piecewise cubics,
\[
D^2:S_3^1\to PL_{\rm disc}
\]
is onto with affine kernel. Jumps and continuous kinks of \(C''\) encode double and simple cubic knots respectively. With \(K_0\) kinks and \(J\) jumps,
\[
\kappa(q)=K_0+2J,
\qquad
N_{\rm ctrl}=4+\kappa(q)
\]
for a minimal open/clamped cubic representation.

### 2. Fixed-endpoint synchronized error is exact and cheap to certify

Let
\[
E=C-\widetilde C,
\qquad e=C''-\widetilde C'',
\qquad E(a)=E(b)=0.
\]
Then
\[
E=G_De,
\qquad N_G=\|E\|_\infty,
\]
and
\[
d_H\le N_G.
\]
For PL \(e\), \(E\) is piecewise cubic and its exact maximum reduces to fixed-degree one-variable polynomial extrema (degree at most five for the basic synchronized max), or certified Bézier subdivision.

### 3. Normal error is the correct first-order geometric residual

Using reference arc length and unit tangent \(T\), a first-order tangential shift removes the synchronized tangential component. Locally,
\[
\gamma(s+\delta)
=\gamma(s)+T\delta+\frac12\kappa_{\rm vec}\delta^2+o(\delta^2).
\]
Thus normal displacement enters at first order, while tangential displacement affects geometry only at second order through curvature.

The normal/tangential terms, curvature, regularity, and monotonicity of the constructed correspondence all remain fixed-degree algebraic certification problems on cubic spans.

---

## First adversarial review — an important negative result

The previous candidate global bound was
\[
\boxed{
d_H\le N_{G,\perp}+\frac K2N_{G,\parallel}^2,
}
\]
where \(K=\sup\kappa\) is one global curvature bound.

The inequality is correct, but Session 0007 produced an explicit **regular \(C^1\) piecewise-cubic counterexample showing that it can be arbitrarily conservative even when the two curve images are exactly identical.**

The construction is simple in principle:

- one part of the reference curve is a straight segment;
- a small monotone piecewise-cubic tangential redistribution changes only the parameterization of that straight segment;
- elsewhere, where the error is exactly zero, the reference curve contains a region of arbitrarily large curvature;
- the candidate and reference trace exactly the same point set, so
  \[
  d_H=0;
  \]
- the synchronized error is purely tangential, so
  \[
  N_{G,\perp}=0;
  \]
- nevertheless the global term \((K/2)N_{G,\parallel}^2\) can be made arbitrarily large by increasing curvature in the unrelated remote region.

Therefore the current global-curvature expression is **rejected as a practical final metric**.

This does not invalidate the first-order analysis. It identifies the actual information loss: curvature was globalized independently of where the tangential displacement occurs.

---

## What survived the attack

The attack did not collapse the main program.

A badly parameterized straight-line family with \(\min\|C'\|\to0\) is still recognized exactly as zero geometric error in exact arithmetic. This means arc-length normalization really does remove fake parameter-speed effects; very small speed is mainly a numerical-conditioning issue.

High curvature itself is also not an artifact. When curvature and tangential shift occur at the same location, the \(\kappa\delta^2/2\) term is the correct second-order geometry and is asymptotically sharp. The repair therefore has to restore **locality**, not delete curvature.

Short knot spans and double knots produce conditioning and one-sided-curvature issues but no logical contradiction.

Near self-approach exposes a different limitation: the current construction uses an order-preserving correspondence and is therefore closer to a Fréchet-style upper bound than a Hausdorff-optimal matching. This is always safe, but can be much more conservative than Hausdorff when spatial correspondence is ambiguous. Later we will need to decide whether preserving traversal/order is desirable CAD semantics or merely unnecessary conservatism.

---

## Current stage verdict

This was a useful failure rather than a collapse.

The following pieces remain strong:
\[
\boxed{
\text{exact representation complexity}
\to
\text{exact synchronized Green error}
\to
\text{fixed-degree certification}
\to
\text{normal error as first-order geometry}
}
\]

What failed is the attempt to close the chain using one global curvature supremum.

Therefore **there is no stage-level TeX note yet**. Writing one now would prematurely polish a framework whose final geometric bridge has already shown a structural weakness.

---

## Next research direction

The preferred repair is now a **nonlinear local normal correspondence** rather than another global estimate.

Seek a local branch \(u=\sigma(t)\) satisfying
\[
\boxed{
(\widetilde C(t)-C(u))\cdot C'(u)=0.
}
\]
This is the natural nonlinear version of “remove tangential error.” For a cubic reference and fixed \(t\), the equation is polynomial of degree at most five in \(u\).

This route is attractive because it should:
- restore locality automatically;
- give exact zero for genuine same-image reparameterizations on the same local branch;
- avoid multiplying tangential error by curvature somewhere else on the curve;
- connect directly to Degen's normal-distance framework already present in the project literature.

The next session will therefore return to Degen with a very specific question: whether the normal correspondence can be made locally unique and certifiable without becoming essentially the full Hausdorff/nearest-point problem.

A secondary fallback is to localize the curvature remainder to the actual shifted arc interval, but that may reintroduce arc-length inversion and is currently less attractive.
