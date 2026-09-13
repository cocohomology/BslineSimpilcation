# Short-Horizon Roadmap — Internal

This file is intentionally volatile. It describes only the next few research sessions and may change whenever a proof or counterexample changes priorities.

## Phase 0 — Initialization

Status: complete.

## Phase 1 — Exact D2 reduction and synchronized error

### Task 1.1 — Reconstruction / complexity structure

Status: **complete (Session 0002)**.

Established:
- \(D^2:S^1_3\to PL_{\rm disc}\) is onto with affine kernel;
- jump/kink structure of \(C''\) exactly records minimal cubic knot multiplicity;
- \(\kappa=K+2J\), with \(N_{\rm ctrl}=4+\kappa\) for a minimal open/clamped cubic.

### Task 1.2a — Fixed-endpoint Green kernel

Status: **complete (Session 0003)**.

Established:
\[
E''=e,\ E(a)=E(b)=0
\quad\Longrightarrow\quad
E=G_De,
\]
with explicit Dirichlet kernel, and
\[
N_G(e)=\|E\|_\infty
\]
exactly equal to synchronized positional error and therefore a Hausdorff upper bound.

### Task 1.2c — PL-specific direct evaluation of \(N_G\)

Status: **complete (Session 0004)**.

Established:
- one global endpoint-correction moment;
- piecewise-cubic \(E\) on the union partition;
- vector Euclidean extrema from degree-5 equations \(E\cdot E'=0\);
- scalar case needs only quadratic derivative roots;
- exact/certified route by real-root isolation;
- robust certified route by cubic Bézier convex-hull subdivision;
- structural linear scaling in the number of union spans, with fixed polynomial degree.

Consequence: ordinary \(L^p\) bounds are no longer needed as the main synchronized metric merely for evaluability.

### Task 1.2b — Sharp \(L^p\to L^\infty\) bounds

Status: open but parked.

Return only if needed for:
- very cheap pruning;
- comparison with Lyche-style discrete/continuous norm estimates;
- quantitative conservatism examples.

Do not let this side task delay the parameterization problem.

---

## Phase 2 — Parameterization: first local test

### Task 2.1 — First-order tangential quotient

**Next session only.**

Setup:
\[
\widetilde C(t)=C(t)+E(t),
\]
with regular \(C\) and small \(E\). Let
\[
T=\frac{C'}{\|C'\|},
\qquad
E=E_\parallel+E_\perp.
\]

Goal:
- seek a small parameter correction
  \[
  \phi(t)=t+\eta(t)
  \]
  that absorbs \(E_\parallel\) to first order;
- derive the sign/formula for \(\eta\) from a Taylor expansion rather than intuition;
- derive an explicit remainder estimate involving quantities such as \(\|E\|,\|E'\|,\|C'\|^{-1},\|C''\|\);
- give a simple sufficient condition for \(\phi'>0\);
- check endpoint behavior under the current endpoint-preserving gauge;
- attack the result with a pure tangential/reparameterization example.

Success criterion:
- a reviewed local statement showing that tangential synchronized error is removable to first order and that the first-order residual is the normal component.

Failure criterion:
- even infinitesimal reparameterization cannot cleanly isolate the normal component without assumptions too strong for CAD use;
- remainder depends on quantities that become uncontrollable in realistic spline inputs.

Out of scope:
- global nearest-point uniqueness;
- full Degen normal correspondence;
- Hausdorff/Fréchet equivalence;
- source code.

### Task 2.2 — Decide whether normal-projected Green error survives

Postponed until Task 2.1 is reviewed.

Only if Task 2.1 succeeds, study
\[
N_{G,\perp}(e)=\sup_t\|P_{N(t)}G_De(t)\|.
\]
Questions:
- precise null directions;
- reference-curve dependence;
- computability on cubic \(E\);
- whether a rigorous higher-order correction can turn it into a certified geometric bound.

---

## Phase 3 — Geometry-aware local certification

Status: postponed.

Possible tools only if demanded by Phase 2:
- normal graphs;
- tubular neighborhoods/reach;
- Degen-style normal correspondence;
- order-preserving reparameterization.

Do not open all of these directions at once.

---

## Phase 4 — Candidate simplification algorithm

Status: postponed.

Only after a geometry-aware metric/certification route survives:
- formulate weighted breakpoint simplification in the PL \(C''\) domain;
- compare delete/merge/move/free-breakpoint primitives;
- write pseudocode before numerical implementation;
- use computation to falsify or measure sharpness, not replace proof.

---

## Side-branch parking lot

- optimized affine reconstruction instead of fixed endpoints;
- force continuous \(q\) for \(C^2\) candidates;
- closed/periodic curves and compatibility constraints;
- classical sharp \(L^p\) Green-operator constants;
- ranking-reversal examples between \(L^p\) and direct \(N_G\);
- convexity/optimization consequences of linear \(G_D\).
