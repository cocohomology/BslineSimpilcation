# BslineSimpilcation

> Working repository for the theoretical study of spline simplification.  
> Repository name is intentionally left unchanged although the spelling is imperfect.

## 1. Purpose

This repository records an ongoing research program on **tolerance-constrained simplification of spline curves**, with special attention to cubic non-rational B-splines and to representations that are geometrically simple but parametrically complicated.

The current side project is deliberately narrower than the full spline-simplification problem:

> **Starting from a \(C^1\) cubic non-rational spline \(C\), use the fact that \(C''\) is piecewise linear to reformulate simplification as a low-complexity approximation problem in the second-derivative domain, while developing an error measure that is tighter and more geometry-aware than ordinary \(L^p\) norms but substantially easier to handle than the Hausdorff distance.**

This line of work runs in parallel with the user's close reading of the Lyche--Mørken series. It should therefore progress independently and preserve enough context that the user can join later without reconstructing the entire history from chat logs.

---

## 2. Two documentation layers

The repository intentionally separates two kinds of documents.

### A. Research-control documents (primarily for the assistant)

These documents are operational. They preserve context between conversations and prevent repeated work.

Location: `docs/internal/`

They contain:
- the current research frontier;
- hypotheses under attack;
- failed approaches and counterexamples;
- the next small batch of tasks;
- iteration rules;
- requests for literature or outside help;
- session logs.

The user is not expected to read these.

### B. User-facing research documents

Location: `docs/user/`

These documents are designed so that the user can quickly re-enter the project after spending time elsewhere. They contain:
- the stable problem statement;
- established results;
- major failed directions that should not be repeated;
- the current research map;
- concise progress summaries;
- later, complete TeX notes for genuine stage-level breakthroughs.

The user-facing layer should remain much cleaner than the internal logs.

---

## 3. Research principles

1. **Do not optimize for speed.** A failed definition that is thoroughly killed is useful progress.
2. **Separate theorem, conjecture, heuristic, and experiment.** Never silently upgrade one into another.
3. **Actively search for counterexamples.** In particular: bad parametrization, very short knot spans, cancellation after integration, nearly singular geometry, and correspondence failure.
4. **Use computation only at the right stage.** When theory reaches a point that needs numerical testing, first write clear pseudocode and test logic. Do not implement source code in this research repository unless the user later explicitly requests it.
5. **Markdown by default.** Most research notes and logs should be `.md`.
6. **TeX only for genuine stage-level results.** When a result becomes coherent enough to deserve a self-contained mathematical note, write it in `.tex`, with sufficient background that the user can read it without having followed all previous assistant-only work.
7. **Record failures.** A discarded definition, false conjecture, or unacceptably loose bound should be documented before moving on.
8. **Prefer small, falsifiable research steps.** Each session should advance one or two concrete questions instead of attempting a full theory at once.
9. **Do not confuse parametrized error with geometric error.** Any norm on \(C-\tilde C\) or \(C''-\tilde C''\) must be explicitly interpreted with respect to parametrization.
10. **Hausdorff distance remains the final geometric reference, not necessarily the optimization metric.**

---

## 4. Current research state

### Stable observations

For a \(C^1\) cubic non-rational spline \(C:[a,b]\to\mathbb R^d\):

- \(C''\) is piecewise linear, possibly discontinuous at double knots;
- if a candidate second derivative \(\tilde q\) is chosen and suitable boundary data are supplied, integrating twice produces a piecewise cubic candidate \(\tilde C\);
- therefore knot simplification of \(C\) can potentially be reframed as simplification of a piecewise-linear object;
- for fixed endpoint conditions, the map from second-derivative error to positional error is a linear Green operator;
- ordinary \(L^p\) norms discard cancellation and spatial influence too early and may therefore be substantially looser than necessary;
- a purely parametrization-dependent norm cannot by itself be equivalent to Hausdorff distance;
- promising intermediate ideas include Green-induced norms, normal-projected Green error, and geometry-aware correspondences inspired by normal-distance constructions.

### Main open question

Find an error quantity on the second-derivative side that satisfies as many of the following as possible:

1. computable on piecewise-linear data;
2. significantly tighter than ordinary \(L^p\) estimates;
3. stable enough for engineering use;
4. partially insensitive to bad parametrization;
5. strong enough to control or closely track geometric error;
6. structured enough to support low-complexity approximation algorithms.

---

## 5. How to resume this project in a new chat

If chat context is lost or a new conversation is opened, proceed in this order:

1. Read this `README.md`.
2. Read `docs/user/current_state.md` for the user-facing stable picture.
3. Read `docs/internal/frontier.md` for the exact current research frontier.
4. Read the newest file in `docs/internal/logs/`.
5. Read `docs/internal/roadmap.md` before choosing the next task.
6. Continue only one small batch of work at a time.
7. At the end of every substantial research session:
   - update `docs/internal/frontier.md`;
   - append a new session log;
   - update `docs/internal/roadmap.md` if priorities changed;
   - update `docs/user/current_state.md` only if something stable changed;
   - create/update a TeX note only if a real stage-level result has emerged.

This repository, not chat memory, is the canonical state of this side project.

---

## 6. Current document map

- `docs/user/current_state.md` -- clean state summary for the user.
- `docs/user/research_map.md` -- evolving high-level map of the research program.
- `docs/internal/frontier.md` -- exact current questions, hypotheses, and risks.
- `docs/internal/roadmap.md` -- short-horizon task plan; expected to change frequently.
- `docs/internal/protocol.md` -- research iteration protocol and documentation rules.
- `docs/internal/logs/2026-09-13_session-0001.md` -- first session initialization log.

Future stage-level mathematical notes should go under `notes/` as `.tex` files.
