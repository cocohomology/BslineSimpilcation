# Short-Horizon Roadmap — Internal

This roadmap is intentionally volatile. It records the next few research decisions, not a fixed program.

## Phase 1 — exact \(D^2\) reduction and synchronized error

Status: **complete**.

Established:
- exact representation-complexity correspondence in the second-derivative domain;
- exact fixed-endpoint Green transport to synchronized positional error;
- direct certified evaluation by fixed-degree one-variable calculations or Bézier subdivision.

## Phase 2 — first geometry-aware correction

Status: **complete as a first-order analysis; not used as final metric**.

Retained:
- tangential synchronized error is the linearized reparameterization direction;
- normal error is the first-order geometric residual;
- the old global-curvature closure is a known conservative boundary, not an active formula.

## Phase 3 — nonlinear local normal correspondence

### Task 3.1 — adversarial review
Status: complete (Session 0007).

### Task 3.2 — Degen revisited as a design method
Status: complete (Session 0008).

### Task 3.3 — local admissibility certificate
Status: complete (Session 0009).

### Task 3.4 — numerical feasibility gate
Status: **complete as evidence, not proof (Codex experiment, 2026-09-14).**

Observed on the structured synthetic suite:
- ordinary close cases almost always certified with depth 0–2;
- all baseline fallbacks were concentrated in the near-self-approach control family;
- independent root checks and exact rational Bernstein-sign audits did not expose a local certificate error;
- Newton prediction did not materially improve the pass/fallback picture;
- no implicit-branch max-deviation certificate was tested.

Decision:
- keep the simple local certificate;
- do not deepen admissibility theory preemptively.

## Phase 4 — complete the geometry-aware verifier

### Task 4.1 — local branch deviation / tolerance structure

Status: **complete theoretically (Session 0014).**

For a certified branch \(u=\sigma(t)\),
\[
\psi(t)=\|\widetilde C(t)-C(\sigma(t))\|^2
\]
satisfies
\[
\psi'(t)
=2(\widetilde C(t)-C(\sigma(t)))\cdot\widetilde C'(t).
\]
Interior extrema are common-normal pairs. For cubic spans this reduces to fixed-degree bivariate polynomial equations. A whole-box Bernstein distance bound is the cheap first layer.

Detailed derivation:
`docs/internal/derivations/normal_branch_tolerance.md`.

### Side study — Hausdorff vs differential/integral stability

Status: **stable conceptual result (Session 0015).**

Keep for the future TeX motivation:
- Hausdorff alone does not control derivative vectors, tangent directions, antiderivatives, or curvature;
- after a correspondence and regularity scale are supplied, first-derivative stability has square-root scaling;
- reach/local feature size is the natural geometric scale coupling curvature and self-approach;
- no inverse recovery of \(q=C''\) from Hausdorff error is available under the current assumptions.

Detailed derivation:
`docs/internal/derivations/hausdorff_derivative_integral_relations.md`.

Before the final TeX note, source-check the precise reach/manifold-reconstruction constants and references.

### Task 4.2 — local-to-global Hausdorff assembly

Status: **resolved by simplification (Session 0016).**

The former plan asked for a globally stitched monotone normal branch. That is stronger than necessary for a pure Hausdorff target.

If local source intervals cover the source curve and each interval has a certified correspondence within \(\varepsilon\), then the corresponding directed Hausdorff distance is at most \(\varepsilon\). Repeating with source and target swapped gives the symmetric Hausdorff bound.

Therefore the minimal architecture is
\[
\boxed{
\text{forward local cover}
+
\text{reverse local cover}
\Longrightarrow
\text{symmetric Hausdorff upper bound}.
}
\]

Consequences:
- local branches need not agree at candidate-span interfaces;
- branch switching is harmless for Hausdorff upper bounds;
- the orientation condition \(F_t>0\) is unnecessary for the two-pass Hausdorff route;
- double knots require only local piecewise sign handling, not a global stitching theorem;
- a globally monotone branch is now an optional Fréchet/order-sensitive layer.

Detailed derivation:
`docs/internal/derivations/local_cover_hausdorff_certificate.md`.

### Task 4.3 — targeted two-sided feasibility gate

**Next active task.**

Use the existing structured curve suite to test the now-complete local Hausdorff architecture.

Compare:
1. old four-condition local certificate versus boundary signs + \(F_u<0\) only;
2. forward and reverse directed pass rates / subdivision depths;
3. two-pass branch bound versus synchronized Green error and an independent numerical Hausdorff reference;
4. cheap whole-box distance bound versus branch-specific common-normal refinement.

Plan:
`docs/internal/experiments/two_sided_hausdorff_certificate_test_plan.md`.

Success signal:
- both directions are usually cheap on ordinary close pairs;
- dropping \(F_t\) reduces work;
- branch bounds are meaningfully tighter than synchronized error in tangential/reparameterized cases;
- difficult behavior stays concentrated in self-approach / genuinely ambiguous cases.

Failure signal:
- reverse certification is routinely expensive;
- branch max certification dominates cost;
- the final two-pass bound is not materially tighter than the synchronized bound;
- fallback frequency makes the normal layer unattractive.

After this gate, perform one short adversarial/theory review of any exposed failure mode. Do not invent new global topology theory unless the data forces it.

## Phase 5 — candidate generation in \(q=C''\) space

Status: **next main phase if Task 4.3 is satisfactory.**

The main problem will be
\[
\text{low-complexity }PL_{\rm disc}\text{ approximation of }q=C''
\]
with kink cost 1 and jump cost 2.

Sessions 0012–0013 explored direct Green-induced optimization and are parked. When Phase 5 begins, revisit `docs/internal/theory_seeds.md`, especially:
- nonlinear/free-breakpoint PL approximation;
- moment-localized Hermite block coarsening;
- possible dynamic-programming / shortest-path restricted baselines.

## TeX note decision

Still deferred, but the trigger is now close.

A strong trigger is:
- Task 4.3 supports the two-directed-pass architecture and the post-test adversarial review reveals no structural failure.

The eventual TeX note should explicitly include the Session-0015 Hausdorff/reach discussion near the motivation section, because it explains why pure Hausdorff geometry cannot be used to infer derivative-domain closeness and why the project introduces correspondence machinery.
