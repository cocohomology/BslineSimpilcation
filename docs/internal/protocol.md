# Research Iteration Protocol — Internal

## Purpose

This file governs how the assistant should continue the research across multiple chats without relying on chat history as the primary memory.

The process is deliberately experimental. If it becomes bureaucratic or stops helping research quality, change it.

---

## At the start of every research session

1. Read `README.md`.
2. Read `docs/internal/frontier.md`.
3. Read `docs/internal/roadmap.md`.
4. Read the most recent session log.
5. Check whether the user has added new constraints, literature, or conclusions.
6. Pick a **small research batch**: ideally one theorem attempt, one counterexample program, or one sharply defined comparison.
7. State what is explicitly **out of scope** for this session.

Do not restart broad literature review unless a specific question requires it.

---

## Epistemic labels

Maintain four labels internally:

- **Established** — proved/reviewed in-session or directly supported by a reliable source.
- **Plausible** — coherent but not yet proved.
- **Heuristic** — intuition or design hypothesis only.
- **Rejected** — false, structurally unhelpful, or too loose for the intended purpose.

When a claim looks strong, actively try to break it before promotion.

---

## Theory workflow

For each candidate theorem or definition:

1. state assumptions precisely;
2. reduce to the simplest nontrivial case;
3. check signs, units, and scaling;
4. test degenerate/boundary cases;
5. search for a counterexample;
6. derive the claim;
7. distinguish exact identity, one-sided bound, asymptotic result, and heuristic;
8. check short knot spans / singular limits when relevant;
9. check parametrization sensitivity when geometry is involved;
10. decide whether the result is useful, not only correct.

A polished derivation is not evidence of truth.

---

## Mandatory end-of-theory review

Every session with a theoretical result must include three reviews.

### Correctness review

Ask whether the statement is actually proved under its stated assumptions and whether simple counterexamples were checked.

### Goal-alignment review

Ask whether the work still advances the original goal: tolerance-constrained simplification of CAD splines. Explicitly flag elegant mathematics that does not help the target problem.

### Complexity review

If a new metric/operator is proposed, ask what it costs to evaluate or optimize. A surrogate that becomes as difficult as direct Hausdorff/Fréchet computation may defeat the project purpose.

---

## Literature workflow

Use literature for one of three reasons:

- identify whether an emerging object/result is already known;
- import a theorem needed for the next proof;
- compare the emerging framework against a mature alternative.

Avoid scope expansion for its own sake. Shape spaces, elastic metrics, reach theory, Fréchet distance, etc. should only be opened when a concrete internal question points there.

If a critical source is unavailable, log:
- title/authors/year if known;
- why it matters;
- what result is needed;
- whether the user should obtain it.

---

## Computation workflow

Numerical work begins only after a clear theoretical question is stated.

Before any implementation, write:
- input;
- output;
- invariant/quantity being tested;
- pseudocode;
- expected scaling/theorem prediction;
- falsification criterion.

Do not write production source code unless the user explicitly asks.

Computation may kill a conjecture, expose hidden dependence, estimate sharpness, or compare candidate rankings. It does not substitute for proof when a certified theorem is claimed.

---

## Documentation rules

### Internal layer

Update only documents whose state genuinely changed:
- `frontier.md` — current exact questions/results;
- `roadmap.md` — short-horizon priorities;
- `logs/YYYY-MM-DD_session-XXXX.md` — always create one per substantive research conversation;
- derivations/counterexamples as needed.

A session log should record:
- objective and out-of-scope items;
- main result or failure;
- unexpected idea;
- correctness/goal/complexity review;
- confidence;
- exact next action;
- whether user/literature/code help is needed.

Do not duplicate a long derivation in the log if it already has its own file.

### User-facing layer

Update `docs/user/current_state.md` only for stable changes.

Update `docs/user/research_map.md` only when the global map changes materially.

Do not flood user-facing docs with transient calculations.

### TeX notes

Create a TeX note under `notes/` only for a real stage-level result. It must be self-contained enough that the user need not read internal logs.

---

## Commit discipline

Preferred policy:

> **One substantive research conversation -> one logical Git commit whenever practical.**

Bundle the session's derivation, log, frontier/roadmap changes, stable user-facing updates, and any relevant meta-process update into the same commit.

The commit message should have:
- a concise session/result title;
- a short summary of the intellectual change and next direction.

Avoid one-file-per-commit noise unless a technical recovery or isolated fix requires it.

This makes `git log` a coarse research history.

---

## Meta-workflow reflection

`docs/meta/research_workflow.md` records lessons about assistant-led research itself.

Do **not** update it every session. Update only when:
- a workflow rule proves useful/useless;
- a recurring failure mode appears;
- handoff/recovery quality changes;
- the user or assistant identifies a practice worth carrying into future research projects.

---

## End-of-session report to the user

Keep the chat summary decision-oriented:
- what was attacked;
- what succeeded;
- what failed or remained unresolved;
- whether the main direction looks stronger/weaker;
- what the next narrow target is;
- whether literature/user/code help is needed.

Explicitly flag:
- **THEORETICAL FAILURE**
- **STAGE BREAKTHROUGH**
- **CODE TEST NEEDED**
- **LITERATURE NEEDED**

when applicable.

## Research integrity rule

The goal is to reduce uncertainty, not to maximize the apparent completeness of the documentation.
