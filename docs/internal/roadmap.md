# Short-Horizon Roadmap — Internal

This file is intentionally volatile. It should describe the next few research sessions, not the whole project.

## Phase 0 — Initialization

Status: complete.

Goals:
- establish repository structure;
- separate user-facing and internal documentation;
- define the narrow scope \(C^1\), cubic, non-rational;
- identify the first theoretical bottleneck as the error metric rather than the simplification algorithm.

## Phase 1 — Make the \(D^2\) reduction exact

### Task 1.1 — Reconstruction structure

Write a compact derivation of the map
\[
C \leftrightarrow (C'',\text{boundary data})
\]
for \(C^1\) cubic splines.

Need to record:
- how simple and double knots appear in \(C''\);
- conditions under which integrating a PL function yields a cubic spline with the intended continuity;
- what boundary constraints uniquely determine the reconstruction.

Deliverable: internal derivation, and user-facing update only if anything nontrivial appears.

### Task 1.2 — Green kernels

Derive exact kernels for at least two boundary choices:

A. \(E(a)=E'(a)=0\).

B. \(E(a)=E(b)=0\).

For each:
- write \(E(t)=\int K(t,s)e(s)\,ds\);
- derive exact \(L^1,L^2,L^\infty\to L^\infty\) operator bounds;
- determine sharp constants if easy;
- construct examples that attain or nearly attain them.

Deliverable: a baseline comparison table.

## Phase 2 — Demonstrate why \(L^p\) is structurally loose

### Task 2.1 — Cancellation examples

Construct minimal PL examples where:
- \(\|e\|_\infty\) is large;
- \(\|e\|_2\) is non-small;
- but \(\|Ge\|_\infty\) is much smaller.

Goal: quantify the gap, not merely illustrate it.

### Task 2.2 — Short-span scaling

Study errors supported on an interval of length \(h\). Determine the exact scaling of:
- \(\|e\|_p\);
- \(\|Ge\|_\infty\);
- positional contribution after enforcing endpoint conditions.

Goal: understand whether high second-derivative amplitudes on tiny spans are naturally suppressed by the induced metric.

## Phase 3 — First-order treatment of parametrization

### Task 3.1 — Tangential perturbations

Let \(\widetilde C=C+E\) with
\[
E=\alpha T+E_\perp.
\]

Derive a small reparametrization
\[
\phi(t)=t+\eta(t)
\]
that cancels \(\alpha T\) to first order.

Need explicit formula for \(\eta\) and an explicit second-order remainder.

### Task 3.2 — Normal projection candidate

Study
\[
N_{G,\perp}(e)=\sup_t\|P_{N(t)}Ge(t)\|.
\]

Questions:
- null space;
- dependence on reference curve;
- whether it is invariant under any useful class of perturbations;
- relation to the linearization of a normal-correspondence distance.

Stop if this quantity turns out to be misleading on simple counterexamples.

## Phase 4 — Local geometric comparison

Only begin after Phase 3 produces a viable object.

Targets:
- formulate a tubular-neighborhood assumption;
- establish existence/uniqueness of nearest/normal correspondence locally;
- compare normal residual, Degen-style normal distance, Fréchet-type distance, and Hausdorff distance;
- isolate a computable sufficient condition for certification.

## Phase 5 — Algorithmic consequences

Do not enter this phase prematurely.

If the metric theory survives:
- formulate low-complexity PL approximation problem;
- determine appropriate primitives: remove breakpoint, merge segments, move breakpoint, fit groups;
- write pseudocode only;
- design small numerical tests to attack the theory.

No source code unless explicitly requested by the user.

## Current next action

Begin with **Task 1.1 and Task 1.2**. These are foundational, relatively self-contained, and likely to reveal whether the Green-induced viewpoint is genuinely useful before investing in geometric correspondence theory.
