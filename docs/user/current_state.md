# Current State — User-Facing Summary

## Scope

The research still targets regular \(C^1\), cubic, non-rational spline curves. The structural reduction remains
\[
C\xrightarrow{D^2}q=C'',
\]
with \(q\) piecewise linear and possibly discontinuous at double knots.

The objective remains: simplify representation complexity under a geometric tolerance.

---

## Stable foundation

### 1. Complexity is exact in the \(C''\) domain

For \(C^1\) piecewise cubics,
\[
D^2:S_3^1\to PL_{\rm disc}
\]
is onto with affine kernel. Jumps and continuous kinks of \(C''\) encode double and simple cubic knots.

### 2. Fixed-endpoint synchronized error is exact

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
For PL \(e\), \(\|E\|_\infty\) is certifiable by fixed-degree one-variable algebra or Bézier subdivision and gives a rigorous Hausdorff upper bound.

### 3. Local normal correspondence is a viable geometry-aware primitive

Define
\[
F(t,u)=(\widetilde C(t)-C(u))\cdot C'(u).
\]
On a local cubic-cubic box, boundary sign separation together with
\[
F_u<0
\]
certifies one unique local normal branch \(u=\sigma(t)\). The 2026-09-14 Codex feasibility experiment strongly supports the permissiveness of this primitive on the tested structured close-curve families, while leaving near-self-approach as the intended difficult regime.

---

## Stable side result — why Hausdorff alone is not enough for differential reasoning

Session 0015 directly studied Hausdorff distance rather than avoiding it.

The main conclusion is asymmetric:

- pure Hausdorff closeness of curve images does **not** control derivative vectors, tangent directions, antiderivative curves, or curvature in general;
- once an ordered correspondence and a regularity scale are supplied, quantitative derivative control becomes possible;
- with synchronized positional error \(\|E\|_\infty\le\varepsilon\) and \(\|E''\|_\infty\le M\), the natural interior estimate is
  \[
  \|E'\|\lesssim \sqrt{M\varepsilon};
  \]
- reach/local feature size is the natural geometric scale behind Hausdorff-to-tangent stability.

This result should be retained for the future TeX note because it explains why a pure set-distance formulation cannot by itself support the derivative-domain reasoning used by the project.

Detailed note:
`docs/internal/derivations/hausdorff_derivative_integral_relations.md`.

---

## Session 0014 — local deviation on one certified branch

On a certified branch, let
\[
r(t)=\widetilde C(t)-C(\sigma(t)),
\qquad
\psi(t)=\|r(t)\|^2.
\]
Then
\[
\boxed{
\psi'(t)=2r(t)\cdot\widetilde C'(t).
}
\]
Hence every interior extremum of the branch deviation is a common-normal pair:
\[
(\widetilde C(t)-C(u))\cdot C'(u)=0,
\]
\[
(\widetilde C(t)-C(u))\cdot\widetilde C'(t)=0.
\]
For cubic spans these are fixed-degree bivariate polynomial equations. A cheap whole-box Bernstein bound on squared distance can be tried first; only inconclusive boxes need common-normal refinement.

---

## Session 0016 — global stitching is not required for a Hausdorff-only target

The previous roadmap treated whole-curve monotone branch stitching as the next mandatory step. That turns out to be stronger than necessary.

If source intervals \(T_i\) cover the candidate parameter domain and, on each interval, a certified local branch \(\sigma_i\) satisfies
\[
\|\widetilde C(t)-C(\sigma_i(t))\|\le\varepsilon_i,
\]
then immediately
\[
\overrightarrow d_H(\widetilde C,C)
\le
\max_i\varepsilon_i.
\]
No continuity or agreement between adjacent local branches is needed for this directed Hausdorff bound.

Repeating the same construction with the two curves swapped gives
\[
\boxed{
d_H(C,\widetilde C)
\le
\max\{B_{\widetilde C\to C},B_{C\to\widetilde C}\}.
}
\]
Therefore a pure Hausdorff verifier can be built from **two local directed passes** and does not require a global monotone correspondence.

A second consequence is that the orientation condition
\[
F_t>0
\]
is not needed for Hausdorff-only certification. Boundary sign separation plus \(F_u<0\) is enough to define the local branch used for a directed upper bound. Orientation remains useful only for a stronger Fréchet/order-preserving interpretation or for a one-pass target-coverage strategy.

Detailed derivation:
`docs/internal/derivations/local_cover_hausdorff_certificate.md`.

---

## Current architecture

The verification layer is now conceptually simpler:

\[
\boxed{
\text{forward local normal cover}
+
\text{reverse local normal cover}
\Longrightarrow
\text{symmetric Hausdorff upper bound}.
}
\]

Each local branch can use the Session-0014 tolerance machinery. Global branch stitching is demoted to an optional stronger semantic layer for Fréchet/order-sensitive applications.

This also cleanly separates two notions:

- **Hausdorff geometry:** only image-set closeness is required;
- **ordered/differential comparison:** requires a globally compatible correspondence and additional regularity.

---

## New candidate-generation constraint — bad parameterization is not shape complexity

The Lyche/Lp replication branch has now made the bad-parameter problem concrete. Session 0017 studied whether the independent route can address it.

A useful exact identity is
\[
\boxed{
C''=v'T+v^2K,
}
\]
where \(v=\|C'\|\), \(T\) is the unit tangent, and \(K=dT/ds\) is the curvature vector. The tangential term \(v'T\) is pure parameter-speed complexity. Thus a straight line can have highly complicated raw \(C''\) while its intrinsic geometry has \(K=0\).

This means the future candidate-generation phase cannot blindly assume that raw \(q=C''\) is always the correct optimization variable.

Two facts were established:

- In the \(C^1\) quadratic toy case, Hausdorff simplification of the derivative polyline **as a set** is insufficient: two derivative PL curves can have identical images while their integrated quadratic curves are geometrically different.
- If a coherent derivative correspondence gives \(\|C'-\widetilde C'\|_\infty\le\varepsilon\), then integration is stable: \(\|C-\widetilde C\|_\infty\le L\varepsilon\), improved to \(L\varepsilon/2\) when both endpoints are fixed.

A deeper intrinsic alternative uses a Bishop frame. If two arc-length curves have nearby Bishop curvature coefficients, their tangent and position errors are controlled by direct integrals of the coefficient error; in particular a uniform intrinsic coefficient error \(\eta\) gives a positional/Hausdorff bound of order \(L^2\eta/2\).

The practical implication is not an immediate pivot. Instead, Phase 5 must first decide whether to:

- **gauge-fix the parameterization** and then use the existing \(q=C''\) spline algebra; or
- generate candidates from **intrinsic shape variables** and recover a spline representation afterward.

Detailed note:
docs/internal/derivations/bad_parameter_intrinsic_routes.md


## Next gate

The next task is a targeted code feasibility experiment, using the existing structured suite, to test:

- the old four-condition certificate versus the Hausdorff-only certificate without \(F_t\);
- forward and reverse pass rates/subdivision depths;
- the final two-pass geometric bound versus synchronized Green error and an independent numerical Hausdorff reference;
- how often the cheap whole-box distance bound avoids common-normal root isolation.

The experiment plan is:
`docs/internal/experiments/two_sided_hausdorff_certificate_test_plan.md`.

---

## Status

- COMPLEXITY REDUCTION IN \(C''\): established.
- SYNCHRONIZED GREEN ERROR: established.
- LOCAL NORMAL ADMISSIBILITY: established theoretically; feasibility evidence positive.
- LOCAL BRANCH TOLERANCE STRUCTURE: established theoretically.
- PURE HAUSDORFF GLOBAL ASSEMBLY: simplified to two directed local covers; no global stitching theorem is required.
- FRÉCHET / ORDER-PRESERVING GLOBAL STITCHING: optional, parked unless application semantics require it.
- NEXT: targeted two-sided verifier experiment.
- TEX NOTE: still deferred until this final verification gate is reviewed.
