# Research Frontier — Internal

## Current setting

Work with regular \(C^1\), cubic, non-rational spline curves \(C:[a,b]\to\mathbb R^d\), preserving endpoints. Canonical notation:
\[
q=C'',\qquad \widetilde q=\widetilde C'',\qquad e=q-\widetilde q,
\qquad E=C-\widetilde C=G_De.
\]

## Stable foundation

### F1 — exact \(D^2\) reduction
\[
D^2:S_3^1\to PL_{\rm disc}
\]
is onto with affine kernel. Jump/kink structure of \(q\) records minimal cubic knot multiplicity exactly.

### F2 — exact synchronized Green error
Under fixed endpoints,
\[
E=G_De,\qquad N_G=\|E\|_\infty,
\]
and \(d_H\le N_G\). For PL \(e\), \(N_G\) is fixed-degree certifiable.

### F3 — first-order geometry
Tangential synchronized displacement is the linearized reparameterization direction; normal displacement is the first-order geometric residual. The former Session-0005 shift is now understood as the first Newton/IFT step for the nonlinear normal equation.

### F4 — global-curvature closure is only a boundary result
The bound
\[
N_{G,\perp}+\frac K2N_{G,\parallel}^2
\]
is correct but can be arbitrarily conservative because remote curvature can pollute a local tangential shift. Keep this as a known capability boundary, not a problem that must be repaired universally.

### F5 — Degen lesson: correspondence before norm
Degen's useful architecture is
\[
\text{admissible normal neighbourhood}
\to\text{unique correspondence}
\to\text{deviation function}
\to\text{sup norm}.
\]
For our space-curve setting, use
\[
F(t,u)=(\widetilde C(t)-C(u))\cdot C'(u).
\]
A normal branch satisfies \(F(t,\sigma(t))=0\).

### F6 — local cubic span-box admissibility certificate (Session 0009)

On a candidate/reference parameter box
\[
T=[t_0,t_1],\qquad U=[u_0,u_1],
\]
assume
\[
F(t,u_0)>0,\qquad F(t,u_1)<0
\]
for all \(t\in T\), and
\[
F_u(t,u)<0
\]
throughout \(T\times U\).

Then for every \(t\in T\) there is exactly one root \(u=\sigma(t)\in U\). It is the unique minimizer of
\[
\Phi(t,u)=\|\widetilde C(t)-C(u)\|^2
\]
over that local reference window. If additionally
\[
F_t(t,u)=\widetilde C'(t)\cdot C'(u)>0
\]
on the box, then \(\sigma'(t)>0\), so the branch is orientation preserving.

For cubic spans the relevant polynomial bidegrees are fixed:
\[
\deg F\le(3,5),\quad
\deg F_u\le(3,4),\quad
\deg F_t\le(2,2).
\]
Thus admissibility can be certified by local Bernstein/interval sign tests rather than global normal-root enumeration.

Detailed derivation: `docs/internal/derivations/local_normal_branch_certificate.md`.

## Green predictor refinement

At the synchronized point \(u=t\), with
\[
B=E\cdot C',\qquad S=\|C'\|^2,
\]
we have
\[
F(t,t)=-B,
\qquad
F_u(t,t)=-(S+E\cdot C'').
\]
Hence the exact one-step Newton predictor is
\[
\boxed{
\sigma_N(t)=t-\frac{B}{S+E\cdot C''}.
}
\]
The earlier predictor \(t-B/S\) is its first-order approximation.

The predictor is not a proof; it is used only to keep the candidate box \(U\) local.

## What Session 0009 deliberately did not solve

- no proof that the local normal foot is the global nearest point on the entire reference curve;
- no exact maximization of nonlinear normal deviation along the implicit branch;
- no global reach/tubular-neighbourhood computation;
- no universal handling of self-approach.

This is intentional. The certificate is designed as a **fast path for ordinary close curves**, not a universal replacement for Hausdorff computation.

## Reality / engineering interpretation

A practical candidate simplification is expected to remain close to the original. In that regime:

1. Green gives an exact synchronized displacement and a cheap branch predictor;
2. a narrow reference window \(U\) is chosen around that predictor;
3. fixed-degree sign tests certify a unique local normal branch;
4. if the certificate fails, the algorithm falls back to synchronized error, subdivision, or a more general verifier.

Failure of the certificate is not failure of the approximation.

## Current decision gate

The next uncertainty is empirical:

> Do these simple sign certificates pass often enough on ordinary close cubic pairs to justify the nonlinear normal layer?

This should be tested before proving stronger admissibility theorems. If pass rates are high with little subdivision, the route has engineering value. If not, deeper normal-bundle theory risks becoming an inference game disconnected from the original simplification problem.

Therefore the next stage is a small numerical feasibility experiment, specified only in pseudocode. No further fine analysis should be added before that gate.
