# Current State — User-Facing Summary

## Scope

The research targets regular \(C^1\), cubic, non-rational spline curves. The structural reduction remains
\[
C\xrightarrow{D^2}q=C'',
\]
with \(q\) piecewise linear and possibly discontinuous at double knots.

The objective remains: simplify representation complexity under geometric tolerance. The current architecture is:

\[
\text{simplify in }C''	ext{ domain}
\rightarrow
\text{construct candidate}
\rightarrow
\text{certify geometric error}.
\]

---

## Stable foundation

### 1. Complexity reduction through \(C''\)

For \(C^1\) piecewise cubics,
\[
D^2:S_3^1\to PL_{disc}
\]
is onto with affine kernel. Jumps and kinks of \(C''\) correspond to knot multiplicity, so the second derivative domain is a natural representation-complexity domain.

### 2. Green synchronized error

For
\[
E=C-\widetilde C,\qquad e=C''-\widetilde C'',\qquad E(a)=E(b)=0,
\]
we have
\[
E=G_De.
\]
The synchronized displacement is exact, cheap, and certifiable for cubic spans.

### 3. Local normal correspondence layer

The earlier tangent/normal analysis is retained as a local geometric layer, not as a replacement for the original problem.

Define
\[
F(t,u)=(\widetilde C(t)-C(u))\cdot C'(u).
\]
A certified local normal branch satisfies
\[
F(t,\sigma(t))=0.
\]

The branch certificate uses fixed-degree sign tests:
\[
F(t,u_0)>0,
\quad F(t,u_1)<0,
\quad F_u(t,u)<0,
\quad F_t(t,u)>0.
\]

For cubic spans these remain low-degree polynomial tests suitable for Bernstein certification and local subdivision.

---

## Feasibility experiment result (Session 0011)

A Codex-generated experiment tested whether the local certificate is practical as a fast path.

Important interpretation:

- This is **not** a proof of the theory.
- Passing does **not** mean the simplification problem is solved.
- Failure would only expose limitations of the certificate.

Results:

- Ordinary close cubic pairs: 800/800 certified.
- 799/800 ordinary cases succeeded with subdivision depth 0–2.
- Near-self-approach negative controls: 124/160 certified; failures concentrated in the expected multi-normal / competing-branch regime.

The experiment supports continuing the local certificate as an engineering verification layer, but does not justify developing a full global normal theory.

---

## Updated research direction

The normal layer has passed its first feasibility gate. The next focus should return to the original bottleneck:

\[
\boxed{
\text{How to construct a low-complexity approximation of }q=C''?
}
\]

The previous work on Green and normal correspondence is now viewed as an error-certification framework:

\[
q\text{-simplification}
\rightarrow
\widetilde C
\rightarrow
\text{Green estimate}
\rightarrow
\text{optional normal verification}.
\]

The project should avoid spending excessive effort strengthening admissibility theory unless a concrete obstacle appears.

---

## Current status

- THEORY: stable first framework established.
- NORMAL CERTIFICATE: promising fast path, not a universal solution.
- CODE TEST: completed as feasibility evidence only.
- TEX NOTE: deferred.
- NEXT MAIN TASK: return to \(C''\)-domain simplification and candidate generation.
