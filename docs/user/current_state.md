# Current State — User-Facing Summary

## Scope of the current side project

The present research branch is intentionally restricted to **\(C^1\), cubic, non-rational spline curves**. The broader spline-simplification problem (degree reduction, arbitrary multiplicities, rational curves, surfaces, topology, etc.) is postponed.

The motivating transformation is

\[
C \xrightarrow{D^2} q=C'',
\]

where \(q\) is piecewise linear, possibly discontinuous at double knots. The plan is to seek low-complexity approximations of \(q\), then integrate twice back to a cubic spline candidate.

The central unresolved question remains the error measure in the \(C''\)-domain: it should be tighter and more geometry-aware than ordinary \(L^p\) norms while remaining much easier to optimize than direct Hausdorff distance.

## Stable result from Session 0002: the D2 reduction is exact

Let \(S^1_3\) denote \(C^1\) piecewise-cubic curves on a fixed partition, and let \(PL_{\rm disc}\) denote piecewise-affine vector functions with possible jumps at the breakpoints. Then

\[
D^2:S^1_3\to PL_{\rm disc}
\]

is surjective and

\[
\ker D^2=\mathcal P_1,
\]

the affine functions of the parameter. Equivalently,

\[
S^1_3/\mathcal P_1\cong PL_{\rm disc}.
\]

Thus the proposed second-derivative route is algebraically closed: every admissible PL second derivative integrates back to a \(C^1\) cubic once two vector integration constants are fixed.

### Exact knot / breakpoint dictionary

For an interior point \(x_i\), let \(q=C''\).

- If \([q]_i\neq0\), then \(C\) is \(C^1\) but not \(C^2\): a minimal cubic representation needs a **double knot**.
- If \([q]_i=0\) but \([q']_i\neq0\), then \(C\) is \(C^2\) but not \(C^3\): a minimal cubic representation needs a **simple knot**.
- If both jumps vanish, the two cubic pieces are restrictions of one cubic polynomial: the breakpoint is representation-redundant.

If \(K\) is the number of continuous kinks of \(q\) and \(J\) the number of jumps, define

\[
\kappa(q)=K+2J.
\]

For a minimal open/clamped cubic B-spline representation,

\[
N_{\rm ctrl}=4+\kappa(q).
\]

So, at fixed cubic degree within the \(C^1\) class, reducing minimal knot multiplicity/control-point count is exactly equivalent to reducing this weighted PL singularity complexity. This is stronger than the informal statement that “knots become polyline breakpoints.”

A detailed derivation is stored in `docs/internal/derivations/d2_reconstruction.md`.

## Important caveat exposed by the proof

The map \(D^2\) kills a two-vector-dimensional affine part. Therefore an error metric on \(q\) is meaningless for positional control until this affine kernel is fixed or optimized.

Two useful reconstruction gauges are:

- fix \(C(a)\) and \(C'(a)\);
- fix both endpoint positions \(C(a),C(b)\).

For CAD/B-Rep use, preserving both endpoints is currently the preferred default. A third possibility—optimizing the affine correction after approximating \(q\)—may later be useful when endpoints need not be preserved.

## What remains structurally clear

1. **Integration is the right place to measure positional effect.**  
   If \(e=C''-\widetilde C''\), then after fixing a reconstruction gauge the positional error \(E=C-\widetilde C\) is obtained by a second-order Green operator:
   \[
   E=Ge.
   \]

2. **Ordinary \(L^p\) norms are likely not the final optimization metric.**  
   They discard sign/direction/cancellation information before integration. They may remain useful as comparison or certification bounds.

3. **A purely parametrized norm cannot solve the geometric problem by itself.**  
   Two geometrically identical curves with different parametrizations can have different second derivatives. Improving bad parametrization will eventually require a correspondence/reparametrization step or a controlled quotient of tangential effects.

4. **Promising intermediate objects remain:**
   - the Green-induced synchronized quantity \(\|Ge\|_\infty\);
   - normal-projected positional error \(\|P_NGe\|_\infty\);
   - nonlinear normal correspondence in the spirit of Degen;
   - Fréchet-type order-preserving correspondence as a conceptual upper layer.

## Current research frontier

The next session will remain narrow: use the **two-endpoint reconstruction gauge** and derive its exact Green kernel and induced synchronized positional error. Only after this baseline is reviewed will the project return to cancellation, \(L^p\) comparison, or parametrization.

## What has not yet been established

- whether a Green-induced metric materially outperforms \(L^p\) in candidate ranking;
- whether a normal-projected Green quantity admits a useful certified Hausdorff upper bound;
- how large the higher-order/tangential remainder is after removing first-order reparametrization effects;
- whether the final metric remains stable on very short knot spans;
- whether geometry-aware treatment destroys the computational advantage of the PL representation.

No TeX stage note has been created yet: the current result is foundational and useful, but still too elementary and too far from the geometric-error breakthrough to justify one.
