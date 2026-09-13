# Research Frontier — Internal

## Current setting

Work with regular \(C^1\), cubic, non-rational spline curves \(C:[a,b]\to\mathbb R^d\), preserving endpoints. Canonical notation:
\[
q=C'',\qquad \widetilde q=\widetilde C'',\qquad e=q-\widetilde q,
\qquad E=C-\widetilde C=G_De.
\]

## Stable foundation

### F1 — exact \(D^2\) reduction
\[
D^2:S_3^1\to PL_{\rm disc}
\]
is onto with affine kernel. Jump/kink structure of \(q\) records minimal cubic knot multiplicity exactly.

### F2 — exact synchronized Green error
Under fixed endpoints,
\[
E=G_De,\qquad N_G=\|E\|_\infty,
\]
and \(d_H\le N_G\). For PL \(e\), \(N_G\) is fixed-degree certifiable.

### F3 — normal displacement is the first-order geometric residual
The Session-0005 arc-length shift removes tangential synchronized error to first order. Session 0008 now identifies this shift as the first Newton/IFT linearization of the nonlinear normal-projection equation.

### F4 — first geometry-aware global-curvature product rejected
The expression
\[
N_{G,\perp}+\frac K2N_{G,\parallel}^2
\]
is correct but can be arbitrarily conservative because curvature may be large far from the support of tangential error. The failure is globalization of geometry, not the local tangent/normal decomposition.

## New structural lesson from Degen — admissibility before the norm

Degen's useful lesson for this project is methodological. His construction proceeds in the order
\[
\boxed{
\text{normal neighbourhood}
\to\text{admissible class}
\to\text{unique correspondence}
\to\text{deviation field}
\to\text{sup norm}
\to\text{Hausdorff relation}.
}
\]

This suggests that our next metric should not be guessed directly as another norm of \(E\). We should first build a certified geometric coordinate chart for nearby candidates.

Detailed analysis: `docs/internal/derivations/degen_admissibility_lesson.md`.

## Current main object — nonlinear normal branch

Define
\[
F(t,u):=(\widetilde C(t)-C(u))\cdot C'(u).
\]
Seek a local branch \(u=\sigma(t)\) satisfying
\[
F(t,\sigma(t))=0.
\]
For fixed \(t\) and cubic reference span, \(\deg_u F\le5\).

At a normal root, with \(r=\widetilde C(t)-C(u)\),
\[
F_u=-\|C'(u)\|^2+r\cdot C''(u).
\]
Hence a natural local nondegeneracy condition is
\[
\boxed{\|C'(u)\|^2-r\cdot C''(u)>0.}
\]
In arc length this becomes \(1-r\cdot\kappa_{\rm vec}>0\), and \(\|r\|\kappa<1\) is a simple sufficient condition.

The branch derivative is
\[
\boxed{
\sigma'(t)=
\frac{\widetilde C'(t)\cdot C'(\sigma(t))}
{\|C'(\sigma(t))\|^2-r\cdot C''(\sigma(t))}.
}
\]
Thus normal-coordinate degeneracy and orientation loss are separate conditions.

## Major synthesis with previous work

At the synchronized guess \(u=t\), one Newton/IFT correction gives
\[
\boxed{
\sigma(t)-t\approx-
\frac{E(t)\cdot C'(t)}{\|C'(t)\|^2}.
}
\]
This is exactly the Session-0005 tangential shift in native parameter.

Therefore the earlier first-order theory is retained as the linearization/predictor for the nonlinear normal branch rather than being discarded after the counterexample.

## Normal-graph target class

If the candidate can be written as a one-to-one normal graph
\[
\widetilde C(\tau(u))=C(u)+r(u),\qquad r(u)\perp C'(u),
\]
and each matched \(C(u)\) is the unique nearest point on the reference, then
\[
\boxed{d_H(C,\widetilde C)=\|r\|_\infty.}
\]
Once admissibility is established, the sup norm of the deviation is exact rather than a global conservative surrogate.

## Revised role of the Green layer

The Green layer remains central but changes role:
- exact representation/synchronized error;
- cheap early bound;
- predictor \(\sigma_0=t-(E\cdot C')/\|C'\|^2\);
- potential source of a local root interval and admissibility certificate.

The nonlinear normal metric is not yet known to be computationally cheap.

## Current main risk

The quintic degree for fixed \(t\) is not the hard part. The hard part is branch certification:
- multiple normal roots;
- continuous selection of the intended root;
- branch switching near self-approach / small reach;
- possible coupled algebra when maximizing the deviation along the implicit branch.

## Next narrow target

Develop a **sufficient admissibility certificate** for one nearby normal branch using quantities already available from \(E=G_De\).

Questions:
- can the first-order predictor be enclosed in a root interval where \(F_u\) has one sign?
- can regularity, curvature/tube separation, and tangent-angle bounds guarantee \(\sigma'>0\)?
- can interval Newton / monotone-root arguments work spanwise without a global nearest-point search?
- what assumptions are realistic for ordinary CAD simplification inputs?

Do not yet maximize \(\|r\|_\infty\), design knot simplification, or claim a stage breakthrough.
