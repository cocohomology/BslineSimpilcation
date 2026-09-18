# Bad Parameterization, Derivative-Space Geometry, and Intrinsic Frame Variables

Session 0017.

## 1. Why this question matters now

The Lyche replication branch has exposed a concrete practical limitation: an approximation theory built on parameter-domain \(L^p\) norms inherits the original parameterization. A geometrically simple curve can therefore remain difficult if its speed law is complicated.

Two possible escapes were proposed:

1. for a \(C^1\) piecewise-quadratic curve, differentiate once, regard the derivative as a geometric polyline, simplify that polyline, then integrate back;
2. abandon parameter-dependent derivatives and work with intrinsic curve data such as curvature/torsion or a moving-frame description.

This note analyzes both ideas and connects them to the existing Hausdorff-verification architecture.

The main conclusion is:

> The first idea is useful but insufficient if "polyline approximation" means only Hausdorff approximation of the derivative image. The second idea identifies the correct quotient by parameterization. A particularly useful bridge is the decomposition
> \[
> C''=v'T+v^2K,
> \]
> where \(v=\|C'\|\), \(T\) is the unit tangent, and \(K=dT/ds\) is the curvature vector.

The tangential term \(v'T\) is pure parameter gauge. This is exactly the term that can be arbitrarily complicated on a geometrically straight line.

---

## 2. Quadratic toy model: differentiation gives a PL curve

Let
\[
C:[0,1]\to\mathbb R^d
\]
be regular, \(C^1\), and piecewise quadratic. Then
\[
V(t):=C'(t)
\]
is a continuous piecewise-linear curve in velocity space.

A tempting program is:

\[
C
\longmapsto
V=C'
\longmapsto
\widetilde V\ \text{(few PL segments)}
\longmapsto
\widetilde C(t)=C(0)+\int_0^t\widetilde V(s)\,ds.
\]

If a geometric PL simplifier could ignore bad parameterization in \(V\), this would be an attractive lower-degree test case for the cubic \(C''\) program.

However, one must distinguish **setwise approximation of the derivative image** from a **coherent time-indexed approximation of the derivative field**.

---

## 3. Negative theorem: Hausdorff closeness of derivative images does not control the integrated curves

Take the scalar one-dimensional example
\[
V(t)=t,
\]
and
\[
\widetilde V(t)=
\begin{cases}
2t,&0\le t\le \frac12,\\
1,&\frac12\le t\le1.
\end{cases}
\]

Both are continuous PL functions and
\[
\operatorname{Im}V
=
\operatorname{Im}\widetilde V
=
[0,1].
\]
Hence
\[
d_H(\operatorname{Im}V,\operatorname{Im}\widetilde V)=0.
\]

Integrating from the common initial point gives
\[
C(t)=\frac{t^2}{2},
\]
while
\[
\widetilde C(t)=
\begin{cases}
t^2,&0\le t\le\frac12,\\
t-\frac14,&\frac12\le t\le1.
\end{cases}
\]

Thus
\[
\operatorname{Im}C=[0,\tfrac12],
\qquad
\operatorname{Im}\widetilde C=[0,\tfrac34],
\]
so
\[
\boxed{
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)=\frac14
}
\]
although the derivative-image Hausdorff distance is exactly zero.

The example remains entirely inside the intended toy class:
- \(V,\widetilde V\) are continuous PL;
- \(C,\widetilde C\) are \(C^1\) piecewise quadratic.

Therefore there is no function \(f(\varepsilon)\to0\) such that
\[
d_H(\operatorname{Im}V,\operatorname{Im}\widetilde V)\le\varepsilon
\]
alone implies
\[
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)\le f(\varepsilon).
\]

This is the same structural obstruction found in Session 0015: integration remembers order and parameter measure, while Hausdorff distance forgets both.

---

## 4. Positive theorem once a coherent derivative correspondence is supplied

Suppose instead that both derivative fields are represented on the same parameter interval \([a,b]\), with
\[
\|V-\widehat V\|_\infty\le\varepsilon.
\]
Let \(L=b-a\), and define
\[
C(t)=C(a)+\int_a^tV(s)\,ds,
\qquad
\widehat C(t)=C(a)+\int_a^t\widehat V(s)\,ds.
\]

Then
\[
\boxed{
\|C-\widehat C\|_\infty\le L\varepsilon.
}
\]

If the two integrated curves also share the final endpoint, then
\[
\int_a^b(V-\widehat V)\,ds=0.
\]
For \(E=C-\widehat C\),
\[
E(t)=\int_a^t(V-\widehat V)\,ds
=
-\int_t^b(V-\widehat V)\,ds,
\]
hence
\[
\boxed{
\|E(t)\|
\le
\min\{t-a,b-t\}\varepsilon
\le
\frac L2\varepsilon.
}
\]

So the endpoint-preserving first-integration analogue of the current Green estimate has the sharp scale \(L/2\).

A geometric derivative-polyline simplifier can exploit this only if it returns more than a set. It must provide a coherent selection
\[
\widehat V(t)\in\operatorname{Im}\widetilde V
\]
that stays within \(\varepsilon\) of the original \(V(t)\). If the selection map is piecewise linear and \(\widetilde V\) is PL, then \(\widehat V\) remains PL and its integral remains piecewise quadratic.

Thus the correct derivative-space analogue is closer to an ordered/Fréchet-style simplification than to pure Hausdorff polyline simplification.

---

## 5. What the toy model does and does not fix about a badly parameterized straight line

Let
\[
C(t)=\phi(t)e,
\]
where \(e\) is a fixed unit vector and \(\phi'(t)>0\). The image of \(C\) is a straight segment regardless of the speed law.

Then
\[
V(t)=\phi'(t)e.
\]

If \(\phi'\) varies monotonically, the velocity-space image is itself one straight segment. A geometric PL simplifier can therefore replace many velocity-space breakpoints by one segment with zero setwise error, and integration yields one quadratic segment whose spatial image is still a straight line. This is a genuine simplification win.

But if \(\phi'\) oscillates repeatedly between slow and fast values, the derivative curve repeatedly traverses the same velocity-space segment. A setwise Hausdorff simplifier still sees only one segment and may discard all oscillations, while integration changes. An order-preserving derivative approximation may be forced to retain much of this backtracking even though the spatial curve is still just a line.

Therefore derivative-image geometry removes some parameter redundancy but not the fundamental speed gauge.

The remaining redundancy is positive radial scaling of the velocity:
\[
V=vT.
\]

For a straight line, \(T\) is constant and all complexity in \(v\) is geometrically irrelevant.

---

## 6. Exact decomposition of \(C''\) into parameter gauge and geometry

For any regular curve, write
\[
C'(t)=v(t)T(t),
\qquad
v(t)=\|C'(t)\|>0.
\]
Let \(s\) denote arc length, so
\[
\frac{ds}{dt}=v.
\]

Differentiating,
\[
C''
=
v'T+vT_t.
\]
Since
\[
T_t=vT_s,
\]
we obtain the exact identity
\[
\boxed{
C''=v'T+v^2K,
\qquad
K:=\frac{dT}{ds}.
}
\]

The two pieces have different meanings:

- \(v'T\): tangential acceleration, entirely caused by the chosen parameter speed;
- \(v^2K\): the geometric turning term, scaled by the square of speed.

Equivalently,
\[
\boxed{
K
=
\frac{P_{T^\perp}C''}{\|C'\|^2}.
}
\]

For a geometrically straight line,
\[
K\equiv0
\]
for every regular parameterization, even if \(C''\) is large and highly oscillatory.

This is the cleanest structural explanation yet for the bad-parameter failure of a raw \(q=C''\) simplifier.

It also reinterprets the earlier tangent/normal theme: the tangential part of the curve's own second derivative is a gauge variable, not shape information.

---

## 7. Intrinsic frame variables

The classical Frenet picture says that an arc-length curve is determined up to rigid motion by curvature and torsion, under the usual nonvanishing-curvature hypotheses.

For the present project, the Bishop/parallel frame is algebraically cleaner because it remains regular through straight and inflectional regions.

Let
\[
R(s)=[T(s),E_1(s),E_2(s)]\in SO(3)
\]
be a Bishop frame. Then
\[
R'(s)=R(s)A(s),
\]
with
\[
A(s)=
\begin{pmatrix}
0&-k_1&-k_2\\
k_1&0&0\\
k_2&0&0
\end{pmatrix},
\]
and
\[
C'(s)=T(s).
\]

Given \(k_1(s),k_2(s)\), one initial point, and one initial orthonormal frame, the ODE determines the curve uniquely. Changing the initial point/frame changes only the ambient rigid motion; rotating the initial normal pair introduces the expected constant Bishop-gauge rotation in \((k_1,k_2)\).

Thus \((k_1,k_2)\), as functions of arc length modulo this constant normal-frame phase, are intrinsic shape data.

---

## 8. Quantitative intrinsic stability theorem

The frame formulation gives more than uniqueness. It gives a direct perturbation estimate.

Let \(C,\widetilde C\) be arc-length curves on \([0,L]\), with initial points and Bishop frames aligned. Let their Bishop coefficients be
\[
(k_1,k_2),
\qquad
(\widetilde k_1,\widetilde k_2).
\]
Define
\[
\delta(s)
=
\sqrt{
(k_1-\widetilde k_1)^2
+
(k_2-\widetilde k_2)^2
}.
\]

Let \(R,\widetilde R\) be the two frame matrices and set
\[
H=R\widetilde R^T.
\]
Because both coefficient matrices are skew-symmetric,
\[
H'
=
R(A-\widetilde A)\widetilde R^T.
\]
Orthogonal invariance of the operator norm gives
\[
\|H'(s)\|_2
=
\|A(s)-\widetilde A(s)\|_2
=
\delta(s).
\]

Since \(H(0)=I\),
\[
\boxed{
\|T(s)-\widetilde T(s)\|
\le
\int_0^s\delta(r)\,dr.
}
\]

Integrating once more,
\[
\boxed{
\|C(s)-\widetilde C(s)\|
\le
\int_0^s (s-r)\delta(r)\,dr.
}
\]

In particular, if
\[
\delta(s)\le\eta
\]
for all \(s\), then
\[
\boxed{
\|C-\widetilde C\|_\infty
\le
\frac{L^2}{2}\eta,
}
\]
and therefore
\[
\boxed{
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)
\le
\frac{L^2}{2}\eta.
}
\]

This is an intrinsic analogue of the project's Green transport:

\[
\text{intrinsic curvature-data error}
\longrightarrow
\text{frame error}
\longrightarrow
\text{position/Hausdorff error}.
\]

A notable feature is the absence of a Gronwall exponential: skew-symmetry of the moving-frame ODE makes the relative-frame derivative depend directly on \(A-\widetilde A\).

For Frenet data the same calculation formally uses
\[
\delta=\sqrt{(\Delta\kappa)^2+(\Delta\tau)^2},
\]
but the Bishop version is preferable near \(\kappa=0\).

---

## 9. Relation to the current cubic \(q=C''\) program

This intrinsic route has a major advantage and a major cost.

### Advantage

It removes bad parameterization at the level of the state variable.

The raw derivative-domain variable
\[
q=C''
\]
mixes
\[
\text{speed gauge}
\quad+\quad
\text{shape}.
\]

The intrinsic variables
\[
T(s),\quad K(s),\quad (k_1(s),k_2(s))
\]
do not.

This means the observed Lyche limitation is not merely a weakness of one ranking heuristic: it is a warning against any candidate generator whose objective remains strongly tied to the original parameter measure.

### Cost

The exact spline-complexity dictionary is lost.

For cubic splines:
- \(C''\) is PL and knot complexity is explicit;
- curvature/Bishop data involve normalization by speed and arc length;
- arc-length inversion is generally nonalgebraic;
- reconstructing from simplified intrinsic coefficients solves an ODE and does not automatically produce a B-spline.

So intrinsic variables should not replace the \(D^2\) route without an engineering bridge.

---

## 10. Two concrete bridges worth testing later

### Bridge A — parameter gauge fixing, then \(q\)-space simplification

Use geometry-aware rebuilding to obtain a near-arc-length or otherwise well-conditioned parameterization of the same shape first. Then apply the existing \(q=C''\) simplification machinery to the gauge-fixed curve.

Architecture:
\[
\text{badly parameterized spline}
\to
\text{geometry-preserving reparameterized spline}
\to
q\text{-space simplification}
\to
\text{Hausdorff verifier}.
\]

This keeps the exact spline algebra after a preprocessing step.

### Bridge B — intrinsic candidate generation, spline recovery last

Simplify an intrinsic signal such as \(T(s)\) or Bishop coefficients, reconstruct an approximate geometric curve, then fit/recover a low-complexity spline and certify it with the current Hausdorff verifier.

Architecture:
\[
\text{intrinsic shape signal}
\to
\text{simple intrinsic model}
\to
\text{reconstructed curve}
\to
\text{spline representation}
\to
\text{Hausdorff verifier}.
\]

This is more parameter-invariant but much more radical.

---

## 11. Current research decision

The two proposed directions are both useful, but at different levels.

1. **Derivative-polyline geometry for quadratic curves** is an excellent toy model and can produce rigorous integration inequalities once a coherent derivative correspondence is supplied. Pure derivative-image Hausdorff is insufficient.
2. **Intrinsic frame analysis** is the deeper route. It explains the bad-parameter pathology exactly and yields a quantitative stability theorem from intrinsic coefficient error to Hausdorff error.
3. The identity
   \[
   C''=v'T+v^2K
   \]
   should be treated as a stable structural result for Phase 5.
4. Candidate generation should no longer begin with the assumption that raw \(q=C''\) is always the correct simplification variable. The first Phase-5 decision must distinguish **parameter complexity** from **shape complexity**.
5. The current Phase-4 Hausdorff verifier remains valuable regardless of which candidate generator wins; in fact, it is what makes parameter-invariant candidate generation safe to explore.

No immediate code task is created from this session. The pending two-sided verifier test remains the active engineering gate. The present result changes the design of the following candidate-generation phase.
