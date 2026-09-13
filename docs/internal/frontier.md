# Research Frontier — Internal

## Current narrow problem

Work with regular \(C^1\), cubic, non-rational spline curves \(C:[a,b]\to\mathbb R^d\), using the endpoint-preserving gauge unless explicitly stated otherwise.

Canonical notation:
\[
q=C'',\qquad \widetilde q=\widetilde C'',\qquad e=q-\widetilde q,
\qquad E=C-\widetilde C=G_De.
\]

---

## Stable foundation

### F1. Exact D2 reduction — Session 0002

\[
D^2:S^1_3\to PL_{\rm disc}
\]
is onto with affine kernel. The jump/kink structure of \(q=C''\) records minimal cubic knot multiplicity exactly. If \(K_0\) counts continuous kinks and \(J\) jumps,
\[
\kappa(q)=K_0+2J,
\qquad N_{\rm ctrl}=4+\kappa(q)
\]
for a minimal open/clamped cubic.

### F2. Fixed-endpoint Green operator — Session 0003

For
\[
E''=e,\qquad E(a)=E(b)=0,
\]
\[
E=G_De,
\qquad
N_G(e):=\|E\|_\infty.
\]
Then \(N_G\) is exact synchronized positional error and
\[
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)\le N_G(e).
\]

### F3. Direct certification of \(N_G\) — Session 0004

For PL \(e\), the error curve \(E\) is piecewise cubic. Its Euclidean max norm is obtained from span boundaries and roots of
\[
E\cdot E'=0,
\]
a degree-at-most-five polynomial per span. A second certified route uses cubic Bézier convex-hull bounds and de Casteljau subdivision.

Thus synchronized error is both exact and low-degree certifiable.

### F4. Arc-length tangential quotient — Session 0005

Let \(s\) be arc length of the regular reference curve, \(T=dC/ds\), and
\[
K:=\operatorname*{ess\,sup}\kappa
\]
the geometric curvature bound.

The candidate displacement is \(\Delta=\widetilde C-C=-E\). Define the signed tangential shift
\[
\delta(s)=\Delta(s)\cdot T(s)=-E(s)\cdot T(s),
\qquad
\rho(s)=s+\delta(s).
\]
If endpoints agree and
\[
\boxed{
\|D_sE\|_\infty+K\|E\|_\infty<1,
}
\]
then \(\rho\) is an orientation-preserving homeomorphism of the complete arc-length interval.

Let
\[
N_{G,\perp}(e)=\sup_t\|P_{N(t)}E(t)\|,
\qquad
N_{G,\parallel}(e)=\sup_t|E(t)\cdot T(t)|.
\]
Then
\[
\boxed{
 d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)
\le d_F^+(C,\widetilde C)
\le
N_{G,\perp}(e)+\frac K2N_{G,\parallel}(e)^2
}
\]
and hence
\[
\boxed{
 d_H\le N_{G,\perp}(e)+\frac K2N_G(e)^2.
}
\]

Interpretation: synchronized normal error is the first-order geometric residual; tangential error is a first-order reparameterization direction and contributes only quadratically through curvature.

Detailed derivation: `docs/internal/derivations/arc_length_tangential_quotient.md`.

---

## Important lesson from Session 0005

A direct correction in the original parameter leads to a remainder involving \(\|C''\|\), which is contaminated by tangential speed variation. A badly parameterized straight line may have large \(C''\) despite zero geometric curvature.

Using reference arc length removes this artifact: the remainder depends on geometric curvature \(K\), and for a straight line \(K=0\) the purely tangential correction is exact.

This is the first point where the framework genuinely improves the bad-parameter problem rather than merely restating synchronized error.

---

## Theorem status

### T1. Exact reconstruction / complexity theorem — ESTABLISHED

Session 0002.

### T2a. Fixed-endpoint Green identity — ESTABLISHED

Session 0003.

### T2c. PL-specific direct certification of \(N_G\) — ESTABLISHED

Session 0004.

### T3a. First-order tangential quotient with finite geometric bound — ESTABLISHED

Session 0005.

Caution: do not claim exact reparameterization invariance. On a curved pure reparameterization, the present bound is generally only second-order rather than zero.

### T3b. Algebraic/certified evaluation of the geometry-aware bound — NEXT TARGET

Need to determine whether the new quantities preserve the fixed-degree computational advantage:
- \(N_{G,\perp}\);
- \(\|D_sE\|_\infty\);
- curvature bound \(K\);
- monotonicity condition.

Questions:
- what rational/polynomial degrees arise spanwise?
- can maxima/inequalities be certified with fixed-degree root isolation or Bernstein subdivision?
- does tangent normalization cause numerical pathologies near low speed?
- is the total cost still structurally local/linear in the number of spans?

Do not design breakpoint optimization yet.

### T4. Stronger nonlinear correspondence / exact reparameterization invariance — POSTPONED

Only open this if the quadratic local bound proves insufficient.

---

## Counterexamples/tests to preserve

1. same straight line with nonlinear parameterization;
2. curved pure reparameterization (true distance zero, current bound quadratic);
3. short-span second-derivative spike;
4. adjacent cancellation pair;
5. near self-approach causing correspondence ambiguity;
6. high curvature;
7. double-knot jump;
8. near-zero speed / loss of regularity.

---

## Goal-alignment review after Session 0005

The research remains strongly aligned. The previous dominant weakness was parameterization sensitivity. Session 0005 shows that a local order-preserving correspondence can quotient out tangential error to first order while retaining a certified Hausdorff upper bound.

The next decision point is computational: if the geometry-aware terms are still fixed-degree certifiable for cubic splines, the framework may have crossed from a useful reformulation into a genuinely viable simplification architecture.

---

## Stop / pivot conditions

Pause or pivot if:
- evaluating \(N_{G,\perp}\), curvature, or monotonicity becomes comparable to full curve-curve correspondence search;
- low-speed regions make the arc-length normalization unstable in realistic inputs;
- the quadratic curvature term is systematically too conservative;
- exact reparameterization invariance is required and forces a problem essentially equivalent to full Fréchet/Hausdorff optimization.
