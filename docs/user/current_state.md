# Current State — User-Facing Summary

## Scope

The research still targets regular \(C^1\), cubic, non-rational spline curves. The structural reduction remains
\[
C\xrightarrow{D^2}q=C'',
\]
with \(q\) piecewise linear and possibly discontinuous at double knots.

The objective remains: simplify representation complexity under geometric tolerance.

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

### 3. Local normal correspondence is a viable geometry-aware fast path

Define
\[
F(t,u)=(\widetilde C(t)-C(u))\cdot C'(u).
\]
On a local cubic-cubic box, boundary sign separation together with
\[
F_u<0
\]
certifies one unique local normal branch \(u=\sigma(t)\); adding
\[
F_t>0
\]
certifies orientation preservation.

The 2026-09-14 Codex feasibility experiment is evidence, not proof, but it strongly supports the permissiveness of this primitive on its structured close-curve samples: ordinary cases almost always certified with little subdivision, while failures concentrated in the intended near-self-approach controls. The experiment also explicitly did **not** prove a whole-curve correspondence theorem and did not compute the maximum deviation along the implicit branch.

---

## Session 0014 correction — what the experiment actually tells us to do next

The active theory should **not** jump yet to a new q-space optimization theory. Sessions 0012–0013 explored a Green-induced metric direction, but that was premature as the next main-line task.

For a fixed endpoint gauge,
\[
\|G_D(q-\widetilde q)\|_\infty
=\|C-\widetilde C\|_\infty,
\]
so the Green norm is best viewed first as the pullback of synchronized positional error through the reconstruction map. Its q-space viewpoint may still become useful for candidate generation later, but it is not by itself a new approximation breakthrough.

The experiment passed the admissibility gate. Therefore the logically next missing piece is to finish the geometry-aware verifier far enough to decide a tolerance along an already-certified local branch.

---

## New local deviation result

On a certified branch, let
\[
r(t)=\widetilde C(t)-C(\sigma(t)),
\qquad
\psi(t)=\|r(t)\|^2.
\]
Because the normal equation gives
\[
r(t)\cdot C'(\sigma(t))=0,
\]
we obtain
\[
\boxed{
\psi'(t)=2r(t)\cdot\widetilde C'(t).
}
\]

Hence every interior extremum of the branch deviation is a **common-normal pair**:
\[
\boxed{
(\widetilde C(t)-C(u))\cdot C'(u)=0,
\qquad
(\widetilde C(t)-C(u))\cdot\widetilde C'(t)=0.
}
\]

For cubic spans these are fixed-degree bivariate polynomial equations with bidegrees at most
\[
(3,5)\quad\text{and}\quad(5,3).
\]
Therefore the exact maximum deviation on one certified smooth box can be reduced to finitely many polynomial intersection candidates plus box boundaries, with a separate benign treatment for degenerate constant-distance branches.

A cheaper sufficient first layer is to Bernstein-bound
\[
\|\widetilde C(t)-C(u)\|^2
\]
over the certified box itself; only inconclusive boxes need sharper common-normal isolation.

---

## Important geometric clarification from the test feedback

A locally certified normal foot does **not** need to be the global nearest point in order to provide an upper bound from the candidate curve to the reference curve. The near-self-approach experiment found locally valid normal feet that were not globally nearest; this is a limitation only if exact nearest-point equality is demanded.

For a full symmetric Hausdorff upper bound, however, local boxes must either:

- stitch into a global monotone bijective correspondence, or
- be complemented by a reverse-direction correspondence.

The existing experiment did not establish that global assembly theorem.

---

## Current active question

The next narrow theoretical task is therefore:

\[
\boxed{
\text{How do certified local normal branches stitch into a whole-curve correspondence?}
}
\]

Only after this is understood should the project decide whether the verification layer is mature enough to return to candidate generation in \(q=C''\) space.

---

## Status

- ADMISSIBILITY THEORY: locally established; feasibility evidence positive.
- LOCAL BRANCH TOLERANCE: polynomial stationary structure established in Session 0014.
- GLOBAL CORRESPONDENCE / SYMMETRIC HAUSDORFF UPPER BOUND: next theoretical gap.
- GREEN-METRIC CANDIDATE-GENERATION DETOUR: parked, not discarded.
- TEX NOTE: still deferred until the verification architecture survives global assembly / second review.
