# Research Frontier — Internal

## Current narrow problem

Work with regular \(C^1\), cubic, non-rational spline curves \(C:[a,b]\to\mathbb R^d\). Algebraic statements below do not require regularity; regularity will matter when geometric correspondence enters.

Let
\[
q=C'',\qquad \widetilde q=\widetilde C'',\qquad e=q-\widetilde q,
\]
and use the endpoint-preserving gauge unless explicitly stated otherwise.

---

## Stable foundation

### F1. Exact D2 reduction — established in Session 0002

\[
D^2:S^1_3\to PL_{\rm disc}
\]
is onto with kernel \(\mathcal P_1\). After fixing two vector integration constants, every discontinuous PL candidate reconstructs uniquely to a \(C^1\) cubic.

Minimal cubic knot multiplicity is encoded exactly by singularities of \(q=C''\):
- jump -> double knot;
- continuous kink -> simple knot;
- neither -> redundant breakpoint.

If \(K\) is the number of continuous kinks and \(J\) the number of jumps,
\[
\kappa(q)=K+2J,
\qquad N_{\rm ctrl}=4+\kappa(q)
\]
for a minimal open/clamped cubic representation.

### F2. Fixed-endpoint Green operator — established in Session 0003

For
\[
E''=e,\qquad E(a)=E(b)=0,
\]
write \(L=b-a\). Then
\[
E(t)=G_De(t)=\int_a^b K_D(t,s)e(s)\,ds,
\]
where
\[
K_D(t,s)=
-\frac{(\min\{t,s\}-a)(b-\max\{t,s\})}{L}.
\]

Properties reviewed:
- \(K_D\) is symmetric;
- \(K_D\le0\) in the interior;
- it vanishes at both endpoints;
- after normalization, the operator scales like \(L^2\), as expected from two integrations;
- \(-K_D(t,\cdot)\) is a positive piecewise-linear tent weight.

Define
\[
N_G(e):=\|G_De\|_\infty.
\]
Under the endpoint gauge,
\[
N_G(e)=\|C-\widetilde C\|_{\infty,\text{synchronized}},
\]
and therefore
\[
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)\le N_G(e).
\]

The operator preserves signed/vector cancellation and location information that a single global \(L^p\) number discards. It does **not** solve reparametrization.

Detailed derivation: `docs/internal/derivations/fixed_endpoint_green.md`.

---

## Current interpretation

The D2 route now has two exact pieces:

1. representation complexity is exact in the \(q=C''\) domain;
2. synchronized positional error under fixed endpoints is exact through a linear Green operator in the same domain.

This is stronger than a heuristic reduction. The unresolved issue is whether this exact structure leads to an error objective that is computationally and geometrically superior enough to matter in CAD.

The most promising immediate observation is that for PL \(e\), \(G_De\) is piecewise cubic. Therefore exact/certified evaluation of \(N_G\) may reduce to low-degree polynomial extrema rather than curve-to-curve nearest-point search. This must be checked carefully before moving to more abstract metric theory.

---

## Theorem status

### T1. Exact reconstruction / complexity theorem — ESTABLISHED

Session 0002.

### T2a. Fixed-endpoint Green kernel and exact synchronized-error identity — ESTABLISHED

Session 0003.

### T2b. Sharp \(L^p\to L^\infty\) operator bounds — OPEN, DEPRIORITIZED

Still useful as a baseline, but direct evaluation of \(N_G\) may make global \(L^p\) bounds secondary rather than central.

### T2c. PL-specific exact/certified evaluation of \(N_G\) — NEXT TARGET

Questions:
- on each union-partition span, what polynomial degree is needed to maximize \(\|G_De(t)\|\)?
- how are jumps in \(e\) handled at span boundaries?
- scalar versus vector-valued cases;
- can a certified maximum be obtained with standard polynomial root isolation / subdivision without dense sampling?
- is the cost local/near-linear in the number of PL pieces, or does global endpoint coupling spoil this?

### T3. First-order quotient by tangential reparametrization — POSTPONED

### T4. Local comparison with normal/Hausdorff geometry — POSTPONED

---

## Candidate objects parked for later

### Normal-projected Green error
\[
N_{G,\perp}(e)=\sup_t\|P_{N(t)}G_De(t)\|.
\]
Do not work on this until synchronized evaluation is understood.

### Nonlinear normal correspondence
Seek monotone \(\sigma\) with
\[
\widetilde C(\sigma(t))-C(t)\perp T(t).
\]
Postponed.

### Optimized affine gauge
Potentially useful for standalone curves, but endpoint preservation is the current CAD default.

---

## Counterexamples to preserve for later

1. straight-line bad parametrization;
2. tiny-span spike;
3. cancellation pair;
4. near self-approach;
5. high-curvature tube failure;
6. double-knot jump.

---

## Goal-alignment review after Session 0003

No drift detected. The Green operator result is directly tied to the original simplification objective because it transports second-derivative approximation error into a certified positional/Hausdorff upper bound while staying in the PL-derived algebraic setting.

However, the next session must test **computational usefulness**, not continue accumulating abstract operator theory. If \(N_G\) cannot be evaluated/certified cheaply on PL errors, the current elegance may not translate into engineering value.

---

## Stop conditions

Pause this direction and report if:
- exact/certified evaluation of the candidate metric becomes comparable in difficulty to Hausdorff/Fréchet search;
- parameterization effects cannot be reduced without destroying the PL advantage;
- bounds are too loose to rank simplifications usefully;
- low weighted complexity of \(q\) does not translate into useful geometric simplification.
