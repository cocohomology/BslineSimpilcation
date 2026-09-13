# Short-Horizon Roadmap — Internal

This roadmap is intentionally volatile.

## Phase 1 — exact \(D^2\) reduction and synchronized error

Status: complete.

Established:
- exact representation-complexity correspondence in the second-derivative domain;
- exact fixed-endpoint Green transport of second-derivative error to synchronized positional error;
- direct certified evaluation of synchronized error by fixed-degree one-variable calculations or Bézier subdivision.

## Phase 2 — first geometry-aware correction

Status: mathematically established but **not accepted as a final metric**.

Established:
- first-order tangential quotient in reference arc length;
- normal error is the first-order geometric residual;
- all first-order geometry-aware ingredients are fixed-degree certifiable on cubic spans;
- direct correspondence monotonicity test \(H>0\).

Rejected as a final certification quantity after Session 0007:
\[
N_{G,\perp}+\frac K2N_{G,\parallel}^2
\]
with one global curvature supremum \(K\). It can be arbitrarily conservative even when the two spline images are identical.

## Phase 3 — adversarial review and repair

### Task 3.1 — first attack

Status: **complete (Session 0007)**.

Results:
- near-zero speed: theoretical framework survives; numerical conditioning remains;
- high curvature at the location of a tangential shift: quadratic curvature term is genuinely necessary;
- global remote curvature: decisive in-class counterexample breaks the usefulness of the global-\(K\) product;
- near self-approach: no correctness failure, but correspondence-based bounds can be much stronger than Hausdorff;
- short spans/double knots: conditioning issues only.

Conclusion: no TeX stage note yet. Repair locality before claiming a stage breakthrough.

### Task 3.2 — targeted Degen / nonlinear normal correspondence review

**Next session only.**

Use the uploaded Degen paper and the new counterexample as the organizing question, not as a broad literature survey.

Study the local normal condition
\[
(\widetilde C(t)-C(u))\cdot C'(u)=0.
\]

Goals:
- recover Degen's precise normal-distance/correspondence definition and hypotheses;
- derive local existence/uniqueness near \(u=t\) using an implicit-function/tubular-neighborhood viewpoint;
- determine exactly which hypothesis prevents branch switching near self-approach;
- check whether same-image reparameterizations give exact zero on the correct branch;
- exploit cubic structure: for fixed \(t\), the normal equation is degree at most five in \(u\);
- estimate whether branch certification and maximization over \(t\) remain substantially simpler than full Hausdorff computation.

Success criterion:
- a local nonlinear correspondence that fixes the remote-curvature counterexample and has a plausible certified algebraic route.

Failure criterion:
- selecting/certifying the correct root branch is essentially the full nearest-point/Hausdorff problem.

Out of scope:
- full simplification algorithm;
- source code;
- broad free-knot literature;
- TeX stage note.

### Task 3.3 — local curvature remainder

Parked as fallback.

Potential idea:
\[
\|R(s)\|\le\int_0^{|\delta(s)|}(|\delta(s)|-r)\,\kappa(s\pm r)\,dr.
\]
This restores locality but may require moving arc-length intervals/inversion. Investigate only if nonlinear normal correspondence proves too expensive.

## Phase 4 — second attack / stage decision

Only after Task 3.2.

Attack:
- branch ambiguity near self-approach;
- high curvature / small reach;
- low-speed parameterization;
- double knots;
- exact same-image parameter changes;
- computational degree and root multiplicity.

If the repaired framework survives:
- perform targeted prior-art verification;
- mark a stage breakthrough;
- write the first self-contained TeX note with Green-function background and pseudocode-level certification logic.

If it fails:
- record the failure mechanism and reconsider whether the project should accept synchronized/Fréchet-like error as the optimization metric with final Hausdorff certification only.

## Phase 5 — simplification algorithm

Postponed.

Only after a geometry-aware bridge survives adversarial review should the project formulate weighted PL simplification under
\[
\kappa=K_0+2J.
\]

## Parking lot

- optimized affine reconstruction instead of fixed endpoints;
- closed/periodic curves;
- forcing \(C^2\) candidates;
- sharp classical Green \(L^p\) constants;
- symmetric use of both curves as reference;
- localized curvature remainder;
- final choice between Hausdorff-only versus order-preserving geometric semantics.
