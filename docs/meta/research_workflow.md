# Assistant-Led Research Workflow — Pilot Reflections

## Purpose

This project is the first deliberate trial in which the assistant is expected to carry a mathematical research branch forward with relatively little user involvement, while the user works on a different branch of the same larger problem.

This document is **not** about spline mathematics. It records what seems to help or hurt this style of collaboration so that the workflow can later be reused, revised, or rejected for larger research tasks.

It should be updated only when there is a real methodological lesson. Routine sessions do not need a meta-reflection.

---

## Current working model

The repository, not the chat transcript, is the canonical research state.

A useful session has five stages:

1. recover the current state from the repository;
2. choose one narrow falsifiable target;
3. work until that target is either established, rejected, or sharpened;
4. perform a correctness and goal-alignment review;
5. update all relevant documents in one session-level commit with a concise commit summary.

The emphasis is on **continuity and error control**, not on maximizing the amount of mathematics produced per conversation.

---

## Commit discipline

The first repository initialization used many single-file commits. That is workable mechanically but poor for research history because one intellectual session becomes fragmented across several commits.

Preferred policy from Session 0003 onward:

> **One substantive research conversation -> one logical commit whenever practical.**

The commit should bundle:
- derivation/result documents created during the session;
- frontier/roadmap changes caused by the result;
- the session log;
- user-facing state changes if something stable changed;
- occasional workflow/meta changes.

The commit message should contain a short title and a compact summary of the intellectual change.

Exceptions are allowed for:
- isolated typo or documentation repairs;
- user-authored changes that should stay distinct;
- literature ingestion unrelated to the active session;
- recovery from a failed/partial write.

This policy should make `git log` itself a coarse research diary.

---

## What counts as a good research session

A good session does not need a positive theorem. It needs a clear reduction in uncertainty.

Before work begins, state:
- the exact question;
- what would count as success;
- what would count as failure;
- what topics are explicitly out of scope for this session.

At the end, record:
- what was established;
- what was rejected or weakened;
- what new question appeared;
- confidence level;
- whether the work still serves the original engineering/scientific goal;
- the smallest sensible next action.

This is intended to prevent the common failure mode where a long derivation feels productive but has not actually changed the research state.

---

## Required review layers

### 1. Correctness review

A polished proof is not enough. Before accepting a result:
- check simple/degenerate cases;
- verify sign and scaling;
- test boundary cases and hidden regularity assumptions;
- distinguish equality, upper bound, asymptotic statement, and heuristic;
- actively search for a counterexample.

### 2. Goal-alignment review

Ask:
- does this result help simplify CAD splines under geometric tolerance?
- has the research drifted into an elegant but irrelevant functional-analysis problem?
- does the new object retain the computational advantage that motivated the transformation?
- are we optimizing a proxy merely because it is mathematically convenient?

If a result is correct but not useful, record that explicitly instead of promoting it to the main line.

### 3. Complexity review

When a theoretically better metric/operator is introduced, ask what it costs to evaluate or optimize. A new metric that is essentially as expensive as Hausdorff/Fréchet computation may defeat the purpose of the project.

---

## Documentation split

The current two-layer design appears useful.

### Internal layer

Optimized for research continuation by the assistant. It may contain:
- speculative hypotheses;
- abandoned routes;
- incomplete calculations;
- operational next steps;
- detailed session logs.

It should favor truthfulness over readability.

### User-facing layer

Optimized for a researcher joining later. It should contain:
- stable definitions and results;
- major negative conclusions;
- current interpretation;
- what remains open;
- enough motivation to understand why the current route exists.

It should not expose every transient branch of thought.

A future test of the workflow is whether the user can rejoin after many sessions by reading only the user-facing state plus any stage-level TeX note.

---

## When to write a TeX note

A TeX note is deliberately expensive and should mark a real stage boundary.

Good triggers:
- a coherent new theorem chain with meaningful consequence;
- a new metric/framework that survives counterexamples and yields an algorithmic route;
- a broad negative result that closes an important family of approaches;
- theory plus pseudocode that forms a self-contained method.

Bad trigger:
- a technically correct but routine lemma;
- a session that merely derives a classical identity;
- a result whose relevance is still unclear.

Markdown remains the default research medium.

---

## Current risks of assistant-led research

### Risk A — fluent overconfidence

The assistant can produce a long coherent derivation faster than it can establish that the derivation matters or is fully correct.

Control:
- narrow session scope;
- explicit counterexample search;
- correctness review;
- avoid immediate promotion to a polished TeX note.

### Risk B — mathematical drift

Open research makes it easy to follow whichever theory is locally interesting.

Control:
- end every theoretical session with a direct connection back to the original simplification goal;
- keep parked ideas in the roadmap rather than pursuing them immediately.

### Risk C — documentation becoming bureaucracy

Too much process can consume the research time it is meant to preserve.

Control:
- internal logs can be compact;
- update only documents whose state genuinely changed;
- meta reflection is occasional, not per-session;
- stage notes are rare.

### Risk D — repeated rediscovery across chats

Chat limits can erase local context.

Control:
- canonical frontier and roadmap;
- one session log per substantive conversation;
- one logical commit per session;
- explicit next action.

### Risk E — lack of human taste checks

An internally consistent route may still be uninteresting or misaligned with engineering reality.

Control:
- user-facing summaries should make the research direction easy to inspect;
- major pivots, failures, code-test thresholds, and literature blocks should be reported to the user promptly;
- the user will eventually rejoin and review stage-level results.

---

## Pilot success criteria

This workflow should be considered successful only if, after several sessions:

1. a new chat can resume with little reconstruction cost;
2. false starts are not repeatedly rediscovered;
3. the user can understand stable progress without reading internal logs;
4. important claims have explicit confidence/review status;
5. research sessions stay small enough to be critically reviewed;
6. repository history reflects intellectual steps rather than file-edit noise;
7. the process produces either useful theory, useful negative results, or sharply designed tests—not merely polished prose.

If these conditions fail, the workflow itself should be redesigned rather than defended.

---

## Reflection after Sessions 0002–0003

Early evidence is positive but limited.

What seems to work:
- a narrow target prevented Session 0002 from jumping prematurely into geometry;
- the goal-alignment review exposed the affine-gauge issue as a modeling choice;
- Session 0003 could build directly on the previous result without reconstructing the whole discussion;
- the roadmap was able to change: direct PL evaluation of the Green norm now appears more urgent than deriving every classical \(L^p\) operator constant.

What should improve:
- session commits should be bundled rather than file-by-file;
- future logs can be shorter when the derivation document already contains the mathematics;
- we should periodically check whether the user-facing summary is still enough for a human researcher to re-enter without reading internal material.

It is too early to conclude that the model scales to a large research program. This repository should remain a pilot until the first genuinely nontrivial stage result survives both assistant review and later user review.
