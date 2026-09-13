# Experiment Plan — Local Normal-Branch Certificate

Session 0009 follow-up gate. Pseudocode only; no production source code.

## Purpose

Before proving a stronger admissibility theorem, measure whether the simple cubic span-box sign certificate is already permissive enough for ordinary close-curve cases.

The experiment is not a performance benchmark. It is a research gate against abstraction drift.

## Inputs

Prepare small families of regular cubic or piecewise-cubic reference/candidate pairs:

1. small normal perturbation;
2. mild tangential reparameterization;
3. mixed normal + tangential perturbation;
4. nonuniform parameter speed / short spans;
5. moderate high-curvature region;
6. one near-self-approach case as an expected difficult/negative control.

Include both same-knot and changed-knot candidates where convenient, because the eventual simplification problem changes knot structure.

## Core quantities

For each candidate span \(T\) and nearby reference span/window \(U\), define
\[
F(t,u)=(\widetilde C(t)-C(u))\cdot C'(u),
\]
\[
F_u(t,u)=-\|C'(u)\|^2+(\widetilde C(t)-C(u))\cdot C''(u),
\]
\[
F_t(t,u)=\widetilde C'(t)\cdot C'(u).
\]

Use the Green-based predictor
\[
\sigma_0=t-\frac{E\cdot C'}{\|C'\|^2}
\]
or the Newton predictor
\[
\sigma_N=t-\frac{E\cdot C'}{\|C'\|^2+E\cdot C''}
\]
to center the initial reference window.

## Pseudocode

```text
for each test curve pair (C, Ctilde):
    build union/span data and synchronized Green error E = C - Ctilde

    for each candidate cubic span T:
        estimate predictor range P(T) from sigma0 or sigmaN
        choose initial nearby reference window U containing P(T)
        depth = 0

        while depth <= MAX_DEPTH:
            represent on T x U in tensor-product Bernstein form:
                F(t,u)
                Fu(t,u)
                Ft(t,u)

            certify:
                left_sign  := F(t, u_left) > 0 for all t in T
                right_sign := F(t, u_right) < 0 for all t in T
                decreasing := Fu(t,u) < 0 on T x U
                oriented   := Ft(t,u) > 0 on T x U

            if all four certificates pass:
                mark span CERTIFIED
                break

            if signs strongly indicate wrong window:
                enlarge or shift U once using predictor information
            else:
                subdivide T (and U only if necessary)
                depth += 1

        if not certified:
            mark span FALLBACK

        independently compute/approximate actual nearby normal roots
        only for validation of the experiment
        compare chosen local branch with the true nearby branch

collect statistics
```

## Recorded statistics

For each family record:
- fraction of spans certified at depth 0;
- fraction certified after 1, 2, ... subdivisions;
- fallback fraction;
- initial and final window width relative to span length;
- failures caused by \(F_u\) versus boundary signs versus \(F_t\);
- whether predictor \(\sigma_0\) or \(\sigma_N\) gave tighter windows;
- whether the certified root agrees with an independent nearest/local-normal computation;
- minimum speed and rough curvature to correlate conditioning with failures.

## Decision rule

Promising:
- normal close cases certify mostly at depth 0–2;
- failures concentrate in deliberately ambiguous cases;
- Newton predictor materially reduces box size or subdivisions.

Unpromising:
- ordinary mild perturbations frequently fail;
- deep subdivision is routine;
- branch windows must become so large that the test resembles a global two-parameter search.

If unpromising, do **not** respond by proving a much more elaborate admissibility theorem. Reconsider the architecture first.
