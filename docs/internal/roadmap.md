# Short-Horizon Roadmap — Internal

This roadmap is intentionally volatile.

## Phase 1 — exact \(D^2\) reduction and synchronized error

Status: complete.

Established:
- exact representation-complexity correspondence in the second-derivative domain;
- exact fixed-endpoint Green transport to synchronized positional error;
- direct certified evaluation by fixed-degree one-variable calculations or Bézier subdivision.

## Phase 2 — first geometry-aware correction

Status: useful first-order theory, but the global-curvature closure is rejected as a final metric.

Retained:
- normal error is the first-order geometric residual;
- tangent removal in arc length;
- fixed-degree algebraic certification of the first-order quantities.

Rejected after Session 0007:
\[
N_{G,\perp}+\frac K2N_{G,\parallel}^2
\]
with one global \(K\), because remote curvature can make the bound arbitrarily conservative.

## Phase 3 — nonlinear local correspondence

### Task 3.1 — first adversarial review

Status: complete (Session 0007).

### Task 3.2 — Degen revisited as a design method

Status: **complete (Session 0008)**.

Main conclusion: inherit Degen's architecture rather than simply copy his planar distance:
\[
\text{admissible neighbourhood}
\to\text{unique correspondence}
\to\text{deviation field}
\to\text{norm}.
\]

For the normal equation
\[
F(t,u)=(\widetilde C(t)-C(u))\cdot C'(u)=0,
\]
we established:
- degree \(\le5\) in \(u\) for fixed \(t\) on a cubic span;
- IFT denominator
  \[
  \|C'(u)\|^2-r\cdot C''(u);
  \]
- orientation formula
  \[
  \sigma'(t)=
  \frac{\widetilde C'(t)\cdot C'(\sigma(t))}
  {\|C'(\sigma(t))\|^2-r\cdot C''(\sigma(t))};
  \]
- the previous first-order shift is exactly the Newton/IFT linearization
  \[
  \sigma-t\approx-(E\cdot C')/\|C'\|^2;
  \]
- on a genuine one-to-one normal graph with unique nearest projection,
  \[
  d_H=\|r\|_\infty.
  \]

### Task 3.3 — sufficient admissibility certificate

**Next session only.**

Goal: avoid solving the global nearest-point problem by proving that one nearby root branch is unique and orientation preserving using cheap data from the Green layer.

Study:
1. predictor
   \[
   u_0(t)=t-\frac{E\cdot C'}{\|C'\|^2};
   \]
2. an interval around \(u_0\) where \(F_u\) keeps one sign;
3. sufficient curvature/tube and tangent-angle conditions;
4. interval-Newton or monotone-root certification per local span;
5. continuity across spline knots and double knots;
6. whether the certificate is realistic for ordinary CAD inputs rather than only tiny perturbations.

Success criterion:
- a branch-existence/uniqueness/orientation certificate that is local and fixed-dimensional, with no global pairwise curve search.

Failure criterion:
- admissibility certification itself requires a global root-selection problem comparable to Hausdorff computation.

Out of scope:
- optimizing the nonlinear normal distance;
- simplification primitives;
- source code;
- full TeX stage note.

## Phase 4 — second adversarial review / stage decision

Only after Task 3.3.

Attack:
- branch ambiguity near self-approach;
- high curvature / small tube radius;
- near-zero speed;
- double knots;
- same-image reparameterization;
- cost of following an implicit normal branch.

If the repaired framework survives, perform targeted prior-art verification and consider the first self-contained TeX note.

## Phase 5 — simplification algorithm

Postponed until a geometric bridge survives review.

## Parking lot

- localized curvature-remainder route;
- symmetric use of both curves as reference;
- exact reach/tube computation;
- final choice between Hausdorff-only and order-preserving semantics;
- optimized affine reconstruction;
- closed/periodic curves;
- sharp classical Green \(L^p\) constants.
