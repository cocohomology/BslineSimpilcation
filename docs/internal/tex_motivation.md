# Future TeX Motivation Notes

This file is not a polished note. It stores arguments that should be integrated into a future stage-level TeX document once the verification architecture closes.

## Why pure Hausdorff distance is not enough

Session 0015 produced a useful motivation chain.

The final CAD tolerance is naturally geometric, but Hausdorff distance only compares image sets. It discards parameterization, traversal order, multiplicity, and speed. Therefore one must not infer derivative-domain closeness from Hausdorff closeness alone.

The future TeX note should include the following compact sequence.

### 1. Reparameterization counterexample

Two parameterizations of the same line segment have
\[
d_H=0
\]
while their derivative vectors can differ arbitrarily. Their parameter antiderivatives can also differ by order one.

Conclusion: velocity and integration are not image-set invariants.

### 2. Small Hausdorff error does not control tangent direction

The graphs
\[
y_n(x)=n^{-1}\sin(nx)
\]
converge to a line in Hausdorff distance but keep order-one tangent-angle oscillation.

Conclusion: Hausdorff-to-\(C^1\) stability requires a regularity scale.

### 3. Even bounded curvature does not recover curvature

The graphs
\[
y_n(x)=n^{-2}\sin(nx)
\]
have Hausdorff error \(O(n^{-2})\), tangent error \(O(n^{-1})\), but order-one curvature oscillation.

Conclusion: no two-sided equivalence between Hausdorff error and the project variable \(q=C''\) exists under the current assumptions.

### 4. Conditional positive result

After fixing a correspondence, if
\[
\|E\|_\infty\le\varepsilon,
\qquad
\|E''\|_\infty\le M,
\]
then the interior interpolation estimate yields
\[
\|E'\|\le\sqrt{2M\varepsilon}
\]
when the optimizing local interval fits.

For arc-length curves with curvature bound \(K\), tangent error therefore has the natural square-root scale
\[
O(\sqrt{K\varepsilon}).
\]

### 5. Reach as the geometric regularity scale

Reach/local feature size is the natural object because it couples local curvature with global self-approach and controls uniqueness of nearby projections.

For the final TeX note, use reach to explain conceptually why Hausdorff closeness plus a geometric regularity scale can control tangent geometry, while Hausdorff alone cannot.

**Important:** before promoting any exact cross-manifold reach inequality or sharp constant to the final note, verify the precise theorem and citation from Federer reach theory / modern manifold reconstruction literature.

### 6. Connection to the project architecture

This motivation should lead directly to the distinction:

- Hausdorff acceptance only needs local setwise correspondences;
- differential/order reasoning needs a compatible ordered correspondence.

Session 0016 then shows that the final Hausdorff verifier can remain local and two-sided, while a global Fréchet-style correspondence is optional rather than mandatory.

Detailed source note:
`docs/internal/derivations/hausdorff_derivative_integral_relations.md`.
