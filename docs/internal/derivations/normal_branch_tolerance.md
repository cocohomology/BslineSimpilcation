# Certified Deviation on an Admissible Local Normal Branch

Session 0014.

## 1. Narrow question

Session 0009 established a local admissibility certificate for

\[
F(t,u):=(\widetilde C(t)-C(u))\cdot C'(u)=0
\]

on a cubic-cubic box \(T\times U\). The 2026-09-14 feasibility experiment then showed that this certificate is permissive on the structured close-curve families that were tested, while also confirming the intended failure mode near self-approach.

The experiment did **not** answer the next mathematical question:

> Once a unique orientation-preserving normal branch \(u=\sigma(t)\) is certified, how can the maximum deviation along that branch be certified without tracing the branch point by point?

This note answers that local question. It does not yet solve global branch stitching across the whole spline.

---

## 2. Setting

Let one candidate cubic span be

\[
P(t):=\widetilde C(t),\qquad t\in T=[t_0,t_1],
\]

and one reference cubic span be

\[
Q(u):=C(u),\qquad u\in U=[u_0,u_1].
\]

Define

\[
r(t,u)=P(t)-Q(u),
\]

\[
D(t,u)=\|r(t,u)\|^2,
\]

and

\[
F(t,u)=r(t,u)\cdot Q'(u).
\]

Assume the Session-0009 box certificate has succeeded, so for every \(t\in T\) there is exactly one root

\[
u=\sigma(t)\in U
\]

of \(F(t,u)=0\), and \(F_u\neq0\) along the branch. If the orientation test also succeeds, then \(\sigma'(t)>0\).

Define the squared branch deviation

\[
\psi(t)=D(t,\sigma(t))
=\|P(t)-Q(\sigma(t))\|^2.
\]

---

## 3. The key derivative identity

Because

\[
D_u(t,u)=-2F(t,u),
\]

we have

\[
D_u(t,\sigma(t))=0.
\]

Therefore the chain rule gives

\[
\begin{aligned}
\psi'(t)
&=D_t(t,\sigma(t))
 +D_u(t,\sigma(t))\sigma'(t)\\
&=D_t(t,\sigma(t)).
\end{aligned}
\]

Since

\[
D_t(t,u)=2r(t,u)\cdot P'(t),
\]

we obtain the exact identity

\[
\boxed{
\psi'(t)
=2\bigl(P(t)-Q(\sigma(t))\bigr)\cdot P'(t).
}
\]

Define

\[
G(t,u):=r(t,u)\cdot P'(t).
\]

Then every interior stationary point of the branch deviation satisfies

\[
\boxed{
F(t,u)=0,\qquad G(t,u)=0.
}
\]

Geometrically, the connecting vector is normal to **both** curve tangents. Thus extrema of the deviation along a certified normal branch occur at local common normals, plus interval boundaries.

This is the central structural result of the session.

---

## 4. Fixed polynomial degree for cubic spans

For cubic \(P\) and \(Q\):

\[
\deg_{(t,u)}F\le(3,5),
\]

because

\[
F=P(t)\cdot Q'(u)-Q(u)\cdot Q'(u),
\]

and

\[
\deg_{(t,u)}G\le(5,3),
\]

because

\[
G=P(t)\cdot P'(t)-Q(u)\cdot P'(t).
\]

Also

\[
\deg_{(t,u)}D\le(6,6).
\]

Hence the exact local maximum problem does not require continuous branch tracing. In the generic case it reduces to:

1. isolate the finitely many roots of \(F=G=0\) in the certified box;
2. keep those roots that lie on the certified branch (uniqueness of the \(F\)-root for each \(t\) makes this local selection simple);
3. evaluate/bound \(D\) at those roots and at the branch endpoints;
4. take the largest value.

The polynomial degrees are independent of the total number of knots in the input spline.

Tensor-product Bernstein subdivision, interval methods, or a resultant followed by univariate root isolation are all possible exact/certified implementations. No implementation choice is fixed yet.

---

## 5. A tolerance-only formulation

For a prescribed tolerance \(\varepsilon\), define

\[
H_\varepsilon(t,u)=D(t,u)-\varepsilon^2.
\]

On the connected branch, \(H_\varepsilon(t,\sigma(t))\) is continuous.

Therefore a sufficient tolerance certificate is:

- one known branch point has \(H_\varepsilon<0\), and
- there is no solution of
  \[
  F(t,u)=0,\qquad H_\varepsilon(t,u)=0
  \]
  on the branch inside the box.

Then

\[
\psi(t)<\varepsilon^2
\]

throughout the branch.

This threshold formulation is useful for a yes/no tolerance query, whereas the \(F=G=0\) formulation gives the actual extremum candidates. Which is cheaper in practice is not decided here.

---

## 6. A cheap first layer before solving stationary equations

Since the certified branch graph lies inside \(T\times U\),

\[
\max_{t\in T}\psi(t)
\le
\max_{(t,u)\in T\times U}D(t,u).
\]

The right side is conservative but \(D\) is a fixed-degree bivariate polynomial. A tensor-product Bernstein upper bound therefore gives an immediate sufficient test:

\[
\max_{T\times U}D\le\varepsilon^2
\quad\Longrightarrow\quad
\max_T\psi\le\varepsilon^2.
\]

This suggests a hierarchy:

1. **cheap box bound** on \(D\);
2. if inconclusive, subdivide/contract the certified box;
3. if still inconclusive, isolate common-normal stationary points \(F=G=0\);
4. only then use a more general geometric fallback.

The feasibility experiment showed that ordinary cases often admit narrow certified boxes, so the cheap first layer is worth testing later. That is an empirical question, not a theorem claim.

---

## 7. Degenerate stationary sets

The statement “the maximum occurs at finitely many solutions of \(F=G=0\)” is generic, not universal.

Special configurations can make \(G=0\) along a nontrivial portion of the already-certified branch. Then

\[
\psi'(t)=0
\]

there, so the deviation is constant on that branch component. Coincident curves and constant-offset configurations are examples of the kind of degeneracy that can cause a positive-dimensional stationary set.

An implementation must therefore not assume that the resultant of \(F\) and \(G\) is always nonzero. The degenerate case is mathematically benign—constant branch deviation—but requires a separate algebraic/interval handling path.

---

## 8. Piecewise splines and knot crossings

The formulas above apply on one cubic-cubic box. For \(C^1\) cubic splines, \(C''\) may jump at double knots, so \(F_u\) and \(\sigma'\) need only be handled one-sidedly there.

The correct construction is the same one already used by the feasibility experiment:

- split candidate parameter intervals at candidate knots;
- split reference windows at reference knots;
- apply the smooth-box argument on every cubic-cubic subbox;
- include branch points on subbox boundaries among the deviation candidates.

No differentiability across a double knot is assumed beyond the global \(C^1\) regularity of the curves.

---

## 9. What the local branch deviation certifies geometrically

A point that was easy to overstate before the experiment is the role of the word “nearest”.

For every candidate point \(P(t)\), the certified branch supplies one reference point \(Q(\sigma(t))\). Therefore

\[
\operatorname{dist}(P(t),\operatorname{Im}Q)
\le
\|P(t)-Q(\sigma(t))\|.
\]

Hence the branch deviation immediately gives a **one-sided directed Hausdorff upper bound** from the candidate to the reference, even if another remote part of the reference curve is closer.

This explains an observation in the feasibility feedback: some locally certified normal feet in near-self-approach examples were not the global nearest points. That does **not** invalidate their use as an upper-bound correspondence.

For a symmetric Hausdorff upper bound, one needs more:

- either a globally stitched branch that is a bijection/homeomorphism between the parameter intervals,
- or a separate certified correspondence in the reverse direction.

The Session-0009 local box theorem alone does not establish this global property. The feasibility report explicitly did not establish a whole-curve global correspondence theorem.

This is the next theoretical gap after the present local deviation result.

---

## 10. Relation to the 2026-09-14 feasibility experiment

The experiment established strong evidence for the **admissibility primitive** on its structured synthetic sample:

- ordinary close cases almost always certified at subdivision depth 0–2;
- failures concentrated in the deliberately difficult near-self-approach family;
- independent root checks and exact rational Bernstein-sign audits found no local certificate inconsistency;
- Newton prediction did not materially improve certification over the simpler first-order predictor.

It did **not** evaluate \(\max\psi\), did not impose a geometric tolerance on the implicit branch, and did not prove whole-curve branch stitching.

Therefore the present derivation is the logically correct next theory step. It uses the experiment to justify continuing the branch framework, but no numerical result is promoted to a theorem.

---

## 11. Goal alignment

This development remains connected to the original CAD simplification problem because it aims to make the geometry-aware verifier complete enough to serve as a bounded-cost acceptance test for already-close simplification candidates.

It is deliberately **not** a global nearest-point or reach theory.

The next session should study only global assembly of the local certificates:

> Under what checkable conditions do adjacent certified local branches stitch into a whole-curve monotone correspondence, and when is a reverse-direction certificate preferable?

Only after that question is understood should the project decide whether another code feasibility test is warranted or whether the verification layer is mature enough to return to candidate generation.
