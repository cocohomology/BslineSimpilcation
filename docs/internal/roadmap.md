# Short-Horizon Roadmap — Internal

This roadmap is intentionally volatile.

## Phase 1 — exact \(D^2\) reduction and synchronized error

Status: complete.

Established:
- exact representation-complexity correspondence in the second-derivative domain;
- exact fixed-endpoint Green transport of second-derivative error to synchronized positional error;
- direct certified evaluation of synchronized error by fixed-degree one-variable calculations or Bézier subdivision.

Classical \(L^p\) bounds remain parked as secondary pruning/comparison tools.

## Phase 2 — first geometry-aware correction

Status: complete through Session 0006.

Established:
- arc-length tangential shift removes synchronized tangential error to first order;
- finite bound
  \[
  d_H\le N_{G,\perp}+\frac K2N_{G,\parallel}^2;
  \]
- normal/tangential error, curvature, and regularity are rational fixed-degree spline-span quantities;
- correspondence monotonicity is exactly testable by
  \[
  H=2S^2-2B'S+BS'>0,
  \]
  with \(\deg H\le8\).

Thus the first geometry-aware layer preserves the fixed-degree univariate character of the synchronized theory.

## Phase 3 — adversarial stage review

**Next session only.**

Do not add another positive theorem before attacking the current framework.

### 3.1 Pure reparameterization families

Study:
- straight line: should give exact zero bound under monotone redistribution;
- circle or another constant-curvature reference: true geometric distance zero for pure reparameterization, current bound should show explicit second-order conservatism;
- determine scaling constants, not only big-O notation.

### 3.2 Low-speed regular parameterizations

Construct geometrically ordinary cubics with \(\min\|C'\|\) small but positive.

Questions:
- which rational quantities become numerically large only because of parameter speed?
- does arc-length invariance prevent theoretical blow-up even if coefficient conditioning is poor?
- should a practical method locally renormalize or reject near-singular spans?

### 3.3 High curvature and short spans

Test whether
\[
\frac K2N_{G,\parallel}^2
\]
becomes useless in realistic high-curvature/tiny-span configurations.

Separate genuine geometric curvature from parameterization artifacts.

### 3.4 Near self-approach

The current correspondence is order preserving and therefore valid without nearest-point uniqueness. Determine whether near self-approach merely makes the bound nonoptimal or creates any actual logical failure.

### 3.5 Separate-maxima conservatism

The current bound uses
\[
N_{G,\perp}+\frac K2N_{G,\parallel}^2.
\]
Worst normal error, worst curvature, and worst tangential error may occur at different locations.

Study whether a tighter still-cheap quantity should be
\[
\sup_s\left(\|P_NE(s)\|+\frac12 K_{\rm local}(s)\,\delta(s)^2\right)
\]
or a related localized bound. Do not adopt it unless certification remains simple.

### 3.6 Targeted literature check

Search specifically for:
- local normal graph / tubular-neighborhood error bounds for curves;
- linearization of Fréchet or shape-space distance under reparameterization;
- certified spline approximation error using tangent/normal decomposition;
- any known form matching the present first-order tangential quotient.

Purpose: identify prior art and missing hypotheses, not broad literature expansion.

## Stage decision after Phase 3

If the framework survives:
- mark the first stage breakthrough;
- write a self-contained TeX note including Green-function background, exact \(D^2\) reduction, certification theory, parameterization quotient, limitations, and a pseudocode-level certification pipeline.

If it fails:
- document the counterexample/failure mechanism;
- decide whether to strengthen the nonlinear correspondence or abandon the normal-projection route.

## Phase 4 — simplification algorithm

Postponed until after the stage review.

Only then consider weighted PL simplification under
\[
\kappa=K_0+2J,
\]
with delete/merge/move/free-breakpoint primitives and pseudocode before implementation.

## Parking lot

- optimized affine reconstruction instead of fixed endpoints;
- closed/periodic curves;
- forcing \(C^2\) candidates;
- sharp classical Green \(L^p\) constants;
- stronger nonlinear correspondence yielding exact reparameterization invariance;
- symmetric bounds using both curves as reference;
- localized curvature remainder if the global \(K\) term proves too loose.
