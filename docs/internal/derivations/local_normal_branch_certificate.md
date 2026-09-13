# Local Normal-Branch Certification on Cubic Span Boxes

Session 0009.

## 1. Narrow question

The nonlinear normal correspondence from Session 0008 is defined by
\[
F(t,u):=(\widetilde C(t)-C(u))\cdot C'(u)=0.
\]
The practical question is not whether a normal root exists somewhere, but whether a **nearby, unique, orientation-preserving branch** can be certified cheaply in the close-curve regime expected during spline simplification.

The present session deliberately avoids global reach theory. It seeks only a sufficient local fast-path certificate.

## 2. Degen lesson used here

Degen does not define a normal-distance norm on arbitrary nearby curves. He first restricts to admissible curves: points lie in the normal field, each reference point has exactly one corresponding candidate point, paired tangents are transverse to the reference normal, and endpoints agree. The implicit function theorem then produces differentiable correspondence/deviation functions. The norm comes afterwards.

Our goal is to replace those qualitative admissibility requirements by directly checkable polynomial sign conditions for cubic span pairs.

## 3. Span-box setting

Let a candidate cubic span be parameterized on
\[
T=[t_0,t_1]
\]
and a nearby reference cubic span (or small union represented piecewise) on
\[
U=[u_0,u_1].
\]
On a single cubic-cubic box define
\[
F(t,u)=(\widetilde C(t)-C(u))\cdot C'(u).
\]
Also define the squared point-to-reference distance
\[
\Phi(t,u)=\|\widetilde C(t)-C(u)\|^2.
\]
Then
\[
\Phi_u=-2F.
\]

For cubic spans,
\[
\deg_{(t,u)}F\le(3,5),
\]
\[
\deg_{(t,u)}F_u\le(3,4),
\]
and
\[
F_t(t,u)=\widetilde C'(t)\cdot C'(u),
\qquad
\deg_{(t,u)}F_t\le(2,2).
\]
The boundary functions \(F(t,u_0)\) and \(F(t,u_1)\) have degree at most three in \(t\).

## 4. Local box certificate

### Proposition

Assume on the rectangle \(T\times U\):

\[
\boxed{F(t,u_0)>0\quad\text{for all }t\in T,}
\]
\[
\boxed{F(t,u_1)<0\quad\text{for all }t\in T,}
\]
\[
\boxed{F_u(t,u)<0\quad\text{for all }(t,u)\in T\times U.}
\]

Then for every \(t\in T\) there exists exactly one
\[
\sigma(t)\in(u_0,u_1)
\]
such that
\[
F(t,\sigma(t))=0.
\]
Moreover, \(\sigma\) is continuously differentiable in the interior of \(T\), and \(u=\sigma(t)\) is the unique minimizer of \(\Phi(t,u)\) over \(U\).

If in addition
\[
\boxed{F_t(t,u)>0\quad\text{on }T\times U,}
\]
then
\[
\boxed{\sigma'(t)>0.}
\]
Thus the certified local branch is orientation preserving.

### Proof

For fixed \(t\), the two boundary signs and the intermediate value theorem give at least one root. Since \(F_u<0\), the function \(u\mapsto F(t,u)\) is strictly decreasing, hence the root is unique.

Because \(F_u\neq0\) at the root, the implicit function theorem gives local differentiability and
\[
\sigma'(t)=-\frac{F_t(t,\sigma(t))}{F_u(t,\sigma(t))}.
\]
Therefore \(F_t>0\) together with \(F_u<0\) yields \(\sigma'>0\).

Finally, \(\Phi_u=-2F\). Before the root, \(F>0\) and \(\Phi_u<0\); after the root, \(F<0\) and \(\Phi_u>0\). Hence the root is the unique minimum of the squared distance over the local reference window \(U\).

## 5. Relation to the geometric nondegeneracy condition

At a root, with
\[
r=\widetilde C(t)-C(u),
\]
we have
\[
F_u=-\|C'(u)\|^2+r\cdot C''(u).
\]
Thus the box condition \(F_u<0\) is exactly
\[
\|C'(u)\|^2-r\cdot C''(u)>0,
\]
the same local nondegeneracy quantity identified in Session 0008. In arc length it is
\[
1-r\cdot\kappa_{\rm vec}>0.
\]
So the polynomial box test is not an unrelated numerical trick; it is a direct computational realization of the normal-coordinate regularity behind Degen's admissibility analysis.

## 6. Why this is computationally plausible

The certificate requires only sign decisions for fixed-degree polynomials:

- two cubic boundary polynomials in \(t\);
- one bivariate polynomial \(F_u\) of bidegree at most \((3,4)\);
- optionally one bivariate polynomial \(F_t\) of bidegree at most \((2,2)\).

A tensor-product Bernstein representation on \(T\times U\) gives an immediate sufficient sign certificate when all coefficients have the same strict sign. If the certificate is inconclusive, the box can be subdivided. Because the degrees are fixed, this is structurally very different from a generic two-parameter Hausdorff optimization: the task is local sign certification, not minimization over all curve pairs.

No claim is made about worst-case bit complexity. Near degeneracy or self-approach may cause repeated subdivision or failure of the fast path.

## 7. Green predictor and box construction

The synchronized Green error provides a natural center for the local reference window.

With
\[
E=C-\widetilde C,\qquad
B=E\cdot C',\qquad S=\|C'\|^2,
\]
the first-order predictor is
\[
\sigma_0(t)=t-\frac{B}{S}.
\]

There is also a slightly sharper one-step Newton predictor. At \(u=t\),
\[
F(t,t)=-B,
\]
and
\[
F_u(t,t)=-(S+E\cdot C'').
\]
Hence, when the denominator is positive,
\[
\boxed{
\sigma_N(t)=t-\frac{B}{S+E\cdot C''}.
}
\]
The older predictor is its first-order version.

A practical box construction can therefore be:

1. on a candidate span \(T\), bound the range of \(\sigma_0\) or \(\sigma_N\);
2. enlarge that range by a safety margin to form \(U\);
3. test the four sign conditions above;
4. subdivide \(T\) or enlarge/split \(U\) only if the test is inconclusive.

The predictor is not used as proof; it only keeps the certification box local.

## 8. What this certificate does and does not guarantee

If the test passes, each candidate point has one and only one local normal foot inside \(U\), and that foot is the unique local distance minimizer inside the window. With \(F_t>0\), the local branch is order preserving.

The test does **not** prove that no remote part of the entire reference curve is even closer. Therefore it is sufficient for constructing a stable local correspondence and a certified geometric upper bound, but exact equality with global Hausdorff distance still needs either remote exclusion or a genuine non-overlapping normal neighbourhood.

This distinction is intentional. The present project does not need to solve global self-approach geometry merely to simplify ordinary close CAD curves.

## 9. Reality review

This session addresses a concrete engineering question: after a candidate simplified cubic is produced and is already expected to be close, can we certify the intended local correspondence without enumerating all normal roots?

The answer is plausibly yes in the ordinary close-curve regime. The certificate is local, fixed-degree, and naturally initialized by quantities already available from the Green layer.

Equally important, failure of the certificate is **not** failure of the approximation. It should trigger a fallback:

- use the exact synchronized Green bound if it already meets tolerance;
- subdivide/refine the local box;
- or invoke a more general geometric verifier only for the ambiguous region.

Thus this branch is best viewed as a fast admissibility layer, not as a universal normal-bundle theory.

## 10. Current uncertainty

The main unknown is now empirical rather than purely formal:

> On ordinary close cubic pairs arising from simplification, how often do these simple Bernstein sign tests pass without excessive subdivision?

If the answer is “usually,” the normal-correspondence route has a credible engineering role. If the answer is “rarely,” proving stronger sufficient theorems would risk exactly the abstraction drift the project wants to avoid.

Therefore the next gate should be a small numerical feasibility test, with pseudocode only at this stage.
