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
On a local cubic-cubic box \(T\times U\),
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
The 2026-09-14 Codex experiment is evidence rather than theorem, but it is strong enough to justify the local-branch primitive:

- ordinary structured close cases certified essentially always, mostly with subdivision depth 0–2;
- failures concentrated in near-self-approach controls;
- independent root checks and exact rational Bernstein-sign audits found no local certificate inconsistency;
- Newton prediction did not materially outperform the simpler first-order predictor;
- the experiment did not certify the maximum implicit-branch deviation and did not establish any whole-curve global correspondence theorem.

Feedback:
`docs/internal/experiments/normal_branch_certificate_feedback.md`.

## Session 0014 — local branch deviation

On a certified branch,
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
Define
\[
G(t,u):=(\widetilde C(t)-C(u))\cdot\widetilde C'(t).
\]
Every interior branch extremum satisfies
\[
F(t,u)=0,
\qquad
G(t,u)=0.
\]
For cubic spans,
\[
\deg G\le(5,3).
\]
Hence the exact generic local maximum reduces to fixed-degree polynomial intersections plus box boundaries. A whole-box Bernstein bound on squared distance provides a cheaper sufficient first layer.

Detailed derivation:
`docs/internal/derivations/normal_branch_tolerance.md`.

## Session 0015 — Hausdorff versus differential/integral stability

This side study is now a stable conceptual result and should be preserved for the future TeX motivation.

### What fails without extra structure

Pure Hausdorff closeness of image sets does not control:

- derivative vectors, because reparameterization can change speed arbitrarily while leaving the image unchanged;
- tangent directions, because high-frequency small-amplitude corrugations can converge in Hausdorff distance while keeping order-one tangent oscillation;
- antiderivative curves, because integration remembers parameter order and speed;
- curvature / \(C''\), even with a uniform curvature bound and converging tangent directions.

Therefore no two-sided norm equivalence
\[
d_H(C,\widetilde C)\leftrightarrow\|C''-\widetilde C''\|
\]
should be expected in the present model.

### What becomes possible with structure

After fixing a correspondence, if
\[
\|E\|_\infty\le\varepsilon,
\qquad
\|E''\|_\infty\le M,
\]
then the interior interpolation estimate gives the square-root scale
\[
\|E'\|\le\sqrt{2M\varepsilon}
\]
when the optimizing local interval fits. For arc-length curves with curvature bound \(K\), this gives tangent error of order \(\sqrt{K\varepsilon}\).

Reach / local feature size is the natural geometric regularity scale because it couples curvature and self-approach. Exact literature constants for cross-manifold Hausdorff-to-tangent estimates should be source-checked before the final TeX note.

Detailed derivation:
`docs/internal/derivations/hausdorff_derivative_integral_relations.md`.

## Session 0016 — local covers replace global stitching for a Hausdorff target

The active global-stitching problem simplifies sharply once the final metric is taken literally as Hausdorff distance.

### F7 — one-sided local-cover theorem

Let source intervals \(T_i\) cover the parameter domain of \(P\). If on each \(T_i\) there is any map \(\sigma_i\) into the target parameter domain with
\[
\|P(t)-Q(\sigma_i(t))\|\le\varepsilon_i,
\]
then
\[
\boxed{
h(P,Q)\le\max_i\varepsilon_i.}
\]
No compatibility between adjacent \(\sigma_i\) is required.

### F8 — symmetric Hausdorff by two directed passes

If an independent reverse family provides
\[
h(Q,P)\le\varepsilon_{Q\to P},
\]
then
\[
\boxed{
d_H(P,Q)
\le
\max\{\varepsilon_{P\to Q},\varepsilon_{Q\to P}\}.}
\]
Therefore global monotone branch stitching is **not a prerequisite** for a pure Hausdorff verifier.

### F9 — orientation test is optional under pure Hausdorff semantics

The local directed theorem needs a branch and a distance bound, not an order-preserving branch. Hence
\[
F_t>0
\]
is unnecessary for the two-pass Hausdorff architecture. Boundary sign separation plus \(F_u<0\) is enough for the current unique-branch construction.

This is not merely aesthetic: \(F_t\) caused subdivision in the higher-curvature experiment family, so dropping it predicts a cheaper verifier.

### F10 — reverse normal equation reuses the common-normal polynomial

With
\[
G(t,u)=(P(t)-Q(u))\cdot P'(t),
\]
the reverse normal equation is
\[
\overline F(u,t)
=(Q(u)-P(t))\cdot P'(t)
=-G(t,u).
\]
Thus the algebra already introduced for branch extrema is exactly the reverse normal algebra up to sign.

### Alternative one-pass coverage route

If the forward branch images \(\sigma_i(T_i)\) cover the entire target parameter interval, the same local correspondences also bound the reverse directed distance. If \(F_t>0\) is retained, each image is an endpoint interval, so coverage becomes a finite interval-union check. This may avoid the second pass but reintroduces orientation/coverage bookkeeping.

### Stronger Fréchet/order layer

If application semantics require traversal order or differential comparison, local branches must still stitch into a global monotone correspondence. That is now an optional stronger layer, not part of the minimal Hausdorff verifier.

Detailed derivation:
`docs/internal/derivations/local_cover_hausdorff_certificate.md`.

## Current architecture

For a pure geometric Hausdorff tolerance, the preferred theoretical architecture is now
\[
\boxed{
\text{forward local normal cover}
+
\text{reverse local normal cover}
\Longrightarrow
\text{symmetric Hausdorff upper bound}.
}
\]

Each local cover uses:

1. branch existence/uniqueness from boundary signs and \(F_u<0\);
2. a cheap box-distance Bernstein bound when sufficient;
3. common-normal / threshold refinement only when needed;
4. local fallback for ambiguous boxes.

No global root-selection topology or branch interface equality is required.

## Current decision gate

Run one targeted feasibility experiment before declaring Phase 4 complete.

Questions:

- how much does removing \(F_t\) reduce subdivision/fallback?
- does the reverse directed pass remain as permissive as the forward pass?
- how tight is the final two-pass branch bound relative to synchronized Green error and an independent numerical Hausdorff reference?
- how often does the cheap whole-box distance bound avoid exact branch-extremum isolation?

Plan:
`docs/internal/experiments/two_sided_hausdorff_certificate_test_plan.md`.

## Explicitly not active now

- no global reach computation;
- no global nearest-point uniqueness theorem;
- no mandatory Fréchet/global monotone branch theorem;
- no q-space candidate-generation algorithm until this final verifier gate is reviewed;
- no final TeX note yet.
