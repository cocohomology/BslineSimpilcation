# BslineSimpilcation

> Working repository for the theoretical study of spline simplification.  
> Repository name is intentionally left unchanged although the spelling is imperfect.

## 1. Purpose

This repository records an ongoing research program on **tolerance-constrained simplification of spline curves**, with special attention to cubic non-rational B-splines and to representations that are geometrically simple but parametrically complicated.

The current side project is deliberately narrower than the full spline-simplification problem:

> **Starting from a \(C^1\) cubic non-rational spline \(C\), use the fact that \(C''\) is piecewise linear to reformulate simplification as a low-complexity approximation problem in the second-derivative domain, while developing an error measure that is tighter and more geometry-aware than ordinary \(L^p\) norms but substantially easier to handle than the Hausdorff distance.**

This line of work runs in parallel with the user's close reading of the Lyche--Mørken series. It should therefore progress independently and preserve enough context that the user can join later without reconstructing chat history.

---

## 2. Documentation layers

### A. Internal research-control documents

Location: `docs/internal/`

These are primarily for research continuation by the assistant. They contain:
- the current research frontier;
- hypotheses under attack;
- failed approaches and counterexamples;
- the next small batch of tasks;
- derivations;
- session logs;
- requests for literature or code tests.

The user is not expected to read them routinely.

### B. User-facing research documents

Location: `docs/user/`

These are intended to let the user rejoin quickly. They contain:
- stable problem statements;
- established results;
- important negative conclusions;
- current interpretation;
- high-level research map;
- later, full TeX notes for stage-level breakthroughs.

### C. Meta-research workflow document

Location: `docs/meta/research_workflow.md`

This records lessons from using the project as a pilot for assistant-led research: session sizing, review standards, handoff quality, commit discipline, and failure modes. It is independent of the spline mathematics and should only be updated when there is a real methodological lesson.

---

## 3. Research principles

1. **Do not optimize for speed.** A thoroughly killed definition is useful progress.
2. **Keep sessions narrow.** Each substantive conversation should have one relatively clear target, explicit success/failure criteria, and explicit out-of-scope topics.
3. **Separate theorem, conjecture, heuristic, and experiment.**
4. **Actively search for counterexamples.** Especially bad parametrization, tiny knot spans, cancellation, near-singular geometry, and correspondence failure.
5. **Review every theoretical advance.** Check correctness, alignment with the original CAD goal, and computational consequences.
6. **Use computation only at the right stage.** First write pseudocode/test logic; no source code unless explicitly requested.
7. **Markdown by default.**
8. **TeX only for genuine stage-level results.** TeX notes must be self-contained enough for the user to read without internal logs.
9. **Record failures and pivots.** Do not erase dead ends that future sessions might rediscover.
10. **Do not confuse synchronized parameter error with geometric error.**
11. **Hausdorff remains the final geometric reference, not necessarily the optimization metric.**
12. **Keep the roadmap flexible.** A later session may reorder or abandon earlier planned directions when evidence changes.

---

## 4. Current stable mathematical state

Two exact reductions are now established for the endpoint-preserving cubic \(C^1\) setting.

### Representation complexity

For \(q=C''\), jumps of \(q\) correspond to double cubic knots, continuous kinks correspond to simple knots, and nonsingular breakpoints are redundant. Thus weighted singularity complexity of the PL second derivative exactly records minimal fixed-degree cubic representation complexity.

### Error transport

Let
\[
E=C-\widetilde C,\qquad e=C''-\widetilde C'',
\qquad E(a)=E(b)=0.
\]
Then
\[
E=G_De
\]
with the explicit fixed-endpoint Green kernel
\[
K_D(t,s)=
-\frac{(\min\{t,s\}-a)(b-\max\{t,s\})}{b-a}.
\]
Therefore
\[
N_G(e)=\|G_De\|_\infty
\]
is exactly the synchronized positional error under this gauge and satisfies
\[
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)\le N_G(e).
\]

The next target is not another abstract norm theorem. It is to determine how cheaply and rigorously \(N_G\) can be evaluated when \(e\) is piecewise linear.

---

## 5. How to resume this project in a new chat

If chat context is lost, proceed in this order:

1. Read this `README.md`.
2. Read `docs/user/current_state.md`.
3. Read `docs/internal/frontier.md`.
4. Read the newest file in `docs/internal/logs/`.
5. Read `docs/internal/roadmap.md`.
6. Choose only the next narrow research batch.
7. At the end of the session, update only documents whose state changed and commit them as one logical session-level commit whenever practical.

This repository, not chat memory, is the canonical state of this side project.

---

## 6. Commit policy

Preferred rule:

> **One substantive research conversation -> one logical commit.**

A session commit should bundle the mathematical derivation, log, frontier/roadmap changes, stable user-facing updates, and occasional meta-workflow changes caused by that session.

The commit message should summarize the intellectual change, not merely list filenames.

Small isolated fixes may remain separate.

---

## 7. Current document map

### User-facing
- `docs/user/current_state.md` — clean current state.
- `docs/user/research_map.md` — evolving high-level map.

### Internal
- `docs/internal/frontier.md` — exact current frontier, theorem status, risks.
- `docs/internal/roadmap.md` — short-horizon research plan.
- `docs/internal/protocol.md` — iteration/review/documentation rules.
- `docs/internal/derivations/d2_reconstruction.md` — exact \(D^2\) reduction and complexity dictionary.
- `docs/internal/derivations/fixed_endpoint_green.md` — fixed-endpoint Green operator and error interpretation.
- `docs/internal/logs/` — one log per substantive research conversation.

### Meta
- `docs/meta/research_workflow.md` — pilot reflections on assistant-led research.

Future stage-level mathematical notes belong under `notes/` as `.tex` files.
