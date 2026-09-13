# Green Functions and Green Kernels — Minimal Background for This Project

This note is only a compact refresher. It is not part of the active research argument, but future self-contained TeX notes should include enough of this material that the reader does not need prior familiarity with Green-function language.

## 1. The basic idea

Consider a linear differential boundary-value problem
\[
Lu=f,
\]
together with boundary conditions such as
\[
B_1u=0,\qquad B_2u=0.
\]
If the problem is well posed, one may often represent its solution as
\[
u(t)=\int G(t,s)f(s)\,ds.
\]
The function \(G(t,s)\) is called the **Green function** for the differential operator together with the chosen boundary conditions.

Equivalently, \(G\) is the integral **kernel** of the inverse operator. In this project the terms “Green function” and “Green kernel” refer to the same two-variable object, while “Green operator” refers to the linear map
\[
(Gf)(t)=\int G(t,s)f(s)\,ds.
\]

The boundary conditions are part of the definition. The same differential operator with different boundary conditions has a different Green function.

## 2. Response-to-a-point-source interpretation

Formally, for fixed \(s\), the Green function satisfies
\[
L_tG(t,s)=\delta(t-s),
\]
where \(\delta\) is the Dirac delta distribution, together with the required boundary conditions in the \(t\)-variable.

Thus \(G(\cdot,s)\) is the response of the system to a unit point source placed at \(s\). A general forcing \(f(s)\) is then obtained by superposing these point responses through integration.

## 3. Our specific operator

The spline-error problem currently uses
\[
E''=e,
\qquad E(a)=E(b)=0.
\]
So the operator is
\[
L=D^2.
\]
For fixed \(s\), away from \(t=s\),
\[
G_{tt}(t,s)=0,
\]
so \(G\) must be linear in \(t\) on each side of \(s\).

The conditions are:

1. \(G(a,s)=0\);
2. \(G(b,s)=0\);
3. \(G\) is continuous at \(t=s\);
4. integrating \(G_{tt}=\delta_s\) across \(s\) gives the slope jump
   \[
   G_t(s^+,s)-G_t(s^-,s)=1.
   \]

Solving these four elementary conditions gives
\[
\boxed{
G(t,s)=
-\frac{(\min\{t,s\}-a)(b-\max\{t,s\})}{b-a}.
}
\]

Because this project uses \(D^2\), the kernel is negative in the interior. Many PDE texts instead define the positive Dirichlet Green function for \(-D^2\); that convention differs by a sign. This sign convention should always be checked rather than memorized.

## 4. Why the representation works

If
\[
E(t)=\int_a^bG(t,s)e(s)\,ds,
\]
then differentiation in \(t\) gives, in the distributional/classical-a.e. sense,
\[
E''(t)=\int_a^b\delta(t-s)e(s)\,ds=e(t).
\]
The endpoint conditions follow directly from \(G(a,s)=G(b,s)=0\).

For the piecewise-linear \(e\) used in this project, no distributional subtlety is needed in practice: \(E\) is simply a \(C^1\) piecewise-cubic function satisfying the equation on every open span.

## 5. Why Green language is useful here

The direct differential statement
\[
E''=e
\]
says that second-derivative error accumulates twice into position error.

The Green representation says more explicitly **how error at parameter location \(s\) influences position at parameter location \(t\)**:
\[
E(t)=\int K_D(t,s)e(s)\,ds.
\]
For fixed \(t\), the weight \(-K_D(t,s)\) is a positive tent-shaped piecewise-linear function of \(s\). This exposes:

- the location dependence of second-derivative error;
- sign/vector cancellation before taking a norm;
- the global correction imposed by fixing both endpoints.

That is why the Green operator is more informative for this project than immediately replacing \(e\) by one global \(L^p\) number.

## 6. Terminology to preserve in future notes

A future full TeX note should introduce these terms explicitly:

- **differential operator**: here \(D^2\);
- **boundary-value problem**: differential equation plus boundary conditions;
- **Green function / Green kernel**: the two-variable kernel \(G(t,s)\);
- **Green operator**: the inverse integral operator \(f\mapsto\int G(\cdot,s)f(s)\,ds\);
- **Dirichlet boundary condition**: prescribed endpoint values, here homogeneous for the error;
- **point-source interpretation** via the Dirac delta;
- sign convention difference between \(D^2\) and \(-D^2\).

The project should not assume the reader remembers this theory when a stage-level TeX note is eventually written.
