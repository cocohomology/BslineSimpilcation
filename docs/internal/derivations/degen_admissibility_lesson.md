# Degen Revisited: Admissibility Before the Norm

Session 0008.

## 1. Purpose

Session 0007 showed that the first geometry-aware bound
\[
d_H\le N_{G,\perp}+\frac K2N_{G,\parallel}^2
\]
is valid but can be arbitrarily conservative because curvature was globalized independently of where tangential error occurs.

This session does not import Degen's 1992 normal distance as a ready-made replacement. It asks instead:

> What is the structural method behind Degen's definition, and what should we inherit from that method?

The main lesson is: **admissibility first, norm second**.

## 2. Structural order in Degen

For a fixed planar reference curve \(C\), Degen first constructs a normal field and restricts candidates to an admissible class. For an admissible candidate there are functions \(\sigma\) and \(\rho\) such that
\[
y(\sigma(t))=x(t)+\rho(t)n(t).
\]
His conditions enforce that candidate points remain in a regular part of the normal field, each reference point has exactly one corresponding candidate point, the candidate tangent is transverse to the reference normal, and endpoints agree. The condition \(\rho\kappa<1\) keeps the normal coordinates nondegenerate. The implicit function theorem then gives differentiable \(\sigma,\rho\), and \(\sigma\) is orientation preserving.

Only after this geometric coordinate chart is established does Degen define
\[
d_N(C,C')=\|\rho\|_\infty.
\]
He proves \(d_H\le d_N\), and equality under a non-overlap condition on the normal field.

The methodological chain is therefore
\[
\boxed{
\text{geometric neighbourhood}
\to\text{admissible class}
\to\text{unique correspondence}
\to\text{deviation field}
\to\text{norm}
\to\text{relation to Hausdorff}.
}
\]

This is more subtle than choosing a norm directly on synchronized parameter error.

## 3. Consequence for our project

Our first geometry-aware attempt proceeded in the reverse order: obtain the exact synchronized Green error, project tangent/normal components, then compensate the missing nonlinear geometry by a global curvature bound. The first attack showed exactly where this loses information.

The more promising target is therefore:

> construct the correct local geometric correspondence first; measure its deviation only afterwards.

The \(D^2\)/Green machinery can remain central, but its role may shift from “final metric” to predictor, initializer, early bound, and admissibility certificate.

## 4. Space-curve normal deviation

Let
\[
C,\widetilde C:[a,b]\to\mathbb R^d
\]
be regular \(C^1\), piecewise-cubic curves with common endpoints. Seek a correspondence \(u=\sigma(t)\) such that
\[
R(t):=\widetilde C(t)-C(\sigma(t))
\]
satisfies
\[
\boxed{R(t)\cdot C'(\sigma(t))=0.}
\]
If \(\sigma\) is an orientation-preserving homeomorphism and \(\tau=\sigma^{-1}\), rewrite the candidate as
\[
\widetilde C(\tau(u))=C(u)+r(u),
\qquad r(u)\perp C'(u).
\]
In \(\mathbb R^3\), \(r\) is a vector in the normal plane, not a signed scalar as in the planar Degen setting.

A natural nonlinear deviation quantity is
\[
N_{\perp}^{\rm nl}(C,\widetilde C):=\|r\|_\infty.
\]
This is not yet declared to be the final metric; its meaning depends on whether the normal graph is uniquely defined.

## 5. Normal equation and local uniqueness

Define
\[
F(t,u):=(\widetilde C(t)-C(u))\cdot C'(u).
\]
A normal correspondence is a root branch
\[
F(t,\sigma(t))=0.
\]
For fixed \(t\), if \(C\) is cubic on the relevant span, then
\[
\boxed{F(t,u)\text{ has degree at most }5\text{ in }u.}
\]

Differentiate in \(u\):
\[
F_u(t,u)
=-\|C'(u)\|^2+(\widetilde C(t)-C(u))\cdot C''(u).
\]
At a normal root let \(r=\widetilde C(t)-C(u)\). A sufficient nondegeneracy condition is
\[
\boxed{
D(u,r):=\|C'(u)\|^2-r\cdot C''(u)>0.
}
\]
Then the implicit function theorem gives a unique local branch \(u=\sigma(t)\).

In reference arc length this becomes
\[
D=1-r\cdot\kappa_{\rm vec},
\]
so a simple sufficient condition is
\[
\|r\|\kappa<1.
\]
This is the space-curve analogue of the curvature-radius condition in Degen's normal field.

## 6. Orientation formula

Implicit differentiation gives
\[
\boxed{
\sigma'(t)=
\frac{\widetilde C'(t)\cdot C'(\sigma(t))}
{\|C'(\sigma(t))\|^2-r(t)\cdot C''(\sigma(t))}.
}
\]
Thus local orientation preservation separates into two conditions:

1. the normal coordinates are nondegenerate (positive denominator);
2. the paired tangents have positive inner product.

This is cleaner than hiding both effects inside a single global norm inequality.

## 7. Previous first-order theory = linearization of the nonlinear normal equation

Recall the canonical synchronized error
\[
E=C-\widetilde C.
\]
At \(u=t\),
\[
F(t,t)=-E(t)\cdot C'(t).
\]
To first order, \(F_u(t,t)\approx-\|C'(t)\|^2\). One Newton/IFT correction from the synchronized guess \(u=t\) therefore gives
\[
\boxed{
\sigma(t)-t\approx
-\frac{E(t)\cdot C'(t)}{\|C'(t)\|^2}.
}
\]
Writing \(B=E\cdot C'\) and \(S=\|C'\|^2\), this is \(-B/S\). In reference arc length it is exactly the Session-0005 shift \(-E\cdot T\).

This is a major synthesis: the first-order tangential quotient was not a separate trick. It is the **first Newton/implicit-function linearization of the full nonlinear normal projection**. Its successes and its curved-reparameterization limitation now have the same explanation.

## 8. Exact Hausdorff distance on an admissible normal graph

Assume the candidate is a normal graph over the reference,
\[
\widetilde C(\tau(u))=C(u)+r(u),
\qquad r(u)\perp C'(u),
\]
with common endpoints. Assume additionally that each \(C(u)\) is the unique nearest point on the reference to the matched candidate point. This is the situation inside a sufficiently small non-overlapping tubular neighbourhood (endpoint details treated by the shared-endpoint condition).

Then
\[
\operatorname{dist}(C(u)+r(u),C)=\|r(u)\|,
\]
so
\[
h(\widetilde C,C)=\|r\|_\infty.
\]
The explicit pairing also gives
\[
h(C,\widetilde C)\le\|r\|_\infty.
\]
Hence
\[
\boxed{d_H(C,\widetilde C)=\|r\|_\infty.}
\]

Thus, on a true one-to-one normal-graph neighbourhood, the deviation norm is not merely a bound: it is the Hausdorff distance. The crucial issue is the admissibility class, not the choice of \(L^\infty\) after the class has been built.

## 9. Role of the Green layer after this revision

The nonlinear normal deviation does not replace the \(D^2\)/Green theory.

- **Representation layer:** \(C''\) still encodes cubic complexity exactly.
- **Synchronized layer:** \(E=G_De\) gives an exact and cheap displacement field.
- **Geometric layer:** use \(E\) to predict and certify the nearby normal branch.

The first predictor is
\[
\sigma_0(t)=t-\frac{E\cdot C'}{\|C'\|^2}.
\]
The Green layer can potentially provide early rejection/acceptance bounds, a small interval containing the desired root, and sufficient admissibility conditions—without globally searching all normal roots.

## 10. Why this is not simply "use Degen"

Our problem differs essentially from Degen's 1992 setting:

- cubic simplification is represented in the \(C''\) PL domain;
- space-curve normal deviation is vector-valued;
- knot structure will eventually change, so the approximation family is not one fixed finite-dimensional Bézier manifold;
- our priority is certified branch construction and complexity reduction, not a Chebyshev alternation theorem;
- the Green error provides a special predictor/certificate absent from Degen's framework.

What we should inherit is the architecture: **build a geometric coordinate chart first, then define and optimize the deviation inside that chart.**

## 11. Remaining difficulty

For each fixed \(t\), the normal equation is only quintic in \(u\), but this alone does not make the full problem cheap:

- several real normal roots may coexist;
- the correct branch must be selected continuously;
- branch switching can occur near small reach / self-approach;
- maximizing \(\|r(t)\|\) along an implicitly defined branch may lead to a coupled algebraic system.

Therefore no claim is made yet that nonlinear normal distance is as cheap as the synchronized Green metric.

## 12. Next target

The next narrow question is:

> Can the existing Green/synchronized quantities give a cheap **sufficient admissibility certificate** for one nearby normal branch, so that we do not solve a global nearest-point problem?

Candidate ingredients:
- certified regularity / speed lower bound;
- a local tube or curvature-separation bound;
- a root interval around the predictor \(t-B/S\);
- tangent-angle positivity for \(\sigma'>0\);
- interval-Newton or monotone-root arguments on local spans.

Do not yet optimize \(\|r\|_\infty\) or design the full simplification algorithm.
