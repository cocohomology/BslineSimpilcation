# Theory Seeds — Parked Connections and Reopen Conditions

Purpose: preserve mathematically suggestive branches without allowing them to silently become the main project. A seed belongs here when it may matter later but does not currently justify spending the next session on it.

The rule is simple: every seed must include a **reopen condition** tied to the spline-simplification objective.

## 1. Localized curvature remainder

The first-order tangential quotient produced a remainder controlled schematically by curvature along the arc actually traversed by the parameter shift. Replacing that local information by one global curvature supremum created the Session-0007 counterexample.

Potential direction:

\[
R(s)=\int_0^{\delta(s)}\bigl(T(s+r)-T(s)\bigr)\,dr,
\]

with a localized integral/envelope involving \(\kappa\) only along the shifted arc.

Why it may matter: could retain most of the first-order theory while avoiding nonlinear normal-branch construction.

Why it is parked: moving arc-length intervals may require inversion/envelopes that destroy the clean native-parameter algebra.

**Reopen if:** the local normal-branch certificate is empirically too restrictive, but the first-order normal/tangential decomposition still appears useful on real data.

---

## 2. Green quotient / shape-space interpretation

The synchronized error is

\[
E=G_De.
\]

The tangent direction is the infinitesimal action of reparameterization, while the normal component is the first-order geometric residual. This resembles taking a quotient of positional perturbations by the tangent space of the reparameterization group.

Potential mathematical languages:
- quotient seminorms;
- shape spaces;
- gauge fixing;
- horizontal/vertical decomposition relative to reparameterization.

Why it may matter: could reveal a principled error functional in q=C'' space rather than a sequence of ad hoc corrections.

Why it is parked: a beautiful quotient theory is useless if it does not yield a tighter or easier simplification criterion.

**Reopen if:** candidate optimization in q-space lacks a natural objective, or if several seemingly different geometry-aware corrections need a common explanation.

---

## 3. Optimized affine reconstruction

Since

\[
\ker D^2=\mathcal P_1,
\]

a second-derivative approximation determines the curve only up to an affine vector function.

The current gauge fixes both endpoints. Another possibility is to choose the affine correction optimally after q_tilde is selected, for example minimizing synchronized or geometric max error.

Why it may matter: free-standing CAD curves or intermediate construction curves may not require exact endpoint preservation, and optimized affine reconstruction could substantially reduce error at negligible complexity cost.

Why it is parked: B-Rep edges often make endpoints topologically meaningful; relaxing them prematurely changes the application semantics.

**Reopen if:** target cases include unconstrained/free curves, or endpoint fixing is empirically identified as a dominant source of failed simplification.

---

## 4. Symmetric geometry-aware certification

Current normal projection is reference-biased: candidate points project to the original curve.

Potential direction: combine normal graphs in both directions, or use a symmetric deviation that remains cheap when curves are close.

Why it may matter: may tighten one-sided conservatism and better approximate Hausdorff symmetry.

Why it is parked: symmetry can double the machinery without changing the main candidate-generation problem.

**Reopen if:** one-sided certification passes often but is demonstrably much looser than the actual symmetric geometric error.

---

## 5. Reach / tubular-neighbourhood theory

A true non-overlapping normal tube gives unique nearest projection and turns the normal deviation max into exact Hausdorff distance.

Why it may matter: supplies a clean theoretical regime in which the nonlinear normal metric is exact.

Why it is parked: computing or certifying global reach for general CAD curves may be as hard as the geometric problem we are trying to avoid, especially near self-approach.

**Reopen if:** empirical data indicate that a simple conservative lower bound on local feature size is already available from CAD context, or if branch ambiguity becomes the primary obstacle after the fast-path experiment.

---

## 6. Distributional second derivatives for lower continuity

Below C1, classical C'' no longer captures all break information. Distributionally:

- a jump in C' contributes a delta term;
- a jump in C contributes a derivative-of-delta term.

This suggests a generalized second-derivative representation consisting of PL density plus atomic singular parts.

Why it may matter: could extend the exact complexity dictionary beyond C1 and unify knot multiplicity / discontinuity in one object.

Why it is parked: it enlarges the mathematical model before the cubic C1 case has demonstrated engineering value.

**Reopen if:** the C1 method proves useful and real target data frequently contain lower-continuity spline joins that cannot simply be split into separate curves.

---

## 7. Nonlinear PL / free-breakpoint approximation in q-space

Once error certification is sufficiently settled, the main simplification problem becomes:

> approximate a complicated vector PL function q by a much lower-complexity PL function q_tilde, where continuous kinks cost 1 and jumps cost 2, under an error constraint induced after double integration.

Connections may include:
- free-knot spline approximation;
- segmented regression;
- polyline simplification;
- dynamic programming;
- sparse change-point models;
- nonlinear approximation / n-term approximation.

This is likely not merely a parked curiosity; it is a probable future main line.

**Reopen if:** the current feasibility test validates at least one usable certification architecture, so the project can safely shift attention from error measurement to candidate generation.

---

## 8. Direct optimization under the Green operator

Rather than approximate q in Lp and then estimate position error, one could formulate candidate selection directly through

\[
\|G_D(q-\widetilde q)\|_\infty
\]

or a localized geometry-aware variant.

Why it may matter: this preserves cancellation and location information and may produce very different optimal breakpoints from ordinary PL approximation norms.

Why it is parked: the optimization landscape and combinatorial structure are not yet understood; premature work here risks solving the wrong metric problem.

**Reopen if:** synchronized Green error becomes the accepted baseline objective after the geometric-certificate experiment, or if normal correspondence is relegated to final verification only.

---

## 9. Relationship to classical approximation theory

DeVore-style nonlinear approximation asks how best n-term / adaptive approximations behave as n grows. The q-space formulation may admit approximation-class questions: rates in terms of smoothness, variation, or curvature-like quantities of q.

Why it may matter: could explain when dramatic simplification is theoretically possible and characterize hard instances.

Why it is parked: asymptotic rates do not directly give a practical CAD algorithm or tolerance certificate.

**Reopen if:** a working algorithm exists and we need to understand its optimality, instance classes, or theoretical limits.

---

## 10. Higher-order generalization

For degree p and continuity C^{p-2}, taking p-1 derivatives reduces the spline to piecewise linear; more generally, differentiation lowers polynomial degree while translating knot multiplicity into continuity defects.

Why it may matter: the cubic C1 story may be one member of a broader derivative-domain simplification principle.

Why it is parked: higher-order derivatives amplify conditioning and the clean geometric interpretation of double integration is special enough that generalization may not preserve engineering value.

**Reopen if:** the cubic method works and high-degree CAD inputs need a principled reduction to cubic or directly to a higher-order derivative domain.

---

## 11. Reminder to future work

These entries are **not a queue**. They are memory anchors.

When the main line stalls, revisit them by asking:

> Does one of these parked structures now address the actual obstacle we have observed, rather than an obstacle we merely know can exist?

If not, leave it parked.
