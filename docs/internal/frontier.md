# Research Frontier — Internal

## Current narrow problem

Work with regular \(C^1\), cubic, non-rational spline curves \(C:[a,b]\to\mathbb R^d\). The algebraic reduction no longer needs regularity, but regularity will matter once geometry enters.

Let
\[
q=C'',\qquad \widetilde q=\widetilde C'',\qquad e=q-\widetilde q.
\]

## Newly established foundation — Session 0002

The map
\[
D^2:S^1_3\to PL_{\rm disc}
\]
is surjective with affine kernel \(\mathcal P_1\). After fixing two vector integration constants, every discontinuous PL candidate reconstructs uniquely to a \(C^1\) cubic.

The minimal cubic knot multiplicity is encoded exactly by the PL singularity type:

- jump in \(q\) -> double cubic knot;
- continuous kink in \(q\) -> simple cubic knot;
- no jump and no kink -> redundant breakpoint.

If \(K\) is the number of continuous kinks and \(J\) the number of jumps,
\[
\kappa(q)=K+2J,
\]
and a minimal open/clamped cubic representation has
\[
N_{\rm ctrl}=4+\kappa(q).
\]

This validates the D2 route as an exact representation-complexity reduction, not merely a heuristic.

Detailed proof: `docs/internal/derivations/d2_reconstruction.md`.

## Immediate modeling issue: the affine gauge

Because \(D^2\) kills affine functions, a metric on \(q\) cannot control position until the affine kernel is fixed or optimized.

Candidate gauges:

1. fixed \(C(a),C'(a)\);
2. fixed endpoints \(C(a),C(b)\) — preferred default for CAD/B-Rep;
3. optimized affine correction — potentially tighter, but postponed.

The next session should use gauge 2 only.

## Candidate objects under study

### 1. Green-induced synchronized error

Under fixed endpoints define
\[
E=Ge,
\]
where \(G\) is the inverse of \(D^2\) with homogeneous endpoint conditions on the error.

Primary quantity:
\[
N_G(e)=\|Ge\|_\infty.
\]

Immediate questions:
- exact Dirichlet Green kernel;
- exact / sharp \(L^p\to L^\infty\) constants, but only after the kernel itself is reviewed;
- efficient exact or certified evaluation when \(e\) is PL;
- whether endpoint fixing is too restrictive for some simplification use cases.

### 2. Normal-projected Green error

For a regular reference curve \(C\) with unit tangent \(T\), later study
\[
N_{G,\perp}(e)=\sup_t\|P_{N(t)}Ge(t)\|.
\]

Status: candidate semi-norm-like quantity only. **Do not work on this yet.**

### 3. Nonlinear normal correspondence

Later seek a monotone map \(\sigma\) such that
\[
\widetilde C(\sigma(t))-C(t)\perp T(t).
\]

Status: postponed until the synchronized Green baseline is understood.

## Theorem status

### T1. Exact reconstruction theorem — ESTABLISHED

Completed in Session 0002, including the weighted breakpoint / knot-complexity dictionary.

### T2. Green operator formulas and operator constants — OPEN

Next target should be split into small pieces:

- T2a: fixed-endpoint kernel and exact identity \(E=Ge\);
- T2b: sharp operator bounds and extremizers;
- T2c: PL-specific exact/certified evaluation.

Do not attempt all three in one session.

### T3. First-order quotient by tangential reparametrization — POSTPONED

### T4. Local comparison with geometric distance — POSTPONED

## Counterexamples to actively preserve for later

1. straight-line bad parametrization;
2. tiny-span spike;
3. cancellation pair;
4. near self-approach;
5. high curvature tube failure;
6. double-knot jump.

## New question exposed by T1

Could optimizing the affine reconstruction mode after simplifying \(q\) materially reduce geometric error compared with hard endpoint constraints? This may be relevant for standalone curves but probably conflicts with B-Rep endpoint preservation. Keep as a side branch; do not pursue now.

## Goal-alignment review

T1 is directly relevant to the original CAD goal because it proves that weighted PL singularity complexity is exactly the minimal cubic knot/control-point complexity. The work has not drifted into an unrelated functional-analysis problem.

The unresolved risk remains entirely in the **error geometry**, not the representation reduction.

## Stop conditions

Pause this direction and report if:
- the geometry-aware metric becomes essentially as hard as Hausdorff/Fréchet optimization;
- parameterization effects cannot be suppressed without destroying the PL advantage;
- certified constants are too loose for engineering value;
- low weighted complexity of \(q\) does not translate into useful geometric simplification.
