# Algebraic Certification of the Geometry-Aware Bound

Session 0006 derivation.

## 1. Question

Session 0005 produced, for a regular reference curve and endpoint-preserving error
\[
E=C-\widetilde C,
\]
a local geometric bound of the form
\[
d_H\le N_{G,\perp}+\frac K2N_{G,\parallel}^2,
\]
provided the arc-length correspondence
\[
\rho(s)=s- E(s)\cdot T(s)
\]
is orientation preserving.

The present question is purely computational/theoretical:

> For cubic splines, do the quantities needed by this geometry-aware bound still reduce to fixed-degree univariate algebraic problems on each span, or does tangent normalization destroy the advantage of the \(D^2\)/Green reduction?

The answer is yes: all required quantities remain rational functions of fixed-degree polynomials, and even the monotonicity condition can be tested directly by positivity of a degree-at-most-eight polynomial.

---

## 2. Spanwise polynomial data

Work on one interval of the union partition where both \(C\) and \(\widetilde C\) are cubic polynomials. Write
\[
v=C',\qquad a=C'',
\]
so \(v\) is vector quadratic and \(a=v'\) vector linear. The synchronized error \(E=C-\widetilde C\) is vector cubic and \(E'\) is vector quadratic.

Define scalar polynomials
\[
S=v\cdot v,
\qquad A=E\cdot E,
\qquad B=E\cdot v,
\qquad U=E'\cdot E'.
\]
Their degree bounds are
\[
\deg S\le4,\qquad
\deg A\le6,\qquad
\deg B\le5,\qquad
\deg U\le4.
\]
Regularity of the reference curve means
\[
S(t)>0.
\]
The unit tangent is
\[
T=\frac{v}{\sqrt S}.
\]
No explicit arc-length inversion is needed below.

---

## 3. Normal synchronized error

The squared normal component is
\[
\|P_NE\|^2
=\|E\|^2-(E\cdot T)^2
=A-\frac{B^2}{S}.
\]
Define
\[
P:=AS-B^2.
\]
Then
\[
\boxed{
\|P_NE\|^2=\frac{P}{S}
}
\]
and
\[
\deg P\le10.
\]
By Cauchy--Schwarz, \(P\ge0\) wherever \(S>0\).

### Exact maximum

On a regular span, stationary points of \(P/S\) satisfy
\[
\boxed{
P'S-PS'=0.
}
\]
This polynomial has degree at most thirteen. Hence
\[
N_{G,\perp}=\sup\|P_NE\|
\]
can be computed/certified from span boundaries and the real roots of one fixed-degree polynomial per span.

### Tolerance certification

For a prescribed radius \(r\ge0\),
\[
\|P_NE\|\le r
\]
is equivalent to
\[
\boxed{
P-r^2S\le0.
}
\]
This is only a degree-at-most-ten polynomial inequality. For the actual simplification use case, where the main question is often whether an error stays below a tolerance, this direct inequality may be more useful than explicitly computing the exact maximum.

---

## 4. Tangential component

The squared tangential magnitude is
\[
|E\cdot T|^2=\frac{B^2}{S}.
\]
Thus
\[
N_{G,\parallel}=\sup\frac{|B|}{\sqrt S}.
\]
Away from zeros of \(B\), stationary points satisfy
\[
\boxed{
2B'S-BS'=0,
}
\]
a polynomial of degree at most eight. Zeros of \(B\) cannot give a positive local maximum.

For a tolerance \(r\), the condition
\[
|E\cdot T|\le r
\]
is equivalent to
\[
\boxed{
B^2-r^2S\le0,
}
\]
with degree at most ten.

---

## 5. Arc-length derivative of the error

Since
\[
D_s=\frac1{\sqrt S}\frac d{dt},
\]
we have
\[
\|D_sE\|^2=\frac{U}{S}.
\]
Stationary points satisfy
\[
\boxed{
U'S-US'=0.
}
\]
Although a naive degree count gives seven, the degree is in fact at most six: if both \(U\) and \(S\) have degree four the leading terms cancel, while unequal degree pairs give at most degree six.

A threshold test
\[
\|D_sE\|\le r
\]
is simply
\[
\boxed{
U-r^2S\le0,
}
\]
a polynomial inequality of degree at most four.

Thus the conservative monotonicity condition from Session 0005,
\[
\|D_sE\|_\infty+K\|E\|_\infty<1,
\]
is already fixed-degree certifiable. However, a substantially better direct test is available below.

---

## 6. Curvature of a cubic reference span

For a regular parametrized curve in \(\mathbb R^d\),
\[
\kappa^2
=
\frac{\|v\|^2\|a\|^2-(v\cdot a)^2}{\|v\|^6}.
\]
Define
\[
W:=S(a\cdot a)-(v\cdot a)^2.
\]
Then
\[
\boxed{
\kappa^2=\frac{W}{S^3}.
}
\]

A naive degree count suggests \(\deg W\le6\), but the leading terms cancel because \(a=v'\). More geometrically,
\[
W=\|v\wedge a\|^2.
\]
If
\[
v(h)=p_0+p_1h+p_2h^2,
\]
then
\[
v\wedge a
=p_0\wedge p_1+2(p_0\wedge p_2)h+(p_1\wedge p_2)h^2,
\]
so
\[
\boxed{
\deg W\le4.
}
\]

Stationary points of \(W/S^3\) satisfy
\[
\boxed{
W'S-3WS'=0,
}
\]
with degree at most seven.

For a proposed curvature bound \(k\),
\[
\kappa\le k
\]
is equivalent to
\[
\boxed{
W-k^2S^3\le0,
}
\]
a polynomial inequality of degree at most twelve.

For a \(C^1\) cubic spline, \(C''\) may jump at double knots. Curvature is therefore treated spanwise with one-sided endpoint values; the essential supremum is the maximum of these finitely many spanwise suprema.

---

## 7. Direct monotonicity test: stronger than the norm smallness condition

Session 0005 used the sufficient condition
\[
\|D_sE\|_\infty+K\|E\|_\infty<1
\]
to guarantee that
\[
\rho(s)=s+\delta(s),
\qquad
\delta=-E\cdot T,
\]
is increasing.

For cubic splines, monotonicity can be tested much more directly.

Since
\[
\delta=-\frac{B}{\sqrt S},
\]
we obtain
\[
D_s\delta
=-\frac{B'}{S}+\frac{BS'}{2S^2}.
\]
Therefore
\[
\rho'(s)=1+D_s\delta
=\frac{H}{2S^2},
\]
where
\[
\boxed{
H:=2S^2-2B'S+BS'.
}
\]
Because \(S>0\),
\[
\boxed{
\rho'(s)>0
\iff
H(t)>0.
}
\]
Moreover,
\[
\deg H\le8.
\]

Thus the exact monotonicity of the constructed first-order correspondence reduces to positivity of one degree-at-most-eight scalar polynomial on each spline span.

This is better than the previous global norm condition in two ways:

1. it is less conservative;
2. it avoids multiplying separate worst cases that may occur at different parameter values.

At a knot, \(E\) and \(v=C'\) are continuous, hence \(\delta\) and \(\rho\) are continuous. Their derivatives may have one-sided jumps. Positivity on every open span, together with endpoint fixing, is enough for global orientation preservation.

---

## 8. Regularity itself is fixed-degree certifiable

All formulas divide by \(S=\|C'\|^2\), so a certified lower speed bound is needed.

Because \(S\) is quartic,
\[
S'=2v\cdot a
\]
has degree at most three. Hence
\[
\min S
\]
can be certified from span boundaries and roots of a cubic equation. The condition
\[
\min S>0
\]
certifies regularity on the span.

This does not remove numerical conditioning issues when the minimum speed is extremely small, but it makes the issue explicit and detectable rather than hidden.

---

## 9. Consequence for the geometry-aware Hausdorff bound

Under endpoint preservation and direct monotonicity certification \(H>0\), Session 0005 gives
\[
 d_H
\le
N_{G,\perp}+\frac K2N_{G,\parallel}^2.
\]
Every term is now certifiable by independent fixed-degree univariate problems:

- \(N_{G,\perp}\): degree-at-most-13 stationarity, or degree-10 threshold inequality;
- \(N_{G,\parallel}\): degree-at-most-8 nonzero stationary equation, or degree-10 threshold inequality;
- \(K\): degree-at-most-7 stationarity, or degree-12 threshold inequality;
- monotonicity: degree-at-most-8 positivity test;
- regularity: quartic minimum / cubic stationary equation.

Hence the geometry-aware certification does **not** introduce a coupled two-parameter nearest-point optimization.

Structurally, for \(n\) union spans, it remains
\[
O(n)
\]
fixed-degree univariate certification subproblems, plus precision refinement near multiple roots or nearly zero speed.

This is a structural algebraic statement, not a uniform bit-complexity theorem.

---

## 10. An important practical observation

The arc-length correspondence was essential in the proof, but a certification implementation need not explicitly construct the arc-length function or invert it.

All quantities above are expressed in the original spline parameter \(t\) through \(E,C',C''\). In particular:

- tangent normalization uses \(S=\|C'\|^2\);
- curvature is rational in \(C',C''\);
- monotonicity is the polynomial inequality \(H>0\).

Thus the geometric argument uses arc length conceptually while the actual certification remains algebraic in the native spline parameter.

---

## 11. Correctness and goal review

### Checks performed

- dimensional consistency;
- regular straight-line case: \(W=0\), so \(K=0\);
- normal projection identity from orthogonal projection;
- cancellation lowering the curvature numerator from degree six to four;
- exact differentiation of \(\delta=-B/\sqrt S\);
- knot continuity: \(E,C'\) continuous for \(C^1\) cubics;
- no claim of parameterization invariance beyond the Session 0005 first-order theorem.

### Main remaining risk

The formal algebraic degrees are fixed, but near-zero speed can make rational quantities ill-conditioned. This is not a theoretical obstruction under regularity, but may become an engineering issue. It should be attacked explicitly in the stage review.

### Goal alignment

This session answers the main question raised by Session 0005: geometry awareness does **not** destroy the computational advantage of the \(D^2\)/Green framework. The new bound still reduces to local univariate algebraic certification, rather than full curve-curve correspondence search.

That is strong enough to trigger a stage-level adversarial review, but not yet strong enough to claim a final framework or novelty.
