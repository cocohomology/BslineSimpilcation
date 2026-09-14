# Local-Cover Hausdorff Certification from Certified Normal Branches

Session 0016.

## 1. Narrow question

Session 0014 left the following apparent gap:

> Must all locally certified normal branches be stitched into one global monotone correspondence before they can certify the symmetric Hausdorff distance?

Session 0015 clarified that Hausdorff distance is fundamentally a set metric: it does not encode order. This changes the answer.

For a pure Hausdorff target, a global monotone branch is **sufficient but not necessary**. Local correspondences that cover the source curve already give a directed Hausdorff upper bound. Two such local-cover constructions, one in each direction, give the full symmetric Hausdorff upper bound without any branch stitching.

This note proves that statement and specializes it to the current cubic normal-branch machinery.

---

## 2. Directed Hausdorff distance

Let

\[
P:I\to\mathbb R^d,
\qquad
Q:J\to\mathbb R^d
\]

be continuous curves on compact parameter intervals.

Define the directed Hausdorff distance

\[
h(P,Q)
:=
\sup_{t\in I}\operatorname{dist}(P(t),\operatorname{Im}Q).
\]

Then

\[
d_H(\operatorname{Im}P,\operatorname{Im}Q)
=
\max\{h(P,Q),h(Q,P)\}.
\]

The key point is that to upper-bound \(h(P,Q)\), one does not need the nearest point on \(Q\). It is enough to provide **any** point of \(Q\) within the tolerance for every source point.

---

## 3. Local-cover theorem

### Theorem 1 — one-sided local-cover certificate

Let \(I\) be covered by finitely many compact intervals

\[
I=\bigcup_{i=1}^N T_i.
\]

Suppose that for each \(i\) there is a map

\[
\sigma_i:T_i\to J
\]

such that

\[
\|P(t)-Q(\sigma_i(t))\|\le \varepsilon_i
\qquad
\text{for all }t\in T_i.
\]

Then

\[
\boxed{
 h(P,Q)
 \le
 \max_i\varepsilon_i.
}
\]

### Proof

For any \(t\in I\), choose an index \(i\) with \(t\in T_i\). Since \(Q(\sigma_i(t))\in\operatorname{Im}Q\),

\[
\operatorname{dist}(P(t),\operatorname{Im}Q)
\le
\|P(t)-Q(\sigma_i(t))\|
\le
\varepsilon_i.
\]

Taking the supremum in \(t\) gives the result. \(\square\)

### Important consequence

No compatibility is required between \(\sigma_i\) and \(\sigma_{i+1}\) on overlaps or at shared source knots.

For directed Hausdorff certification, the correspondence may jump from one locally valid branch to another. That would matter for Fréchet distance or differential transfer, but it does not matter for the set-distance inequality above.

---

## 4. Symmetric Hausdorff by two directed local covers

### Theorem 2 — two-pass certificate

Assume the hypotheses of Theorem 1 give

\[
h(P,Q)\le\varepsilon_{P\to Q}.
\]

Independently, let \(J\) be covered by compact intervals \(S_j\), and suppose that for each \(j\) there is a map

\[
\tau_j:S_j\to I
\]

with

\[
\|Q(u)-P(\tau_j(u))\|
\le
\delta_j
\qquad
(u\in S_j).
\]

Then

\[
\boxed{
 d_H(\operatorname{Im}P,\operatorname{Im}Q)
 \le
 \max
 \left\{
 \max_i\varepsilon_i,
 \max_j\delta_j
 \right\}.
}
\]

Again, there is no global stitching requirement in either direction.

This is the cleanest theorem for the current application if the final semantics is purely geometric Hausdorff closeness.

---

## 5. Specialization to the certified normal branch

Use the notation

\[
F(t,u)
=
(P(t)-Q(u))\cdot Q'(u).
\]

On one source interval \(T=[t_0,t_1]\) and target window \(U=[u_L,u_R]\), the existing local certificate is

\[
F(t,u_L)>0,
\qquad
F(t,u_R)<0,
\qquad
F_u(t,u)<0.
\]

These conditions imply that for every \(t\in T\) there is exactly one normal root

\[
u=\sigma(t)\in U.
\]

Because \(F_u\neq0\), the implicit-function theorem gives a continuous smooth branch on every smooth cubic-cubic subbox. The branch-deviation result from Session 0014 then certifies

\[
\|P(t)-Q(\sigma(t))\|
\le\varepsilon
\]

throughout the source interval.

Theorem 1 immediately converts this into a directed Hausdorff bound.

### Orientation is not required for Hausdorff

The earlier fourth condition

\[
F_t(t,u)=P'(t)\cdot Q'(u)>0
\]

was introduced to prove

\[
\sigma'(t)>0.
\]

That property is essential if one wants an order-preserving correspondence. It is **not** needed for Theorem 1 or Theorem 2.

Therefore, for a Hausdorff-only verifier, the basic local admissibility test can be reduced to

\[
\boxed{
F(t,u_L)>0,
\quad
F(t,u_R)<0,
\quad
F_u<0.
}
\]

This is a concrete simplification of the active verifier.

The feasibility experiment already showed that \(F_t\) was one source of subdivision in the higher-curvature family. Removing it may therefore reduce the certification cost; that is an empirical prediction, not yet a measured result.

---

## 6. Reverse direction and the common-normal polynomial

For the reverse directed problem, use \(Q\) as the source and \(P\) as the target. Its normal equation is

\[
\overline F(u,t)
=(Q(u)-P(t))\cdot P'(t).
\]

If

\[
G(t,u)
=(P(t)-Q(u))\cdot P'(t),
\]

as in Session 0014, then

\[
\boxed{
\overline F(u,t)=-G(t,u).
}
\]

Thus the polynomial that appeared previously as the stationarity condition for the forward branch is exactly the reverse normal equation up to sign.

The common-normal system

\[
F=0,
\qquad
G=0
\]

therefore has a second interpretation: it consists of point pairs that are simultaneously normal correspondences in both directed problems.

This does not eliminate the need for two directional covers, but it shows that the algebra required by the two-pass architecture is already present in the Session-0014 tolerance machinery.

---

## 7. A one-pass alternative: cover the target by branch images

Two directed passes are sufficient, but not logically necessary.

Suppose the forward local branches satisfy the hypotheses of Theorem 1 and, in addition,

\[
J
\subset
\bigcup_i\sigma_i(T_i).
\]

Then every target parameter \(u\in J\) occurs as \(u=\sigma_i(t)\) for some local branch. The same pairwise distance bound therefore gives

\[
h(Q,P)\le\max_i\varepsilon_i.
\]

Hence

\[
\boxed{
 d_H(\operatorname{Im}P,\operatorname{Im}Q)
 \le
 \max_i\varepsilon_i.
}
\]

This requires target-parameter coverage but still does **not** require the branches to agree at source interfaces.

If \(F_t>0\) is also certified, every \(\sigma_i\) is increasing and its image is simply

\[
\sigma_i(T_i)
=
[\sigma_i(t_i^-),\sigma_i(t_i^+)].
\]

Then the target-coverage condition reduces to a finite interval-union problem on branch endpoint values.

This gives two competing symmetric architectures:

1. **dual directed pass:** no orientation or global coverage bookkeeping, but run the local machinery twice;
2. **single oriented family plus image coverage:** one branch family, but keep \(F_t>0\) and certify coverage of the target parameter interval.

Which is cheaper is an empirical question.

---

## 8. When genuine global stitching is needed

A single global order-preserving correspondence is stronger.

Let the source intervals form an ordered partition

\[
I=[t_0,t_1]\cup\cdots\cup[t_{N-1},t_N]
\]

and let \(\sigma_i\) be strictly increasing local branches. If

\[
\sigma_i(t_i)=\sigma_{i+1}(t_i)
\qquad(i=1,\ldots,N-1),
\]

then the branches glue to one continuous strictly increasing map \(\sigma:I\to J\).

If additionally

\[
\sigma(t_0)=u_0,
\qquad
\sigma(t_N)=u_1,
\]

where \(J=[u_0,u_1]\), then \(\sigma\) is a homeomorphism onto \(J\), and

\[
d_F(P,Q)
\le
\sup_t\|P(t)-Q(\sigma(t))\|.
\]

A practical sufficient interface check is to certify uniqueness of the normal root on the **union** of the two adjacent reference windows at the shared source parameter. If \(F_u<0\) on that union and the outer boundary signs bracket one root, both local endpoint roots must coincide.

However, this stronger construction should be treated as an optional Fréchet/order layer, not as a prerequisite for Hausdorff simplification.

---

## 9. Piecewise cubic splines and double knots

For the current \(C^1\) cubic setting, target double knots may make \(Q''\) jump, so \(F_u\) is only one-sided there. The local monotonicity argument remains valid after splitting the target window at every reference knot:

- \(F\) itself is continuous because \(Q\) and \(Q'\) are continuous;
- certify \(F_u<0\) on each smooth subwindow;
- continuity plus strict decrease on every subwindow implies strict decrease across their union.

Source knots are even less problematic for a pure directed-cover theorem. One may simply end one source interval and begin another. Since interface branch equality is unnecessary for Hausdorff, there is no extra cross-knot theorem to prove.

This is another concrete advantage over the global-stitching route.

---

## 10. Adversarial review

### Branch switching at adjacent source boxes

A local branch may jump to a different nearby normal root after a source knot. The directed bound remains correct because each source point still has an explicit target point within tolerance.

Classification: harmless for Hausdorff, fatal only for an ordered/Fréchet interpretation.

### Remote closer branch

A certified local normal foot may not be globally nearest, as already observed in the near-self-approach experiment. The bound remains valid because an arbitrary target point supplies an upper bound on the true nearest distance.

Classification: harmless for upper-bound certification.

### Gaps in target coverage

A forward pass alone does not control \(h(Q,P)\). This is a genuine issue for symmetric Hausdorff.

Resolution: either run the reverse directed pass or certify target coverage by forward branch images.

### Overlapping local images

Overlap is harmless. Hausdorff distance does not require one-to-one pairing.

### Low speed / high curvature / short spans

These may still cause the local sign certificate to fail or require subdivision. The new theorem does not repair local admissibility; it only removes an unnecessary global compatibility requirement.

### Self-intersections and repeated traversal

Two curves can be Hausdorff-close while traversing the same geometry in very different orders. The two-pass certificate intentionally accepts this if the image sets are close. If CAD semantics later require traversal order, the optional Fréchet layer must be restored.

---

## 11. Goal alignment and complexity

This result materially simplifies the original CAD verification problem.

The previous active plan was:

\[
\text{local branch}
\to
\text{global stitching}
\to
\text{global monotone map}
\to
\text{Hausdorff bound}.
\]

For a pure geometric tolerance, the middle two steps are unnecessary. A sufficient architecture is

\[
\boxed{
\text{forward local cover}
+
\text{reverse local cover}
\Longrightarrow
\text{symmetric Hausdorff bound}.
}
\]

Every primitive remains fixed-degree on cubic-cubic boxes. The price is roughly a second local certification pass; the gain is removal of global branch topology, interface matching, onto proofs, and the orientation test.

This is a favorable trade until experiment shows otherwise.

---

## 12. Next decision gate

The next step should be a targeted feasibility experiment on the existing structured suite, not more global topology theory.

The experiment should compare:

- original four-condition local certificate versus the Hausdorff-only three-condition certificate without \(F_t\);
- forward-only and reverse-only pass rates/subdivision depth;
- two-pass symmetric success rate;
- certified/local branch deviation versus synchronized Green error and an independent numerical Hausdorff reference;
- conservatism of the cheap whole-box distance bound before common-normal refinement.

If both directed passes are usually cheap and the resulting bound is materially tighter than synchronized error in tangential/reparameterized cases, Phase 4 is close to complete.

If the reverse pass or tolerance bound is routinely expensive, reconsider whether the geometry-aware layer earns its complexity.
