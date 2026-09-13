# Short-Horizon Roadmap — Internal

This file is intentionally volatile. It should describe the next few research sessions, not the whole project.

## Phase 0 — Initialization

Status: complete.

## Phase 1 — Make the D2 reduction exact

### Task 1.1 — Reconstruction structure

Status: **complete (Session 0002)**.

Established:
- \(D^2:S^1_3\to PL_{\rm disc}\) is onto with affine kernel;
- two vector constraints fix reconstruction uniquely;
- jump/kink structure of \(C''\) exactly records minimal cubic knot multiplicity;
- weighted PL complexity \(\kappa=K+2J\) gives \(N_{\rm ctrl}=4+\kappa\) in a minimal open/clamped cubic representation.

Detailed derivation: `docs/internal/derivations/d2_reconstruction.md`.

### Task 1.2a — Fixed-endpoint Green kernel

**Next session only. Do not automatically continue into 1.2b.**

Assume error boundary conditions
\[
E(a)=E(b)=0,
\qquad E''=e.
\]

Goals:
- derive the exact kernel \(K_D(t,s)\);
- check sign, symmetry after interval normalization, scaling with \(L=b-a\), and endpoint behavior;
- verify that \(N_G(e)=\|Ge\|_\infty\) is exactly synchronized positional error under this gauge;
- identify the kernel null/cancellation structure relevant to PL \(e\);
- perform a goal-alignment review: does this representation expose a useful simplification metric, or merely rewrite the original synchronized error?

Success criterion: a clean, reviewed operator identity and a precise statement of what information it preserves that ordinary \(L^p\) discards.

Failure criterion: discover that the induced quantity is algebraically correct but offers no exploitable structure on PL errors.

### Task 1.2b — Sharp operator bounds

Postponed until 1.2a is reviewed.

Potential goals later:
- sharp \(L^1,L^2,L^\infty\to L^\infty\) constants;
- extremizers or near-extremizers;
- compare looseness with direct \(N_G\) evaluation.

### Task 1.2c — PL-specific evaluation

Postponed.

Question: because \(e\) is piecewise linear and the kernel is piecewise linear in \(s\), can \(Ge\) be represented/evaluated exactly with low algebraic cost and can its max norm be certified without dense sampling?

## Phase 2 — Demonstrate why Lp is structurally loose

Status: waiting for Phase 1.2 baseline.

Later targets:
- cancellation pairs;
- short-span scaling;
- ranking reversals between \(L^p\) and \(N_G\).

## Phase 3 — First-order treatment of parametrization

Status: postponed.

Do not enter until the synchronized metric is understood and reviewed against the original CAD objective.

## Phase 4 — Local geometric comparison

Status: postponed.

## Phase 5 — Algorithmic consequences

Status: postponed.

If theory survives, write pseudocode only before any numerical test. No source code unless explicitly requested.

## Side branch parking lot

- optimize the affine reconstruction mode instead of fixing endpoints;
- impose continuity on \(q\) to force a \(C^2\) simplified cubic;
- treat closed/periodic curves with compatibility constraints;
- parameter normalization or geometric gauge choices.

These are intentionally parked so they do not dilute the next session.
