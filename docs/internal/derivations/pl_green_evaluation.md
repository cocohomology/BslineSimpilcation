# PL-Specific Evaluation of the Fixed-Endpoint Green Error

Session 0004 derivation.

## 1. Question

Assume the endpoint-preserving gauge
\[
E''=e,\qquad E(a)=E(b)=0,
\]
with
\[
e=C''-\widetilde C''.
\]
For cubic \(C,\widetilde C\), the function \(e\) is piecewise affine on the union of their second-derivative breakpoints and may jump at double knots.

The quantity of interest is
\[
N_G(e)=\|E\|_\infty
=\max_{t\in[a,b]}\|E(t)\|_2.
\]

The goal here is not to optimize breakpoints. It is only to decide whether \(N_G\) can be evaluated or certified directly, without dense sampling and without replacing it by a global \(L^p\) surrogate.

---

## 2. Union partition and local form of the forcing

Let
\[
a=x_0<x_1<\cdots<x_n=b
\]
be the union partition of all breakpoints of \(q=C''\) and \(\widetilde q=\widetilde C''\).

On the open span \((x_i,x_{i+1})\), write
\[
e(t)=\alpha_i+\beta_i h,
\qquad h=t-x_i,
\qquad 0<h<h_i,
\]
where \(h_i=x_{i+1}-x_i\) and \(\alpha_i,\beta_i\in\mathbb R^d\).

A jump of \(e\) at \(x_i\) causes no difficulty: point values of \(e\) do not affect the integral solution. The left and right affine pieces are simply treated as different spans.

---

## 3. Endpoint correction is only one global vector

Start from the initial-value representation
\[
E(t)=(t-a)v_0+\int_a^t (t-s)e(s)\,ds,
\]
where \(v_0=E'(a)\).

Enforcing \(E(b)=0\) gives
\[
0=(b-a)v_0+\int_a^b(b-s)e(s)\,ds.
\]
Therefore
\[
\boxed{
 v_0=-\frac{1}{b-a}\int_a^b(b-s)e(s)\,ds.
}
\]

This is important computationally: the fixed-endpoint condition does not create a global linear system. It contributes one global vector moment, after which the solution propagates span by span.

For a piecewise-affine \(e\), the moment above is exactly integrable by fixed-degree polynomial formulas.

---

## 4. Exact cubic form on every span

Let
\[
P_i=E(x_i),\qquad V_i=E'(x_i).
\]
On the span \([x_i,x_{i+1}]\), integration gives
\[
\boxed{
E(t)=P_i+V_i h+\frac12\alpha_i h^2+\frac16\beta_i h^3,
}
\]
and
\[
\boxed{
E'(t)=V_i+\alpha_i h+\frac12\beta_i h^2.
}
\]

Hence the propagation rules are
\[
P_{i+1}=P_i+V_i h_i+\frac12\alpha_i h_i^2+\frac16\beta_i h_i^3,
\]
\[
V_{i+1}=V_i+\alpha_i h_i+\frac12\beta_i h_i^2.
\]

Starting from
\[
P_0=0,
\qquad
V_0=-\frac{1}{b-a}\int_a^b(b-s)e(s)\,ds,
\]
we recover the complete piecewise-cubic error curve \(E\) in one forward pass.

In exact arithmetic the final consistency check is
\[
P_n=E(b)=0.
\]

### Continuity at jumps of \(e\)

Even if \(e\) jumps at \(x_i\), the integral construction makes \(E\) and \(E'\) continuous. Only \(E''=e\) jumps. Thus no additional candidate point beyond the ordinary span boundary is needed to handle a double knot.

---

## 5. Exact finite maximization: vector-valued case

On one span, \(E\) is a vector polynomial of degree at most three. Define
\[
F(t)=\|E(t)\|_2^2=E(t)\cdot E(t).
\]
Then \(F\) is a scalar polynomial of degree at most six and
\[
F'(t)=2E(t)\cdot E'(t).
\]
Since \(E\) is cubic and \(E'\) is quadratic,
\[
\boxed{
E(t)\cdot E'(t)
\text{ has degree at most }5.
}
\]
The degree five is generic: if the cubic coefficient of \(E\) is nonzero, the leading coefficient of \(E\cdot E'\) is three times the squared norm of that cubic coefficient and therefore does not cancel.

Consequently, the maximum of \(\|E(t)\|\) on a span occurs among:

1. the two span endpoints;
2. the real roots in the open span of
   \[
   E(t)\cdot E'(t)=0.
   \]

There are at most five isolated interior stationary points per span, counting multiplicity only coarsely.

If \(E\cdot E'\equiv0\) on a span, then \(\|E\|^2\) is constant there, so the endpoints already suffice.

Therefore the global quantity \(N_G\) is the maximum over a finite set obtained by independent fixed-degree root problems on the union partition.

### Scalar case

If \(d=1\), the task is even simpler. Away from zeros of \(E\), an interior extremum of \(|E|\) satisfies
\[
E'(t)=0,
\]
which is only a quadratic equation on each span. Zeros of \(E\) cannot create a positive local maximum of \(|E|\).

---

## 6. Certified evaluation strategy A: isolate the quintic stationary roots

For exact rational/algebraic coefficients, each span can be treated by a standard real-root isolation method such as a Sturm-sequence or Bernstein/Descartes procedure.

Conceptually:

1. construct the quintic
   \[
   p_i(h)=E_i(h)\cdot E_i'(h),
   \qquad h\in(0,h_i);
   \]
2. isolate every real root of \(p_i\) in that interval;
3. evaluate or enclose \(F_i=\|E_i\|^2\) at each isolated root and at span endpoints;
4. refine root/value intervals until the maximum is uniquely determined or enclosed to the desired tolerance;
5. take the maximum over all spans.

There is no useful generic radicals formula because a quintic is genuinely present, but this is not an obstacle to certification: the polynomial degree is fixed.

For floating-point CAD data, the mathematically honest statement is different from symbolic exactness. One can certify an enclosure for the stored floating model using outward-rounded interval arithmetic, or rationalize the stored coefficients first. The underlying physical geometry is already represented by finite-precision data, so “exactness” must always be interpreted relative to that representation.

### Structural cost

If the union partition has \(n\) spans, then:
- building the endpoint correction is one linear pass;
- propagating all cubic pieces is one linear pass;
- each span requires one polynomial root-isolation problem of degree at most five.

Thus the structural arithmetic count is
\[
O(n)
\]
fixed-degree subproblems. This is not a claim about bit complexity: nearly multiple roots can demand additional precision. The important point is that the polynomial degree does not grow with the spline complexity.

---

## 7. Certified evaluation strategy B: cubic Bézier subdivision

There is a second route that may be more natural in a CAD kernel and avoids explicit quintic solving.

Represent each cubic error segment on \([x_i,x_{i+1}]\) in Bernstein form
\[
E(u)=\sum_{j=0}^3 B_j^3(u)Q_j,
\qquad u\in[0,1].
\]
Because the Bernstein basis is nonnegative and sums to one,
\[
E(u)\in\operatorname{conv}\{Q_0,Q_1,Q_2,Q_3\}.
\]
The Euclidean norm is convex, hence
\[
\boxed{
\|E(u)\|\le \max_j\|Q_j\|.
}
\]
This gives an immediate certified upper bound for the entire span.

A lower bound is obtained by evaluating \(E\) at any parameter values, for example the segment endpoints and midpoint.

Using de Casteljau subdivision:
- split the cubic segment;
- obtain two child control polygons exactly from affine combinations;
- apply the same control-point norm upper bound on each child;
- discard a child if its upper bound is already below the current global lower bound or a prescribed tolerance.

Repeated subdivision makes the control polygons converge to the curve, so the upper and lower bounds converge to the true maximum. Therefore this yields a certified branch-and-bound procedure to arbitrary tolerance, without dense uniform sampling.

For a pure yes/no tolerance test \(N_G\le\varepsilon\):
- if every active control-polygon upper bound is \(\le\varepsilon\), accept;
- if any evaluated point has norm \(>\varepsilon\), reject;
- otherwise subdivide the ambiguous segments.

If the true maximum is exactly equal to \(\varepsilon\), a purely interval/subdivision decision procedure may refine indefinitely; a root-isolation fallback resolves the algebraic boundary case.

This gives a practical pair of methods:

- **root isolation** for direct algebraic extremum calculation;
- **Bézier subdivision** for robust geometric certification and pruning.

---

## 8. Comparison with direct Hausdorff evaluation

The synchronized Green error can be reinterpreted as follows:

> construct the piecewise-cubic error curve \(E(t)=C(t)-\widetilde C(t)\), then find its farthest point from the fixed origin.

That is a one-parameter polynomial extremum problem.

By contrast, a directed Hausdorff distance has the form
\[
h(C,\widetilde C)
=\max_t\min_u\|C(t)-\widetilde C(u)\|.
\]
Even before considering the reverse direction, it contains:
- an inner nearest-point problem in \(u\);
- an outer maximization in \(t\);
- possible switching of the nearest-point branch;
- segment-pair combinatorics when both splines are piecewise cubic.

Certified Hausdorff algorithms can of course exploit subdivision and bounding, so this is not a runtime theorem. But structurally the difference is substantial:

\[
\boxed{
N_G:\ \text{independent univariate fixed-degree extrema},
}
\]
versus
\[
\boxed{
 d_H:\ \text{coupled correspondence / nearest-point geometry}.
}
\]

Thus the hoped-for computational advantage of the synchronized Green layer survives this review.

---

## 9. What this result changes

Before this session it was plausible that \(N_G\) would merely replace one hard error calculation by another. That concern is now substantially reduced.

Within the endpoint-preserving cubic \(C^1\) setting:

1. the representation complexity of the candidate is exact in the PL second-derivative domain;
2. the synchronized positional error is exact in that same domain;
3. the synchronized error can be evaluated/certified by fixed-degree local polynomial calculations or cubic Bézier subdivision.

Therefore there is currently no theoretical need to replace \(N_G\) by an \(L^p\) surrogate merely for evaluability.

Ordinary \(L^p\) bounds may still be useful later as very cheap pruning bounds or for comparison with Lyche-type methods, but they are no longer the main metric candidate at the synchronized level.

---

## 10. Correctness and scope review

### Checked

- local integration formula;
- endpoint correction sign using constant forcing;
- continuity of \(E,E'\) across jumps in \(e\);
- polynomial degrees: cubic \(E\), quadratic \(E'\), quintic \(E\cdot E'\);
- compactness guarantees existence of the maximum;
- span boundaries are included explicitly;
- Bézier convex-hull norm bound follows from convexity of the Euclidean norm.

### Important limitations

- \(N_G\) is still synchronized-parameter error, not a parameterization-invariant geometry metric;
- the \(O(n)\) statement is structural, not a uniform finite-precision runtime bound;
- an exact equality decision at a tolerance boundary may require algebraic root handling;
- none of this yet tells us how hard it is to optimize breakpoint locations under \(N_G\).

### Goal alignment

The work remains directly aligned with the original CAD goal. The purpose was to preserve a simpler-than-Hausdorff error calculation after moving to the \(C''\) domain. This session establishes that the synchronized baseline does preserve that advantage.

The dominant theoretical risk has now moved from **evaluability** to **parameterization/geometric tightness**.

---

## 11. Next narrow question

The next session should not continue polishing the synchronized metric.

Instead, begin the parameterization problem with the smallest local question:

> For a nearby regular curve \(\widetilde C=C+E\), can the tangential component of \(E\) be removed to first order by a small monotone reparameterization, leaving the normal component as the first-order geometric residual?

The target should be an explicit reparameterization correction and an explicit second-order remainder, with failure conditions recorded. Do not jump directly to a full Hausdorff theorem.
