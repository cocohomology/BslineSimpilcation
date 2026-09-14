# Two-Sided Local Hausdorff Certificate — Feasibility Test Plan

Session 0016.

## Purpose

Test the architectural consequence of the local-cover theorem:

> For a pure Hausdorff tolerance, global branch stitching and orientation preservation are not required. It may be enough to certify local directed correspondences in both directions.

This experiment is diagnostic evidence only. It does not replace the theorems in the derivation files.

## Inputs

Reuse the existing 72 deterministic curve pairs from `normal_branch_certificate_feedback.md` when possible:

- small normal perturbation;
- mild tangential reparameterization;
- mixed perturbation;
- nonuniform speed / short spans;
- higher curvature;
- near-self-approach negative controls.

Do not change the existing samples merely to improve pass rates.

If a reverse-direction window selector requires a new predictor, use the exact role-reversed analogue of the existing first-order predictor. Keep Newton optional; the first experiment already showed no strong engineering advantage.

## Quantities to record

For each curve pair and for each direction separately:

1. source-span count;
2. certified original spans / total spans;
3. maximum subdivision depth;
4. failures of left/right boundary sign tests;
5. failures of `F_u<0`;
6. failures that would have occurred only because of `F_t>0` in the old four-condition certificate;
7. final local branch-deviation upper bound;
8. synchronized Green / same-parameter upper bound;
9. independent high-accuracy numerical directed Hausdorff estimate for audit only.

For the pair as a whole record

\[
B_{2\text{-pass}}
=
\max\{B_{P\to Q},B_{Q\to P}\},
\]

and compare it with the synchronized bound and the independent numerical Hausdorff estimate.

Do not choose one arbitrary application tolerance as the main statistic. Report ratios instead:

\[
\frac{B_{2\text{-pass}}}{H_{\rm num}},
\qquad
\frac{B_{\rm sync}}{H_{\rm num}}.
\]

This makes the experiment informative across scales.

## Local certification variants

For each direction run at least:

### Variant A — previous certificate

- boundary sign separation;
- `F_u<0`;
- `F_t>0`.

### Variant B — Hausdorff-only certificate

- boundary sign separation;
- `F_u<0`;
- no `F_t` requirement.

Use the same window-selection and subdivision budgets so the comparison is meaningful.

## Deviation certification hierarchy

For every admissible leaf:

1. bound
   \[
   D(t,u)=\|P(t)-Q(u)\|^2
   \]
   over the whole certified box by tensor-product Bernstein coefficients;
2. record the whole-box upper bound;
3. obtain a sharper branch maximum using the Session-0014 common-normal condition
   \[
   F=0,\qquad G=0
   \]
   plus branch endpoints, or an equivalent certified threshold subdivision;
4. independently audit the result by dense / root-based numerical evaluation of the actual branch.

The exact common-normal implementation is not prescribed. The experiment should distinguish:

- cost/conservatism of the cheap box bound;
- cost/conservatism after branch-specific refinement.

## Independent geometric audit

For a diagnostic numerical reference, compute both directed distances by solving all source-to-target cubic-span nearest-point problems at a sufficiently dense adaptive source set, including endpoints and critical parameter regions. This is not a proof of the true Hausdorff value; label it `H_num` and use it only to judge conservatism.

If a certified bound is ever below the numerical audit estimate beyond numerical tolerance, treat that as a bug and stop.

## Pseudocode

```text
for each curve pair (P,Q):
    for direction in [(P,Q), (Q,P)]:
        source = direction.source
        target = direction.target

        for each source span T:
            U = predicted_target_window(T)

            run Variant A on (T,U)
            run Variant B on (T,U)

            if Variant B certifies after allowed subdivision:
                for each certified leaf box:
                    B_box = BernsteinUpperBound(D on box)
                    B_branch = CertifiedBranchMaximum(F,G,D on branch)
                    audit branch numerically
            else:
                mark directed fallback

        if all source spans certified:
            B_direction = max(all B_branch)
        else:
            B_direction = FALLBACK

    if both directions certified:
        B_two_pass = max(B_forward, B_reverse)

    B_sync = certified synchronized Green bound
    H_num = independent numerical symmetric Hausdorff audit

    report pass rates, depths, failure causes,
           B_two_pass / H_num,
           B_sync / H_num,
           B_box / B_branch statistics
```

## Success signals

The two-pass route remains promising if, on the ordinary five families:

- both directions usually certify with low subdivision depth;
- removing `F_t` measurably reduces subdivision or fallback, especially in high-curvature cases;
- the branch-specific bound is materially tighter than synchronized error in tangential / mixed reparameterization cases;
- the cheap box bound is often sufficient or becomes sufficient after little subdivision;
- failures remain concentrated in deliberately ambiguous/self-approaching cases.

No fixed percentage is promoted to theorem. The important question is whether the geometry-aware layer produces a useful accuracy/cost trade.

## Failure signals

Reconsider Phase 4 if any of the following is routine on ordinary close pairs:

- the reverse direction fails much more often than the forward direction;
- branch-specific tolerance certification requires deep two-dimensional root work on most spans;
- the final two-pass bound is usually little better than the synchronized Green bound;
- removing `F_t` does not simplify the computation in practice;
- local fallback frequency is high enough that a general Hausdorff routine would dominate anyway.

## Expected interpretation

A positive result would not prove industrial performance and would not solve candidate generation. It would only close the main uncertainty in the verification layer:

> whether a purely local, fixed-degree, two-directed-pass certificate is practical enough to use as the final geometric acceptance test for already-close spline simplification candidates.
