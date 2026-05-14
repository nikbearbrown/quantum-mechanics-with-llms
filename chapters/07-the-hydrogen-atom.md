# Chapter 7 — The Hydrogen Atom
*The one place quantum mechanics went up against experiment and won completely.*

In 1885 a Swiss mathematics teacher named Johann Balmer published a four-page note observing that the four visible spectral lines of hydrogen fit a single formula:
$$\lambda = B\cdot\frac{n^2}{n^2 - 4}, \qquad n = 3, 4, 5, 6,$$
with $B \approx 364.5$ nm. He had no theory. He had four numbers from a lab notebook and a pattern that fit them perfectly. The formula was right. Nobody knew why for twenty-eight years.

The reason this should bother you is the specificity. It is not merely that the lines form a series — that is not so surprising. It is that the spacing between lines is exactly this formula. Not approximately. The formula nails the wavelengths to the precision of the measurement. Either nature is telling you something very specific, or it is the most remarkable numerical coincidence in the history of spectroscopy. It is not a coincidence.

Bohr gave a partial answer in 1913 with his planetary model — quantized circular orbits, energies $E_n = -13.6\text{ eV}/n^2$ — that reproduced Balmer's formula. But Bohr's model was an ansatz. Why integer $n$ and not half-integer? Why no radiation from those orbits, as classical electromagnetism demands? Why circular and not elliptical? The numbers were right; the explanation was not there yet.

Erwin Schrödinger, working at an Alpine resort over Christmas 1925, wrote down the wave equation for hydrogen. The energies $-13.6\text{ eV}/n^2$ fell out again — same numbers as Bohr, but now from a calculation with no unjustified postulates. What also fell out, and what Bohr had no machinery for, was the full probability density $|\psi_{n\ell m}(r,\theta,\phi)|^2$ — the distribution of where the electron would be found on a position measurement. Not a path. Not an orbit. A probability cloud.

This chapter does that calculation.

---

## Reducing two bodies to one

A hydrogen atom is a proton and an electron, interacting via the Coulomb potential. Write the two-body Hamiltonian, introduce center-of-mass coordinates $\vec R$ and relative coordinates $\vec r = \vec r_e - \vec r_p$, and the Hamiltonian separates:
$$H = \frac{P^2}{2M} + \frac{p^2}{2\mu} - \frac{e^2}{4\pi\epsilon_0 r}.$$
The center-of-mass piece $P^2/(2M)$ is a free particle — ignore it. The relative-motion piece is a single particle of mass $\mu = m_p m_e/(m_p + m_e)$ in a Coulomb potential. Because $m_p \approx 1836 m_e$, the reduced mass differs from $m_e$ by about one part in 1836. For the headline numbers, we use $\mu \approx m_e$. The correction matters in precision spectroscopy: Harold Urey discovered deuterium in 1932 precisely by spotting the predicted isotope shift in the Balmer lines — a slightly different reduced mass, a slightly different set of wavelengths.

<!-- → [TABLE: Two-column comparison of ordinary hydrogen vs. muonic hydrogen vs. deuterium — rows: reduced mass μ, Bohr radius a₀, ground-state energy E₁, Balmer α wavelength — student should see that mass enters every observable and that the Urey discovery follows directly from the formula] -->

The Schrödinger equation to solve is then
$$\left[-\frac{\hbar^2}{2\mu}\nabla^2 - \frac{e^2}{4\pi\epsilon_0 r}\right]\psi(\vec r) = E\psi(\vec r).$$

---

## Separating variables

The potential depends only on $r$. From Chapter 5 you already know what to do: write $\psi(r,\theta,\phi) = R(r)Y_{\ell m}(\theta,\phi)$, separate variables, and the angular part gives the spherical harmonics immediately — that part is universal, the same for any central potential. The radial equation that remains, after the substitution $u(r) = rR(r)$, is a one-dimensional Schrödinger equation with an effective potential:
$$-\frac{\hbar^2}{2\mu}\frac{d^2u}{dr^2} + V_{\text{eff}}(r)\,u(r) = E\,u(r),$$
where
$$V_{\text{eff}}(r) = -\frac{e^2}{4\pi\epsilon_0 r} + \frac{\hbar^2\ell(\ell+1)}{2\mu r^2}.$$

<!-- → [CHART: Plot of V_eff(r) vs. r for ℓ = 0, 1, 2 with the Coulomb potential V(r) = −e²/(4πε₀r) shown as a dashed reference curve — for ℓ=0 the effective potential is just the Coulomb well; for ℓ=1,2 the centrifugal barrier creates a local maximum near the origin; horizontal lines at E_1, E_2, E_3 indicate bound-state energies; student should see that higher ℓ suppresses the wave function near r=0] -->

The second term is the centrifugal barrier from Chapter 5 — the angular kinetic energy in disguise. For $\ell = 0$, it vanishes and the electron can reach the nucleus. For $\ell \geq 1$, it diverges as $r \to 0$ and pushes the wave function away from the origin. This is why $|\psi(0)|^2$ is nonzero only for s-states — a fact you can measure in hyperfine spectroscopy, where the electron's probability density at the nucleus determines the coupling to the nuclear magnetic moment.

The boundary conditions: $u(0) = 0$ to keep $R = u/r$ finite at the origin, and $u(r) \to 0$ as $r \to \infty$ for normalizability. These two conditions together will quantize the energy.

---

## The ground state, worked through

Here is the central calculation. Set $\ell = 0$. The centrifugal barrier vanishes. Try the ansatz
$$u(r) = Ar\,e^{-r/a},$$
where $a$ is an unknown length and $A$ a normalization constant. Differentiate twice:
$$u'' = Ae^{-r/a}\!\left(-\frac{2}{a} + \frac{r}{a^2}\right).$$
Substitute into the radial equation, divide by $Ae^{-r/a}$, and collect by powers of $r$:
$$\underbrace{\frac{\hbar^2}{\mu a} - \frac{e^2}{4\pi\epsilon_0}}_{\text{constant in }r} = \underbrace{\left(E + \frac{\hbar^2}{2\mu a^2}\right)}_{\text{must be zero}}\cdot r.$$
For this to hold at every $r$, both groupings must vanish separately.

From the constant terms:
$$\frac{\hbar^2}{\mu a} = \frac{e^2}{4\pi\epsilon_0} \quad\Longrightarrow\quad a = a_0 = \frac{4\pi\epsilon_0\hbar^2}{\mu e^2}.$$
This is the Bohr radius. Plugging in numbers: $a_0 \approx 5.29 \times 10^{-11}\text{ m} = 0.529$ Å.

From the linear terms:
$$E = -\frac{\hbar^2}{2\mu a_0^2} = -\frac{\mu e^4}{2(4\pi\epsilon_0)^2\hbar^2} \approx -13.6\text{ eV}.$$
The ansatz gave us both numbers from a single calculation. The cleverness is that $u(r) = Are^{-r/a}$ has the right behavior at both boundaries — it vanishes at $r = 0$ (the $r$ factor) and at $r \to \infty$ (the exponential) — and it has exactly one free length scale that the equation determines for you.

Normalize: $\int_0^\infty |u|^2\,dr = 1$ gives $A = 2/a_0^{3/2}$, so $R_{10}(r) = (2/a_0^{3/2})e^{-r/a_0}$, and the full ground-state wave function is
$$\psi_{100}(r) = \frac{1}{\sqrt{\pi a_0^3}}\,e^{-r/a_0}.$$
Spherically symmetric. No angular structure. A blob of probability density centered on the nucleus, falling off exponentially.

<!-- → [IMAGE: Side-by-side 2D cross-sections of |ψ_{100}|² in the xz-plane — left panel: raw density with Viridis color scale, brightest at origin, smoothly fading outward; right panel: the same data as a surface plot showing the peak at center; axes labeled in units of a₀; caption: "The 1s probability density is maximal at the nucleus — but the most probable radius is a₀, not zero, because spherical shells at r=0 have zero volume"] -->

---

## Two radii — and why they are different

Here is the signature move of this chapter, and the clearest demonstration that the orbital is not a path.

The radial probability density — the probability per unit radial distance of finding the electron between $r$ and $r+dr$, after integrating over all angles — is
$$P(r) = r^2|R_{10}(r)|^2 = \frac{4}{a_0^3}\,r^2 e^{-2r/a_0}.$$
The $r^2$ factor matters. Even though $|\psi_{100}|^2$ is maximal at $r = 0$, the surface area of a shell at $r = 0$ is zero, so the *probability* of finding the electron near $r = 0$ is zero. It is the product of the density and the available volume that gives the probability.

**Most probable radius.** Set $dP/dr = 0$:
$$\frac{d}{dr}\left[r^2 e^{-2r/a_0}\right] = e^{-2r/a_0}\left(2r - \frac{2r^2}{a_0}\right) = 0.$$
This vanishes at $r = 0$ (a minimum) and at $r = a_0$. The most probable radius is exactly the Bohr radius.

**Expectation value.** Compute $\langle r\rangle = \int_0^\infty r\cdot P(r)\,dr$:
$$\langle r\rangle = \frac{4}{a_0^3}\int_0^\infty r^3 e^{-2r/a_0}\,dr = \frac{4}{a_0^3}\cdot\frac{3!}{(2/a_0)^4} = \frac{3}{2}a_0.$$
The mean radius is $1.5a_0$.

<!-- → [CHART: Plot of P(r) = r²|R_{10}(r)|² vs. r/a₀ for the 1s state — a smooth curve rising from zero, peaking at r = a₀, then decaying with a long tail; two vertical lines: solid at r_mp = a₀ labeled "most probable radius" and dashed at ⟨r⟩ = 1.5a₀ labeled "expectation value"; shading under the tail illustrates the skew that pulls the mean rightward; caption: "The peak and mean of the same distribution differ because P(r) is skewed. A path has one radius; a probability distribution does not."] -->

Two different numbers describe the same probability distribution: the peak is at $a_0$, the mean is at $1.5a_0$. They differ because $P(r)$ is skewed — a long tail at large $r$ pulls the mean to the right of the peak.

If the orbital were a path — a circular orbit at some radius — there would be exactly one radius. There would be no distinction between "most probable" and "average." The fact that these are different is the geometric fingerprint of the orbital being a probability distribution, not a path. A path has one radius. A probability distribution has a peak and a mean and they need not coincide.

Bohr put the electron at radius $a_0$. Schrödinger says the *peak* of the probability distribution is at $a_0$ and the *mean* is at $1.5a_0$. Same number, different meaning, completely different picture of what is happening.

---

## The full spectrum

The 1s solution was straightforward because of the ansatz. The general $(n, \ell)$ solution requires a Frobenius series method on the radial equation, leading to the associated Laguerre polynomials $L_{n-\ell-1}^{2\ell+1}$. The radial wave functions take the form
$$R_{n\ell}(r) = \mathcal{N}_{n\ell}\cdot r^\ell\cdot e^{-r/(na_0)}\cdot L_{n-\ell-1}^{2\ell+1}\!\left(\frac{2r}{na_0}\right),$$
and the energies are
$$E_n = -\frac{13.6\text{ eV}}{n^2}, \quad n = 1, 2, 3, \ldots$$
The energy depends only on $n$, not on $\ell$ or $m$. This is the Coulomb degeneracy, a consequence of a hidden symmetry I will come back to. For now, the constraints on quantum numbers: $n \geq 1$, $0 \leq \ell \leq n-1$, $|m| \leq \ell$. Each comes from a different place.

$n \geq 1$ comes from normalizability at infinity. The Frobenius series for the radial wave function terminates only when a certain dimensionless parameter takes integer values — below $n = 1$, the series fails to terminate and the wave function blows up exponentially.

$\ell \leq n - 1$ comes from the Laguerre polynomial. Its degree is $n - \ell - 1$, and a polynomial of negative degree does not exist, so $\ell \leq n - 1$ is forced.

$|m| \leq \ell$ comes from Chapter 5 — the angular momentum algebra forces this.

**Degeneracy.** At each $n$, the number of orbital states is $\sum_{\ell=0}^{n-1}(2\ell+1) = n^2$. Including spin ($m_s = \pm 1/2$) this becomes $2n^2$. The $n=1$ shell holds 2 electrons, $n=2$ holds 8, $n=3$ holds 18, $n=4$ holds 32. These are the row lengths of the periodic table. Not a coincidence — a structural consequence of the quantum numbers.

<!-- → [TABLE: Hydrogen quantum number table — rows for n = 1..4; columns: n, allowed ℓ values, allowed m values for each ℓ, total orbital states (n²), total states with spin (2n²), correspondence to periodic table row capacity (2, 8, 18, 32)] -->

---

## What the wave functions look like

For $n \leq 2$, the explicit forms are:
$$\psi_{100} = \frac{1}{\sqrt{\pi a_0^3}}\,e^{-r/a_0} \qquad \text{(1s, spherical)}$$
$$\psi_{200} = \frac{1}{\sqrt{32\pi a_0^3}}\!\left(2 - \frac{r}{a_0}\right)\!e^{-r/(2a_0)} \qquad \text{(2s, radial node at }r = 2a_0\text{)}$$
$$\psi_{210} = \frac{1}{\sqrt{32\pi a_0^3}}\frac{r}{a_0}\,e^{-r/(2a_0)}\cos\theta \qquad \text{(2p}_z\text{)}$$
$$\psi_{21\pm 1} = \mp\frac{1}{\sqrt{64\pi a_0^3}}\frac{r}{a_0}\,e^{-r/(2a_0)}\sin\theta\,e^{\pm i\phi} \qquad \text{(2p}_{\pm 1}\text{)}$$

<!-- → [IMAGE: Gallery of 2D heat maps of |ψ_{nℓm}(x,0,z)|² in the xz-plane for (n,ℓ,m) = (1,0,0), (2,0,0), (2,1,0), (2,1,±1) — Viridis color scale, ±10 a₀ range; student should see: 1s is a single blob; 2s has a dark ring (radial node) at r = 2a₀; 2p_z has a dumbbell shape with a node on the equatorial plane; 2p_{±1} are azimuthally symmetric rings; caption: "All four n=2 states share E = −3.4 eV. Their spatial structures are completely different."] -->

A node-counting rule: the total number of nodes is $n - 1$, divided into $n - \ell - 1$ radial nodes and $\ell$ angular nodes. The 2s state has one radial node and zero angular nodes. The 2p states have zero radial nodes and one angular node. At the same principal quantum number $n = 2$, all four states (2s, $2p_0$, $2p_{\pm 1}$) share the same energy but carry entirely different shapes.

The same distinction from Chapter 5 reappears here. The $\psi_{21,\pm 1}$ states are eigenstates of $\hat{L}_z$ with eigenvalues $\pm\hbar$ — they have definite $z$-component of angular momentum but no definite spatial orientation other than the $z$-axis. The chemistry textbook combinations $p_x \propto \sin\theta\cos\phi$ and $p_y \propto \sin\theta\sin\phi$ are real mixtures of $m = \pm 1$, with dumbbell shapes pointing along the Cartesian axes but no definite $L_z$. Both descriptions span the same subspace. Physics prefers the complex eigenstates because they diagonalize $L_z$. Chemistry prefers the real combinations because the pictures are beautiful. Neither is wrong.

<!-- → [INFOGRAPHIC: Side-by-side comparison of complex vs. real orbital representations for the n=2, ℓ=1 subshell — left: three complex eigenstates ψ_{210}, ψ_{21+1}, ψ_{21−1} with their L_z eigenvalues labeled; right: real chemistry orbitals p_x, p_y, p_z shown as dumbbell isosurfaces with Cartesian axis labels; connecting arrows show the linear combinations; caption: "The same subspace, two bases. Physics diagonalizes L_z; chemistry maximizes spatial clarity."] -->

---

## The hidden symmetry

The $n^2$-fold degeneracy of hydrogen — that 2s and 2p have the same energy, that 3s, 3p, 3d are all degenerate — is not generic to central potentials. For the 3D harmonic oscillator, energy depends on $2n_r + \ell$. For a generic Coulomb-like-but-not-quite potential (as in a multi-electron atom where inner electrons screen the nucleus), energy depends on both $n$ and $\ell$.

Hydrogen's special extra degeneracy has a deeper source. The Coulomb potential $-1/r$ admits a second conserved vector beyond angular momentum: the Laplace–Runge–Lenz vector, which in classical mechanics points along the major axis of the Kepler ellipse and is conserved because Coulomb orbits do not precess. In quantum mechanics, the commutators of the six components $\{\vec L, \vec M\}$ close on each other, forming the algebra $\mathfrak{so}(4)$ — the symmetry of rotations in four dimensions. Wolfgang Pauli used this algebra in 1926 to solve hydrogen algebraically, before Schrödinger published the wave-mechanical solution.

The moment the potential departs from $1/r$ — in sodium, where ten inner electrons partially screen the nucleus — the LRL symmetry breaks and the $\ell$-degeneracy splits. The 3s lies below 3p lies below 3d. The bright yellow sodium D lines at 589 nm are the 3p → 3s transitions, and their existence is direct evidence that sodium's effective potential is no longer purely $-1/r$.

<!-- → [IMAGE: Side-by-side energy level diagrams — left: hydrogen n=1,2,3 shells with all ℓ states at the same horizontal line per n (showing the full Coulomb degeneracy); right: sodium-like atom with the same n shells but ℓ levels split (3s lowest, 3p above it, 3d highest), the 3p→3s transition marked with an arrow and labeled "589 nm Na D line"; caption: "When the potential departs from pure 1/r, the ℓ-degeneracy breaks. The sodium D lines are the directly observable consequence."] -->

---

## The spectrum and the selection rules

Transitions between hydrogen levels emit photons of energy $\hbar\omega = E_{n_i} - E_{n_f}$:
$$\hbar\omega = 13.6\text{ eV}\!\left(\frac{1}{n_f^2} - \frac{1}{n_i^2}\right).$$
Series named by final state: Lyman ($n_f = 1$, ultraviolet), Balmer ($n_f = 2$, visible), Paschen ($n_f = 3$, near-infrared). The Balmer $\alpha$ line — the 3 → 2 transition — sits at
$$\lambda = \frac{hc}{\Delta E} = \frac{1240\text{ eV nm}}{13.6\times(1/4 - 1/9)} = \frac{1240}{1.889} \approx 656.3\text{ nm},$$
compared to the experimental 656.281 nm. Agreement to better than 0.05%, with no fudge factors. This is what Balmer's 1885 formula was missing: an explanation.

Not every transition is allowed. The electric-dipole matrix element $\langle\psi_f|\vec r|\psi_i\rangle$ governs single-photon emission rates, and the angular integral of this matrix element vanishes unless
$$\Delta\ell = \pm 1, \qquad \Delta m = 0, \pm 1.$$

<!-- → [INFOGRAPHIC: Hydrogen energy level diagram with allowed transitions drawn as arrows connecting levels — Lyman series arrows in UV (purple), Balmer series in visible (red/blue/violet), Paschen in IR; arrows drawn only for Δℓ = ±1 transitions; one forbidden transition (2s→1s, Δℓ=0) shown as a dashed arrow with a red X; caption: "Electric-dipole selection rules determine which transitions emit photons. The 2s→1s transition is forbidden; it proceeds via two-photon emission with a 0.12 s lifetime."] -->

The $\Delta\ell = \pm 1$ rule comes from parity: a photon carries angular momentum 1, and the angular integrand has definite parity, so $\ell$ must change by an odd integer; the algebra forces exactly $\pm 1$. A transition that violates these rules is electric-dipole *forbidden* — it can still occur via magnetic dipole, electric quadrupole, or two-photon emission, but at rates many orders of magnitude slower. The 2s → 1s transition in hydrogen has $\Delta\ell = 0$ and proceeds via two-photon emission with a lifetime of about 0.12 s, compared to the nanosecond lifetimes of allowed transitions. This eight-order-of-magnitude difference is what makes the 2s state metastable and what enables precision hydrogen spectroscopy: the 2s state lives long enough to measure.

<!-- → [TABLE: Comparison of electric-dipole allowed vs. forbidden transitions — columns: transition, Δℓ, Δm, allowed/forbidden, dominant decay channel, typical lifetime; rows covering 2p→1s (allowed, ns), 2s→1s (forbidden, 0.12 s), 3d→2p (allowed), 3s→1s (forbidden via E2), 4f→3d (allowed) — student should see the eight-orders-of-magnitude lifetime contrast] -->

---

## Three pictures to dismantle

**The orbital is not a path the electron travels.** $|\psi_{n\ell m}|^2$ is a probability density. The "dumbbell" pictures in chemistry textbooks are isosurfaces of $|\psi|^2$ enclosing some fixed fraction of the total probability — usually 90%. The electron does not orbit inside the dumbbell. It has some probability of being found inside the dumbbell on a given measurement, and a 10% probability of being found outside it. The most-probable-radius vs. $\langle r\rangle$ comparison is the direct evidence: a path has one radius; a probability distribution has a peak and a mean that differ.

**The Bohr model is not essentially correct.** It gets $E_n = -13.6\text{ eV}/n^2$ right by a numerical accident — hydrogen's hidden $\mathfrak{so}(4)$ symmetry makes the energy depend on a single quantum number, and Bohr's quantization rule $L = n\hbar$ correctly identifies that quantum number for circular orbits. But the model has no wave functions, no radial probability density, no node structure, no $\ell$-values other than $\ell = n$ (Bohr orbits have maximum angular momentum always; Schrödinger says $\ell$ can be anything from 0 to $n - 1$), and no selection rules. Bohr's model is pre-Schrödinger numerology that worked once and stopped working immediately thereafter.

**$|\psi|^2$ is not the electron's charge distribution smeared continuously over space.** It is the probability density for finding the electron at a point on a single position measurement. The electron is a point particle. When you fire something at hydrogen, you get a probability distribution of scattering events; run enough events and the histogram converges to $|\psi|^2$. The fluid picture is closer to right than the orbit picture — at least there is no path — but the fluid is not where the charge *is*, it is where the charge *might be*.

<!-- → [INFOGRAPHIC: Three-panel "misconception vs. reality" diagram — panel 1: Bohr orbit (circle with electron dot on path) crossed out, replaced by 1s probability density blob; panel 2: 90% isosurface dumbbell with caption "electron not confined here — 10% probability outside"; panel 3: fluid charge distribution crossed out, replaced by a histogram of simulated position measurements converging to |ψ|² — caption: "The cloud shows where measurements land, not where charge sits"] -->

---

## Why this problem matters

What Schrödinger did in those Alpine weeks was show that the Balmer formula is not empirical numerology — it is the eigenvalue spectrum of a second-order differential equation. The spectrum is a consequence of the boundary conditions on a wave equation. Every atomic spectrum since is a variation on this theme.

The hydrogen results have been tested to extraordinary precision. The 1S–2S transition, measured by two-photon laser spectroscopy, is one of the most precisely known physical frequencies in nature. The ALPHA collaboration at CERN has measured the same transition in antihydrogen — hydrogen with a positron instead of an electron, orbiting an antiproton — and found agreement with hydrogen at the parts-per-trillion level. A direct test of CPT symmetry, using the same Balmer series that Schrödinger computed in 1926.

---

## LLM Exercise — Building the Hydrogen Orbital Visualizer

This is the headline simulation of the book. You are going to render $|\psi_{n\ell m}(x, 0, z)|^2$ as a 2D heat map, the radial probability density $P(r) = r^2|R_{n\ell}|^2$ as a line plot beneath it, and an interactive energy-level diagram. Drag the $(n, \ell, m)$ sliders and watch the orbital reorganize. Click a state to highlight it on the energy diagram. Toggle into transition mode and pick an initial and final state to compute the emitted photon's wavelength.

### Part 1 — The CLAUDE.md prompt

Append this to your existing project's CLAUDE.md:

```
## Chapter 7 — Hydrogen Orbital Visualizer Rules

- Single HTML file, single SVG canvas. No three.js, no WebGL.
- Layout: primary heat-map panel (top, ~400 × 400 px), radial probability
  plot directly below it (~400 × 200 px), energy-level diagram on the right
  (~200 × 400 px). Numeric readouts at the very bottom.
- Sliders for (n, ℓ, m) in a left-hand sidebar, plus a particle/orbital-set
  dropdown ("complex Y_lm" vs. "real chemistry orbitals: p_x, p_y, p_z,
  d_z², ...").
- Color scale: d3.interpolateViridis, sequential. Domain rescaled per state
  to [0, max(|ψ|²)] on the rendered grid.
- Grid resolution: 200 × 200 pixels covering ±20 a₀ × ±20 a₀ in the xz-plane.
- Radial probability plot marks r_mp (peak) and ⟨r⟩ (mean) with vertical lines,
  labeled.
- Energy-level diagram: horizontal lines at E_n = −13.6/n² eV for n = 1..5,
  with spectroscopic labels (1s, 2s, 2p, 3s, 3p, 3d, 4s, 4p, 4d, 4f, 5s, ...).
  Currently selected state is highlighted.
- Numeric readouts (≤ 3 sig figs, monospaced): ⟨r⟩, ⟨r²⟩, r_mp, E_n,
  radial nodes (n − ℓ − 1), angular nodes (ℓ), total nodes (n − 1).
- No DOM mutation outside the redraw function.
```

### Part 2 — The simulation prompt — four-move structure

```
Build me a D3 v7 hydrogen orbital visualizer following CLAUDE.md.

HOOK. Render |ψ_{nℓm}(x, 0, z)|² for the hydrogen atom as a 2D heat map
in the xz-plane. The user drags sliders for (n, ℓ, m) and the orbital
reorganizes.

UNFOLD. The hydrogen wave function factorizes:
  ψ_{nℓm}(r, θ, φ) = R_{nℓ}(r) Y_{ℓm}(θ, φ),
where R_{nℓ}(r) involves the associated Laguerre polynomial L^{2ℓ+1}_{n−ℓ−1}
and an exponential e^{−r/(n a₀)}, and Y_{ℓm}(θ, φ) is the spherical harmonic
from Chapter 5. Set a₀ = 1 internally and rescale axes accordingly.

Compute R_{nℓ}(r) explicitly for (n, ℓ) up to (4, 3) — code each as a
Python-style sympy-or-manual polynomial expansion, then plug into your D3
code as a JavaScript function. Use the recursive definition of associated
Laguerre polynomials if you prefer general (n, ℓ).

Compute Y_{ℓm}(θ, φ) — use either explicit closed forms for ℓ ≤ 3
or the recursive definition of associated Legendre polynomials.

MECHANISM. Three coupled panels.
  (1) Primary 2D heat map: at each pixel (x, z) on a 200×200 grid,
      compute r = √(x²+z²), θ = atan2(x, z), φ = 0. Evaluate
      |ψ_{nℓm}(r, θ, 0)|² and color via Viridis. (For real chemistry
      orbitals, the heat map is computed in the relevant cut plane, e.g.,
      xy for p_x.)
  (2) Radial probability P(r) = r² |R_{nℓ}(r)|² as a line plot, from
      r = 0 to r = 20 a₀. Vertical lines at r_mp (the maximum of P) and
      ⟨r⟩ = ∫ r · P(r) dr.
  (3) Energy-level diagram: horizontal lines at E_n = −13.6/n² eV for
      n = 1 through 5. Spectroscopic labels (1s, 2s, 2p, …). Current
      state highlighted.

SYNTHESIZE. Add a "Transition mode" toggle. When on, two state selectors
appear: |ψ_i⟩ and |ψ_f⟩. Compute ΔE = E_{n_i} − E_{n_f}. Display the
photon wavelength λ = hc/ΔE in nm. Identify the spectral series
(Lyman if n_f = 1, Balmer if 2, Paschen if 3). Check the dipole selection
rules Δℓ = ±1, Δm = 0, ±1 and flag the transition as ALLOWED or FORBIDDEN.
For forbidden transitions, display the note: "Electric-dipole forbidden;
proceeds via higher-order processes."

Output a single self-contained HTML file using the D3 v7 CDN.
```

### Part 3 — Exploration tasks

1. **Confirm the 1s headline numbers.** Set $(n, \ell, m) = (1, 0, 0)$. Read off $r_{mp}$ and $\langle r\rangle$. Confirm $r_{mp} \approx 1.00\,a_0$ and $\langle r\rangle \approx 1.50\,a_0$. These two different numbers describe the same probability distribution. Stop and look at the heat map: it is a spherical blob. There is no ring at $a_0$.

2. **Count nodes.** Set $(2, 0, 0)$ — the 2s state. The radial probability plot should show two peaks separated by a zero at $r = 2a_0$. Now set $(3, 1, 0)$ — the $3p_z$ state. Predict the node count: $n - 1 = 2$ total, partitioned into $n - \ell - 1 = 1$ radial and $\ell = 1$ angular. Verify on the simulation.

3. **The $n^2$ degeneracy.** Switch among $(2, 0, 0)$, $(2, 1, 0)$, $(2, 1, +1)$, $(2, 1, -1)$. All four share $E = -3.4$ eV, sitting on the same horizontal line in the energy diagram. Shapes differ dramatically. Same energy, different geometry.

4. **Compute the Balmer $\alpha$ wavelength.** Enter transition mode. Set $(n_i, \ell_i, m_i) = (3, 1, 0)$ and $(n_f, \ell_f, m_f) = (2, 0, 0)$. Read the wavelength. Confirm $\lambda \approx 656$ nm. Verify the transition is ALLOWED ($\Delta\ell = -1$).

5. **A forbidden transition.** Set $(n_i, \ell_i, m_i) = (2, 0, 0)$ and $(n_f, \ell_f, m_f) = (1, 0, 0)$ — the 2s → 1s transition. The simulation should flag this as FORBIDDEN ($\Delta\ell = 0$). This is the metastable 2s state.

6. **Real vs. complex orbitals.** Switch the orbital-set dropdown from "complex $Y_{\ell m}$" to "real chemistry orbitals." Set $(n, \text{sub-shell}) = (2, p)$. Cycle through $p_x, p_y, p_z$ and watch the dumbbells rotate. Switch back to complex; cycle through $m = -1, 0, +1$. The $m = 0$ case is identical to $p_z$; the $m = \pm 1$ cases are azimuthally symmetric blobs.

### Part 4 — Extension prompt: Time evolution in a superposition

A stationary state has a time-independent probability density. To see something move, you build a superposition:

```
Extend the hydrogen visualizer to include a "Superposition mode."

In this mode the state is
  ψ(t) = (1/√2) [ψ_{100} e^{−i E_1 t/ℏ} + ψ_{210} e^{−i E_2 t/ℏ}]
        = (1/√2) [ψ_{1s} + e^{−iω_{12} t} ψ_{2p_z}]
        × e^{−i E_1 t/ℏ},
where ω_{12} = (E_2 − E_1)/ℏ ≈ 1.55 × 10^{16} rad/s.

Animate |ψ(x, 0, z, t)|² in real time. Use a slowed-down clock (display
"physical time" alongside the simulation frame number, with a slowdown
factor visible at the top).

The probability density should slosh between the 1s blob and the 2p_z
dumbbell with period T_{12} = 2π/ω_{12} ≈ 0.405 fs. This is the
classical-limit picture of an "oscillating electric dipole" — what an
atom does when it is in the process of transitioning between 1s and 2p,
in the dipole approximation.
```

This is the simulation that makes "atomic transitions are coherent superpositions evolving in time" finally visible. The electron's wave function continuously sloshes between configurations; the photon emission is the dipole-radiation tail of the oscillation.

<!-- → [IMAGE: Four animation frames of |ψ(x,0,z,t)|² for the 1s+2p_z superposition — frames at t=0, T/4, T/2, 3T/4 of the beat period T₁₂ — showing the density shifting from a spherical blob (t=0) through an asymmetric deformation to a dumbbell (t=T/2) and back; caption: "A coherent superposition oscillates. This is what an atom looks like while it is emitting a photon."] -->

### Part 5 — Six failure modes to watch for

1. **Color-scale domain not reset on state change.** If the Viridis domain is set once at $n = 1$ and not updated, high-$n$ orbitals appear uniformly dark. Recompute the domain at every state change.

2. **Forgetting the $r^2$ Jacobian in $P(r)$.** Plotting $|R_{n\ell}|^2$ instead of $r^2|R_{n\ell}|^2$ makes the 1s density peak at $r = 0$ instead of $r = a_0$. The difference is visible and dramatic.

3. **Energy formula off by a sign.** $E_n = -13.6/n^2$, negative. If the energy diagram shows positive values, a sign was dropped.

4. **Selection rule logic too strict.** $\Delta m$ must be $0, +1,$ or $-1$ — all three. Some students implement this as exactly $0$.

5. **Quantum number ranges not enforced.** The combination $(n, \ell, m) = (1, 1, 0)$ asks for a Laguerre polynomial of degree $-1$. Constrain the sliders: $\ell$ max is $n - 1$; $m$ range is $-\ell$ to $+\ell$.

6. **Heat-map coordinate confusion.** For $x < 0$ in the xz-plane, $\phi = \pi$ not $\phi = 0$. Handling the sign of $x$ when computing the azimuthal angle correctly is required; otherwise the simulation renders a half-orbital.

---

## Still puzzling

The Laplace–Runge–Lenz vector — the classical conserved quantity that signals the $\mathfrak{so}(4)$ symmetry of the Coulomb problem — exists because $-1/r$ orbits do not precess. Bertrand's theorem says only the $1/r$ and $r^2$ potentials have all bound orbits closed. The quantum degeneracy and the classical closed-orbit property must be the same fact in different clothing. I can state the algebra; I cannot make the connection feel inevitable. The math is settled. The explanation, at the level of "of course it had to be this way," is not there for me.

---

## Exercises

### Warm-up

1. *[Tests: two-body reduction, reduced mass]* A muonic hydrogen atom replaces the electron with a muon ($m_\mu \approx 207 m_e$). (a) Compute the reduced mass $\mu$ for muonic hydrogen. (b) Compute the Bohr radius $a_0^\mu = 4\pi\epsilon_0\hbar^2/(\mu e^2)$. By what factor is it smaller than the ordinary Bohr radius? (c) By what factor does the ground-state energy $E_1 = -\mu e^4/(2(4\pi\epsilon_0)^2\hbar^2)$ change? Express the answer in eV. *Difficulty: warm-up.*

2. *[Tests: ground-state normalization, radial probability density]* Verify that $\psi_{100}(r) = (1/\sqrt{\pi a_0^3})e^{-r/a_0}$ is normalized by computing $\int|\psi_{100}|^2 d^3r$ explicitly. Use $\int_0^\infty r^2 e^{-2r/a_0}dr = a_0^3/4$. Then write down $P(r) = r^2|R_{10}(r)|^2$, and verify $\int_0^\infty P(r)\,dr = 1$. *Difficulty: warm-up.*

3. *[Tests: quantum number constraints, counting states]* List all allowed $(n, \ell, m)$ combinations for $n = 3$. Verify the count is $n^2 = 9$ orbital states and $2n^2 = 18$ states including spin. State in one sentence where each of the three constraints ($n \geq 1$, $\ell \leq n-1$, $|m| \leq \ell$) comes from. *Difficulty: warm-up.*

### Application

4. *[Tests: the two-radii distinction, skewness of P(r)]* For the 2s state, the radial wave function is $R_{20}(r) = (1/\sqrt{8a_0^3})(2 - r/a_0)e^{-r/(2a_0)}$ (verify the normalization). (a) Find the radial node — the value of $r$ where $R_{20} = 0$. (b) Compute the most probable radius by finding the maximum of $P(r) = r^2|R_{20}|^2$. (c) Compute $\langle r\rangle_{2s}$ using $\int_0^\infty r^n e^{-r/b}\,dr = n!\,b^{n+1}$. Compare $r_{mp}$ and $\langle r\rangle_{2s}$. *Difficulty: application.*

5. *[Tests: spectral series, Rydberg formula]* (a) Compute the wavelength of the Lyman $\alpha$ line ($n = 2 \to n = 1$) and confirm it falls in the ultraviolet. (b) Compute the wavelength of the Paschen $\alpha$ line ($n = 4 \to n = 3$) and confirm it falls in the near-infrared. (c) In 1932, Urey discovered deuterium by spotting a faint line shifted slightly from H$_\alpha$ (656.3 nm). Estimate the wavelength of the deuterium Balmer $\alpha$ line using the reduced mass $\mu_D = m_p m_d m_e/(m_p m_d + m_d m_e + m_p m_e)$ where $m_d \approx 2 m_p$. How large is the shift in nm? *Difficulty: application.*

6. *[Tests: selection rules, forbidden transitions]* For each of the following transitions, state whether it is electric-dipole allowed or forbidden, and give the reason: (a) $3p \to 1s$; (b) $3d \to 1s$; (c) $3p \to 2p$; (d) $3d \to 2p$; (e) $2s \to 1s$. For any forbidden transition, name one higher-order process by which it could still occur. *Difficulty: application.*

### Synthesis

7. *[Tests: radial probability density, comparison across n and ℓ]* (a) For general $n$ and $\ell = 0$ (s-states), the most probable radius scales approximately as $r_{mp} \approx n^2 a_0$ for large $n$. Verify this for $n = 1, 2, 3$ by finding the peaks of $P(r)$ for 1s, 2s, and 3s explicitly. (b) For a given $n$, does increasing $\ell$ move the most probable radius inward or outward? Use the centrifugal barrier picture to explain why. *Difficulty: synthesis.*

8. *[Tests: Coulomb degeneracy, physical consequences]* (a) In hydrogen, 2s and 2p are degenerate at $-3.4$ eV. What physical observable could distinguish them without measuring the energy directly? (Hint: consider the selection rules and their lifetimes.) (b) In sodium, 3s lies at $-5.14$ eV and 3p at $-3.04$ eV — the $\ell$-degeneracy is broken. Use the LRL symmetry argument to explain qualitatively why breaking the $1/r$ potential breaks the degeneracy. (c) The sodium D lines at 589 nm are actually a doublet — two closely spaced lines. What causes this fine splitting? (The answer involves spin-orbit coupling from Chapter 9, but name the effect.) *Difficulty: synthesis.*

### Challenge

9. *[Tests: expectation values by ladder operators, connection to Chapter 3]* Using the ladder-operator algebra of Chapter 3 applied to the hydrogen radial equation, show that $\langle r\rangle_{n\ell} = a_0[3n^2 - \ell(\ell+1)]/2$. Verify for $(1, 0)$ giving $3a_0/2$ and for $(2, 0)$ giving $6a_0$. (Hint: express $r$ in terms of the appropriate operators and use the known matrix elements.) *Difficulty: challenge.*

10. *[Tests: superposition, time evolution, connection to classical dipole radiation]* Consider the superposition $\Psi(r,t) = (1/\sqrt{2})[\psi_{100}e^{-iE_1 t/\hbar} + \psi_{210}e^{-iE_2 t/\hbar}]$. (a) Show that $|\Psi|^2$ contains a time-dependent cross-term oscillating at frequency $\omega_{12} = (E_2 - E_1)/\hbar$. (b) Compute the expectation value $\langle z\rangle(t) = \langle\Psi|\hat{z}|\Psi\rangle$ and show it oscillates sinusoidally at $\omega_{12}$. (c) An oscillating dipole moment $\langle z\rangle \propto \cos(\omega_{12}t)$ is the classical picture of a radiating antenna. Explain in two sentences why this superposition physically represents the atom in the process of emitting a photon at frequency $\omega_{12}$, rather than sitting in either eigenstate. *Difficulty: challenge.*

---

**Chapter 8:** You have solved one-electron hydrogen completely. The next step is two electrons — helium — and immediately the problem becomes unsolvable analytically. The reason: electron-electron repulsion. Chapter 8 sets up the machinery of identical particles, antisymmetry, and the Pauli exclusion principle that governs every multi-electron atom in the periodic table.
