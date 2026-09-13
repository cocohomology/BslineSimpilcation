# Current State — User-Facing Summary

## Scope

The research still targets regular \(C^1\), cubic, non-rational spline curves. The structural reduction remains
\[
C\xrightarrow{D^2}q=C'',
\]
with \(q\) piecewise linear and possibly discontinuous at double knots.

The long-term objective is unchanged: simplify representation complexity under a geometric tolerance, using a structure tighter than global \(L^p\) surrogates but cheaper and more controllable than a full Hausdorff optimization.

---

## Stable foundation

### 1. Complexity is exact in the \(C''\) domain

For \(C^1\) piecewise cubics,
\[
D^2:S_3^1\to PL_{\rm disc}
\]
is onto with affine kernel. Jumps and continuous kinks of \(C''\) encode double and simple cubic knots, so fixed-degree representation complexity is carried exactly by the second derivative.

### 2. Fixed-endpoint synchronized error is exact and cheap

With
\[
E=C-\widetilde C,
\qquad e=C''-\widetilde C'',
\qquad E(a)=E(b)=0,
\]
we have
\[
E=G_De.
\]
The synchronized max error \(\|E\|_\infty\) is a rigorous Hausdorff upper bound and, for cubic splines, is directly certifiable by fixed-degree one-variable calculations or Bézier subdivision.

### 3. First-order tangent/normal analysis remains useful

Tangential synchronized displacement is the linearized reparameterization direction; normal displacement is the first-order geometric residual. The earlier tangential correction is now understood as the first Newton/implicit-function step toward the full nonlinear normal correspondence.

The earlier global-curvature upper bound remains mathematically valid but is not treated as a final engineering metric because remote curvature can make it arbitrarily conservative.

---

## Latest result — a cheap local admissibility certificate

Following the lesson from Degen, the project now asks for a good geometric correspondence before defining the final deviation norm.

For a candidate point \(\widetilde C(t)\), define
\[
F(t,u)=(\widetilde C(t)-C(u))\cdot C'(u).
\]
A normal correspondence is a root branch
\[
F(t,\sigma(t))=0.
\]

Take one candidate cubic span \(T=[t_0,t_1]\) and a nearby reference interval \(U=[u_0,u_1]\). If the following signs hold everywhere:
\[
F(t,u_0)>0,
\qquad
F(t,u_1)<0,
\qquad
F_u(t,u)<0,
\]
then for every \(t\in T\) there is exactly one normal root
\[
\sigma(t)\in U.
\]
That root is also the unique local minimizer of the squared distance from \(\widetilde C(t)\) to the reference segment inside \(U\).

If additionally
\[
F_t(t,u)=\widetilde C'(t)\cdot C'(u)>0
\]
throughout the box, then
\[
\sigma'(t)>0,
\]
so the certified branch is orientation preserving.

For cubic spans these tests involve only fixed-degree polynomials:
\[
\deg F\le(3,5),
\qquad
\deg F_u\le(3,4),
\qquad
\deg F_t\le(2,2).
\]
Therefore tensor-product Bernstein sign tests and local subdivision can certify the branch without enumerating all quintic normal roots or solving a global nearest-point problem.

---

## Green error now has a concrete geometric role

The synchronized Green error provides a predictor for where the desired normal root should lie.

Let
\[
B=E\cdot C',
\qquad S=\|C'\|^2.
\]
The first-order predictor is
\[
\sigma_0(t)=t-\frac{B}{S}.
\]
A slightly sharper exact one-step Newton predictor at the synchronized point is
\[
\boxed{
\sigma_N(t)=t-\frac{B}{S+E\cdot C''}.
}
\]

These predictors are not proofs; they are used only to choose a narrow reference window \(U\), after which the polynomial sign tests provide the certification.

---

## Why this remains connected to the original CAD problem

The normal-branch theory is not being developed as a universal differential-geometric theory.

The intended use is a fast path for the ordinary simplification regime:

1. a simplified candidate is expected to stay close to the original;
2. Green gives a cheap synchronized displacement and branch predictor;
3. a narrow local normal branch is certified by fixed-degree sign tests;
4. if the test fails, the method falls back to synchronized error, subdivision, or a more general verifier.

Failure of the certificate is therefore not failure of the approximation.

This avoids forcing rare self-approach or pathological cases into an increasingly elaborate theory.

---

## Current gate — theory should pause for a small code experiment

At this point the main unknown is no longer whether a sufficient theorem can be written. It is whether the simple certificate is **practically permissive**.

The next task is a small numerical feasibility test on representative close cubic pairs:
- mild normal perturbations;
- mild tangential reparameterization;
- nonuniform speed and knot spans;
- moderate curvature;
- one near-self-approach case as a negative control.

The experiment should record how often the Bernstein sign tests certify the local branch with zero or few subdivisions.

If ordinary close cases pass easily, the nonlinear normal layer is worth developing further. If they routinely fail, the project should stop strengthening the theory and prefer synchronized Green error plus occasional general geometric verification.

So this session reaches **CODE TEST NEEDED: yes**, but only a pseudocode-level experiment plan is required at this stage. No TeX stage note yet.
