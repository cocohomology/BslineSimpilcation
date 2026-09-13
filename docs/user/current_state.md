# Current State — User-Facing Summary

## Scope of the current side project

The present research branch is intentionally restricted to **\(C^1\), cubic, non-rational spline curves**. The broader spline-simplification problem (degree reduction, arbitrary multiplicities, rational curves, surfaces, topology, etc.) is postponed.

The motivating observation is that for a cubic spline \(C\), the second derivative \(C''\) is piecewise linear. This suggests the transformation

\[
C \xrightarrow{D^2} q=C''
\]

followed by a low-complexity approximation of \(q\), then two integrations back to a cubic spline candidate.

The research goal is not merely to fit \(C''\) with a smaller polyline. The central question is how to define and exploit an error measure in the \(C''\)-domain that is:

- tighter than ordinary \(L^p\) bounds;
- sensitive to cancellation under integration;
- less vulnerable to bad parametrization;
- still much easier to optimize than direct Hausdorff distance;
- useful for deriving a practical simplification strategy.

## What is already structurally clear

1. **Piecewise-linear reduction**  
   For a \(C^1\) cubic spline, \(C''\) is piecewise linear. Double knots may produce jumps in \(C''\), which are still compatible with a \(C^1\) cubic after integrating twice.

2. **Integration is the right place to measure positional effect**  
   If
   \[
   e=C''-\widetilde C'',
   \]
   then the positional error \(E=C-\widetilde C\) is obtained by applying a second-order Green operator after boundary conditions are fixed:
   \[
   E=Ge.
   \]
   Therefore large local derivative error can have small positional effect after integration, and different derivative errors can partially cancel.

3. **Ordinary \(L^p\) norms are likely not the right optimization metric**  
   They discard sign/direction/cancellation information before integration. They may still provide useful comparison or certification bounds, but are not assumed to be the final metric.

4. **A purely parametrized norm cannot solve the geometric problem by itself**  
   Two geometrically identical curves with different parametrizations can have nonzero \(C''\)-difference. Therefore any attempt to improve bad parametrization must either introduce a correspondence/reparametrization step or quotient out tangential effects in some controlled manner.

5. **A promising intermediate metric family exists**  
   Current candidates include:
   - the Green-induced quantity \(\|e\|_G=\|Ge\|_\infty\);
   - normal-projected positional error \(\|P_NGe\|_\infty\);
   - a nonlinear normal-correspondence distance in the spirit of Degen;
   - Fréchet-type order-preserving correspondence metrics as a conceptual upper layer.

## Current research frontier

The first serious theoretical task is to compare, for nearby regular curves,

\[
\|e\|_{L^p},\qquad
\|Ge\|_\infty,\qquad
\|P_NGe\|_\infty,\qquad
 d_N,\qquad
 d_H.
\]

The aim is to determine which relationships are exact, which are one-sided bounds, which are only local asymptotics, and which fail by counterexample.

The current preferred direction is **not** to search for a fashionable named norm first. Instead, derive the natural error quantity from the integration operator and from geometric correspondence, then identify whether it coincides with a known function-space norm afterward.

## What has not yet been established

No new theorem beyond the basic Green-operator structure has yet been accepted as a stage-level breakthrough. In particular, the following remain open:

- whether a normal-projected Green quantity admits a useful certified Hausdorff upper bound;
- how large the higher-order/tangential remainder is after removing first-order reparametrization effects;
- whether the resulting quantity remains computationally simple for piecewise-linear \(C''\);
- whether the metric is sufficiently stable on very short knot spans;
- whether it gives a better ordering of candidate simplifications than \(L^p\) in practical examples.

## When this document should change

Update this file only when something stable changes: a theorem is established, a direction is decisively killed, a new central definition is adopted, or the overall research program changes. Routine experiments and speculative ideas belong in the internal documents.
