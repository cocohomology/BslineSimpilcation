# Current State — User-Facing Summary

## Scope

The current research branch remains restricted to **\(C^1\), cubic, non-rational spline curves**. The basic transformation is
\[
C\xrightarrow{D^2}q=C'',
\]
where \(q\) is piecewise linear and may jump at double knots.

The long-term goal is to simplify \(q\) while preserving a useful geometric tolerance, ideally using an error quantity that is substantially tighter than ordinary \(L^p\) surrogates but much easier to handle than direct Hausdorff distance.

---

## Stable result 1 — representation complexity is exact in the \(C''\) domain

Let \(S^1_3\) be the \(C^1\) piecewise-cubic space and \(PL_{\rm disc}\) the piecewise-affine space with possible jumps. Then
\[
D^2:S^1_3\to PL_{\rm disc}
\]
is onto with
\[
\ker D^2=\mathcal P_1.
\]
Thus
\[
S^1_3/\mathcal P_1\cong PL_{\rm disc}.
\]

For \(q=C''\):
- a jump corresponds to a double cubic knot;
- a continuous kink corresponds to a simple knot;
- no jump/kink means the breakpoint is redundant.

If \(K\) is the number of continuous kinks and \(J\) the number of jumps,
\[
\kappa(q)=K+2J,
\qquad
N_{\rm ctrl}=4+\kappa(q)
\]
for a minimal open/clamped cubic representation.

So fixed-degree spline complexity is not merely correlated with the PL second derivative; it is encoded exactly by its singularity structure.

---

## Stable result 2 — fixed-endpoint positional error has an exact Green representation

Use the endpoint-preserving gauge. Let
\[
E=C-\widetilde C,
\qquad e=C''-\widetilde C'',
\qquad E(a)=E(b)=0.
\]
Then
\[
E(t)=G_De(t)=\int_a^bK_D(t,s)e(s)\,ds,
\]
with
\[
K_D(t,s)=
-\frac{(\min\{t,s\}-a)(b-\max\{t,s\})}{b-a}.
\]

Define
\[
N_G(e)=\|G_De\|_\infty.
\]
Then
\[
\boxed{
N_G(e)=\|C-\widetilde C\|_{\infty,\text{synchronized parameter}}
}
\]
and therefore
\[
\boxed{
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)\le N_G(e).
}
\]

The Green operator retains where the second-derivative error occurs and allows sign/vector cancellation before taking the final norm. A single global \(L^p\) number discards that information earlier.

A short refresher on Green functions/kernels is stored in `docs/user/background/green_functions.md` so a later self-contained TeX note need not assume this theory is fresh in memory.

---

## Stable result 3 — the exact Green error is directly certifiable on PL data

This resolves the main concern from the previous session: perhaps \(N_G\) was exact but too expensive to evaluate.

Let
\[
a=x_0<x_1<\cdots<x_n=b
\]
be the union partition of the breakpoints of \(C''\) and \(\widetilde C''\). On each span write
\[
e(t)=\alpha_i+\beta_i(t-x_i).
\]
The endpoint condition requires only one global vector correction:
\[
E'(a)=-\frac{1}{b-a}\int_a^b(b-s)e(s)\,ds.
\]
After that, \(E\) propagates span by span and is cubic on every span:
\[
E(t)=P_i+V_i h+\frac12\alpha_i h^2+\frac16\beta_i h^3,
\qquad h=t-x_i.
\]

For Euclidean vector error,
\[
F(t)=\|E(t)\|^2
\]
is degree at most six and its stationary points satisfy
\[
E(t)\cdot E'(t)=0,
\]
a polynomial equation of degree at most five (generically exactly five).

Hence the exact maximum needs only:
- union-partition boundaries;
- the real roots of one fixed-degree quintic per span.

This gives a finite certified procedure without dense sampling. Structurally the work is linear in the number of union spans, apart from the fixed-degree root-isolation cost and precision issues near multiple roots.

There is also a CAGD-style alternative: express each cubic error segment in Bézier form, bound the entire segment by the maximum norm of its four control vectors, and use de Casteljau subdivision to tighten the bound. This gives a robust certified tolerance test with root isolation as a boundary-case fallback.

### Why this matters

The synchronized Green error is therefore not merely mathematically exact; it is also much simpler structurally than direct curve-to-curve Hausdorff evaluation. It reduces to one-parameter local polynomial extrema, whereas directed Hausdorff has the nested form
\[
\max_t\min_u\|C(t)-\widetilde C(u)\|
\]
and must handle changing nearest-point correspondences.

This is not a universal runtime theorem against all Hausdorff algorithms, but the algebraic simplification is real.

---

## Current assessment

The synchronized part of the framework is now strong:

1. candidate complexity is exact in the \(C''\) domain;
2. synchronized positional error is exact in the same domain;
3. that error can be evaluated/certified by low-degree univariate calculations.

This changes the role of ordinary \(L^p\) norms. They may still be useful for cheap pruning or comparison with Lyche--Mørken, but there is currently no reason to use them as the primary error metric merely because they are easy to compute.

The main unresolved weakness has moved to **parameterization**. A synchronized metric can overestimate geometric mismatch when two nearby curves mainly differ by tangential sliding of parameter points.

---

## Next research target

The next session will attack only the first local parameterization question:

> For a nearby regular curve \(\widetilde C=C+E\), can a small monotone reparameterization absorb the tangential component of \(E\) to first order, leaving the normal component as the first-order geometric residual?

The goal is an explicit correction and explicit remainder estimate, not yet a full Hausdorff or Fréchet theorem.

---

## What is deliberately not claimed

- \(N_G\) is not parameterization-invariant.
- No claim yet that normal projection gives a certified geometric metric.
- No breakpoint optimization algorithm has been designed.
- The structural \(O(n)\) statement for \(N_G\) evaluation is not a uniform finite-precision bit-complexity theorem.
- No source-code test is currently needed.

No TeX stage note has been created yet. The synchronized theory is now coherent, but the genuinely geometry-aware step has not yet survived review.
