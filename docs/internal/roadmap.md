# Short-Horizon Roadmap — Internal

This roadmap is intentionally volatile.

## Phase 1 — exact \(D^2\) reduction and synchronized error

Status: complete.

Established:
- exact representation-complexity correspondence in the second-derivative domain;
- exact fixed-endpoint Green transport to synchronized positional error;
- direct certified evaluation by fixed-degree one-variable calculations or Bézier subdivision.

## Phase 2 — first geometry-aware correction

Status: useful first-order theory; global-curvature closure retained only as a known boundary.

## Phase 3 — nonlinear local correspondence

### Task 3.1 — first adversarial review

Status: complete (Session 0007).

### Task 3.2 — Degen revisited as a design method

Status: complete (Session 0008).

Main lesson: build an admissible geometric correspondence before choosing the deviation norm.

### Task 3.3 — sufficient local admissibility certificate

Status: **complete (Session 0009)**.

For
\[
F(t,u)=(\widetilde C(t)-C(u))\cdot C'(u),
\]
on a local cubic span box \(T\times U\), the sign conditions
\[
F(t,u_0)>0,
\qquad
F(t,u_1)<0,
\qquad
F_u(t,u)<0
\]
certify exactly one local normal root \(u=\sigma(t)\) for every \(t\in T\). If also
\[
F_t(t,u)>0,
\]
then the branch is orientation preserving.

The root is the unique minimizer of local squared distance over \(U\), and all sign tests are fixed-degree:
\[
\deg F\le(3,5),
\quad
\deg F_u\le(3,4),
\quad
\deg F_t\le(2,2).
\]
Tensor-product Bernstein sign tests with adaptive subdivision provide a natural certified implementation route.

The Green layer supplies a local predictor. Besides the first-order
\[
\sigma_0=t-\frac{E\cdot C'}{\|C'\|^2},
\]
the exact one-step Newton predictor at the synchronized point is
\[
\sigma_N=t-\frac{E\cdot C'}{\|C'\|^2+E\cdot C''}.
\]

Detailed derivation:
`docs/internal/derivations/local_normal_branch_certificate.md`.

### Task 3.4 — numerical feasibility gate

**Next stage. Do not deepen the analysis before this test.**

Question:

> On ordinary close cubic pairs resembling simplification outputs, does the local box certificate succeed with small windows and little subdivision?

The experiment is deliberately small and diagnostic. No production source code is required at this stage.

Test families:
1. same or nearly same parameterization with small normal perturbation;
2. mild tangential reparameterization plus small normal perturbation;
3. nonuniform knot spans / speed variation;
4. moderate curvature;
5. one controlled near-self-approach case as a negative control.

For each candidate span:
- build a predicted reference interval from \(\sigma_0\) or \(\sigma_N\);
- test Bernstein signs of boundary \(F\), \(F_u\), and \(F_t\);
- if inconclusive, subdivide the candidate span up to a small depth;
- record pass/fail, subdivisions, window size, and whether a general nearest-point check agrees with the selected branch.

Success criterion:
- ordinary close cases mostly certify with zero or very few subdivisions;
- failures concentrate in deliberately ambiguous/high-curvature cases.

Failure criterion:
- routine close pairs frequently fail the simple sign tests or require deep subdivision.

If successful, continue to tolerance certification along the implicit branch.
If unsuccessful, stop strengthening admissibility theory and reconsider whether synchronized Green error plus occasional general verification is the better engineering architecture.

## Phase 4 — branch-error certification / second attack

Blocked on Task 3.4.

Possible next question only if the feasibility gate succeeds:
- can \(\|\widetilde C(t)-C(\sigma(t))\|\le\varepsilon\) be certified without explicitly solving the entire branch?

Do not open this question before the feasibility gate.

## Phase 5 — simplification algorithm

Postponed.

## Parking lot

- localized curvature-remainder route;
- symmetric use of both curves as reference;
- exact reach/tube computation;
- final choice between Hausdorff-only and order-preserving semantics;
- optimized affine reconstruction;
- closed/periodic curves;
- sharp classical Green \(L^p\) constants.
