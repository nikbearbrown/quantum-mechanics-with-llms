# Chapter 5 — Quantum Mechanics in Three Dimensions
*One angular equation to rule them all.*

---

Open any chemistry textbook to the page on atomic orbitals and you will find beautiful pictures: spheres, dumbbells, four-leaf clovers, a donut. The story is that electrons "occupy" these shapes. Before you accept this, ask a harder question: *what exactly is the picture showing?*

Is it the wave function $\psi$? The probability density $|\psi|^2$? The angular part only, or the full thing with the radial factor included? Is the shape what the electron *is*, or the distribution of where you would *find* it?

The answers are specific, and they correct something the pictures quietly get wrong. The shapes are the angular probability density $|Y_{\ell m}(\theta,\phi)|^2$, not the full wave function. The "p-orbitals" in chemistry are not the $Y_1^{\pm 1}$ states of physics — they are real linear combinations of $Y_1^{\pm 1}$ and $Y_1^0$, chosen because they point conveniently along the Cartesian axes. The complex spherical harmonics physics uses (eigenstates of the $z$-component of angular momentum) and the real combinations chemistry uses (not eigenstates of any component of angular momentum) are different states of the same energy. The pictures are not wrong, exactly, but they are showing you something more specific than they admit.

That is the payoff at the end of this chapter. The path to it begins with a fortunate accident.

---

## The accident

The three-dimensional Schrödinger equation is

$$-\frac{\hbar^2}{2m}\nabla^2\psi(\vec r) + V(\vec r)\psi(\vec r) = E\psi(\vec r).$$

In Cartesian coordinates, $\nabla^2 = \partial_x^2 + \partial_y^2 + \partial_z^2$. Three variables tangled together. For a general potential $V(\vec r)$, you cannot disentangle them. The problem is genuinely three-dimensional.

The accident is this: the most physically important potentials depend only on the distance $r$, not on direction. The Coulomb potential $-e^2/(4\pi\epsilon_0 r)$ in the hydrogen atom. The confining potential in a nucleus. The effective potential between nucleons in a shell-model calculation. All of these are **central potentials** — $V(\vec r) = V(r)$ — and for any central potential, the angular part of the Schrödinger equation has a universal solution. You solve it once, in this chapter. Then for hydrogen, you plug in $V(r) = -e^2/(4\pi\epsilon_0 r)$ and solve a one-dimensional radial equation. For the nuclear well, you plug in something else and solve a different one-dimensional radial equation. The angular structure is always the same.

To see why, rewrite the Laplacian in spherical coordinates:

$$\nabla^2 = \frac{1}{r^2}\frac{\partial}{\partial r}\!\left(r^2\frac{\partial}{\partial r}\right) + \frac{1}{r^2\sin\theta}\frac{\partial}{\partial\theta}\!\left(\sin\theta\frac{\partial}{\partial\theta}\right) + \frac{1}{r^2\sin^2\theta}\frac{\partial^2}{\partial\phi^2}.$$

The first term is purely radial. The second and third are purely angular — and they are divided by $r^2$. Pull out the $r^2$ and the angular piece stands alone. Define:

$$\hat{L}^2 \equiv -\hbar^2\!\left[\frac{1}{\sin\theta}\frac{\partial}{\partial\theta}\!\left(\sin\theta\frac{\partial}{\partial\theta}\right) + \frac{1}{\sin^2\theta}\frac{\partial^2}{\partial\phi^2}\right].$$

This is the square of the orbital angular momentum operator. The kinetic energy splits cleanly into a radial piece and an angular piece:

$$-\frac{\hbar^2}{2m}\nabla^2 = -\frac{\hbar^2}{2m}\cdot\frac{1}{r^2}\frac{\partial}{\partial r}\!\left(r^2\frac{\partial}{\partial r}\right) + \frac{\hat{L}^2}{2mr^2}.$$

<!-- → [INFOGRAPHIC: Side-by-side split of the Laplacian in spherical coordinates — left box highlights the purely radial first term in one color, right box highlights the angular second-and-third terms in another; arrow from right box to "= L̂²/r²"; caption: "The angular piece, isolated, is L̂² divided by r². This is why central-potential problems separate."] -->

The angular kinetic energy is $\hat{L}^2/(2mr^2)$ — the same expression as $L^2/(2I)$ for a classical rotor with moment of inertia $I = mr^2$. The quantum and classical formulas are identical in structure.

---

## Separating variables

Try the product ansatz $\psi(r, \theta, \phi) = R(r)Y(\theta, \phi)$. Substitute into the Schrödinger equation with $V(\vec r) = V(r)$, divide by $RY$, multiply by $r^2$. The $r$-dependent terms go to one side, the $(\theta, \phi)$-dependent terms to the other. Each side depends on different variables, so each must equal a constant. Call it $\ell(\ell+1)$. The equation splits into two:

**Angular equation:**
$$\hat{L}^2 Y(\theta, \phi) = \hbar^2\ell(\ell+1)\,Y(\theta, \phi)$$

**Radial equation:**
$$\frac{1}{R}\frac{d}{dr}\!\left(r^2\frac{dR}{dr}\right) - \frac{2mr^2}{\hbar^2}[V(r) - E] = \ell(\ell+1)$$

The angular equation knows nothing about which central potential you chose. It is an eigenvalue equation for $\hat{L}^2$ on the unit sphere. Its solutions are the spherical harmonics $Y_{\ell m}(\theta, \phi)$ — and solving it once solves the angular part of every central-potential problem simultaneously. The radial equation has $V(r)$ in it. That is where the specific physics lives.

<!-- → [INFOGRAPHIC: Flow diagram — "Central potential V(r)" → "Separation of variables" → two branches: left branch "Angular equation: L̂²Y = ℏ²ℓ(ℓ+1)Y, solved once, valid for ALL central potentials" and right branch "Radial equation: depends on V(r), solved separately for hydrogen / spherical well / harmonic oscillator / etc."] -->

---

## The angular equation: what falls out

Separate once more: $Y(\theta, \phi) = \Theta(\theta)\Phi(\phi)$. The $\phi$ equation is immediate:

$$\Phi''(\phi) = -m^2\Phi(\phi), \quad \Phi_m(\phi) = \frac{e^{im\phi}}{\sqrt{2\pi}}.$$

Single-valuedness — $\Phi(\phi + 2\pi) = \Phi(\phi)$ — forces $m$ to be an integer.

The $\theta$ equation, with the substitution $u = \cos\theta$, becomes the **associated Legendre equation**. Its physically acceptable solutions — those that remain finite at the poles $\theta = 0$ and $\theta = \pi$ — are the associated Legendre functions $P_\ell^m(\cos\theta)$, and they exist only when $\ell$ is a non-negative integer and $|m| \leq \ell$. These two constraints are not imposed by hand. They fall out of requiring the solutions to be non-singular. That is why the eigenvalues of $\hat{L}^2$ are $\hbar^2\ell(\ell+1)$ — the discreteness is forced by the boundary conditions on the sphere.

Stitch the pieces together with the normalization:

$$Y_{\ell m}(\theta, \phi) = \sqrt{\frac{2\ell+1}{4\pi}\,\frac{(\ell - |m|)!}{(\ell + |m|)!}}\;P_\ell^m(\cos\theta)\,e^{im\phi}.$$

These are the **spherical harmonics**. They are orthonormal on the unit sphere:

$$\int_0^{2\pi}d\phi\int_0^\pi\sin\theta\,d\theta\;Y_{\ell' m'}^*\,Y_{\ell m} = \delta_{\ell\ell'}\delta_{mm'}.$$

They form a complete basis for functions on the sphere: any function $f(\theta, \phi)$ can be expanded as $f = \sum_{\ell m}c_{\ell m}Y_{\ell m}$.

The first few are worth writing out:

$Y_0^0 = 1/\sqrt{4\pi}$ — a constant. The s-orbital has no angular structure whatsoever.

$Y_1^0 = \sqrt{3/(4\pi)}\cos\theta$ — maximal at the poles, zero on the equator. The physics $p_z$.

$Y_1^{\pm 1} = \mp\sqrt{3/(8\pi)}\sin\theta\,e^{\pm i\phi}$ — the minus sign for $m = +1$ is the **Condon-Shortley phase convention**. Note that $|Y_1^{\pm 1}|^2 = (3/8\pi)\sin^2\theta$: the probability density is the same for $m = +1$ and $m = -1$, independent of $\phi$. The two states differ only in their phase rotation.

$Y_2^0 = \sqrt{5/(16\pi)}(3\cos^2\theta - 1)$ — the $d_{z^2}$ orbital. It has nodes where $\cos\theta = \pm1/\sqrt{3}$, about $54.7°$ from the $z$-axis. The "donut belt" visible in chemistry textbooks is the region between those nodal cones.

<!-- → [IMAGE: Gallery of polar plots r(θ) = |Y_{ℓm}|² for (ℓ,m) = (0,0), (1,0), (1,±1), (2,0), (2,±1), (2,±2) — six plots arranged in a triangular grid matching the ℓ=0,1,2 rows; each labeled with its quantum numbers; +z axis drawn as vertical reference; caption: "The angular probability densities. Note that all are axially symmetric about z — the φ-dependence is only in the phase."] -->

One structural fact to internalize: $|Y_{\ell m}|^2$ is independent of $\phi$ — always. The $\phi$-dependence of $Y_{\ell m}$ lives entirely in the phase $e^{im\phi}$, and the modulus squared kills it. The angular probability density is axially symmetric about the $z$-axis for every spherical harmonic, regardless of $m$.

---

## The angular momentum operators

The classical angular momentum $\vec L = \vec r \times \vec p$ becomes, in quantum mechanics:

$$\hat{L}_x = \hat{y}\hat{p}_z - \hat{z}\hat{p}_y, \quad \hat{L}_y = \hat{z}\hat{p}_x - \hat{x}\hat{p}_z, \quad \hat{L}_z = \hat{x}\hat{p}_y - \hat{y}\hat{p}_x.$$

In spherical coordinates, the $z$-component simplifies to

$$\hat{L}_z = -i\hbar\frac{\partial}{\partial\phi}.$$

Act on $Y_{\ell m}$. The $\phi$-dependence is $e^{im\phi}$, so $\hat{L}_z Y_{\ell m} = -i\hbar\cdot im\cdot e^{im\phi} \cdot(\ldots) = m\hbar\, Y_{\ell m}$. The spherical harmonic $Y_{\ell m}$ is simultaneously an eigenstate of $\hat{L}^2$ with eigenvalue $\hbar^2\ell(\ell+1)$ and an eigenstate of $\hat{L}_z$ with eigenvalue $m\hbar$. The integer $m$ with $-\ell \leq m \leq +\ell$ is the **magnetic quantum number**.

The $x$ and $y$ components have more complex expressions in spherical coordinates and are *not* diagonal in the $Y_{\ell m}$ basis. They satisfy:

$$[\hat{L}_x, \hat{L}_y] = i\hbar\hat{L}_z, \quad [\hat{L}_y, \hat{L}_z] = i\hbar\hat{L}_x, \quad [\hat{L}_z, \hat{L}_x] = i\hbar\hat{L}_y.$$

Compactly: $[\hat{L}_i, \hat{L}_j] = i\hbar\epsilon_{ijk}\hat{L}_k$. And:

$$[\hat{L}^2, \hat{L}_i] = 0 \quad \text{for } i = x, y, z.$$

This last relation is the reason $\hat{L}^2$ and *one* component can be simultaneously diagonalized. Their joint eigenstates — the states where both $L^2$ and $L_z$ are sharp — are the spherical harmonics. The other two components are then necessarily sharp, which is forced by the non-zero commutators between $\hat{L}_x$, $\hat{L}_y$, and $\hat{L}_z$.

---

## Why $\hbar^2\ell(\ell+1)$, not $\hbar^2\ell^2$

Here is a fact that trips up almost everyone the first time. The maximum value of $\hat{L}_z$ in the $\ell$ subspace is $m = \ell$, giving $L_z = \ell\hbar$. But the magnitude of the angular momentum vector is $\sqrt{\langle L^2\rangle} = \hbar\sqrt{\ell(\ell+1)}$, which is strictly *greater* than $\ell\hbar$ for any $\ell > 0$.

This means the angular momentum vector can never be fully aligned with the $z$-axis. Even in the state $|\ell, m = \ell\rangle$, which has the maximum possible $z$-component, the vector still has transverse components. Geometrically: the angular momentum precesses on a cone. The half-angle of the cone is $\arccos(\ell/\sqrt{\ell(\ell+1)})$ — for $\ell = 1$, exactly $45°$.

Why does this happen? Because $\hat{L}_x$ and $\hat{L}_y$ cannot both be zero simultaneously. If $L_z = \ell\hbar$ exactly, and $L^2 = \hbar^2\ell(\ell+1)$, then $L_x^2 + L_y^2 = \hbar^2\ell(\ell+1) - \ell^2\hbar^2 = \hbar^2\ell$. The transverse components are unavoidably non-zero. They are not zero in the state $|\ell, m = \ell\rangle$; they are merely uncertain — their *expectation values* are zero, but their *variances* are not. The Robertson inequality $\sigma_{L_x}\sigma_{L_y} \geq \hbar|\langle L_z\rangle|/2 = \hbar\cdot\ell\hbar/2$ enforces a minimum spread.

<!-- → [IMAGE: Cone diagram for ℓ=1, m=1 — a cone of half-angle 45° with the z-axis as the cone's axis; the angular momentum vector drawn as an arrow of length √2 ℏ lying on the cone surface; its z-projection labeled "L_z = ℏ"; the transverse projection labeled "√(L_x² + L_y²) = ℏ"; caption: "Even in the maximally aligned state |ℓ=1, m=1⟩, the angular momentum cannot point along z. It precesses on a cone."] -->

This kills the Bohr-model picture of an electron orbiting in a definite plane. A definite orbital plane would require a definite direction for $\vec L$ — which the angular momentum algebra forbids. The electron has a definite $L^2$ and a definite $L_z$. It does not have a definite $L_x$ or $L_y$. There is no "orbital plane." There is a cone.

---

## The chemistry-textbook orbitals

The spherical harmonics $Y_1^{\pm 1}$ are eigenstates of $\hat{L}_z$ with eigenvalues $\pm\hbar$. Their probability densities $|Y_1^{\pm 1}|^2$ are axially symmetric about $z$ — donuts around the $z$-axis. There is no definite spatial direction in these states other than the $z$-axis itself.

Chemistry prefers something different: wave functions that point along the Cartesian axes, so you can say "the electron is along $x$" or "along $y$." The real combinations are:

$$p_x = -\tfrac{1}{\sqrt{2}}(Y_1^1 - Y_1^{-1}) \propto \sin\theta\cos\phi$$
$$p_y = \tfrac{i}{\sqrt{2}}(Y_1^1 + Y_1^{-1}) \propto \sin\theta\sin\phi$$
$$p_z = Y_1^0 \propto \cos\theta.$$

These are real wave functions with the familiar dumbbell shapes pointing along $x$, $y$, $z$. But act with $\hat{L}_z = -i\hbar\partial_\phi$ on $p_x \propto \sin\theta\cos\phi$:

$$\hat{L}_z(\sin\theta\cos\phi) = -i\hbar\frac{\partial}{\partial\phi}\cos\phi = i\hbar\sin\phi \propto ip_y.$$

The result is $ip_y$, not a multiple of $p_x$. The $p_x$ orbital is *not* an eigenstate of $\hat{L}_z$. It has a definite spatial direction ($\hat x$) but no definite $z$-component of angular momentum.

<!-- → [IMAGE: Two-row comparison for ℓ=1. Top row: physics basis — three polar plots of |Y_1^{-1}|², |Y_1^0|², |Y_1^1|² showing axially symmetric shapes (two donuts and a dumbbell along z); label "eigenstates of L̂_z, eigenvalues −ℏ, 0, +ℏ." Bottom row: chemistry basis — three polar plots of p_x, p_y, p_z showing dumbbells along x, y, z; label "NOT eigenstates of L̂_z." Caption: "Same subspace, different bases. Choose physics basis for angular momentum bookkeeping; chemistry basis for spatial orientation."] -->

Both bases — the complex $\{Y_1^{-1}, Y_1^0, Y_1^1\}$ and the real $\{p_x, p_y, p_z\}$ — span the same three-dimensional subspace of states with $\ell = 1$. Any state in the subspace can be written in either basis. They are related by a unitary transformation; they describe the same physics. Chemistry picks the real basis because the pictures are beautiful. Physics picks the complex basis because $\hat{L}_z$ is diagonal. Neither is more "correct." The mistake is thinking the chemistry pictures *are* the eigenstates of angular momentum. They are not.

---

## The radial equation and the centrifugal barrier

With $\psi = R(r)Y_{\ell m}$ and the angular part handled, the radial equation still has an inconvenient structure. Define $u(r) = rR(r)$. A short calculation converts the radial equation into:

$$-\frac{\hbar^2}{2m}\frac{d^2 u}{dr^2} + \left[V(r) + \frac{\hbar^2\ell(\ell+1)}{2mr^2}\right]u(r) = E\,u(r).$$

This is a **one-dimensional Schrödinger equation** in $u(r)$ on the half-line $r \in [0, \infty)$, with effective potential

$$V_{\text{eff}}(r) = V(r) + \frac{\hbar^2\ell(\ell+1)}{2mr^2}.$$

The extra term — positive, diverging at $r = 0$, falling off as $1/r^2$ at large $r$ — is the **centrifugal barrier**. For $\ell > 0$, it pushes probability away from the origin. For $\ell = 0$ (s-states), there is no barrier, and the wave function can have finite amplitude at $r = 0$.

<!-- → [CHART: Three overlaid plots of V_eff(r) = −1/r + ℏ²ℓ(ℓ+1)/(2mr²) for ℓ = 0, 1, 2 (Coulomb potential as example) — x-axis is r, y-axis is V_eff; ℓ=0 shows the bare −1/r well; ℓ=1 shows the Coulomb well with a centrifugal hump near the origin; ℓ=2 shows a taller hump; caption: "The centrifugal barrier grows with ℓ. For ℓ>0, it suppresses the wave function near r=0 and shifts the bound-state energies upward."] -->

One misconception to clear up: the centrifugal barrier is not a force pushing the electron outward. It is a *kinetic energy* contribution — specifically, the angular part of the kinetic energy, which has been absorbed into the effective potential because we have already projected onto an angular momentum eigenstate. Mathematically it sits where $V(r)$ sits. Physically it is kinetic, not potential. Students who absorbed centrifugal force from classical mechanics often confuse these. The distinction matters when you ask where the energy comes from.

The $u$ substitution does the key work: a 3D central-force problem is exactly equivalent to a 1D Schrödinger equation with an $\ell$-dependent effective potential. The angular machinery built above is what allows this reduction. The trade is clean: kill the explicit angle dependence, pay with the centrifugal term.

Boundary conditions: $u(0) = 0$ to keep $R = u/r$ finite at the origin; $u(r) \to 0$ as $r \to \infty$ for normalizability. The radial probability density $|u(r)|^2$ is the probability per unit length of finding the particle at distance $r$.

---

## A solvable example: the spherical well

Take $V(r) = 0$ for $r < a$ and $V = \infty$ for $r \geq a$. Inside the well, with $k = \sqrt{2mE/\hbar^2}$ and $\rho = kr$, the radial equation reduces to an equation whose solutions are the spherical Bessel functions $j_\ell(\rho)$. The boundary condition $u(a) = 0$ means $j_\ell(ka) = 0$, so $ka$ must be the $n$-th zero of $j_\ell$, call it $\beta_{n\ell}$:

$$E_{n\ell} = \frac{\hbar^2\beta_{n\ell}^2}{2ma^2}.$$

For $\ell = 0$: $j_0(\rho) = \sin\rho/\rho$, zeros at $\rho = n\pi$. So $E_{n,0} = n^2\pi^2\hbar^2/(2ma^2)$ — exactly the 1D infinite-well spectrum. The s-states of the spherical well, after the $u$ transformation, are identical to the 1D infinite-well states. That is not a coincidence. It is the statement that $\ell = 0$ states have no angular structure; they are purely radial, and the 3D and 1D problems are literally the same equation.

For $\ell = 1$: $j_1(\rho) = \sin\rho/\rho^2 - \cos\rho/\rho$. Its first zero is near $\rho \approx 4.49$, giving $E_{1,1} \approx 2.05 E_{1,0}$. The centrifugal barrier raises the energy above the corresponding s-state.

<!-- → [TABLE: Energy level table for the 3D spherical well — columns: state label (1s, 1p, 1d, 2s, 1f, 2p), ℓ, n, β_{nℓ}/π (ratio to 1s energy), E_{nℓ}/E_{1s}; rows sorted by increasing energy; caption: "The level ordering is 1s, 1p, 1d, 2s, 1f, 2p, ... This sequence, modified by spin-orbit coupling, produces the nuclear magic numbers."] -->

The level ordering — 1s, 1p, 1d, 2s, 1f, 2p, ... — is what you get by sorting the zeros of successive Bessel functions. This is not a curiosity. It is the foundation of the nuclear shell model. Maria Goeppert Mayer and J. Hans D. Jensen showed in 1949 that adding a strong spin-orbit coupling to a spherical-well-like potential reproduces the observed nuclear magic numbers 2, 8, 20, 28, 50, 82, 126 — for which they shared the 1963 Nobel Prize in Physics. The angular machinery of this chapter, applied to a nucleus, predicts which proton and neutron numbers make unusually stable nuclei.

One more note on the spectrum: higher $\ell$ does not universally mean higher energy. For the spherical well it does, because the centrifugal barrier raises the kinetic energy. For the hydrogen atom (Chapter 7), energies depend only on the principal quantum number $n$, with no $\ell$-dependence — a special "accidental" degeneracy of the $1/r$ Coulomb potential. For the 3D harmonic oscillator, energies depend on $2n_r + \ell$. The angular structure is universal; the ordering of levels is potential-specific.

---

## The same mathematics, much larger

Here is a thought to carry forward. The spherical harmonics $Y_{\ell m}(\theta, \phi)$ are the universal basis for functions on any sphere. They appear in atomic orbitals (electrons in atoms), in the nuclear shell model (nucleons in nuclei), in the multipole expansion of any electromagnetic field, in the gravitational potential of any nearly-spherical body, and in the cosmic microwave background.

The Planck collaboration reports the CMB's temperature anisotropies — the tiny ripples in the temperature of the sky left over from 380,000 years after the Big Bang — as a power spectrum $C_\ell$, where $\ell$ is the spherical-harmonic index. The peak of the CMB power spectrum at $\ell \approx 220$ corresponds to the acoustic scale of the universe at recombination. The same $\ell$ that distinguishes s, p, d, f atomic orbitals labels the multipoles of the cosmos. The mathematics is identical. Learning spherical harmonics properly here is not preparation for atomic physics only. It is preparation for anything that lives on a sphere.

<!-- → [INFOGRAPHIC: Two-column comparison — left: atomic orbital polar plot gallery (s, p, d shapes with their ℓ values labeled); right: CMB temperature anisotropy map of the sky (Planck result) with the power spectrum C_ℓ vs. ℓ shown below it, peak at ℓ≈220 marked; connecting arrow labeled "same ℓ, same mathematics"; caption: "Spherical harmonics organize both the electron orbitals in a hydrogen atom and the temperature fluctuations of the cosmic microwave background."] -->

---

## LLM Exercise — the spherical harmonics visualizer

You are going to build a single-file D3 simulation that displays the spherical harmonics $Y_{\ell m}(\theta, \phi)$ in two synchronized panels — a polar cross-section and a pseudo-3D mesh on the sphere — with a toggle between physics (complex) and chemistry (real) conventions, and an animation mode that visualizes the $\phi$-phase rotation generated by $\hat{L}_z$. The deliverable is `05-spherical-harmonics.html`.

### Part 1 — Update `PROJECT.md`

```
Append a new entry to PROJECT.md describing the Chapter 5 simulation:

Chapter 05 — Quantum Mechanics in Three Dimensions
Deliverable: 05-spherical-harmonics.html
Status: in progress

The simulation visualizes Y_{l m}(theta, phi) with two side-by-side panels:

1. Left panel: polar cross-section at phi = 0. Plot r(theta) = |Y_{l m}|^2
   in polar coordinates, with theta measured from the +z axis. Lobes
   appear naturally - Y_1^0 gives a dumbbell, Y_2^0 a peanut-with-belt.
   Color: lobes filled with semi-transparent fill; outline darker. When
   "Re(Y)" mode is active, positive lobes are one color (e.g. blue) and
   negative lobes are another (e.g. red).

2. Right panel: pseudo-3D unit sphere with surface shaded by |Y|^2. The
   sphere is meshed in 30 latitude bands and 30 longitude bands, giving
   ~900 patches. Each patch is colored by |Y_{l m}|^2 at its center.
   Patches are sorted by mean projected depth (painter's algorithm) so
   that front-facing patches occlude back-facing ones in the SVG render
   order. View angles (alpha, beta) draggable.

   Alternative right-panel display: "balloon" mode, where each surface
   patch is moved radially outward by an amount proportional to
   |Y_{l m}(theta, phi)|^2, producing the familiar dumbbell / clover shapes
   in 3D rather than as a flat-sphere color map.

3. Bottom strip: eigenvalue display:
     L^2 = hbar^2 * l (l+1) = [value]
     L_z = hbar * m = [value]
     Nodes in theta: l - |m| - [list of nodal-cone angles]
     Convention: physics (complex Y) or chemistry (real combinations)

Controls:
- l selector (0 to 4)
- m selector (-l to +l, range updates when l changes)
- Convention toggle: "physics (complex)" vs "chemistry (real)"
- Display mode: "|Y|^2 (probability)" vs "Re(Y) (signed wave function)"
- Right panel display: "sphere with shading" vs "balloon"
- Animate phi-phase toggle: when enabled, multiply Y by exp(-i omega t)
  with omega = m (in natural units), so the phase wheel rotates at rate m.
  Visible on the right panel as a rotation of the wave-function color
  pattern when Re(Y) mode is active. The physical interpretation: this
  is the time evolution generated by L_z. m = 0 states are static
  (no phi rotation); higher |m| states rotate faster.

No three.js, no babylon, no math.js. Pure D3 SVG with hand-rolled
orthographic projection and painter's-algorithm depth sorting. Single
HTML file. This decision is documented in PROJECT.md to keep the
Brutalist system clean - one dependency, D3 v7 from CDN, no exceptions.
```

### Part 2 — The CLAUDE.md amendment

```
Append to CLAUDE.md the following physics rules for Chapter 5 simulations:

SPHERICAL HARMONICS PHYSICS RULES

1. Associated Legendre polynomials computed by recurrence:
     P_l^l(x) = (-1)^l * (2l-1)!! * (1-x^2)^(l/2)     [Condon-Shortley]
     P_{l+1}^l(x) = x * (2l+1) * P_l^l(x)
     (l - m + 1) * P_{l+1}^m(x) = (2l + 1) * x * P_l^m(x)
                                  - (l + m) * P_{l-1}^m(x)
   for l > m. The CONDON-SHORTLEY phase (the (-1)^l in the first line and
   the implicit (-1)^m in some other formulations) is the physics standard.
   Verify by computing Y_1^1 and checking it equals:
     Y_1^1 = -sqrt(3 / (8 pi)) * sin(theta) * exp(i phi)
   The minus sign matters.

2. Spherical harmonic:
     Y_l^m(theta, phi) = sqrt((2l+1) / (4 pi) * (l - m)! / (l + m)!)
                         * P_l^m(cos theta) * exp(i m phi)
   For m < 0, use Y_l^{-m}(theta, phi) = (-1)^m * conj(Y_l^m(theta, phi)).

3. Real combinations (chemistry convention):
     m > 0: Y_{l, m}^real = (1 / sqrt(2)) * (Y_l^{-m} + (-1)^m * Y_l^m)
     m = 0: Y_{l, 0}^real = Y_l^0
     m < 0: Y_{l, m}^real = (i / sqrt(2)) * (Y_l^m - (-1)^m * Y_l^{-m})
   Verify: the m=1 real combination is p_x ~ sin theta cos phi, and the
   m=-1 real combination is p_y ~ sin theta sin phi. Sanity-check that
   p_x has its maximum at theta = pi/2, phi = 0 (the +x direction).

4. Normalization sanity check (run at startup for each (l, m)):
   Riemann-sum the integral of |Y_{l m}|^2 over the sphere on a 100 x 100
   (theta, phi) grid with sin(theta) measure. The result should be 1
   within 0.01. If it is not, the normalization prefactor is wrong.

5. (1 - x^2) where x = cos(theta) can dip slightly negative due to
   floating-point near theta = 0 or pi. Clamp:
     sqrt_arg = max(0, 1 - x * x)
   before taking the square root in P_l^l.

6. Factorial: use a small lookup table for l up to 10. (l + m)! / (l - m)!
   may be computed as a product to avoid two large factorial overflows.

7. Painter's algorithm for the 3D sphere panel:
   For each of the ~900 surface patches, compute the patch center in 3D,
   project to 2D using the current view rotation, AND record the depth
   (signed distance from viewer; greater = farther). Sort the patch list
   by depth descending (back first, front last), then render in that
   order. The last patch drawn is on top. Without this sort, patches
   are rendered in mesh order and the orbital looks "inside out."

KNOWN FAILURE MODES to avoid:
(a) Condon-Shortley phase missing or wrong - check Y_1^1 sign.
(b) Factorial overflow for l > ~10 - cap or use log-gamma.
(c) (1 - x^2) negative due to floating-point - clamp.
(d) Forgetting normalization check at startup - the plot will look
    right in shape but wrong in absolute scale.
(e) Painter's algorithm omitted or wrong direction - orbital looks inverted.
(f) Real-combination signs wrong - p_x might point in the -x direction.
    Verify against the chemistry textbook canon (p_x maximum at +x).
(g) Y-axis labels saying "psi" instead of "|Y|^2" or "Y_{lm}" - this is
    the chapter's whole point and the label must reflect it.
```

### Part 3 — The simulation prompt

```
You are working in my directory which contains CLAUDE.md, DESIGN.md, and
PROJECT.md (with the Chapter 5 entry just added). Read all three first.

Build 05-spherical-harmonics.html: a single self-contained HTML file using
D3 v7 from a CDN, no other dependencies, that implements the Chapter 5
simulation specified in PROJECT.md following the physics rules in CLAUDE.md
and the visual constitution in DESIGN.md.

Layout: one SVG of 1100 x 650, divided as:

- Left panel (polar plot, 450 x 500 with controls below): a polar plot
  of r(theta) = |Y_{l m}(theta, phi=0)|^2 for the active (l, m). Render
  by sampling theta on a 360-point grid from 0 to 2 pi, computing
  Y_{l m}(theta, 0) (using the modulus or real part depending on mode),
  converting (r, theta) to Cartesian for SVG with the +z axis pointing
  up. Use d3.lineRadial() with d3.curveCardinalClosed for the outline.
  Fill the interior with a semi-transparent color; if Re(Y) mode is on,
  positive lobes blue and negative lobes red; if |Y|^2 mode, single
  color (e.g., teal). Draw the +z axis as a vertical reference line.
  Display the |Y|^2 magnitude scale with tick marks.

- Right panel (pseudo-3D, 500 x 500): the unit sphere with surface shading
  by |Y_{l m}|^2 at each patch. Mesh: 30 theta bands x 30 phi bands.
  For each patch, compute (theta_center, phi_center), evaluate
  Y_{l m}(theta_center, phi_center), and color the patch by:
    - magnitude (gray to bright color) if |Y|^2 mode
    - sign (blue-red diverging) if Re(Y) mode
  Project each patch corner to 2D using orthographic projection with view
  angles (alpha, beta). Sort patches by mean projected depth (painter's
  algorithm) and append in back-to-front order. Add the +z axis as a
  small arrow protruding from the sphere.

- Bottom strip (1100 x 100): eigenvalue display:
    L^2 = hbar^2 * l(l+1) = [value]   L_z = hbar * m = [value]
    Nodes in theta: [comma-separated list of nodal-cone angles in degrees]
    [m bar showing -l to +l, current m highlighted]

- Top strip (1100 x 50): controls:
  l selector (radio or stepper), m selector (constrained to -l..+l),
  convention toggle, display mode toggle, right-panel mode toggle,
  animate phi-phase toggle.

Mathematical implementation:
- Cache the patch grid (~900 entries) for the active (l, m), recompute
  on (l, m) or convention change.
- View rotation: alpha (azimuth, drag horizontally), beta (elevation, drag
  vertically). Default alpha = 20 degrees, beta = -10 degrees.
- Phi-phase animation: when enabled, replace exp(i m phi) by
  exp(i m (phi - omega t)) where omega = 1 in natural units. The shading
  of the right panel rotates at rate m. For m = 0 nothing changes.

Runtime sanity checks (write to console):
- At startup, for each (l, m) up to l = 4, integral of |Y_{l m}|^2 over
  sphere via Riemann sum must equal 1 within 0.01.
- For (l, m) = (1, 1) in physics convention, Y_1^1 at (theta=pi/2, phi=0)
  must equal -sqrt(3 / (8 pi)) within 1e-6 (real part) and 0 (imaginary
  part); the negative sign is the Condon-Shortley check.
- For chemistry-convention (l, m) = (1, 1) (the p_x orbital), the max
  of Y at theta = pi/2 should occur at phi = 0 (the +x direction).

Do NOT use any 3D library. Pure D3 with hand-rolled orthographic
projection and painter's-algorithm sorting. The decision to use pure
D3 (no three.js) is documented in PROJECT.md to keep the dependency
graph clean - one library, D3 v7 from CDN, no exceptions. Comments at
every non-trivial physics step.
```

### Part 4 — Exploration tasks and extension prompt

Run the simulation and answer the following:

1. **$|Y|^2$ is independent of $\phi$.** Set $(\ell, m) = (1, 1)$ in physics convention. Look at the polar cross-section at $\phi = 0$. Then toggle to "Re(Y)" mode: the real part has a $\cos\phi$ dependence, but $|Y|^2$ has the same shape at every $\phi$. The right panel makes this visible: in $|Y|^2$ mode the sphere is shaded with axial symmetry about $\hat z$, regardless of which $m$ you pick.

2. **The $p$-orbital basis swap.** Set $(\ell, m) = (1, 1)$. Toggle from "physics (complex)" to "chemistry (real)." The polar cross-section shape changes — from a donut-symmetric ring (the complex $|Y_1^1|^2$, rotationally symmetric about $z$) to a dumbbell pointing along $\hat x$ (the real $p_x$). The eigenvalue display shows that the chemistry-convention state is no longer an eigenstate of $\hat{L}_z$.

3. **$\ell(\ell+1)$, not $\ell^2$.** Set $\ell = 1$. The eigenvalue strip shows $L^2 = 2\hbar^2$ — not $\hbar^2$. The maximum value of $L_z$ is $1\hbar$ — less than $\sqrt{L^2} = \sqrt{2}\hbar$. Compute the cone half-angle: $\arccos(1/\sqrt{2}) = 45°$. For $\ell = 2, m = 2$: $L_z = 2\hbar$, $\sqrt{L^2} = \sqrt{6}\hbar$, cone angle $\arccos(2/\sqrt{6}) \approx 35°$. As $\ell$ grows, the cone closes toward the axis — the classical limit.

4. **$\hat{L}_z$ generates $\phi$-rotation.** Toggle "animate phi-phase" on. For $m = 0$ ($Y_1^0$, the $p_z$), nothing happens — no $\phi$ dependence. For $m = 1$, the right panel's color pattern rotates around the $z$-axis at rate $\omega = 1$. For $m = 2$, it rotates twice as fast. For $m = -1$, it rotates the other way. This is $\hat{L}_z$ as the generator of rotations about $\hat z$ — the eigenvalue $m\hbar$ is the rate of phase accumulation.

5. **Nodes.** Set $\ell = 2, m = 0$. The polar cross-section of $|Y_2^0|^2$ has two nodes at $\cos\theta = \pm 1/\sqrt{3}$, about $54.7°$ and $125.3°$. Verify the eigenvalue strip lists these. Then set $\ell = 4, m = 0$: four nodes in $\theta$. As $\ell$ grows with $m = 0$ fixed, angular kinetic energy increases.

**Extension prompt:**

```
Modify 05-spherical-harmonics.html to add a "central potential" panel
on the bottom right (additional 400 x 400 SVG region) that displays the
effective potential V_eff(r) = V(r) + hbar^2 l(l+1) / (2 m r^2) for a
choice of central potential V(r). Choices: 3D infinite spherical well
(V = 0 for r < 1, infinity otherwise), 3D harmonic oscillator
(V = (1/2) m omega^2 r^2), and Coulomb (V = -1/r). For each, plot the
total effective potential and the bound-state energies (computed via
matrix diagonalization on a discrete radial grid - use the Numerov
method or simple finite differences).

As l changes (the user changes l in the main simulation), the
centrifugal barrier grows, the effective potential shape changes, and
the energy levels reorganize. Highlight the connection: the angular
machinery the chapter just built is what allows the radial equation
to be one-dimensional with an l-dependent effective potential.

Update PROJECT.md to mark Chapter 05 complete and note the central-
potential panel as the bridge to Chapter 7 (hydrogen atom), where the
Coulomb-potential radial equation gets solved analytically.
```

---

## Still puzzling

The accidental degeneracy of the hydrogen atom — energies depending only on $n$, not on $\ell$ — has an explanation: a conserved Runge-Lenz vector and a hidden SO(4) symmetry of the $1/r$ Coulomb potential. The same accidental degeneracy in the 3D harmonic oscillator has an SU(3) explanation. Both are clean and settled mathematically. What I do not understand, to my own satisfaction, is *why* these particular symmetries arise in these particular potentials and not others. Bertrand's theorem says the $1/r$ and $r^2$ potentials are the only ones for which all classical bound orbits close. The quantum degeneracy and the classical closed-orbit property must be the same fact in different clothing. But I do not know a derivation that makes the connection feel inevitable rather than coincidental. The math is done. The conceptual unity is not, for me.

---

## Exercises

**Warm-up**

1. *[Tests: separation of variables, identifying the angular operator]* Write the full 3D Schrödinger equation in spherical coordinates for the Coulomb potential $V(r) = -e^2/(4\pi\epsilon_0 r)$. Without solving anything: (a) identify which terms depend only on $r$ and which depend only on $(\theta, \phi)$; (b) write down the separation constant and explain why it is conventionally called $\ell(\ell+1)$ rather than just $\lambda$; (c) state the two equations the separation produces. *Difficulty: warm-up.*

2. *[Tests: normalization of spherical harmonics, explicit computation]* Verify $\int|Y_0^0|^2\,d\Omega = 1$ and $\int|Y_1^0|^2\,d\Omega = 1$ by explicit integration. (You will need $\int_0^\pi\sin\theta\,d\theta = 2$ and $\int_0^\pi\cos^2\theta\sin\theta\,d\theta = 2/3$.) *Difficulty: warm-up.*

3. *[Tests: axial symmetry of |Y|², Condon-Shortley sign]* (a) Show that $|Y_{\ell m}(\theta,\phi)|^2$ is independent of $\phi$ for any $\ell, m$, by inspecting the form of the spherical harmonics. (b) Evaluate $Y_1^1$ at $(\theta = \pi/2, \phi = 0)$ explicitly and confirm the value is $-\sqrt{3/(8\pi)}$ — not $+\sqrt{3/(8\pi)}$. What goes wrong if you omit the Condon-Shortley sign? *Difficulty: warm-up.*

**Application**

4. *[Tests: L̂_z eigenvalue equation, magnetic quantum number]* Verify $\hat{L}_z Y_1^1 = \hbar Y_1^1$ by direct calculation: write out $Y_1^1 = -\sqrt{3/(8\pi)}\sin\theta\,e^{i\phi}$, apply $\hat{L}_z = -i\hbar\partial_\phi$, and show the result is $+\hbar$ times the original. Then verify that $p_x \propto \sin\theta\cos\phi$ is *not* an eigenstate of $\hat{L}_z$ by computing $\hat{L}_z\,p_x$ explicitly and showing the result is a multiple of $p_y$ rather than $p_x$. *Difficulty: application.*

5. *[Tests: centrifugal barrier, u-substitution]* Starting from the radial equation for $R(r)$, apply the substitution $u(r) = rR(r)$ and show explicitly that the result is a 1D Schrödinger equation with effective potential $V_{\text{eff}} = V(r) + \hbar^2\ell(\ell+1)/(2mr^2)$. Identify which derivative of $r^2 dR/dr$ produces the centrifugal term. Then explain in one sentence why the centrifugal barrier is a kinetic energy contribution, not a potential energy contribution. *Difficulty: application.*

6. *[Tests: spherical well energies, connection to 1D well]* For the 3D infinite spherical well of radius $a$: (a) Show that the 1s ground-state energy is $E_{1,0} = \pi^2\hbar^2/(2ma^2)$, the same as the 1D infinite well of width $a$. (b) Find the energy of the first 1p state using $j_1(\beta_{1,1}) = 0$ with $\beta_{1,1} \approx 4.493$ and express it as a multiple of $E_{1,0}$. (c) Explain why the 1s and 1D results match but the 1p result has no 1D analog. *Difficulty: application.*

7. *[Tests: ℓ(ℓ+1) vs ℓ², angular momentum cone]* For the state $|\ell = 2, m = 2\rangle$: (a) Compute $\sqrt{\langle L^2\rangle}$ and $L_z$. (b) Find the half-angle of the angular momentum cone. (c) Find the magnitude of the transverse angular momentum $\sqrt{L_x^2 + L_y^2}$ in this state. (d) Explain why this quantity cannot be zero, using the Robertson inequality for $\hat{L}_x$ and $\hat{L}_y$. *Difficulty: application.*

**Synthesis**

8. *[Tests: physics vs. chemistry basis, L̂_z measurement outcomes]* Consider the $p_x$ chemistry orbital $\propto \sin\theta\cos\phi$. (a) Express $p_x$ as a linear combination of $Y_1^{-1}$, $Y_1^0$, $Y_1^1$. (b) If you measure $L_z$ on a large ensemble of particles each in the state $p_x$, what are the possible outcomes and with what probabilities? (c) What is $\langle L_z\rangle$ for $p_x$? Does this mean $p_x$ "has no $z$-angular momentum"? Explain the distinction between zero expectation value and zero eigenvalue. *Difficulty: synthesis.*

9. *[Tests: level ordering, nuclear shell model connection]* The nuclear magic numbers — unusually stable nucleon counts — are 2, 8, 20, 28, 50, 82, 126. The first three (2, 8, 20) correspond to filled shells in a spherical well without spin-orbit coupling. Using the level ordering 1s, 1p, 1d, 2s, 1f, 2p, ... and the degeneracy $2(2\ell+1)$ per level (including both spin orientations): (a) show that filling 1s, 1p, 1d, and 2s gives cumulative counts 2, 8, 18, 20, matching the first three magic numbers; (b) explain why the higher magic numbers (28, 50, ...) require a spin-orbit term to appear. *Difficulty: synthesis.*

**Challenge**

10. *[Tests: angular momentum algebra, ladder operators, connection to Chapter 3]* Define $\hat{L}_\pm = \hat{L}_x \pm i\hat{L}_y$. (a) Show $[\hat{L}_z, \hat{L}_+] = \hbar\hat{L}_+$ using the commutation relations $[\hat{L}_i, \hat{L}_j] = i\hbar\epsilon_{ijk}\hat{L}_k$. (b) Use this to argue that $\hat{L}_+|Y_{\ell m}\rangle$ is an eigenstate of $\hat{L}_z$ with eigenvalue $(m+1)\hbar$. (c) The descent must terminate at $m = -\ell$ by the same non-negativity argument used for the harmonic oscillator in Chapter 3. State the termination condition ($\hat{L}_-|Y_{\ell,-\ell}\rangle = 0$) and show it forces $\ell$ to be a non-negative integer — the algebraic derivation of the spectrum without solving the Legendre equation. *Difficulty: challenge.*

---

*Chapter 7: You now have the universal angular machinery. The spherical harmonics solve the angular equation for any central potential. The remaining task is to solve the radial equation for the Coulomb potential $V(r) = -e^2/(4\pi\epsilon_0 r)$ specifically — and discover why the hydrogen atom's energy levels depend only on $n$.*
