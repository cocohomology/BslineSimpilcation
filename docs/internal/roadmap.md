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
- no whole-curve global correspondence theorem or implicit-branch max-deviation certificate was tested.

Decision:
- keep the simple local certificate;
- do not deepen admissibility theory preemptively;
- move to tolerance certification along an already-certified branch.

## Phase 4 — complete the geometry-aware verifier

### Task 4.1 — local branch deviation / tolerance structure

Status: **complete theoretically (Session 0014).**

For a certified branch \(u=\sigma(t)\), define
\[
\psi(t)=\|\widetilde C(t)-C(\sigma(t))\|^2.
\]
Then
\[
\psi'(t)
=2(\widetilde C(t)-C(\sigma(t)))\cdot\widetilde C'(t).
\]
Therefore interior extrema satisfy the common-normal system
\[
(\widetilde C(t)-C(u))\cdot C'(u)=0,
\]
\[
(\widetilde C(t)-C(u))\cdot\widetilde C'(t)=0.
\]
For cubic spans the bidegrees are at most \((3,5)\) and \((5,3)\).

A cheap whole-box Bernstein bound on
\[
D(t,u)=\|\widetilde C(t)-C(u)\|^2
\]
can be tried first; common-normal root isolation is the exact generic fallback inside the certified box.

Detailed derivation:
`docs/internal/derivations/normal_branch_tolerance.md`.

### Task 4.2 — global assembly of local branches

**Next session only.**

Goal:
turn local one-span certificates into a mathematically valid whole-curve geometric upper bound without solving a global nearest-point problem.

Study:
1. compatibility of adjacent local roots at shared candidate knots;
2. sufficient conditions for continuous stitching of locally increasing branches;
3. coverage/onto conditions for the reference parameter interval;
4. alternative architecture: two one-sided directed correspondences instead of one global bijection;
5. knot-crossing / double-knot endpoint conventions.

Success criterion:
- a small set of checkable local/interface conditions that gives a global monotone correspondence or two directed upper-bound correspondences.

Failure criterion:
- proving global assembly requires a global root-selection/topology problem comparable to the geometry we were trying to avoid.

Out of scope for Task 4.2:
- free knots;
- q-space candidate generation;
- production code;
- global reach computation;
- exact global nearest-point uniqueness.

### Task 4.3 — second adversarial review / optional code gate

Only after Task 4.2.

Attack:
- branch switching across adjacent windows;
- gaps/overlaps in reference coverage;
- near self-approach;
- low-speed / short-span interfaces;
- double knots;
- constant-distance / common-factor degeneracies.

If the global assembly theorem is simple enough, prepare one targeted Codex feasibility test for branch-deviation certification and stitching. If it becomes global-nearest-point theory in disguise, stop and fall back to synchronized Green verification.

## Phase 5 — candidate generation in \(q=C''\) space

Status: **postponed until Phase 4 reaches a stable decision.**

The likely future main problem remains:
\[
\text{low-complexity }PL_{\rm disc}\text{ approximation of }q=C''
\]
with kink cost 1 and jump cost 2.

Sessions 0012–0013 explored direct Green-induced optimization. That direction is now parked rather than active: for a fixed endpoint gauge, the Green norm is exactly the pullback of synchronized positional error, so it should not be treated as a metric breakthrough by itself.

When Phase 5 begins, revisit `docs/internal/theory_seeds.md`, especially free-breakpoint approximation and moment-localized Hermite block coarsening.

## TeX note decision

Still deferred.

A good trigger is either:
- Phase 4 yields a coherent local-to-global certified geometric verifier that survives the second attack; or
- Phase 4 fails in a theoretically informative way that clearly defines the useful boundary of the normal-correspondence approach.
