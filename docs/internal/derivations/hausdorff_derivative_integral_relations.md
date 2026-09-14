# Hausdorff Distance versus Differentiation and Integration of Curves

Session 0015 side investigation.

## 1. Question

The project has mostly treated Hausdorff distance as a final geometric target to be upper-bounded indirectly. This note asks the opposite question directly:

> If two curve images are close in Hausdorff distance, must their derivative curves or integral curves also be close? Conversely, when can differential/integral information control Hausdorff distance, and what constants appear?

The answer is strongly asymmetric.

At the level of unparameterized curve images, Hausdorff distance alone controls neither differentiation nor integration. Two additional structures are required before positive estimates become possible:

1. an **ordered correspondence** between points of the two curves;
2. a **regularity scale**, such as a curvature/reach bound or a higher-derivative bound.

This distinction is directly relevant to the current normal-branch work: a globally stitched normal branch is precisely a device for supplying the missing correspondence.

---

## 2. Pure geometry: derivative vectors are not even shape invariants

Let

\[
\Gamma=[0,1]\times\{0\}.
\]

Take

\[
\gamma(t)=(t,0),
\]

and for \(k>0\),

\[
\widetilde\gamma_k(t)=\bigl(\phi_k(t),0\bigr),
\qquad
\phi_k(t)=\frac{e^{kt}-1}{e^k-1}.
\]

Every \(\phi_k\) is a smooth increasing diffeomorphism of \([0,1]\), so

\[
\operatorname{Im}\gamma
=
\operatorname{Im}\widetilde\gamma_k
=\Gamma,
\]

and hence

\[
d_H(\operatorname{Im}\gamma,\operatorname{Im}\widetilde\gamma_k)=0.
\]

However,

\[
\widetilde\gamma_k'(t)
=
\left(\frac{k e^{kt}}{e^k-1},0\right),
\]

whose maximum speed is asymptotic to \(k\). Thus the derivative vectors can differ arbitrarily while Hausdorff distance is exactly zero.

The obstruction is not geometric roughness. It is simply that the velocity vector depends on parameterization.

Therefore the correct geometric first-derivative object is not \(C'(t)\) but the tangent **line** (or an oriented unit tangent after an orientation has been fixed).

---

## 3. Even tangent directions are not continuous in Hausdorff distance without regularity

Parameterization ambiguity can be removed by looking only at tangent directions. Hausdorff distance is still too weak.

Let

\[
\Gamma_0=\{(x,0):0\le x\le1\},
\]

and

\[
\Gamma_n
=\left\{\left(x,\frac1n\sin(nx)\right):0\le x\le1\right\}.
\]

Then

\[
d_H(\Gamma_n,\Gamma_0)\le \frac1n\to0.
\]

But the graph slope is

\[
y_n'(x)=\cos(nx),
\]

so at infinitely many points the tangent angle relative to the horizontal is \(\pi/4\) in magnitude. Reparameterizing by arc length does not change this tangent direction.

Hence

\[
d_H(\Gamma_n,\Gamma_0)\to0
\]

does **not** imply uniform convergence of tangent directions.

The price paid by this example is unbounded curvature:

\[
\kappa_n(x)
=
\frac{n|\sin(nx)|}{(1+\cos^2(nx))^{3/2}}.
\]

This already suggests the correct scale of any positive theorem: Hausdorff closeness must be combined with a second-order regularity bound.

---

## 4. Bounded curvature still does not recover curvature from Hausdorff distance

Even a uniform curvature bound is enough only for first-derivative stability, not for second-derivative stability.

Consider

\[
\widehat\Gamma_n
=\left\{\left(x,\frac1{n^2}\sin(nx)\right):0\le x\le1\right\}.
\]

Then

\[
d_H(\widehat\Gamma_n,\Gamma_0)\le \frac1{n^2}\to0,
\]

and

\[
y_n'(x)=\frac1n\cos(nx)\to0
\]

uniformly, so tangent directions converge.

But

\[
y_n''(x)=-\sin(nx),
\]

and the geometric curvature satisfies

\[
\kappa_n(x)
=
\frac{|\sin(nx)|}{\left(1+n^{-2}\cos^2(nx)\right)^{3/2}},
\]

which remains order one. Thus the line has zero curvature while the nearby curves have order-one curvature oscillations.

So even

- Hausdorff convergence,
- regular embedded curves,
- a uniform curvature bound,
- and uniform tangent convergence

still do not force curvature convergence.

To recover a second derivative from a \(C^0\) geometric perturbation one needs one more level of regularity, e.g. a bound on the third derivative / curvature variation.

This is important for the current project: no equivalence of the form

\[
d_H(C,\widetilde C)\ll1
\quad\Longrightarrow\quad
\|C''-\widetilde C''\|\ll1
\]

can hold in the present generality.

---

## 5. Integration is also not controlled by shape alone

Using the same reparameterized segment as in Section 2, define the antiderivative curves

\[
A(t)=\int_0^t\gamma(s)\,ds,
\qquad
\widetilde A_k(t)=\int_0^t\widetilde\gamma_k(s)\,ds.
\]

Although the original image sets are identical, at \(t=1\),

\[
A(1)=\left(\frac12,0\right),
\]

while

\[
\widetilde A_k(1)
=
\left(
\frac1k-\frac1{e^k-1},0
\right)
\longrightarrow (0,0).
\]

Thus Hausdorff distance zero does not control an antiderivative when the parameter measure is allowed to change.

The reason is again structural: integration remembers **order, multiplicity, and speed**, all of which Hausdorff distance discards.

---

## 6. Once a correspondence is fixed, integration is stable

Let \(f,g:[a,b]\to\mathbb R^d\), and let \(L=b-a\). If

\[
\|f-g\|_\infty\le\delta,
\]

then for

\[
F(t)=F(a)+\int_a^t f(s)\,ds,
\qquad
G(t)=G(a)+\int_a^t g(s)\,ds,
\]

we have

\[
\boxed{
\|F-G\|_\infty
\le
\|F(a)-G(a)\|+L\delta.
}
\]

In particular, for two parameterized curves,

\[
\|C'-\widetilde C'\|_\infty\le\delta
\]

and one aligned initial point imply

\[
\|C-\widetilde C\|_\infty\le L\delta.
\]

This is the basic asymmetry:

- integration is a bounded smoothing operator;
- differentiation is not a bounded operator in the \(C^0\) norm.

The fixed-endpoint Green estimate used in the main project is the second-order version of the same fact. If

\[
E=C-\widetilde C,
\qquad E(a)=E(b)=0,
\qquad \|E''\|_\infty\le\eta,
\]

then

\[
\boxed{
\|E\|_\infty
\le
\frac{L^2}{8}\eta.
}
\]

The constant \(L^2/8\) is the exact \(L^\infty\to L^\infty\) operator norm of the Dirichlet Green inverse of \(D^2\). It is attained by a constant second-derivative error in one fixed vector direction.

---

## 7. Conditional inverse estimate: position plus second-order regularity controls tangent

The instability of differentiation disappears if an a priori second-derivative bound is supplied.

Let

\[
E:[a,b]\to\mathbb R^d
\]

be \(C^2\), with

\[
\|E\|_\infty\le\varepsilon,
\qquad
\|E''\|_\infty\le M.
\]

For a point \(t\) and any \(h>0\) such that \([t-h,t+h]\subset[a,b]\), Taylor's theorem at \(t\) gives

\[
E(t+h)-E(t-h)
=2hE'(t)+R,
\qquad
\|R\|\le Mh^2.
\]

Therefore

\[
\boxed{
\|E'(t)\|
\le
\frac{\varepsilon}{h}+\frac{Mh}{2}.
}
\]

If

\[
h_*=\sqrt{\frac{2\varepsilon}{M}}
\]

fits inside the interval on both sides, optimization yields

\[
\boxed{
\|E'(t)\|
\le
\sqrt{2M\varepsilon}.
}
\]

At an endpoint, the analogous one-sided estimate is

\[
\|E'(a)\|
\le
\frac{2\varepsilon}{h}+\frac{Mh}{2},
\]

which optimizes to

\[
\boxed{
\|E'(a)\|
\le
2\sqrt{M\varepsilon}
}
\]

when the optimal \(h=2\sqrt{\varepsilon/M}\) is available.

### Arc-length interpretation

Suppose two curves are already expressed under one synchronized arc-length correspondence and both have curvature bounded by \(K\). Then

\[
\|E''\|_\infty
\le
\|C''\|_\infty+\|\widetilde C''\|_\infty
\le 2K.
\]

For interior points,

\[
\boxed{
\|T-\widetilde T\|
\le
2\sqrt{K\varepsilon}.
}
\]

Since for unit vectors

\[
\|T-\widetilde T\|=2\sin\frac\theta2,
\]

we get

\[
\boxed{
\sin\frac\theta2
\le
\sqrt{K\varepsilon}.
}
\]

Thus the natural inverse stability scale is **square root**, not linear in the positional error.

This square-root scaling is sharp in order: a bounded-curvature bump of height \(\varepsilon\) can turn through an angle of order \(\sqrt{K\varepsilon}\) over a lateral scale of order \(\sqrt{\varepsilon/K}\).

This theorem is about a fixed synchronized correspondence. Hausdorff distance alone does not supply that correspondence.

---

## 8. From Hausdorff closeness to tangent closeness: reach is the natural geometric scale

For an embedded \(C^2\) curve \(\Gamma\), the **reach** \(\tau\) is the radius of the largest tubular neighbourhood in which nearest-point projection onto \(\Gamma\) is unique.

Positive reach simultaneously controls two effects relevant here:

1. local curvature: roughly \(\kappa\le1/\tau\);
2. global self-approach: distinct remote pieces cannot create a nearer projection inside the \(\tau\)-tube.

A standard reach estimate is

\[
\operatorname{dist}(q,T_p\Gamma)
\le
\frac{\|q-p\|^2}{2\tau},
\qquad p,q\in\Gamma,
\]

and tangent spaces along the same positive-reach manifold satisfy

\[
\sin\frac{\angle(T_p\Gamma,T_q\Gamma)}2
\le
\frac{\|p-q\|}{2\tau}.
\]

These facts are classical consequences of Federer reach theory and are used in modern manifold-reconstruction literature.

Now suppose two embedded curves have Hausdorff distance \(\varepsilon\) and both have a common reach lower bound \(\tau\), with \(\varepsilon\ll\tau\). At a local length scale \(r\), two errors compete:

- set-position uncertainty contributes about \(\varepsilon/r\) to a secant/tangent angle;
- curvature contributes about \(r/\tau\).

Hence one expects

\[
\theta
\lesssim
\frac{\varepsilon}{r}+\frac r\tau.
\]

Optimizing at

\[
r\asymp\sqrt{\varepsilon\tau}
\]

gives

\[
\boxed{
\theta
=O\!\left(\sqrt{\frac{\varepsilon}{\tau}}\right).
}
\]

This square-root Hausdorff-to-tangent scale is standard in smooth-manifold reconstruction. The exact constant depends on the chosen point correspondence and boundary hypotheses; this note does not claim a new sharp cross-manifold theorem.

The important point for the spline project is the structure:

> Hausdorff + reach/correspondence can control tangent lines, but Hausdorff alone cannot.

---

## 9. Why second derivatives remain fundamentally harder

The example in Section 4 shows that a curvature bound is not enough to make curvature depend continuously on Hausdorff distance.

This is a special case of the interpolation hierarchy. Schematically, if a synchronized error \(E\) satisfies a highest-derivative bound

\[
\|E^{(m)}\|_\infty\le M_m,
\]

then intermediate derivatives obey estimates of Landau--Kolmogorov / Gagliardo--Nirenberg type

\[
\|E^{(k)}\|_\infty
\lesssim
\|E\|_\infty^{1-k/m}
M_m^{k/m},
\qquad 0<k<m,
\]

up to finite-interval boundary terms.

For tangent control, \(k=1,m=2\) gives the square-root law.

For curvature/second-derivative control from positional error, one needs at least one more derivative, e.g. \(k=2,m=3\), leading to a cube-root-type scale rather than a direct Hausdorff equivalence.

Therefore the current derivative-domain variable

\[
q=C''
\]

should not be expected to be recoverable from geometry alone under the project's present assumptions.

---

## 10. Hausdorff versus Fréchet: the missing ingredient is order

Hausdorff distance compares only image sets. It forgets the order in which points are traversed.

For parameterized curves, the Fréchet distance instead minimizes the maximum pointwise discrepancy over monotone reparameterizations. In particular,

\[
d_H(\operatorname{Im}C,\operatorname{Im}\widetilde C)
\le d_F(C,\widetilde C).
\]

A globally stitched monotone normal branch

\[
u=\sigma(t)
\]

with endpoint coverage provides one explicit Fréchet-type matching:

\[
d_F(C,\widetilde C)
\le
\max_t\|\widetilde C(t)-C(\sigma(t))\|.
\]

If \(\sigma\) is a homeomorphism onto the full reference interval, the same matching immediately bounds both directed Hausdorff distances and therefore the symmetric Hausdorff distance.

This reframes the current main-line stitching problem:

> the local normal-branch machinery is not trying to compute nearest points globally; it is constructing a certified order-preserving lift from set geometry to a Fréchet-style correspondence.

Once that lift exists, differential comparisons become meaningful as well, because one can differentiate

\[
C(\sigma(t))
\]

and track the additional factor \(\sigma'(t)\).

---

## 11. Consequences for the spline-simplification project

This side investigation gives several durable conclusions.

### 11.1 The main architecture is necessarily asymmetric

The direction

\[
C''-\widetilde C''
\longrightarrow
C-\widetilde C
\]

is stable because integration smooths. This is why the Green operator is useful.

The reverse direction

\[
\text{small geometric/Hausdorff error}
\longrightarrow
\text{small }C''-\widetilde C''
\]

is false without substantially stronger regularity assumptions.

Therefore q-space error should be used as a **sufficient certificate / candidate-construction coordinate**, not as something geometrically equivalent to Hausdorff distance.

### 11.2 The complexity of the normal-correspondence layer is not accidental

Hausdorff distance by itself contains too little information to support derivative arguments. An ordered correspondence must be supplied somehow.

The present normal-branch certificate is one computable way to build that missing structure for close CAD curves.

### 11.3 Reach is the natural geometric constant, but not automatically the right algorithm

Theoretical control from Hausdorff distance to tangent variation is naturally expressed in terms of reach or local feature size. This is conceptually valuable because it identifies the correct dimensionless parameter

\[
\frac{\varepsilon}{\tau}.
\]

But globally computing reach may be as hard as the geometric problem itself. The current local Bernstein certificate can be viewed as a local algebraic substitute for assuming a globally known reach.

### 11.4 Do not seek a two-sided equivalence between Hausdorff and q-space norms

The side branch argues against spending research time trying to prove

\[
\|q-\widetilde q\|
\asymp
 d_H(C,\widetilde C)
\]

under the current model. Such an equivalence is structurally false.

The more realistic hierarchy is

\[
\text{q-space candidate}
\to
\text{integrated positional bound}
\to
\text{certified ordered correspondence}
\to
\text{Hausdorff / Fréchet-style geometric acceptance}.
\]

---

## 12. Status of this side task

Established in this note:

- pure Hausdorff distance does not control velocity vectors, tangent directions, antiderivatives, or curvature;
- even bounded curvature plus Hausdorff convergence does not force curvature convergence;
- with a fixed correspondence and a second-derivative bound, a square-root positional-to-tangent estimate follows explicitly;
- derivative-to-position control is linear under one integration and has the exact \(L^2/8\) Green coefficient under fixed-endpoint double integration;
- positive reach supplies the correct geometric regularity scale, with Hausdorff-to-tangent stability of order \(\sqrt{\varepsilon/\tau}\) under suitable local matching assumptions;
- the current normal-branch construction is naturally interpreted as an order-preserving Fréchet-style lift, not merely as a nearest-point device.

Not established:

- a sharp global constant relating Hausdorff distance of two arbitrary positive-reach curves to the distance of their tangent bundles;
- a global theorem that the present local normal branches automatically stitch into a homeomorphism;
- any inverse control of \(C''\) from Hausdorff distance under the current cubic \(C^1\) assumptions.

The side task is therefore useful but does not replace the current main-line global-stitching problem.

## References consulted for geometric regularity

- H. Federer, *Curvature Measures*, 1959 (reach and tubular-neighbourhood framework).
- J.-D. Boissonnat, A. Lieutier, M. Wintraecken, *The reach, metric distortion, geodesic convexity and the variation of tangent spaces*, Journal of Applied and Computational Topology, 2019.
- Modern manifold-reconstruction literature using the same reach/curvature scaling, in which tangent accuracy naturally appears at order \(\sqrt{\varepsilon/\tau}\).
