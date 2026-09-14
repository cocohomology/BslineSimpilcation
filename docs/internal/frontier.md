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
E=G_De,
\qquad
N_G=\|E\|_\infty,
\]
and
\[
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)\le N_G.
\]
For PL \(e\), \(N_G\) is fixed-degree certifiable.

### F3 — tangent/normal first-order interpretation
Tangential synchronized displacement is the linearized reparameterization direction; normal displacement is the first-order geometric residual. The earlier tangential shift is the first Newton/IFT step for the nonlinear normal equation.

### F4 — global-curvature closure is only a boundary result
The bound
\[
N_{G,\perp}+\frac K2N_{G,\parallel}^2
\]
is mathematically correct but can be arbitrarily conservative because remote curvature can pollute a local tangential shift. Keep this as a capability boundary, not a formula to repair universally.

### F5 — local normal branch architecture
Define
\[
F(t,u)=(\widetilde C(t)-C(u))\cdot C'(u).
\]
On a local cubic-cubic box \(T\times U\), the Session-0009 sign certificate
\[
F(t,u_L)>0,\qquad F(t,u_R)<0,\qquad F_u<0
\]
gives one unique local normal root \(u=\sigma(t)\) for each \(t\in T\). Adding
\[
F_t=\widetilde C'(t)\cdot C'(u)>0
\]
gives \(\sigma'(t)>0\).

For cubic spans,
\[
\deg F\le(3,5),
\qquad
\deg F_u\le(3,4),
\qquad
\deg F_t\le(2,2).
\]

### F6 — feasibility gate passed, with explicit limits
The 2026-09-14 Codex experiment is evidence rather than theorem, but it is strong enough to justify continuing the local-branch line:

- ordinary structured close cases certified essentially always, mostly with subdivision depth 0–2;
- failures concentrated in near-self-approach controls;
- independent root checks and exact rational Bernstein-sign audits found no local certificate inconsistency;
- Newton prediction did not materially outperform the simpler first-order predictor;
- the experiment did **not** establish a whole-curve global correspondence theorem and did **not** certify the maximum implicit-branch deviation.

The feedback file is:
`docs/internal/experiments/normal_branch_certificate_feedback.md`.

## Session 0014 correction of the post-test route

Sessions 0012–0013 explored q-space optimization under
\[
\|q-\widetilde q\|_G:=\|G_D(q-\widetilde q)\|_\infty.
\]
The observation is mathematically valid, but it was promoted too quickly as the next main-line question.

For the fixed endpoint reconstruction map \(R:q\mapsto C\),
\[
\|q-\widetilde q\|_G
=\|R(q)-R(\widetilde q)\|_\infty.
\]
Thus the Green norm is first of all the pullback of synchronized positional \(L^\infty\) through \(D^{-2}\). This coordinate view may become useful for candidate generation later, but it does not by itself establish a new approximation paradigm.

The active main line therefore returns to the pre-test roadmap: finish the geometry-aware verifier far enough to make a tolerance decision, then return to candidate generation.

## New result — extrema along a certified branch are common normals

On a certified smooth branch, set
\[
r(t)=\widetilde C(t)-C(\sigma(t)),
\qquad
\psi(t)=\|r(t)\|^2.
\]
Because
\[
D(t,u):=\|\widetilde C(t)-C(u)\|^2
\]
satisfies
\[
D_u=-2F,
\]
we have \(D_u=0\) on the branch. Hence
\[
\boxed{
\psi'(t)
=2r(t)\cdot\widetilde C'(t).
}
\]

Define
\[
G(t,u):=(\widetilde C(t)-C(u))\cdot\widetilde C'(t).
\]
Then every interior branch extremum satisfies
\[
\boxed{F(t,u)=0,\qquad G(t,u)=0.}
\]

For cubic spans,
\[
\deg G\le(5,3).
\]
Thus, in the generic case, the exact local maximum deviation reduces to finitely many fixed-degree bivariate polynomial intersections plus box boundaries. Degenerate positive-dimensional stationary sets correspond to constant branch deviation and require a separate benign handling path.

Detailed derivation:
`docs/internal/derivations/normal_branch_tolerance.md`.

## Cheap tolerance hierarchy now visible

On a certified box:

1. first Bernstein-bound the squared distance polynomial
   \[
   D(t,u)=\|\widetilde C(t)-C(u)\|^2,
   \]
   whose bidegree is at most \((6,6)\);
2. if the whole-box bound is already below \(\varepsilon^2\), accept;
3. otherwise contract/subdivide the box;
4. if still inconclusive, isolate stationary common-normal roots \(F=G=0\) and evaluate \(D\) there plus at boundaries;
5. only then fall back to a more general verifier.

This has not yet been numerically tested. It is the current theoretical completion of the single-box tolerance problem.

## Important geometric correction — local nearest is stronger than needed

A certified local normal foot need not be the global nearest point to give a directed-distance upper bound:
\[
\operatorname{dist}(\widetilde C(t),\operatorname{Im}C)
\le
\|\widetilde C(t)-C(\sigma(t))\|.
\]
Therefore the near-self-approach cases in the experiment where a certified local foot was not globally nearest do not invalidate upper-bound certification.

However, a **full symmetric Hausdorff upper bound** requires either:

- a globally stitched, onto, monotone correspondence, or
- a second certified correspondence in the reverse direction.

The local box theorem alone does not provide this. This is now the main theoretical gap.

## Current main question

Develop a **global assembly theorem** for the local certificates, without drifting into a general global nearest-point theory.

Questions for the next session:

- what endpoint / overlap conditions ensure adjacent local branches select the same normal root at shared candidate knots?
- when do locally increasing branches stitch into a continuous globally increasing map?
- what guarantees coverage of the reference parameter domain?
- is it cleaner to certify two directed correspondences rather than enforce a single global bijection?
- how do double knots and branch windows crossing reference knots affect the stitching conditions?

## Explicitly not active now

- no new global reach/tubular-neighbourhood theory;
- no further optimization of the Newton predictor;
- no free-knot / q-space candidate-generation algorithm yet;
- no claim that the Codex experiment proves industrial success;
- no TeX stage note yet.
