# Exact D2 Reduction for C1 Cubic Splines

Status: **Established foundation** (Session 0002)

This note isolates the algebraic part of the proposed simplification route. It deliberately does **not** address the error metric or geometric distance yet.

## 1. Setting

Let

\[
a=x_0<x_1<\cdots <x_m=b
\]

be a partition. Let \(S^1_3(\Pi;\mathbb R^d)\) denote vector-valued functions \(C:[a,b]\to\mathbb R^d\) such that

- \(C\in C^1[a,b]\);
- on every open span \((x_{j-1},x_j)\), \(C\) is a polynomial of degree at most three.

Let \(PL_{\rm disc}(\Pi;\mathbb R^d)\) denote piecewise-affine vector functions \(q\), with finite one-sided traces at every interior breakpoint. Values assigned exactly at breakpoints are irrelevant; the natural object is the collection of affine pieces (equivalently an \(L^\infty\) class plus one-sided traces).

The standard spline continuity rule is consistent with this setting: for degree three, an interior knot of multiplicity one generically gives \(C^2\) continuity and multiplicity two generically gives \(C^1\). Lyche--Mørken (1988, Sec. 1) state the general continuity rule in terms of order and multiplicity. Schumaker's derivative/antiderivative formulas in Chapter 5 give the corresponding B-spline coefficient maps.

## 2. Reconstruction theorem

### Theorem 2.1

The second derivative map

\[
D^2:S^1_3(\Pi;\mathbb R^d)\longrightarrow PL_{\rm disc}(\Pi;\mathbb R^d)
\]

(where \(D^2C\) is understood piecewise / almost everywhere) is surjective and

\[
\ker D^2=\mathcal P_1(\mathbb R^d),
\]

the vector-valued affine functions of the parameter.

Hence

\[
S^1_3(\Pi;\mathbb R^d)/\mathcal P_1(\mathbb R^d)
\cong
PL_{\rm disc}(\Pi;\mathbb R^d).
\]

### Proof

If \(C\in S^1_3\), then on each span its second derivative is affine, so \(D^2C\in PL_{\rm disc}\). Because only \(C\) and \(C'\) are required to be continuous, \(C''\) may jump at an interior point.

Conversely, take any \(q\in PL_{\rm disc}\), a position \(P\in\mathbb R^d\), and a velocity \(V\in\mathbb R^d\). Define

\[
C(t)=P+(t-a)V+\int_a^t (t-s)q(s)\,ds.
\]

Then

\[
C'(t)=V+\int_a^t q(s)\,ds
\]

is continuous even when \(q\) jumps, while \(C''=q\) on each open span. Since integrating an affine function twice gives a cubic polynomial, \(C\in S^1_3\). This proves surjectivity.

Finally, \(D^2C=0\) iff \(C\) is affine, so the kernel is exactly \(\mathcal P_1\). QED.

## 3. Two useful gauges for the affine kernel

The reduction is not unique until the affine kernel is fixed. This is a structural issue, not a numerical detail.

### Initial position and tangent

Given \(q\), \(C(a)=P\), and \(C'(a)=V\), reconstruction is unique:

\[
C(t)=P+(t-a)V+\int_a^t(t-s)q(s)\,ds.
\]

### Two endpoint positions

Given \(q\), \(C(a)=P_0\), and \(C(b)=P_1\), reconstruction is also unique. Let \(L=b-a\). Then

\[
V=\frac{P_1-P_0-\int_a^b(b-s)q(s)\,ds}{L}
\]

and substitute this into the previous formula.

Equivalently,

\[
C(t)=P_0+\frac{t-a}{L}(P_1-P_0)
+\int_a^t(t-s)q(s)\,ds
-\frac{t-a}{L}\int_a^b(b-s)q(s)\,ds.
\]

For CAD simplification, fixing the two endpoints is likely the more relevant default, but this should remain an explicit modeling choice.

### Important consequence

A metric on \(q=C''\) alone cannot control positional error until the affine kernel has been fixed (or optimized). Two curves with identical second derivative may differ by an arbitrary affine function of the parameter.

This clarifies a hidden assumption in the original idea: every Green-induced error quantity depends on a **gauge / reconstruction constraint**.

## 4. Exact knot / breakpoint dictionary

At an interior breakpoint \(x_i\), write

\[
[q]_i=q(x_i^+)-q(x_i^-)
\]

and, because \(q\) is affine on each side, let

\[
[q']_i=q'(x_i^+)-q'(x_i^-).
\]

There are exactly three essential cases.

### Case A: jump in q

If

\[
[q]_i\neq0,
\]

then \(C\) is \(C^1\) but not \(C^2\) at \(x_i\). A minimal cubic B-spline representation therefore needs interior multiplicity two at \(x_i\).

### Case B: continuous kink in q

If

\[
[q]_i=0,\qquad [q']_i\neq0,
\]

then \(C\) is \(C^2\) but not \(C^3\) at \(x_i\). A minimal cubic representation needs a simple interior knot.

### Case C: no singularity in q

If

\[
[q]_i=0,\qquad [q']_i=0,
\]

then the affine pieces of \(q\) are the same across \(x_i\). Since \(C\) and \(C'\) already agree there, the two cubic pieces are restrictions of one cubic polynomial. Thus \(x_i\) is representation-redundant and requires no knot in a minimal representation.

This is stronger than the informal statement "knots become polyline breakpoints": the **type** of PL singularity records the minimal cubic knot multiplicity.

## 5. Complexity dictionary

Let

- \(K\) = number of essential continuous kinks of \(q\);
- \(J\) = number of essential jumps of \(q\).

Define the multiplicity-weighted PL complexity

\[
\kappa(q)=K+2J.
\]

For a fixed set of breakpoint locations and these continuity types:

\[
\dim PL_{\rm disc}=2+K+2J=2+\kappa(q)
\]

per scalar component, while

\[
\dim S^1_3=4+K+2J=4+\kappa(q).
\]

The difference of two is exactly the affine kernel of \(D^2\).

For a minimal open/clamped cubic B-spline representation, the number of vector control points is

\[
N_{\rm ctrl}=4+\kappa(q).
\]

Thus, at fixed cubic degree and within the \(C^1\) class, reducing minimal knot multiplicity / control-point count is algebraically equivalent to reducing the weighted singularity complexity of the piecewise-linear second derivative.

Important nuance: this statement concerns representation complexity for a given candidate (and fixed breakpoint locations in the dimension count). If breakpoint locations are also free variables, they add nonlinear parameters and the optimization problem remains nonlinear.

## 6. Review against the original research goal

### What this validates

The proposed route is algebraically closed:

1. differentiating a \(C^1\) cubic twice lands exactly in discontinuous piecewise-linear data;
2. **any** such PL candidate can be integrated back to a \(C^1\) cubic after fixing two vector integration constants;
3. PL singularity type carries exact information about minimal cubic knot multiplicity.

Therefore simplification in the \(C''\) domain is not merely a heuristic proxy for knot simplification.

### What this does not solve

It says nothing yet about whether closeness of \(q\) implies useful geometric closeness of curves. Bad parametrization remains untouched. The affine kernel must be fixed. The correct error metric remains the central unresolved question.

### New issue exposed by the proof

The choice of reconstruction gauge may itself become part of the theory:

- preserve position and tangent at one endpoint;
- preserve both endpoints;
- or, in settings where endpoints need not be fixed, optimize the affine correction after approximating \(q\).

The third option could tighten error substantially but is not pursued yet because endpoint preservation is usually natural in CAD/B-Rep settings.

## 7. Decision

**Keep the D2 route.** Session 0002 found no structural failure in the reduction. On the contrary, the exact weighted-complexity correspondence strengthens the motivation.

Next session should not expand scope. Use the CAD-relevant two-endpoint gauge and derive the corresponding Green kernel / induced synchronized positional error. Review its exactness and sharp operator constants before touching reparametrization.
