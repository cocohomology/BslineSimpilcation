# Research Frontier — Internal

## Current narrow problem

Work with regular \(C^1\), cubic, non-rational spline curves \(C:[a,b]\to\mathbb R^d\), using the endpoint-preserving gauge unless explicitly stated otherwise.

Let
\[
q=C'',\qquad \widetilde q=\widetilde C'',\qquad e=q-\widetilde q,
\qquad E=C-\widetilde C.
\]

---

## Stable foundation

### F1. Exact D2 reduction — Session 0002

\[
D^2:S^1_3\to PL_{\rm disc}
\]
is onto with kernel \(\mathcal P_1\). After fixing two vector integration constants, every discontinuous PL second derivative reconstructs uniquely to a \(C^1\) cubic.

Minimal cubic knot multiplicity is encoded exactly by \(q=C''\):
- jump -> double knot;
- continuous kink -> simple knot;
- neither -> redundant breakpoint.

If \(K\) is the number of continuous kinks and \(J\) the number of jumps,
\[
\kappa(q)=K+2J,
\qquad N_{\rm ctrl}=4+\kappa(q)
\]
for a minimal open/clamped cubic.

### F2. Fixed-endpoint Green operator — Session 0003

For
\[
E''=e,\qquad E(a)=E(b)=0,
\]
\[
E(t)=G_De(t)=\int_a^bK_D(t,s)e(s)\,ds,
\]
with
\[
K_D(t,s)=-\frac{(\min\{t,s\}-a)(b-\max\{t,s\})}{b-a}.
\]
Define
\[
N_G(e)=\|G_De\|_\infty.
\]
Then
\[
N_G(e)=\|C-\widetilde C\|_{\infty,\mathrm{sync}},
\qquad
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)\le N_G(e).
\]

### F3. PL-specific exact/certified evaluation — Session 0004

On the union partition \(a=x_0<\cdots<x_n=b\), write
\[
e(t)=\alpha_i+\beta_i(t-x_i).
\]
The endpoint correction requires only
\[
E'(a)=-\frac1{b-a}\int_a^b(b-s)e(s)\,ds.
\]
Then on each span, with \(h=t-x_i\),
\[
E(t)=P_i+V_i h+\frac12\alpha_i h^2+\frac16\beta_i h^3.
\]
Thus \(E\) is piecewise cubic and \(E'\) piecewise quadratic.

For Euclidean vector error,
\[
F(t)=\|E(t)\|^2,
\qquad
F'(t)=2E(t)\cdot E'(t),
\]
and the stationarity polynomial has degree at most five, generically exactly five. Hence \(N_G\) is obtained from span boundaries plus the real roots of one fixed-degree quintic per span.

Two certification routes are now available:

1. fixed-degree real-root isolation of \(E\cdot E'\);
2. cubic Bézier convex-hull bounds with de Casteljau subdivision, with root isolation as an exact-boundary fallback.

Structural cost is one global moment + a linear pass + \(O(n)\) fixed-degree local subproblems. This is not a uniform bit-complexity claim.

Detailed derivation: `docs/internal/derivations/pl_green_evaluation.md`.

---

## Current interpretation

The synchronized part of the D2 framework is now unusually clean:

1. **complexity** is represented exactly by PL jump/kink structure;
2. **endpoint-preserving synchronized positional error** is represented exactly by the Green operator;
3. **that exact error can be certified directly** using low-degree univariate polynomial geometry.

Therefore ordinary \(L^p\) norms are no longer required as the primary synchronized metric merely because they are easy to compute. They remain possible cheap bounds/pruning tools and comparison points with Lyche--Mørken.

The main theoretical risk has moved decisively to **parameterization**. A synchronized error may still be much larger than the true geometric mismatch if one curve mainly slides points tangentially along essentially the same shape.

---

## Theorem status

### T1. Exact reconstruction / complexity theorem — ESTABLISHED

Session 0002.

### T2a. Fixed-endpoint Green kernel / synchronized-error identity — ESTABLISHED

Session 0003.

### T2c. PL-specific exact/certified evaluation of \(N_G\) — ESTABLISHED

Session 0004.

### T2b. Sharp \(L^p\to L^\infty\) bounds — OPEN, SECONDARY

Return only if useful for pruning, comparison with Lyche, or quantifying conservatism.

### T3a. First-order removal of tangential error by reparameterization — NEXT TARGET

Given a nearby regular reference curve \(C\) and
\[
\widetilde C=C+E,
\]
decompose
\[
E=E_\parallel+E_\perp.
\]
Seek a small monotone parameter change
\[
\phi(t)=t+\eta(t)
\]
whose first-order effect cancels \(E_\parallel\).

Questions for the next session only:
- derive the correct formula for \(\eta\) and fix the mapping direction/sign carefully;
- derive an explicit second-order remainder rather than writing only \(O(\|E\|^2)\);
- identify the assumptions needed on \(\|C'\|\), curvature/\(C''\), and \(E'\);
- determine a simple sufficient condition for monotonicity \(\phi'>0\);
- test against a pure reparameterization of a straight line and a curved reference;
- decide whether \(\|P_NE\|_\infty\) deserves promotion from heuristic to first-order quotient quantity.

Do **not** attempt a full Hausdorff theorem in the same session.

### T3b. Normal-projected Green quantity — POSTPONED UNTIL T3a REVIEW

Potential quantity
\[
N_{G,\perp}(e)=\sup_t\|P_{N(t)}G_De(t)\|.
\]
Do not call it a norm before understanding its null directions and reference-curve dependence.

### T4. Local normal/Hausdorff comparison — POSTPONED

---

## Counterexamples/tests to preserve

1. same straight line with nonlinear parameterization;
2. short-span second-derivative spike;
3. adjacent cancellation pair;
4. near self-approach causing correspondence ambiguity;
5. high curvature / tubular-neighborhood failure;
6. double-knot jump;
7. tangential perturbation large in synchronized error but small geometrically.

---

## Goal-alignment review after Session 0004

No drift detected. The synchronized Green metric was introduced specifically to retain more structure than \(L^p\) while remaining cheaper than direct Hausdorff evaluation. Session 0004 confirms the evaluability side: it reduces to independent univariate fixed-degree problems.

The project should now stop polishing synchronized theory and confront the original geometric weakness: parameterization dependence.

---

## Stop conditions

Pause/report if:
- removing parameterization sensitivity requires an optimization essentially equivalent to full Fréchet/Hausdorff search;
- tangential quotient ideas fail even locally on simple regular curves;
- geometry-aware correction destroys the low-degree/local structure inherited from \(C''\);
- low weighted complexity of \(q\) does not translate into useful geometric simplification.
