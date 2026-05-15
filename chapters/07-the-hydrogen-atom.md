# Chapter 7 — The Hydrogen Atom
*The one place quantum mechanics went up against experiment and won completely.*

In 1885 a Swiss mathematics teacher named Johann Balmer published a four-page note. He had been looking at the four visible spectral lines of hydrogen — red, blue-green, violet, deep violet — and he noticed that their wavelengths fit a formula:

$$\lambda = B\cdot\frac{n^2}{n^2 - 4}, \qquad n = 3, 4, 5, 6,$$

with $B \approx 364.5$ nm. He had no theory. He had four numbers from a lab notebook and a pattern that fit them exactly.

Now, you might think: so what? People fit numbers to formulas all the time. But this is different, and I want you to feel why. The formula does not approximately fit the wavelengths. It *exactly* fits them, to the precision of the measurement. The spacing between lines — the ratio of wavelengths — comes out right. Balmer's formula nails hydrogen's visible spectrum with no free parameters left over. That kind of precision does not come from coincidence. Nature is telling you something very specific, and Balmer had no idea what it was.

Nobody did, for twenty-eight years.

Bohr gave a partial answer in 1913. He assumed electrons move in circular orbits but can only occupy orbits where the angular momentum is an integer multiple of $\hbar$. From this ansatz he derived energies $E_n = -13.6\,\text{eV}/n^2$, and the Balmer formula followed immediately — the photon energy for a transition from level $n_i$ to $n_f$ is

$$\hbar\omega = 13.6\,\text{eV}\!\left(\frac{1}{n_f^2} - \frac{1}{n_i^2}\right).$$

The numbers were right. But why must angular momentum be quantized? Why do orbiting electrons not radiate, as Maxwell's equations demand they should? Bohr had no answers. The model was a conjecture that happened to work, and it was wrong about almost everything except the energy levels.

Schrödinger, working at an Alpine resort over Christmas 1925, wrote down the wave equation for hydrogen. The energies $-13.6\,\text{eV}/n^2$ fell out again — same numbers as Bohr, but now from a calculation with no arbitrary postulates. What also fell out, and what Bohr had absolutely no machinery for, was the full probability density $|\psi_{n\ell m}(r,\theta,\phi)|^2$ — the complete picture of where the electron is likely to be found on a measurement. Not a path. Not an orbit. A cloud of probability.

This chapter does that calculation, follows it to its consequences, and then asks you to confront what it means.

---

## One equation, two bodies

A hydrogen atom is a proton and an electron, interacting via the Coulomb potential $-e^2/(4\pi\epsilon_0 r)$. You could write a Schrödinger equation for both particles simultaneously, but you do not need to. The standard trick: introduce the center-of-mass coordinate $\vec{R} = (m_p\vec{r}_p + m_e\vec{r}_e)/(m_p + m_e)$ and the relative coordinate $\vec{r} = \vec{r}_e - \vec{r}_p$. The Hamiltonian separates cleanly into a free-particle piece for the center of mass — which drifts and is uninteresting — and a one-body piece for the relative coordinate:

$$\hat{H} = \frac{\hat{p}^2}{2\mu} - \frac{e^2}{4\pi\epsilon_0 r},$$

where $\mu = m_p m_e/(m_p + m_e)$ is the reduced mass. Because the proton is about 1836 times heavier than the electron, $\mu \approx m_e$ to one part in 1836. For headline numbers we use $\mu = m_e$. For precision spectroscopy, the difference matters: Harold Urey discovered deuterium in 1932 by finding a faint second copy of every Balmer line, shifted slightly because deuterium's heavier nucleus changes the reduced mass and therefore every wavelength. The isotope shift is about 1.79 Å at the Balmer $\alpha$ line — small, but unmistakable to a careful spectroscopist.

<!-- → [TABLE: three-column comparison of ordinary hydrogen, deuterium, and muonic hydrogen — rows: reduced mass μ (in units of m_e), Bohr radius a₀, ground-state energy E₁ (eV), Balmer α wavelength (nm); caption: "Mass enters every observable. The Urey isotope shift follows directly from changing μ; muonic hydrogen is ~207× smaller with ~207× more binding energy"] -->

The equation to solve is now a single-particle Schrödinger equation in three dimensions with a $1/r$ potential:

$$\left[-\frac{\hbar^2}{2\mu}\nabla^2 - \frac{e^2}{4\pi\epsilon_0 r}\right]\psi(\vec{r}) = E\,\psi(\vec{r}).$$

The potential is spherically symmetric, which tells us what to do.

---

## Separating the problem

From Chapter 5 you know that any spherically symmetric Hamiltonian separates in spherical coordinates. Write $\psi(r,\theta,\phi) = R(r)Y_\ell^m(\theta,\phi)$ and the angular part gives the spherical harmonics immediately — that part is universal, unchanged from Chapter 5, completely independent of whatever $V(r)$ turns out to be. The spherical harmonics know nothing about Coulomb; they only know about the rotation group.

The radial part is where hydrogen lives. After substituting and making the standard simplification $u(r) = rR(r)$ — which turns the three-dimensional radial equation into a one-dimensional one — you get:

$$-\frac{\hbar^2}{2\mu}\frac{d^2u}{dr^2} + \underbrace{\left[-\frac{e^2}{4\pi\epsilon_0 r} + \frac{\hbar^2\ell(\ell+1)}{2\mu r^2}\right]}_{V_\text{eff}(r)}\,u(r) = E\,u(r).$$

The effective potential has two pieces. The Coulomb well $-e^2/(4\pi\epsilon_0 r)$ pulls the electron in toward the nucleus. The centrifugal term $+\hbar^2\ell(\ell+1)/(2\mu r^2)$ pushes it out, and grows without bound as $r \to 0$. For $\ell = 0$ the centrifugal barrier vanishes entirely and the electron can, in principle, be found at the nucleus. For $\ell \geq 1$ the barrier diverges at the origin and the wave function is pushed away. This is why the probability density at the nucleus is nonzero only for s-states — a fact you can measure in hyperfine spectroscopy, where the electron's probability at the nucleus couples to the nuclear magnetic moment.

The boundary conditions are simple to state: $u(0) = 0$ so that $R = u/r$ stays finite, and $u(r) \to 0$ as $r \to \infty$ so that the wave function is normalizable. These two requirements together — sensible behavior at both ends — will quantize the energy.

<!-- → [CHART: V_eff(r) vs. r for ℓ = 0, 1, 2 on the same axes — the ℓ=0 curve is the bare Coulomb well (dashed reference); ℓ=1 and ℓ=2 curves show the centrifugal barrier lifting V_eff above the Coulomb well near the origin, creating a local maximum before the well reasserts itself at larger r; horizontal lines mark E_1, E_2, E_3; caption: "The centrifugal barrier suppresses the wave function near r = 0 for all ℓ ≥ 1. Only s-states (ℓ=0) reach the nucleus"] -->

---

## The ground state, worked all the way through

I want to show you the actual calculation, not just the result, because the calculation reveals something about how this kind of physics works. Set $\ell = 0$. The centrifugal barrier vanishes. We need a function that goes to zero at the origin (the $r$ factor in $u = rR$ handles this) and decays at infinity. Try

$$u(r) = A r\,e^{-r/a},$$

where $a$ is an unknown length scale and $A$ is a normalization constant to be fixed later. This is the simplest thing consistent with both boundary conditions.

Differentiate twice:

$$u''(r) = Ae^{-r/a}\!\left(-\frac{2}{a} + \frac{r}{a^2}\right).$$

Substitute into the radial Schrödinger equation (with $\ell = 0$), divide through by $Ae^{-r/a}$, and collect terms by powers of $r$:

$$\underbrace{\left(\frac{\hbar^2}{\mu a} - \frac{e^2}{4\pi\epsilon_0}\right)}_{\text{constant}} + \underbrace{\left(E + \frac{\hbar^2}{2\mu a^2}\right)}_{\text{must vanish}}\cdot r = 0.$$

For this to hold at every value of $r$, both groupings must vanish independently. From the constant terms:

$$\frac{\hbar^2}{\mu a} = \frac{e^2}{4\pi\epsilon_0} \quad\Longrightarrow\quad a = a_0 = \frac{4\pi\epsilon_0\hbar^2}{\mu e^2} \approx 0.529\,\text{Å}.$$

This is the Bohr radius. It fell out of the calculation; we did not put it in. From the $r$-coefficient:

$$E = -\frac{\hbar^2}{2\mu a_0^2} = -\frac{\mu e^4}{2(4\pi\epsilon_0)^2\hbar^2} \approx -13.6\,\text{eV}.$$

Both the size of the atom and the ground-state energy emerge from a single requirement: that our trial function satisfies the wave equation everywhere. Normalizing gives $A = 2/a_0^{3/2}$, so

$$\psi_{100}(r) = \frac{1}{\sqrt{\pi a_0^3}}\,e^{-r/a_0}.$$

Spherically symmetric. No preferred direction. A blob of probability density centered on the nucleus and falling off exponentially in every direction.

<!-- → [IMAGE: 2D cross-section of |ψ_{100}|² in the xz-plane — Viridis color scale, range ±5 a₀, brightest point at the origin fading smoothly outward with no ring or shell structure; axes labeled in units of a₀; caption: "The 1s wave function: spherically symmetric, maximum density at the nucleus, exponential decay in every direction. No ring, no orbit — just a probability cloud"] -->

---

## Two radii, and why they differ

Here is the thing that trips people up, and it is worth going slowly.

The radial probability density — the probability per unit radial distance of finding the electron between $r$ and $r + dr$, after integrating over all angles — is not $|R_{10}|^2$. It is

$$P(r) = r^2|R_{10}(r)|^2 = \frac{4}{a_0^3}\,r^2 e^{-2r/a_0}.$$

The $r^2$ factor comes from the volume element in spherical coordinates: a shell at radius $r$ has area $4\pi r^2$, so even though the density $|\psi|^2$ is largest at $r = 0$, the probability of finding the electron near the nucleus is nearly zero because the shell volume at small $r$ is nearly zero. It is the product of density and available volume that gives probability.

Set $dP/dr = 0$ to find the most probable radius:

$$\frac{d}{dr}\!\left[r^2 e^{-2r/a_0}\right] = 0 \quad\Longrightarrow\quad r_\text{mp} = a_0.$$

Now compute the mean radius:

$$\langle r\rangle = \int_0^\infty r\cdot P(r)\,dr = \frac{4}{a_0^3}\int_0^\infty r^3 e^{-2r/a_0}\,dr = \frac{4}{a_0^3}\cdot\frac{3!}{(2/a_0)^4} = \frac{3}{2}a_0.$$

The most probable radius is $a_0$. The mean radius is $1.5\,a_0$. Two different numbers describing the same distribution.

They differ because $P(r)$ is skewed — it has a long tail at large $r$ that pulls the mean to the right of the peak. This is worth staring at because it is the direct geometric fingerprint of the orbital being a probability distribution rather than a path. If the electron were on a circular orbit at some fixed radius, there would be one radius. Full stop. The most probable radius and the mean radius would be identical because there would be only one radius to speak of. The fact that $r_\text{mp} \neq \langle r\rangle$ is not a numerical detail. It is evidence, built into the ground state of the simplest atom, that we are dealing with a probability distribution and not a trajectory.

Bohr put the electron at radius $a_0$. Schrödinger says the *peak* of the distribution is at $a_0$ — same number — but means something completely different by it.

<!-- → [CHART: P(r) = r²|R_{10}(r)|² vs. r/a₀ for the 1s state — smooth curve rising from zero, peaking at r = a₀, decaying with a right-skewed tail to large r; solid vertical line at r_mp = a₀ labeled "most probable radius"; dashed vertical line at ⟨r⟩ = 1.5 a₀ labeled "mean radius"; light shading under the right tail illustrating the skew; caption: "Two numbers, one distribution. The peak at a₀ and the mean at 1.5 a₀ differ because P(r) is skewed. A path has one radius. A probability distribution does not"] -->

---

## The full spectrum

The ground state worked out cleanly because we guessed a simple ansatz. For general $(n, \ell)$ the calculation requires a Frobenius series expansion, which I will not carry through here. The solutions are the associated Laguerre polynomials $L_{n-\ell-1}^{2\ell+1}$, and the full radial wave functions take the form

$$R_{n\ell}(r) = \mathcal{N}_{n\ell}\cdot\left(\frac{r}{a_0}\right)^\ell\cdot e^{-r/(na_0)}\cdot L_{n-\ell-1}^{2\ell+1}\!\!\left(\frac{2r}{na_0}\right).$$

The energies are

$$E_n = -\frac{13.6\,\text{eV}}{n^2}, \qquad n = 1, 2, 3, \ldots$$

The energy depends only on $n$ — not on $\ell$, not on $m$. This is the Coulomb degeneracy, and it is not obvious. For a generic central potential, energy depends on both $n$ and $\ell$. The $1/r$ potential has a special extra symmetry — I will come to it — that collapses all those levels together.

The quantum number constraints follow from the mathematics. The requirement $n \geq 1$ comes from normalizability at infinity: the Frobenius series for the radial function terminates only when a certain dimensionless combination takes positive integer values, and below $n = 1$ the series fails to terminate and the wave function blows up. The constraint $\ell \leq n - 1$ comes from the Laguerre polynomial: its degree is $n - \ell - 1$, and a polynomial of negative degree does not exist. The constraint $|m| \leq \ell$ comes from Chapter 5 — that is the angular momentum algebra, unchanged.

At each $n$, the number of orbital states is $\sum_{\ell=0}^{n-1}(2\ell+1) = n^2$. Including the two spin states $m_s = \pm 1/2$ from Chapter 6, each shell holds $2n^2$ electrons. Shell $n = 1$ holds 2, $n = 2$ holds 8, $n = 3$ holds 18, $n = 4$ holds 32. These are the row lengths of the periodic table. Not numerology. A structural consequence of the quantum numbers derived in this and the previous two chapters.

A node-counting rule ties the structure together neatly: the total number of nodes in $\psi_{n\ell m}$ is $n - 1$, partitioned into $n - \ell - 1$ radial nodes and $\ell$ angular nodes. The 2s state has one radial node and no angular nodes; the 2p states have no radial nodes and one angular node. Both kinds of node cost the same in energy — the $n$ quantum number counts the total, and the distribution between radial and angular is what $\ell$ specifies.

<!-- → [TABLE: quantum number table for n = 1 through 4 — columns: n, allowed ℓ values, spectroscopic label for each (n,ℓ) pair, total orbital states n², total states with spin 2n², periodic table row capacity; student should see the 2/8/18/32 pattern emerge directly from the quantum number counting] -->

<!-- → [IMAGE: gallery of 2D cross-sections of |ψ_{nℓm}(x,0,z)|² in the xz-plane for (1,0,0), (2,0,0), (2,1,0), and (2,1,±1) — Viridis color scale, ±10 a₀ range, laid out in a 2×2 grid with panel labels; 1s: spherical blob; 2s: dark ring (radial node) at r=2a₀; 2p_z: dumbbell with equatorial node; 2p_{±1}: azimuthally symmetric ring; caption: "All four n=2 states share E = −3.4 eV. Their shapes are entirely different"] -->

---

## The shape question: complex or real?

The $\psi_{21,\pm 1}$ states are eigenstates of $\hat{L}_z$ with eigenvalues $\pm\hbar$. They have definite $z$-component of angular momentum but they look, in the xz-plane, like azimuthally symmetric rings — no dumbbell. The chemistry textbook $p_x$ and $p_y$ orbitals are real linear combinations of $m = \pm 1$:

$$p_x \propto \psi_{21,-1} - \psi_{21,+1} \propto \sin\theta\cos\phi, \qquad p_y \propto i(\psi_{21,-1} + \psi_{21,+1}) \propto \sin\theta\sin\phi.$$

These have the dumbbell shape pointing along the Cartesian axes — beautiful pictures, and useful for thinking about bonding — but they are *not* eigenstates of $\hat{L}_z$. They are superpositions of $m = +1$ and $m = -1$.

Both descriptions span exactly the same subspace of states. Physics prefers the complex eigenstates because they diagonalize $\hat{L}_z$ and are the natural output of the Schrödinger equation in spherical coordinates. Chemistry prefers the real combinations because molecular bonding is about directionality. Neither is wrong. The choice of basis is a choice of what you want to make obvious, and different choices make different things obvious.

<!-- → [INFOGRAPHIC: side-by-side comparison of the ℓ=1 subshell in two bases — left column: three complex eigenstates ψ_{210}, ψ_{21+1}, ψ_{21−1} shown as 2D density cross-sections with their L_z eigenvalues (0, +ℏ, −ℏ) labeled; right column: real chemistry orbitals p_z, p_x, p_y shown as dumbbell isosurfaces with Cartesian axis labels; center: arrows showing the linear combination relationships; caption: "Same subspace, two bases. Physics diagonalizes L_z. Chemistry maximizes spatial intuition for bonding"] -->

---

## The hidden symmetry

The Coulomb degeneracy — the fact that 2s and 2p share the same energy, that 3s, 3p, 3d are all at $-13.6/9$ eV — is peculiar and worth understanding. For any central potential, energy depends only on $n$ and $\ell$; the $m$ degeneracy is a consequence of rotational symmetry and is universal. But the additional $\ell$-degeneracy is special to the $1/r$ potential.

The classical version of this fact is that Kepler orbits do not precess. A $1/r$ orbit closes on itself exactly, returning to the same point with the same velocity. For any other power law, the orbit precesses — the ellipse rotates slowly in space. The classical quantity that is conserved because of this non-precession is the Laplace–Runge–Lenz vector, which points along the major axis of the Kepler ellipse and is constant of the motion. In quantum mechanics, the six operators $\{\hat{L}_x, \hat{L}_y, \hat{L}_z, \hat{M}_x, \hat{M}_y, \hat{M}_z\}$ — three angular momentum components and three Runge–Lenz components — satisfy commutation relations that close on each other, forming the algebra $\mathfrak{so}(4)$: the symmetry of rotations in four dimensions. Wolfgang Pauli used this algebra in 1926 to solve hydrogen algebraically, before Schrödinger published the wave-mechanical solution.

The moment the potential departs from $1/r$, this symmetry breaks and the $\ell$-degeneracy splits. In sodium, ten inner electrons partially screen the nuclear charge, and the effective potential felt by the valence electron is no longer purely $-1/r$. The 3s level falls below 3p, which falls below 3d. The bright yellow sodium D lines at 589 nm are the 3p $\to$ 3s transitions, and they exist *because* sodium's effective potential is not Coulomb. Those lines are direct spectroscopic evidence of broken $\mathfrak{so}(4)$ symmetry.

<!-- → [IMAGE: side-by-side energy level diagrams — left: hydrogen n=1,2,3 with all ℓ states degenerate at each horizontal level (full Coulomb degeneracy, labels 1s, 2s/2p, 3s/3p/3d all on one line per n); right: sodium-like atom with same n shells but ℓ levels split, 3s lowest, 3p above, 3d highest, downward arrow on 3p→3s gap labeled "589 nm Na D line"; caption: "The ℓ-degeneracy is a fingerprint of the pure 1/r potential. Sodium's D lines exist because sodium is not hydrogen"] -->

---

## Transitions and selection rules

Two hydrogen levels separated by energy $\Delta E$ can be connected by emitting a photon of frequency $\omega = \Delta E/\hbar$. The Balmer $\alpha$ line — the $n = 3 \to n = 2$ transition — sits at

$$\lambda = \frac{hc}{\Delta E} = \frac{1240\,\text{eV nm}}{13.6\times(1/4 - 1/9)} = \frac{1240}{1.889} \approx 656.3\,\text{nm},$$

compared to the experimental 656.281 nm. Agreement to better than 0.05%. This is what Balmer's 1885 formula was missing: a derivation.

Not every transition is allowed. A photon carries angular momentum 1, and conservation of angular momentum during emission requires that the electron's orbital angular momentum change by $\pm 1$. The full electric-dipole selection rules, derived by evaluating the matrix element $\langle\psi_f|\hat{\vec{r}}|\psi_i\rangle$ and requiring it to be nonzero, are

$$\Delta\ell = \pm 1, \qquad \Delta m = 0, \pm 1.$$

The 2s $\to$ 1s transition has $\Delta\ell = 0$ and is electric-dipole *forbidden*. It still occurs — via two-photon emission — but at an eight-orders-of-magnitude slower rate: lifetime $\approx 0.12$ s, compared to nanosecond lifetimes for allowed transitions. This is not a curiosity. That eight-order-of-magnitude difference is what makes the 2s state metastable and what enables precision hydrogen spectroscopy: the 2s state lives long enough to interrogate carefully.

<!-- → [INFOGRAPHIC: hydrogen energy level diagram with allowed transitions drawn as colored arrows — Lyman series (n_f=1) arrows in violet, Balmer series (n_f=2) in visible colors with Hα labeled at 656 nm, Paschen series (n_f=3) in red/IR; arrows drawn only between levels satisfying Δℓ=±1; the 2s→1s transition shown as a dashed arrow with label "Δℓ=0, forbidden, τ ≈ 0.12 s"; caption: "Selection rules determine which transitions produce single photons. The 2s state is metastable because Δℓ=0 forbids direct decay to 1s"] -->

The 1S–2S two-photon transition in hydrogen is, in fact, one of the most precisely measured frequencies in all of physics. It has been measured to fifteen significant figures using optical frequency combs. The ALPHA collaboration at CERN has now measured the same transition in antihydrogen — hydrogen made from a positron orbiting an antiproton — and found agreement with ordinary hydrogen at parts-per-trillion precision. That is a direct test of CPT symmetry, using spectral lines that Balmer first catalogued in 1885 and that Schrödinger explained in 1926.

---

## What the orbital is not

Three pictures to be careful about.

The orbital is not a path. The isosurface pictures in chemistry textbooks — the 90% probability surfaces, the dumbbells, the cloverleaves — are not containing walls. The electron does not orbit inside the dumbbell. The dumbbell is the surface enclosing a region where there is 90% probability of finding the electron on a single measurement. On 10% of measurements the electron would be found outside it. The most-probable-radius versus $\langle r\rangle$ comparison I showed you earlier is the direct evidence: a path has one radius; a probability distribution has a peak and a mean that need not coincide.

The Bohr model is not essentially correct. It gets $E_n = -13.6\,\text{eV}/n^2$ right because hydrogen's $\mathfrak{so}(4)$ symmetry makes the energy depend on a single quantum number, and Bohr's angular momentum quantization $L = n\hbar$ happens to count that quantum number correctly for circular orbits. But Bohr's model has no wave functions, no radial probability densities, no node structure, no $\ell$-values other than $\ell = n$ (Bohr orbits always have maximum angular momentum; Schrödinger says $\ell$ runs from 0 to $n - 1$), and no selection rules. It is numerology that worked once.

And $|\psi|^2$ is not a continuous charge distribution smeared through space. It is the probability density for finding the electron at a point on a single position measurement. The electron remains a point particle. When you fire particles at hydrogen, you get a distribution of scattering events; run enough events and the histogram converges to $|\psi|^2$. The cloud shows where measurements land. It does not show where charge sits.

<!-- → [INFOGRAPHIC: three-panel misconception-vs-reality — panel 1: Bohr circular orbit (electron dot on ring) crossed out, replaced by 1s spherical density blob; panel 2: 90% isosurface dumbbell with dotted boundary and annotation "10% of measurements land outside"; panel 3: fluid-filled orbital crossed out, replaced by scatter plot of simulated position measurements converging toward |ψ|² as N grows; caption: "The cloud shows where measurements land, not where charge sits"] -->

---

## Still puzzling

There is one thing I cannot make feel inevitable, and I want to say it honestly.

The Laplace–Runge–Lenz vector is conserved classically because $1/r$ orbits do not precess, and Bertrand's theorem tells you that only $1/r$ and $r^2$ potentials have all bound orbits closed. The quantum $\mathfrak{so}(4)$ degeneracy and the classical closed-orbit property must be the same fact expressed in different languages. I can state the algebra; the commutators are well-defined; the derivation is correct. But I cannot make the connection feel obvious in the sense of "of course it had to be this way, look." The math is settled. The explanation, at the level of deep understanding rather than algebraic bookkeeping, is not there for me. If it ever becomes clear to you, let me know.

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

### Part 5 — Six failure modes to watch for

1. **Color-scale domain not reset on state change.** If the Viridis domain is set once at $n = 1$ and not updated, high-$n$ orbitals appear uniformly dark. Recompute the domain at every state change.

2. **Forgetting the $r^2$ Jacobian in $P(r)$.** Plotting $|R_{n\ell}|^2$ instead of $r^2|R_{n\ell}|^2$ makes the 1s density peak at $r = 0$ instead of $r = a_0$. The difference is visible and dramatic.

3. **Energy formula off by a sign.** $E_n = -13.6/n^2$, negative. If the energy diagram shows positive values, a sign was dropped.

4. **Selection rule logic too strict.** $\Delta m$ must be $0, +1,$ or $-1$ — all three. Some students implement this as exactly $0$.

5. **Quantum number ranges not enforced.** The combination $(n, \ell, m) = (1, 1, 0)$ asks for a Laguerre polynomial of degree $-1$. Constrain the sliders: $\ell$ max is $n - 1$; $m$ range is $-\ell$ to $+\ell$.

6. **Heat-map coordinate confusion.** For $x < 0$ in the xz-plane, $\phi = \pi$ not $\phi = 0$. Handling the sign of $x$ when computing the azimuthal angle correctly is required; otherwise the simulation renders a half-orbital.

---

## Exercises

### Warm-up

**7.1** The reduced mass of ordinary hydrogen is $\mu = m_p m_e/(m_p + m_e)$, where $m_p \approx 1836\,m_e$. (a) Compute $\mu$ as a fraction of $m_e$ to four significant figures. (b) By what fractional amount does using the exact $\mu$ rather than $m_e$ change the Bohr radius $a_0 = 4\pi\epsilon_0\hbar^2/(\mu e^2)$? (c) A muonic hydrogen atom replaces the electron with a muon ($m_\mu \approx 207\,m_e$). Compute the muonic Bohr radius $a_0^\mu$ and ground-state energy $E_1^\mu$. By what factors do they differ from ordinary hydrogen? *(Tests: reduced-mass arithmetic; understanding that every length and energy scale in hydrogen depends on μ.)*

**7.2** Verify that $\psi_{100}(r) = (\pi a_0^3)^{-1/2} e^{-r/a_0}$ is normalized by computing $\int |\psi_{100}|^2\,d^3r$ explicitly, using $\int_0^\infty r^2 e^{-2r/a_0}\,dr = a_0^3/4$. Then write down the radial probability density $P(r) = r^2|R_{10}(r)|^2$ and verify $\int_0^\infty P(r)\,dr = 1$. *(Tests: three-dimensional normalization integral; the role of the r² Jacobian.)*

**7.3** List all allowed $(n, \ell, m)$ combinations for $n = 3$. Verify the count gives $n^2 = 9$ orbital states and $2n^2 = 18$ states including spin. For each of the three constraints — $n \geq 1$, $\ell \leq n-1$, $|m| \leq \ell$ — write one sentence explaining where it comes from mathematically. *(Tests: quantum number enumeration; connecting each constraint to its origin.)*

### Application

**7.4** The ground-state calculation gives $r_\text{mp} = a_0$ and $\langle r\rangle = \frac{3}{2}a_0$ for the 1s state. For the 2s state the radial wave function is $R_{20}(r) = (8a_0^3)^{-1/2}(2 - r/a_0)e^{-r/(2a_0)}$. (a) Find the radial node — the value of $r$ at which $R_{20} = 0$. (b) Find $r_\text{mp}$ for the 2s state by maximizing $P(r) = r^2|R_{20}|^2$. (c) Compute $\langle r\rangle_{2s}$ using $\int_0^\infty r^n e^{-r/b}\,dr = n!\,b^{n+1}$. Do $r_\text{mp}$ and $\langle r\rangle_{2s}$ still differ? Why? *(Tests: two-radii argument applied to a higher state; node location; skewness of P(r).)*

**7.5** (a) Compute the wavelength of the Lyman $\alpha$ line ($n = 2 \to n = 1$) and confirm it falls in the ultraviolet. (b) Compute the wavelength of the Paschen $\alpha$ line ($n = 4 \to n = 3$) and confirm it falls in the near-infrared. (c) The Balmer $\alpha$ wavelength scales as $\lambda \propto 1/\mu$. Estimate the isotope shift in nm between ordinary hydrogen and deuterium ($m_d \approx 2m_p$), and explain why Urey could detect it. *(Tests: Rydberg formula across spectral series; isotope shift from reduced mass.)*

**7.6** For each of the following transitions, state whether it is electric-dipole allowed or forbidden and give the reason in terms of $\Delta\ell$: (a) $3p \to 1s$; (b) $3d \to 1s$; (c) $3p \to 2p$; (d) $3d \to 2p$; (e) $2s \to 1s$. For each forbidden transition, name one higher-order process through which it can still occur. *(Tests: selection rule application; the distinction between forbidden and impossible.)*

### Synthesis

**7.7** The $\mathfrak{so}(4)$ symmetry of hydrogen makes 2s and 2p degenerate at $-3.4$ eV. In sodium, the effective potential is no longer $-1/r$ and 3s lies at $-5.14$ eV, 3p at $-3.04$ eV. (a) Without measuring energy, what observable could distinguish 2s from 2p in hydrogen? (b) Compute the wavelength of the sodium 3p $\to$ 3s transition. (c) The sodium D line is a closely spaced doublet at 589.0 nm and 589.6 nm. What interaction — not discussed until Chapter 9 — splits the 3p level into two? Name the effect. *(Tests: connecting degeneracy to observables; sodium D line calculation; previewing spin-orbit coupling.)*

**7.8** Consider the superposition $\Psi(r,t) = \frac{1}{\sqrt{2}}\left[\psi_{100}e^{-iE_1t/\hbar} + \psi_{210}e^{-iE_2t/\hbar}\right]$. (a) Show that $|\Psi|^2$ contains a time-dependent cross-term oscillating at $\omega_{12} = (E_2 - E_1)/\hbar$. Compute $\omega_{12}$ in rad/s and the period $T_{12}$ in femtoseconds. (b) Compute $\langle z\rangle(t)$ and show it oscillates sinusoidally at $\omega_{12}$. (c) In two sentences, explain why this oscillating dipole moment represents the atom in the act of emitting a photon at frequency $\omega_{12}$, rather than sitting in either stationary state. *(Tests: time evolution of a superposition; oscillating dipole picture of a transition.)*

### Challenge

**7.9** The $n^2$ orbital degeneracy follows from $\sum_{\ell=0}^{n-1}(2\ell+1) = n^2$. Prove this identity. Then: in a hypothetical atom where energy depends on $n_r + \ell + 1$ (with $n_r = n - \ell - 1$ radial nodes), how many orbital states share energy level $N = n_r + \ell + 1$? Compare to hydrogen and explain in one sentence why Coulomb degeneracy requires energy to depend on $n = n_r + \ell + 1$ rather than on $n_r$ and $\ell$ separately. *(Tests: combinatorial counting; what is special about the accidental degeneracy.)*

**7.10** The general formula $\langle r\rangle_{n\ell} = \frac{a_0}{2}\left[3n^2 - \ell(\ell+1)\right]$ gives the mean radius for any hydrogen state. (a) Verify it for $(1,0)$ giving $\frac{3}{2}a_0$ and for $(2,0)$ giving $6a_0$. (b) For fixed $n$, does increasing $\ell$ increase or decrease $\langle r\rangle$? Use the centrifugal barrier picture to explain why this makes physical sense. (c) For $(n,\ell) = (3,2)$, compute $\langle r\rangle$ and compare it to the estimate $r_\text{mp} \approx n^2 a_0$. Are they the same? *(Tests: general expectation-value formula; connecting ℓ to the radial distribution; peak vs. mean for higher states.)*

---

**Chapter 8:** You have solved one-electron hydrogen completely. The next step is two electrons — helium — and immediately the problem becomes unsolvable analytically. The reason: electron-electron repulsion. Chapter 8 sets up the machinery of identical particles, antisymmetry, and the Pauli exclusion principle that governs every multi-electron atom in the periodic table.
