# Stage 01 Theory Checkpoint — From Second-Derivative Reduction to a Testable Local Geometric Bridge

Date: 2026-09-13
Scope: Sessions 0002–0009
Audience: primarily the assistant / future research continuation

## 0. Why this checkpoint exists

The project has reached its first natural pause. The theory has moved far enough that further formal sharpening should be conditioned on a small feasibility experiment. This document reconstructs the whole path, separates established facts from rejected ideas and open hypotheses, and records why the next action is empirical rather than another theorem.

The original engineering phenomenon must remain the anchor:

> CAD systems may receive cubic or higher-order spline curves whose parameter representation is extremely complex—many knots, high multiplicity, or arbitrary free construction—while the geometric image is visually ordinary. The goal is to replace such curves, under a geometric tolerance, by a representation that is as simple as possible or at least dramatically simpler.

The current branch deliberately restricts to regular, non-rational, cubic, C1 splines. The aim is not to solve all spline simplification at once, but to see whether the cubic C1 case contains a cleaner mathematical structure than classical iterative knot removal or dense-sampling refit.

---

## 1. Core structural discovery: simplify the second derivative, not the curve directly

For a C1 piecewise-cubic curve C,

\[
q=C''
\]

is piecewise linear and may jump at double knots. Conversely, any vector-valued piecewise-linear function with jumps integrates twice to a C1 piecewise cubic, up to an affine function.

Formally,

\[
D^2:S_3^1\to PL_{\rm disc}
\]

is surjective and

\[
\ker D^2=\mathcal P_1.
\]

Hence

\[
S_3^1/\mathcal P_1\cong PL_{\rm disc}.
\]

This was the first genuinely useful reduction because it also preserves representation complexity. For q=C'',

- a jump corresponds to a double cubic knot;
- a continuous kink corresponds to a simple cubic knot;
- no jump/kink means the breakpoint is redundant.

If K0 is the number of continuous kinks and J the number of jumps, define

\[
\kappa(q)=K_0+2J.
\]

For a minimal open/clamped cubic representation,

\[
N_{\rm ctrl}=4+\kappa(q).
\]

### Status

Stable. High confidence.

### Why it matters to the original problem

It converts a spline-complexity problem into a PL-complexity problem without losing the meaning of knot multiplicity. This is not merely a convenient representation change: in the present model class, it is an exact structural dictionary.

### Boundary

The D2 map removes affine information. A reconstruction gauge is required. The current main gauge fixes both endpoints; optimized affine correction remains parked.

---

## 2. Exact transport of second-derivative error through a Green operator

Let

\[
e=C''-\widetilde C'',
\qquad E=C-\widetilde C,
\]

and impose the endpoint-preserving gauge

\[
E(a)=E(b)=0.
\]

Then

\[
E=G_De,
\]

where GD is the Dirichlet Green operator for the second derivative. Therefore

\[
N_G(e):=\|G_De\|_\infty=\|E\|_\infty.
\]

This is exact synchronized positional error, not an Lp surrogate. Since matching equal parameters is a valid point pairing,

\[
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)\le N_G(e).
\]

The Green kernel retains cancellation, vector direction, and position of the second-derivative error before taking the final supremum. This is already qualitatively stronger than collapsing e immediately to one Lp number.

### Computational consequence

For PL e, E is piecewise cubic. On each span, exact Euclidean maxima of E reduce to the stationarity condition

\[
E\cdot E'=0,
\]

which is polynomial of degree at most five. Alternatively, cubic Bézier convex-hull subdivision gives a certified branch-and-bound route.

Thus the exact synchronized Green error remains O(n) fixed-degree one-variable work over n union spans, ignoring precision refinement.

### Status

Stable. High confidence.

### Major consequence for the project

Classical Lp norms are no longer needed as the primary error quantity merely because they are easier to compute. They may still be useful for pruning, theory comparisons, or very cheap preliminary rejection.

---

## 3. First attempt to become geometry-aware: quotient tangential error

Synchronized error is parameterization sensitive. A tangential displacement may represent mainly a sliding of corresponding parameter points rather than genuine geometric shape change.

Using reference arc length s and unit tangent T, the synchronized error decomposes into tangent and normal parts. The first-order shift

\[
\rho(s)=s-E(s)\cdot T(s)
\]

removes the synchronized tangential component to first order.

A finite estimate was derived:

\[
d_H\le N_{G,\perp}+\frac K2N_{G,\parallel}^2,
\]

provided the constructed correspondence is orientation preserving, where K is a global curvature supremum.

Important positive result: the normal component is indeed the first-order geometric residual, while tangential error contributes only at second order through curvature.

### Algebraic certification

For cubic spans, all ingredients remain rational functions of fixed-degree polynomials in the native parameter. The arc-length proof does not force arc-length inversion in an implementation.

Normal error, tangential error, curvature, regularity, and even the monotonicity of the first-order correspondence reduce to fixed-degree polynomial sign/extremum problems.

### Status

The local first-order interpretation is retained.

The global-curvature bound itself is *not* retained as a preferred final metric.

---

## 4. First adversarial review: what broke and what survived

The strongest negative result was an in-class counterexample showing that

\[
N_{G,\perp}+\frac K2N_{G,\parallel}^2
\]

can be arbitrarily conservative even when the reference and candidate have exactly the same image.

Construction idea: place a pure tangential reparameterization error on a straight part of the curve, and put arbitrarily high curvature in a disjoint region where the error is zero. The true Hausdorff distance remains zero, while the global curvature K makes the bound arbitrarily large.

### Interpretation

This did *not* invalidate the tangent/normal linearization. It identified the precise information loss: **globalizing curvature independently of where tangential displacement occurs**.

The attack also found:

- near-zero parameter speed is a conditioning issue rather than a theoretical contradiction;
- high curvature where the tangential shift actually occurs produces a genuine quadratic effect, so curvature cannot simply be deleted;
- short spans and double knots are mainly scaling / one-sided-regularity issues;
- near self-approach exposes a modeling distinction between Hausdorff and order-preserving / Fréchet-like correspondence.

### Classification of the counterexample

Boundary-defining, not fatal.

The example is mathematically decisive against a universal global-K metric, but it does not show that ordinary CAD simplification pairs routinely exhibit this pathology.

---

## 5. Degen revisited: the important lesson was methodological

Degen's normal-distance framework suggested a more disciplined order of construction:

\[
\text{geometric neighbourhood}
\to
\text{admissible class}
\to
\text{unique correspondence}
\to
\text{deviation field}
\to
\text{norm}.
\]

This differs from guessing an improved norm of synchronized error.

For a candidate point \(\widetilde C(t)\), define the nonlinear normal equation

\[
F(t,u)=\bigl(\widetilde C(t)-C(u)\bigr)\cdot C'(u)=0.
\]

A branch u=\sigma(t) gives a genuinely local normal correspondence. For fixed t and a cubic reference span,

\[
\deg_u F\le5.
\]

At a normal root, with r=\widetilde C(t)-C(u),

\[
F_u=-\|C'(u)\|^2+r\cdot C''(u).
\]

The local normal-coordinate nondegeneracy condition is therefore

\[
\|C'(u)\|^2-r\cdot C''(u)>0.
\]

In arc length this becomes

\[
1-r\cdot\kappa_{\rm vec}>0.
\]

The branch derivative is

\[
\sigma'(t)=
\frac{\widetilde C'(t)\cdot C'(\sigma(t))}
{\|C'(\sigma(t))\|^2-r\cdot C''(\sigma(t))}.
\]

This separates normal-coordinate degeneracy from orientation loss.

### Key synthesis

The earlier first-order tangential shift is exactly the Newton / implicit-function linearization of the nonlinear normal equation:

\[
\sigma(t)-t\approx-
\frac{E(t)\cdot C'(t)}{\|C'(t)\|^2}.
\]

Thus Sessions 0005–0006 were not a dead branch. They derived the linearized version of the more geometric correspondence later suggested by Degen.

### Status

Stable conceptual synthesis. High confidence locally.

Global computational viability remains open.

---

## 6. Local normal-branch certificate: current end point of the theory

To avoid turning normal correspondence into a full global nearest-point theory, Session 0009 asked for a deliberately local fast-path certificate.

Take a candidate parameter span

\[
T=[t_0,t_1]
\]

and a nearby reference window

\[
U=[u_0,u_1].
\]

If on T x U

\[
F(t,u_0)>0,
\qquad
F(t,u_1)<0,
\qquad
F_u(t,u)<0,
\]

then for every t in T there is exactly one normal root

\[
u=\sigma(t)\in U.
\]

Because

\[
\Phi(t,u)=\|\widetilde C(t)-C(u)\|^2,
\qquad
\Phi_u=-2F,
\]

that root is also the unique local minimizer of distance over U.

If additionally

\[
F_t(t,u)=\widetilde C'(t)\cdot C'(u)>0,
\]

then

\[
\sigma'(t)>0.
\]

For cubic-cubic span boxes,

\[
\deg F\le(3,5),
\qquad
\deg F_u\le(3,4),
\qquad
\deg F_t\le(2,2).
\]

This makes tensor-product Bernstein sign certification plausible: same-sign coefficients immediately certify a box; ambiguous boxes are subdivided.

The Green layer provides a predictor for the window center. The first-order predictor is

\[
\sigma_0=t-\frac{E\cdot C'}{\|C'\|^2},
\]

and a one-step Newton predictor is

\[
\sigma_N=t-
\frac{E\cdot C'}{\|C'\|^2+E\cdot C''}.
\]

### What this certificate guarantees

A unique nearby normal foot within the chosen local window, local distance minimization there, and optionally orientation preservation.

### What it deliberately does not guarantee

It does not rule out a remote part of the reference curve being even closer. Therefore it is a local correspondence certificate, not a universal global Hausdorff solver.

This limitation is acceptable if the certificate is used as a fast path in the close-curve simplification regime with fallback verification for ambiguous regions.

---

## 7. Current architecture after the first theory stage

The present research architecture is now three-layered.

### Representation layer

Work in q=C''. Complexity of a C1 cubic is encoded exactly by PL kinks and jumps.

### Synchronized-error layer

For a candidate q_tilde, reconstruct under the endpoint gauge and compute

\[
E=G_D(q-\widetilde q).
\]

This gives a cheap exact synchronized displacement, a rigorous Hausdorff upper bound, and branch predictors.

### Optional local geometric layer

For candidates that need a tighter geometric test, use E to localize a nearby normal branch and certify it with fixed-degree Bernstein sign tests. If certification fails, fall back rather than deepen the local theory indefinitely.

This layered architecture is more important than any one error formula.

---

## 8. Major unresolved problems

### U1. Does the local branch certificate actually pass often enough?

This is the immediate gate. The theorem is easy to state; its value depends on whether ordinary close cubic pairs certify at depth 0–2 rather than requiring deep subdivision.

### U2. Candidate generation / optimization has not yet been designed

The project has mainly studied representation and certification. It has not yet solved the core nonlinear optimization problem:

> Given a complex PL q=C'', find a much lower-complexity PL q_tilde minimizing kinks/jumps subject to an acceptable error certificate.

This is where free-breakpoint / PL simplification / combinatorial decisions will eventually enter.

### U3. Fixed-endpoint gauge may be unnecessarily restrictive

The affine kernel of D2 gives two integration constants. Fixing endpoints is natural for B-Rep semantics, but optimized affine reconstruction may improve approximation for free-standing curves.

### U4. Hausdorff versus correspondence semantics

Near self-approach, an order-preserving normal graph may be much stricter than point-set Hausdorff. The project has not yet fixed whether this extra structure should be considered desirable CAD semantics or avoidable conservatism.

### U5. Global exactness of normal deviation

On a genuine non-overlapping normal graph with unique nearest projection, the normal deviation sup equals Hausdorff. The current local box certificate does not prove the full global non-overlap condition.

### U6. Extension beyond regular C1 cubic non-rational curves

Closed/periodic curves, rational curves, lower continuity, and higher degree remain outside the current stage.

---

## 9. Theory branches deliberately parked rather than discarded

The project should keep these as seeds, not active tasks.

### P1. Localized curvature remainder

Instead of one global K, use curvature only along the actual shifted arc interval. This directly repairs the remote-curvature counterexample but may require moving arc-length intervals or more complicated envelopes.

Reopen if the nonlinear normal certificate is too expensive but the first-order geometry is empirically useful.

### P2. Green-induced quotient / shape-space interpretation

The normal component of G_De behaves like the first-order quotient of positional error by reparameterization directions. There may be a clean functional-analytic or shape-space formulation behind this.

Reopen only if it gives a stronger optimization principle or a useful lower-dimensional metric; do not pursue for elegance alone.

### P3. Optimized affine gauge

Instead of fixing both endpoints, minimize over the affine kernel after selecting q_tilde. This may materially improve free-curve approximation and could interact nicely with Green operators.

Reopen when the target application includes curves whose endpoints are not topologically fixed.

### P4. Symmetric geometry-aware certification

Current geometry is reference-biased. A symmetric construction using both curves might tighten bounds or reduce orientation artifacts.

Reopen only after the one-sided fast path proves useful.

### P5. Distributional second derivative for lower continuity

For curves below C1, jumps of C' produce delta terms and jumps of C produce delta-prime terms in distributional derivatives. This could extend the D2 representation dictionary to lower continuity.

Reopen only after the C1 cubic program demonstrates value.

### P6. Free-knot / nonlinear PL approximation in q-space

Once certification is settled, the simplification problem becomes a low-complexity PL approximation problem with weighted costs for kinks and jumps. Connections to free-knot spline approximation, segmented regression, dynamic programming, and nonlinear approximation may become central.

This is likely a future main line, but it is premature before the error/certification gate is understood.

---

## 10. What has *not* been learned yet from the literature

The active literature work so far has been selective:

- Lyche–Morken supplies the classical knot-removal / data-reduction context and a useful contrast with derivative-domain thinking.
- Degen supplies a careful normal-distance/admissibility architecture.

A full prior-art search for the precise combination

\[
\text{PL second derivative reduction}
+\text{Green transport}
+\text{local certified normal branch}
\]

has not yet been done. Novelty should not be claimed before that search.

---

## 11. TeX note decision

### Decision: do not write the full user-facing TeX note yet.

Reasons:

1. The synchronized D2/Green theory is coherent, but the geometry-aware layer is only at a **testable hypothesis / fast-path certificate** stage.
2. The next experiment can still show that the admissibility certificate is too restrictive on ordinary data.
3. Candidate-generation theory has not yet been designed, so a polished note would currently end before the actual simplification algorithm begins.
4. Writing TeX now risks psychologically freezing a framework that is intentionally still flexible.

### TeX trigger

Write the first self-contained TeX note after one of two events:

**Positive trigger:** the feasibility experiment shows the local certificate is useful, followed by a second adversarial review confirming a credible geometry-aware pipeline.

**Negative trigger:** the experiment rejects the normal-branch route but leaves a coherent negative result / boundary theorem substantial enough to preserve as a finished stage.

When written, the note should include Green-function background explicitly, because that machinery is not assumed fresh for the user.

---

## 12. Immediate resume protocol

Do not continue fine theory before the feasibility experiment unless a genuinely new external fact changes the picture.

After experiment results arrive:

- if ordinary cases certify cheaply, study how to compute/certify the normal-deviation maximum and perform a second attack;
- if ordinary cases frequently fail, stop strengthening admissibility and evaluate a simpler architecture based on synchronized Green certification plus selective general Hausdorff verification;
- regardless of outcome, then revisit candidate-generation in q-space, because error theory must ultimately serve simplification rather than become the project itself.

---

## 13. Stage assessment

This stage did not solve spline simplification. It did establish a coherent and nontrivial structural route:

\[
\boxed{
\text{C1 cubic complexity}
\leftrightarrow
\text{PL second derivative}
\to
\text{exact Green positional error}
\to
\text{optional local geometric correspondence}
}
\]

The first two arrows are now strong. The third is plausible but explicitly gated by experiment.

The main methodological success is that the project found a place to stop: enough theory exists to ask a falsifiable computational question, and further analysis is postponed until that question is answered.
