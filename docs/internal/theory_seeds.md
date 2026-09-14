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

## 4. Symmetric geometry-aware certification — REOPENED IN SESSION 0016

This seed is no longer parked.

Session 0016 proved that a pure Hausdorff verifier does not require a single globally stitched normal branch. A local directed cover gives one directed Hausdorff upper bound; a second local cover with the curves swapped gives the other direction. Thus

\[
\text{forward local cover}
+
\text{reverse local cover}
\Longrightarrow
\text{symmetric Hausdorff upper bound}.
\]

A stronger single-family alternative is to certify that forward branch images cover the full target parameter interval.

The important simplification is that the orientation condition \(F_t>0\) is optional in the two-pass Hausdorff architecture. It remains relevant only for target-coverage bookkeeping or an ordered/Fréchet interpretation.

Active documents:
- `docs/internal/derivations/local_cover_hausdorff_certificate.md`
- `docs/internal/experiments/two_sided_hausdorff_certificate_test_plan.md`

Do not reopen this as a separate theory branch unless the new two-sided experiment exposes a concrete asymmetry or failure.

---

## 5. Reach / tubular-neighbourhood theory

A true non-overlapping normal tube gives unique nearest projection and turns the normal deviation max into exact Hausdorff distance.

Session 0015 additionally showed why reach is conceptually important even when we do not compute it: Hausdorff distance alone cannot control tangent directions, while reach/local feature size supplies the geometric regularity scale coupling curvature and self-approach.

Why it may matter: supplies a clean theoretical regime in which normal projection is exact and explains the square-root scale of Hausdorff-to-tangent stability.

Why it is parked: computing or certifying global reach for general CAD curves may be as hard as the geometric problem we are trying to avoid, especially near self-approach.

**Reopen if:** empirical data indicate that a simple conservative lower bound on local feature size is already available from CAD context, or if branch ambiguity becomes the primary obstacle after the fast-path experiment.

Before the final TeX note, independently verify the precise reach/manifold-reconstruction references and constants used in the motivation discussion.

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

This remains a probable future main line.

**Reopen if:** the geometry-aware verifier reaches a stable local-to-global decision (successful or deliberately abandoned), so candidate generation can become the main problem without leaving an unfinished verification gap.

---

## 8. Direct optimization under the Green operator

Rather than approximate q in Lp and then estimate position error, one could formulate candidate selection through

\[
\|G_D(q-\widetilde q)\|_\infty
\]

or a localized geometry-aware variant.

Session 0014 clarified an important limitation: under the fixed endpoint reconstruction map, this quantity is exactly the synchronized positional \(L^\infty\) error pulled back to q-space. Therefore “Green metric” alone is not a new approximation objective; its value must come from computational structure exposed by q-space, not from renaming the positional norm.

Why it may matter: q-space may expose locality, moments, sparse break structure, or useful optimization variables even though the norm itself is only a pullback.

**Reopen if:** candidate generation begins and a concrete q-space structure makes the optimization simpler than direct cubic approximation.

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

## 11. Moment-localized q-block replacement / cubic Hermite coarsening

Session 0014 re-analysis exposed a concrete q-space locality mechanism.

On an interval \(I=[\alpha,\beta]\), let \(q=C''\). Choose the unique affine function \(\ell\) such that
\[
\int_\alpha^\beta(q-\ell)(s)\,ds=0,
\]
\[
\int_\alpha^\beta(\beta-s)(q-\ell)(s)\,ds=0.
\]

If \(\widetilde C''=\ell\) on the block and \(\widetilde C(\alpha)=C(\alpha)\), \(\widetilde C'(\alpha)=C'(\alpha)\), these two moment conditions force
\[
\widetilde C(\beta)=C(\beta),
\qquad
\widetilde C'(\beta)=C'(\beta).
\]
Thus \(\widetilde C\) is exactly the standard cubic Hermite interpolant of \(C\) on the block, and the position/tangent error does not propagate outside the block if q is unchanged elsewhere.

Potential consequence: if retained breakpoints are restricted to an ordered candidate set, an edge \(i\to j\) could represent replacing all intervening q-knots by one Hermite cubic block. Feasible edges could then support a shortest-path / block-deletion architecture, naturally allowing several knots to disappear together rather than through single-knot greedy removal.

Why it may matter: this is one of the first q-space observations that creates genuine locality rather than merely re-expressing synchronized error.

Why it is parked:
- it pins the original position and derivative at every retained breakpoint;
- joins are generically only C1, hence double cubic knots;
- standard Hermite interpolation is parameterization dependent;
- it may be much more restrictive than the true best low-complexity approximant.

**Reopen if:** Phase 4 finishes and candidate generation becomes active. Test it first as a globally optimizable restricted baseline, not as the presumed final algorithm.

---

## 12. Reminder to future work

These entries are **not a queue**. They are memory anchors.

When the main line stalls, revisit them by asking:

> Does one of these parked structures now address the actual obstacle we have observed, rather than an obstacle we merely know can exist?

If not, leave it parked.
