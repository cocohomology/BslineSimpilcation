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
is onto with affine kernel. Jumps/kinks of \(q\) encode minimal cubic knot multiplicity exactly. With \(K_0\) continuous kinks and \(J\) jumps,
\[
\kappa(q)=K_0+2J,
\qquad N_{\rm ctrl}=4+\kappa(q).
\]

### F2 — exact synchronized error
Under \(E(a)=E(b)=0\),
\[
E=G_De,
\qquad N_G=\|E\|_\infty,
\]
and
\[
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)\le N_G.
\]

### F3 — direct certification of \(N_G\)
For PL \(e\), \(E\) is piecewise cubic. Its Euclidean maximum reduces to degree-at-most-five stationarity equations, or to certified cubic Bézier subdivision.

### F4 — first-order quotient of tangential error
Using reference arc length, let \(T\) be unit tangent and \(K\) an essential curvature bound. Define
\[
N_{G,\perp}=\sup\|P_NE\|,
\qquad
N_{G,\parallel}=\sup|E\cdot T|.
\]
The correspondence
\[
\rho(s)=s-E(s)\cdot T(s)
\]
removes tangential synchronized error to first order. When \(\rho\) is orientation preserving,
\[
\boxed{
d_H\le N_{G,\perp}+\frac K2N_{G,\parallel}^2.
}
\]
For a straight line, pure tangential redistribution is recognized exactly; for curved pure reparameterization the residual is generally quadratic, not zero.

### F5 — geometry-aware terms remain fixed-degree certifiable
On a cubic span define
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
For curvature,
\[
\kappa^2=\frac{W}{S^3},
\qquad
W=S(a\cdot a)-(v\cdot a)^2,
\]
and the derivative relation \(a=v'\) lowers \(\deg W\) to at most four.

Exact maxima reduce to fixed-degree one-variable equations:
- normal error: degree \(\le13\);
- tangential error: degree \(\le8\) after removing a zero factor;
- \(\|D_sE\|\): degree \(\le6\);
- curvature: degree \(\le7\).

More importantly, the correspondence monotonicity can be checked directly. Since
\[
\delta=-\frac{B}{\sqrt S},
\]
\[
\rho'(s)=\frac{H}{2S^2},
\qquad
\boxed{H=2S^2-2B'S+BS'.}
\]
Thus, under regularity \(S>0\),
\[
\boxed{\rho'>0\iff H>0,}
\]
and \(H\) has degree at most eight.

This is stronger and less conservative than the previous sufficient condition based on separate global norm maxima.

Detailed derivations:
- `docs/internal/derivations/arc_length_tangential_quotient.md`
- `docs/internal/derivations/geometry_aware_certification.md`

## Current interpretation

The current framework now has a coherent chain:

1. exact representation complexity in the \(C''\) domain;
2. exact synchronized positional error through a Green operator;
3. low-degree certification of synchronized error;
4. first-order removal of parameterization artifacts by tangential quotient;
5. a certified Hausdorff upper bound whose required quantities remain local fixed-degree univariate problems.

This is strong enough to trigger a stage review, but not yet enough to claim a final method or novelty.

## Main risks to attack next

- near-zero speed: formulas are valid under regularity but may be ill-conditioned;
- high curvature: quadratic tangential correction may become too large;
- curved pure reparameterization: true distance can be zero while current bound is only second-order small;
- near self-approach: the constructed order-preserving correspondence may be safe but far from optimal;
- use of separate global maxima \(N_{G,\perp}\), \(K\), \(N_{G,\parallel}\) may still be conservative;
- short knot spans may create large coefficients even when geometry is mild;
- double knots require one-sided curvature treatment.

## Next target

A dedicated adversarial stage review, not more forward derivation.

The review should attempt to break the framework with explicit families and determine whether the remaining conservatism is acceptable, structural, or fatal. A targeted literature search should accompany the review before any novelty claim.

If the framework survives, write the first full TeX note. If it fails, record the failure before redesigning the metric/correspondence.
