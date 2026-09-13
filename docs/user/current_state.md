# Current State — User-Facing Summary

## Scope of the current side project

The present research branch remains restricted to **\(C^1\), cubic, non-rational spline curves**. The broader spline-simplification problem is intentionally postponed.

The basic transformation is
\[
C\xrightarrow{D^2}q=C'',
\]
where \(q\) is piecewise linear, possibly discontinuous at double knots. The strategy is to simplify \(q\), then reconstruct a cubic candidate.

The central long-term question is still the error measure: it should exploit the simple PL structure, be tighter than ordinary \(L^p\) surrogates, and eventually move closer to geometric/Hausdorff error without becoming equally difficult.

---

## Stable result 1 — the D2 reduction is exact

Let \(S^1_3\) denote \(C^1\) piecewise-cubic curves and \(PL_{\rm disc}\) piecewise-affine vector functions with possible jumps. Then
\[
D^2:S^1_3\to PL_{\rm disc}
\]
is surjective with
\[
\ker D^2=\mathcal P_1.
\]
Thus
\[
S^1_3/\mathcal P_1\cong PL_{\rm disc}.
\]

The singularity type of \(q=C''\) exactly records minimal cubic knot multiplicity:
- jump in \(q\) -> double knot;
- continuous kink -> simple knot;
- neither -> redundant breakpoint.

If \(K\) is the number of continuous kinks and \(J\) the number of jumps,
\[
\kappa(q)=K+2J,
\qquad
N_{\rm ctrl}=4+\kappa(q)
\]
for a minimal open/clamped cubic representation.

This means simplification in the second-derivative domain is not merely a visual polyline analogy: at fixed cubic degree it carries the representation complexity exactly.

---

## Stable result 2 — fixed-endpoint error has an exact Green representation

The current default gauge preserves both endpoint positions. Let
\[
E=C-\widetilde C,
\qquad e=C''-\widetilde C'',
\]
with
\[
E(a)=E(b)=0.
\]
Then
\[
E(t)=G_De(t)=\int_a^b K_D(t,s)e(s)\,ds,
\]
where
\[
\boxed{
K_D(t,s)=
-\frac{(\min\{t,s\}-a)(b-\max\{t,s\})}{b-a}.
}
\]

The kernel is symmetric, one-signed in the interior, vanishes at the endpoints, and scales correctly under interval rescaling.

Define
\[
N_G(e):=\|G_De\|_\infty.
\]
Then under this endpoint-preserving reconstruction,
\[
\boxed{
N_G(e)=\|C-\widetilde C\|_{\infty,\text{synchronized parameter}}.
}
\]
Moreover,
\[
\boxed{
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)
\le N_G(e).
}
\]
So the Green-induced quantity is still parameterization-sensitive, but it is already a rigorous geometric upper bound.

### Why this is potentially better than measuring \(e\) with one global \(L^p\) number

For fixed \(t\), \(-K_D(t,s)\) is a positive piecewise-linear tent weight. Therefore the integral retains:
- sign and vector cancellation in \(e\);
- where the error occurs along the parameter interval;
- the global effect of forcing the reconstructed curve to hit both endpoints.

A global \(L^p\) norm compresses much of this information before integration.

This does **not** yet prove that \(N_G\) is the final desired metric, and it does not solve bad parametrization.

---

## Current assessment

The route is stronger after the first two theory sessions than at the start:

1. **complexity** is exact in the \(C''\) domain;
2. **synchronized positional error** is also exact there through an explicit linear operator;
3. the same quantity gives a safe Hausdorff upper bound.

The next risk is practical rather than algebraic: perhaps evaluating or optimizing \(N_G\) is still too expensive.

A promising structural fact is that when \(e\) is piecewise linear, \(G_De\) is piecewise cubic. This suggests that its maximum norm might be certified by low-degree polynomial extremum calculations instead of dense sampling or curve-to-curve nearest-point search.

That is the next narrow research target.

---

## What is deliberately not claimed

- No claim that \(N_G\) is parameterization-invariant.
- No claim yet that it ranks simplification candidates better than every \(L^p\) norm.
- No normal-projection or Fréchet theory has been established.
- No complete simplification algorithm exists yet.
- No code test is currently required.

No TeX stage note has been created: the results are coherent foundations, but the geometry-aware breakthrough has not yet happened.
