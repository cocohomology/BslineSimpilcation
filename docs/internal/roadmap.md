# Short-Horizon Roadmap — Internal

This file is intentionally volatile. It describes only the next few research sessions.

## Phase 1 — D2 reduction and synchronized error

Status: complete.

Established across Sessions 0002–0004:
- exact correspondence between cubic representation complexity and PL second-derivative singularity structure;
- exact fixed-endpoint Green transport of second-derivative error to synchronized positional error;
- direct certified evaluation of that synchronized error by fixed-degree univariate calculations or Bézier subdivision.

Classical \(L^p\) operator bounds remain parked as secondary pruning/comparison tools.

---

## Phase 2 — Parameterization / geometry-aware correction

### Task 2.1 — Tangential quotient

Status: **complete (Session 0005)**.

Using the reference arc-length coordinate, define the tangential arc-length shift
\[
\delta=-E\cdot T,
\qquad \rho(s)=s+\delta(s).
\]
Under
\[
\|D_sE\|_\infty+K\|E\|_\infty<1,
\]
this is a monotone endpoint-fixing correspondence. The resulting certified bound is
\[
 d_H\le
N_{G,\perp}(e)+\frac K2N_{G,\parallel}(e)^2
\le
N_{G,\perp}(e)+\frac K2N_G(e)^2.
\]

This promotes normal projection from heuristic to a rigorous first-order quotient quantity.

### Task 2.2 — Is the geometry-aware bound still cheap?

**Next session only.**

Goal: determine whether all terms needed by the Session 0005 theorem remain fixed-degree certifiable on cubic spline spans.

Study:

1. Normal error
   \[
   N_{G,\perp}=\sup\|P_NE\|.
   \]
   On one span \(E\) is cubic and \(C'\) quadratic. Derive the rational/polynomial form of
   \[
   \|P_NE\|^2
   =\|E\|^2-\frac{(E\cdot C')^2}{\|C'\|^2}.
   \]
   Determine the degree of the stationary equation after clearing denominators.

2. Arc-length derivative term
   \[
   \|D_sE\|=\frac{\|E'\|}{\|C'\|}.
   \]
   Determine a certified finite procedure for its maximum.

3. Curvature
   \[
   \kappa=\left\|\frac{dT}{ds}\right\|.
   \]
   Express \(\kappa^2\) rationally in \(C',C''\) and determine whether \(K=\sup\kappa\) is fixed-degree certifiable.

4. Monotonicity condition
   Decide whether
   \[
   \|D_sE\|_\infty+K\|E\|_\infty<1
   \]
   can be certified with the above ingredients without a difficult coupled optimization.

Success criterion:
- all quantities reduce to independent fixed-degree univariate algebraic problems per span, so geometry awareness preserves the computational advantage.

Failure criterion:
- tangent/curvature normalization introduces degree growth, singular conditioning, or coupled optimization severe enough to erase the advantage.

Out of scope:
- breakpoint optimization;
- exact nonlinear normal correspondence;
- full simplification pseudocode;
- source code.

---

## Phase 3 — Stage review

Only after Task 2.2.

If the geometry-aware theorem and its certification both survive:
- perform an adversarial review with pure reparameterizations, high curvature, low-speed regular curves, short knot spans, and near self-approach;
- decide whether the framework merits the first full TeX note;
- check literature specifically for closely related local normal/Fréchet bounds before making any novelty claim.

If Task 2.2 fails, reconsider whether a cheaper surrogate for the normal quantity is needed.

---

## Phase 4 — Low-complexity approximation algorithm

Postponed.

Only after the geometry-aware bound survives the stage review:
- formulate weighted PL simplification with \(\kappa=K_0+2J\);
- identify delete/merge/move/free-breakpoint primitives;
- write pseudocode before any implementation;
- design computation primarily to falsify assumptions and measure conservatism.

---

## Parking lot

- optimized affine reconstruction instead of fixed endpoints;
- force continuous second derivative for \(C^2\) candidates;
- closed/periodic curves;
- sharp classical \(L^p\to L^\infty\) Green constants;
- ranking reversals between \(L^p\) and Green/normal metrics;
- stronger nonlinear correspondence to remove the remaining quadratic error of curved pure reparameterization;
- symmetric use of both reference orientations and taking the better bound.
