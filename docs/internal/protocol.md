# Research Iteration Protocol — Internal

## Purpose

This file governs how the assistant should continue the research across multiple chats without relying on chat history as the primary memory.

## At the start of every research session

1. Read `README.md`.
2. Read `docs/internal/frontier.md`.
3. Read `docs/internal/roadmap.md`.
4. Read the most recent session log.
5. Check whether the user has added new constraints, literature, or conclusions elsewhere in the project.
6. Pick a **small research batch**. Prefer one theorem attempt, one counterexample program, or one sharply defined comparison.

Do not restart broad literature review unless the roadmap explicitly calls for it.

## During the session

Maintain four epistemic labels:

- **Established** — proved in-session or directly supported by a cited source.
- **Plausible** — coherent but not yet proved.
- **Heuristic** — useful intuition only.
- **Rejected** — false, structurally unhelpful, or too loose for the intended purpose.

When a claim looks strong, actively try to break it before promoting it.

## Theory workflow

For each candidate theorem or definition:

1. State assumptions precisely.
2. Reduce to the lowest-dimensional/simple case possible.
3. Test degenerate cases.
4. Search for a counterexample.
5. Derive the claim.
6. Check units/scaling.
7. Check reparametrization sensitivity.
8. Check very short knot spans.
9. If geometry is involved, check normal-correspondence uniqueness and near self-approach.
10. Only then decide whether the result is stable enough to preserve.

## Literature workflow

Use literature for one of three reasons only:

- identify whether the object/result is already known;
- import a theorem needed for the next proof;
- compare the emerging framework against a mature alternative.

Avoid uncontrolled scope expansion. Shape analysis, elastic metrics, Sobolev metrics, Fréchet distance, reach theory, etc. should only be opened when a specific internal question points there.

If a critical paper is unavailable, log:
- exact title/authors/year if known;
- why it matters;
- what theorem or definition is needed from it;
- whether the user should be asked to obtain it.

## Computation workflow

Numerical work is allowed only after a clear theoretical question is stated.

Before any implementation, write:
- input;
- output;
- invariant/quantity being tested;
- pseudocode;
- expected scaling or theorem prediction;
- falsification criterion.

Do not write production source code unless the user explicitly asks.

Computation may:
- kill a conjecture;
- expose a hidden parameter dependence;
- estimate sharpness;
- compare rankings of candidate metrics.

Computation may **not** substitute for proof when a certified theorem is claimed.

## Documentation rules

### Internal layer

Update after each substantial session:
- `frontier.md` — only if the frontier changed;
- `roadmap.md` — if next priorities changed;
- `logs/YYYY-MM-DD_session-XXXX.md` — always append a new log.

Internal logs should include:
- objective;
- work performed;
- successful results;
- failed attempts;
- current confidence;
- exact next action;
- whether user input/literature is needed.

### User-facing layer

Update `docs/user/current_state.md` only for stable changes.

Update `docs/user/research_map.md` when the global direction changes.

Do not flood user-facing docs with transient calculations.

### TeX notes

Create a TeX note under `notes/` only if there is a stage-level result worth reading independently.

A TeX note should contain:
- motivation;
- precise setting;
- relevant background;
- definitions;
- lemmas/theorems with proofs;
- counterexamples/limitations;
- algorithmic consequence if any;
- open questions.

It should not assume the user has read the internal logs.

## End-of-session report to the user

Keep the chat summary short and decision-oriented:

- what was attacked;
- what succeeded;
- what failed;
- whether the main direction looks stronger/weaker;
- what will be attempted next;
- whether any literature or user help is needed.

Explicitly flag any of the following:
- **THEORETICAL FAILURE** — a major candidate direction is dead;
- **STAGE BREAKTHROUGH** — a result is strong enough to justify a TeX note;
- **CODE TEST NEEDED** — theory reached a point where numerical falsification/validation is the correct next step;
- **LITERATURE NEEDED** — progress is blocked on a source not currently available.

## Research integrity rule

A polished derivation is not evidence of truth. The goal is to reduce uncertainty, not to maximize the apparent completeness of the documentation.
