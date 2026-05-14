# Chapter 7 — The Hydrogen Atom

> The first system where quantum mechanics made precise predictions that matched experiment exactly: the Coulomb radial equation, the energy spectrum, and a visualizer that lets you see what an orbital actually is.

---

## 1. A 28-year-old empirical formula

In 1885, a Swiss mathematics teacher named Johann Balmer published a four-page note in *Annalen der Physik* observing that the visible spectral lines of hydrogen — H$_\alpha$ red, H$_\beta$ blue-green, H$_\gamma$ violet, H$_\delta$ violet — fit the formula

$$ \lambda = B \cdot \frac{n^2}{n^2 - 4}, \qquad n = 3, 4, 5, 6, $$

with $B \approx 364.5$ nm. He had no theory. He had four wavelengths from a lab notebook and a formula that nailed them. The formula was right. Nobody knew why for 28 years.

Niels Bohr offered a partial answer in 1913 with his planetary model — quantized circular orbits at radii $a_n = n^2 a_0$, with energies $E_n = -13.6 \text{ eV}/n^2$ — that reproduced Balmer's formula and extended it to the ultraviolet (Lyman) and infrared (Paschen) series. But Bohr's model had embarrassments. Why are the orbits quantized at integer $n$ and not, say, half-integer? Why circular and not elliptical? Why no radiation from accelerating charges in those orbits, as classical electromagnetism predicts? Bohr's quantization rule $L = n\hbar$ worked, but it was an ansatz, not a derivation.

Erwin Schrödinger spent Christmas of 1925 at the Alpine resort of Arosa working out the equation that would replace Bohr's planetary picture with a wave-mechanical description of hydrogen. He published the solution in *Annalen der Physik* the following spring (Schrödinger 1926 [verify volume]). The energies $E_n = -13.6 \text{ eV}/n^2$ fell out — same numbers as Bohr, but now without unjustified postulates. The orbits did not. Instead, what fell out was a probability density $|\psi_{n\ell m}(r,\theta,\phi)|^2$ — a function on space, telling you where the electron is likely to be found, but never *where it is*.

This chapter solves the hydrogen atom. We will use everything from Chapters 4 (operators), 5 (3D quantum mechanics and angular momentum), and 6 (spin). We will do the radial equation explicitly for the ground state and let the Schrödinger equation hand us $E_1 = -13.6$ eV and the Bohr radius $a_0 = 0.529$ Å. And we will confront the most damaging picture students arrive with from high-school chemistry — the orbital as the electron's path — with the simulation that finally makes the alternative visible.

**Learning objectives.** By the end of this chapter, you should be able to:

- Reduce the two-body hydrogen problem to a one-body problem with the reduced mass and a $1/r$ potential.
- Separate variables in spherical coordinates and write the radial equation with its effective potential, including the centrifugal barrier.
- Solve the radial equation for the 1s ground state from an exponential ansatz, recovering $E_1 = -13.6$ eV and $a_0 = 0.529$ Å.
- Compute the most probable radius and the expectation value $\langle r \rangle$ for 1s, and explain why they differ.
- State and apply the quantum-number constraints $n \geq 1$, $0 \leq \ell \leq n-1$, $|m| \leq \ell$, and explain where each constraint comes from.
- Identify the Lyman, Balmer, and Paschen series and compute photon wavelengths from $E_n$.
- State the electric-dipole selection rules $\Delta\ell = \pm 1$, $\Delta m = 0, \pm 1$ and recognize allowed vs. forbidden transitions.
- Build an interactive hydrogen orbital visualizer that displays $|\psi_{n\ell m}|^2$ as a 2D heat map, the radial probability $P(r) = r^2|R_{n\ell}|^2$ as a line plot, and an energy-level diagram with the $n^2$-degeneracy visible.

**Prerequisites.** Wave functions, the Born rule (Ch. 1–2). The time-independent Schrödinger equation (Ch. 2). Hilbert-space machinery and Hermitian operators (Ch. 4). Spherical harmonics, $L^2$ and $L_z$ eigenvalues, the universal angular part of central-force problems (Ch. 5). Spin and the fourth quantum number $m_s = \pm 1/2$ (Ch. 6). Calculus including integration by parts and gamma-function integrals of the form $\int_0^\infty x^n e^{-ax} dx = n!/a^{n+1}$.

---

## 2. Reducing two bodies to one

A hydrogen atom is a proton ($m_p \approx 1.673 \times 10^{-27}$ kg [verify CODATA]) and an electron ($m_e \approx 9.109 \times 10^{-31}$ kg), interacting via the Coulomb potential. The classical Hamiltonian for the two-body system is

$$ H = \frac{p_p^2}{2m_p} + \frac{p_e^2}{2m_e} - \frac{e^2}{4\pi\epsilon_0 |\vec{r}_e - \vec{r}_p|}. $$

Introduce center-of-mass and relative coordinates:

$$ \vec{R} = \frac{m_p \vec{r}_p + m_e \vec{r}_e}{m_p + m_e}, \qquad \vec{r} = \vec{r}_e - \vec{r}_p. $$

The Hamiltonian separates into a free-particle center-of-mass piece and a relative-motion piece:

$$ H = \frac{P^2}{2M} + \frac{p^2}{2\mu} - \frac{e^2}{4\pi\epsilon_0 r}, $$

where $M = m_p + m_e$ is the total mass and

$$ \mu = \frac{m_p m_e}{m_p + m_e} $$

is the **reduced mass**. The center-of-mass moves freely; drop it. The relative-motion Schrödinger equation,

$$ \left[ -\frac{\hbar^2}{2\mu}\nabla^2 - \frac{e^2}{4\pi\epsilon_0 r}\right]\psi(\vec{r}) = E \psi(\vec{r}), $$

is identical to that of a single particle of mass $\mu$ in an external Coulomb potential. Because $m_p \approx 1836 m_e$, the reduced mass differs from $m_e$ by about one part in 1836 — a 0.05% correction. For all the headline numbers in this chapter, we use $\mu \approx m_e$. The correction shows up in precision spectroscopy as the **isotope shift**: hydrogen, deuterium, and tritium have slightly different reduced masses and slightly different spectral lines. Harold Urey discovered deuterium in 1932 (with Brickwedde and Murphy, *Physical Review* 39, 164 [verify]) precisely by spotting the predicted shift in the Balmer series — Nobel 1934.

---

## 3. Separating variables and the centrifugal barrier

The potential $V(r) = -e^2/(4\pi\epsilon_0 r)$ depends only on $r$. So we can separate variables in spherical coordinates: $\psi(r,\theta,\phi) = R(r) Y(\theta,\phi)$. From Chapter 5 you already know that the angular part is solved universally by the spherical harmonics:

$$ Y_{\ell m}(\theta,\phi), \qquad \hat{L}^2 Y_{\ell m} = \hbar^2 \ell(\ell+1) Y_{\ell m}, \qquad \hat{L}_z Y_{\ell m} = m\hbar Y_{\ell m}, $$

with $\ell \in \{0, 1, 2, \ldots\}$ and $m \in \{-\ell, \ldots, +\ell\}$. The radial equation that remains, after substituting $u(r) = rR(r)$, looks like a 1D Schrödinger equation with an **effective potential**:

$$ -\frac{\hbar^2}{2\mu} \frac{d^2 u}{dr^2} + V_{\text{eff}}(r) u(r) = E u(r), $$

where

$$ \boxed{ V_{\text{eff}}(r) = -\frac{e^2}{4\pi\epsilon_0 r} + \frac{\hbar^2 \ell(\ell+1)}{2\mu r^2}. } $$

The second term is the **centrifugal barrier** — a repulsive $1/r^2$ contribution proportional to $\ell(\ell+1)$. It comes from the angular kinetic energy and plays the same role as the centrifugal pseudo-potential in classical orbits: angular momentum keeps the particle away from $r = 0$. For $\ell = 0$ ($s$ orbitals), no barrier — the electron can reach the nucleus. For $\ell \geq 1$ ($p$, $d$, $f$ orbitals), the barrier pushes the wave function away from the origin. This is exactly why $|\psi_{n\ell m}(0)|^2$ is nonzero only for $\ell = 0$ states — a fact that matters when atomic electrons interact with the nucleus, e.g., in the hyperfine 21 cm line of radio astronomy or in muonic-atom spectroscopy.

Boundary conditions. We need $u(r) \to 0$ at both $r = 0$ and $r \to \infty$, so that $\psi$ is normalizable. The first kills any divergence at the origin; the second kills any growing exponential at infinity. These two conditions together quantize the energy.

---

## 4. The 1s ground state — the deep dive

This is the chapter's earned explanation. We will solve the radial equation for $n = 1, \ell = 0$ by ansatz, recover $E_1 = -13.6$ eV and $a_0 = 0.529$ Å, normalize the wave function, and compute two different "average" radii. Half a page. Take your time.

### 4.1 Solving by ansatz

Set $\ell = 0$. The centrifugal barrier vanishes; $V_{\text{eff}} = V = -e^2/(4\pi\epsilon_0 r)$. The radial equation for $u(r)$:

$$ -\frac{\hbar^2}{2\mu} u'' - \frac{e^2}{4\pi\epsilon_0 r} u = E u. $$

Try the ansatz $u(r) = A r e^{-r/a}$, where $a$ is an unknown length scale and $A$ a normalization constant. Differentiate:

$$ u'(r) = A e^{-r/a}\left(1 - \frac{r}{a}\right), $$
$$ u''(r) = A e^{-r/a}\left(-\frac{2}{a} + \frac{r}{a^2}\right). $$

Substitute into the radial equation and divide by $A e^{-r/a}$ (the common factor):

$$ -\frac{\hbar^2}{2\mu}\left(-\frac{2}{a} + \frac{r}{a^2}\right) - \frac{e^2}{4\pi\epsilon_0 r} \cdot r = E \cdot r. $$

(Note the trick: the Coulomb term contributes $-(e^2/(4\pi\epsilon_0 r)) \cdot u(r) = -(e^2/(4\pi\epsilon_0 r)) \cdot A r e^{-r/a}$, so after dividing by $A e^{-r/a}$ we get $-e^2/(4\pi\epsilon_0)$, not $-e^2/(4\pi\epsilon_0 r)$.)

Distribute and collect terms by powers of $r$:

$$ \underbrace{\frac{\hbar^2}{\mu a}}_{\text{constant}} - \underbrace{\frac{\hbar^2}{2\mu a^2} r}_{\text{linear in }r} - \underbrace{\frac{e^2}{4\pi\epsilon_0}}_{\text{constant}} = E r. $$

For this to hold for all $r$, the constant terms and the linear terms must balance separately:

**Constant terms:** $\dfrac{\hbar^2}{\mu a} - \dfrac{e^2}{4\pi\epsilon_0} = 0$, giving

$$ \boxed{ a = a_0 = \frac{4\pi\epsilon_0 \hbar^2}{\mu e^2}. } $$

This is the **Bohr radius**. Plug in numbers:

$$ a_0 = \frac{(8.854 \times 10^{-12})(1.055 \times 10^{-34})^2}{(9.109 \times 10^{-31})(1.602 \times 10^{-19})^2} \approx 5.29 \times 10^{-11} \text{ m} \approx 0.529 \text{ Å}. $$

[CODATA 2018: $a_0 = 5.29177210903 \times 10^{-11}$ m, [verify current value].]

**Linear terms:** $-\dfrac{\hbar^2}{2\mu a^2} = E$. Substitute $a = a_0$:

$$ E_1 = -\frac{\hbar^2}{2\mu a_0^2} = -\frac{\mu e^4}{2(4\pi\epsilon_0)^2 \hbar^2} \approx -13.6 \text{ eV}. $$

[Precise CODATA value: $E_1 = -R_\infty hc \approx -13.6057$ eV [verify current Rydberg constant].]

The ansatz gave us both the Bohr radius and the ground-state energy from a single calculation. The cleverness is that $u(r) = A r e^{-r/a}$ has the right behavior at both boundaries — vanishing at $r = 0$ (because of the $r$ factor) and at $r \to \infty$ (because of the exponential) — and exactly one free length scale, which the equation itself determines.

### 4.2 Normalizing

The full ground-state wave function is

$$ \psi_{100}(r,\theta,\phi) = R_{10}(r) Y_{00}(\theta,\phi). $$

Since $u_{10}(r) = r R_{10}(r) = A r e^{-r/a_0}$, we have $R_{10}(r) = A e^{-r/a_0}$. Demand $\int |\psi_{100}|^2 d^3 r = 1$. The angular part contributes $\int |Y_{00}|^2 d\Omega = 1$ (because $Y_{00} = 1/\sqrt{4\pi}$ is already normalized over the sphere). The radial part gives

$$ \int_0^\infty |R_{10}|^2 r^2 dr = |A|^2 \int_0^\infty r^2 e^{-2r/a_0} dr = |A|^2 \cdot \frac{2}{(2/a_0)^3} = |A|^2 \cdot \frac{a_0^3}{4}. $$

Set this equal to 1: $A = 2/a_0^{3/2}$. So

$$ \boxed{ \psi_{100}(r) = \frac{1}{\sqrt{\pi a_0^3}} e^{-r/a_0}. } $$

Spherically symmetric. No angular structure. The ground state is, geometrically, a cloud of probability density centered on the nucleus, falling off exponentially.

### 4.3 The most probable radius and the expectation value — the chapter's signature move

If the electron were a particle on a definite orbit, "where is it?" would have one answer: the orbit's radius. The wave function gives a probability *distribution*, and any distribution has multiple summary statistics — the peak, the mean, the median — and these can differ.

The **radial probability density** $P(r)$ is the probability per unit radial distance of finding the electron between $r$ and $r + dr$, after integrating over angles:

$$ P(r) = r^2 |R_{10}(r)|^2 = \frac{4}{a_0^3} r^2 e^{-2r/a_0}. $$

The $r^2$ factor comes from the spherical volume element $r^2 \sin\theta \, dr \, d\theta \, d\phi$ and is doing real geometric work: even though $|\psi_{100}|^2$ is maximal at $r = 0$, the surface area of a shell at $r = 0$ is zero, so the *probability* of being near $r = 0$ is zero.

**Most probable radius.** Maximize $P(r)$. Take the derivative:

$$ \frac{dP}{dr} = \frac{4}{a_0^3}\left[2r - \frac{2r^2}{a_0}\right] e^{-2r/a_0} = \frac{8r}{a_0^3}\left(1 - \frac{r}{a_0}\right) e^{-2r/a_0}. $$

Zero at $r = 0$ (trivial minimum) and at

$$ \boxed{ r_{\text{mp}} = a_0. } $$

The most probable radius is exactly the Bohr radius. The peak of the probability distribution sits where Bohr put his orbit.

**Expectation value.** Compute $\langle r \rangle$:

$$ \langle r \rangle = \int_0^\infty r \cdot P(r) dr = \frac{4}{a_0^3} \int_0^\infty r^3 e^{-2r/a_0} dr. $$

Using $\int_0^\infty x^n e^{-bx} dx = n!/b^{n+1}$ with $n = 3$, $b = 2/a_0$:

$$ \langle r \rangle = \frac{4}{a_0^3} \cdot \frac{3!}{(2/a_0)^4} = \frac{4}{a_0^3} \cdot \frac{6 a_0^4}{16} = \frac{3 a_0}{2}. $$

$$ \boxed{ \langle r \rangle_{1s} = \frac{3}{2} a_0. } $$

The expectation value of $r$ is $1.5 a_0$, fifty percent larger than the most probable radius.

**Stop and look.** These two numbers describe the same probability distribution $P(r)$. The peak is at $a_0$. The mean is at $1.5 a_0$. They are different because $P(r)$ is *skewed* — a long tail at large $r$ pulls the mean to the right of the peak.

This is the chapter's signature pedagogical move. If the orbital were a path the electron travels — a circular path at some radius — there would be exactly one radius. There would be no distinction between "most probable" and "average." The fact that these two numbers are different is the geometric fingerprint of the orbital being a probability distribution, not a path. A single number cannot describe where the electron is, because the electron is not anywhere in particular until you measure it.

The Bohr model put the electron in a circular orbit at radius $a_0$ and got the energy right. The Schrödinger solution puts the *peak* of the probability distribution at $a_0$ and the *mean* at $1.5 a_0$, and reproduces the same $-13.6$ eV. Same number, different meaning. The Bohr model is, in retrospect, a numerical accident — an accident enabled by hydrogen's hidden $SO(4)$ symmetry, of which more in §6.

---

## 5. The full spectrum and the quantum-number rules

The 1s solution was straightforward because of the ansatz. The general $(n, \ell)$ solution requires the full Frobenius series method applied to the radial equation, which leads to the **associated Laguerre polynomials** $L_{n-\ell-1}^{2\ell+1}$. The radial wave functions take the form

$$ R_{n\ell}(r) = \mathcal{N}_{n\ell} \cdot r^\ell \cdot e^{-r/(n a_0)} \cdot L_{n-\ell-1}^{2\ell+1}\!\left(\frac{2r}{n a_0}\right), $$

with normalization constant $\mathcal{N}_{n\ell}$ fixed by $\int_0^\infty |R_{n\ell}|^2 r^2 dr = 1$. The energies are

$$ \boxed{ E_n = -\frac{\mu e^4}{2(4\pi\epsilon_0)^2 \hbar^2 n^2} = -\frac{13.6 \text{ eV}}{n^2}. } $$

Two surprises hide in this formula. First, the energy depends *only* on $n$, not on $\ell$ or $m$. Second, the allowed range of $\ell$ is restricted to $0 \leq \ell \leq n - 1$. Let me explain where each constraint comes from, because students who memorize the rules without seeing the reasons stumble in upper-division courses.

**Where $n \geq 1$ comes from.** Normalizability at $r \to \infty$. The Frobenius series for the radial wave function terminates only if a certain dimensionless parameter (related to $E$) takes integer values. Below $n = 1$, the series fails to terminate and $u(r)$ grows exponentially at infinity, killing normalizability.

**Where $\ell \leq n - 1$ comes from.** The Laguerre polynomial $L_{n-\ell-1}^{2\ell+1}$ has degree $n - \ell - 1$. For the radial wave function to exist, this degree must be $\geq 0$, hence $\ell \leq n - 1$. For $n = 1$, only $\ell = 0$ is allowed (1s). For $n = 2$, $\ell \in \{0, 1\}$ (2s, 2p). For $n = 3$, $\ell \in \{0, 1, 2\}$ (3s, 3p, 3d).

**Where $|m| \leq \ell$ comes from.** Chapter 5. The angular operator inequality $L^2 \geq L_z^2$ forces $\ell(\ell+1)\hbar^2 \geq m^2 \hbar^2$, hence $|m| \leq \ell$.

**Degeneracy.** At each $n$, the number of orbital states is

$$ \sum_{\ell=0}^{n-1}(2\ell + 1) = n^2. $$

Adding spin ($m_s = \pm 1/2$) doubles this to $2n^2$. So the $n = 1$ shell holds 2 electrons, $n = 2$ holds 8, $n = 3$ holds 18, $n = 4$ holds 32 — exactly the row lengths of the periodic table. This is not a coincidence we hand back; it is structural.

### 5.1 The first few wave functions

Here are the explicit forms for $n \leq 2$, which the simulation will plot:

$$ \psi_{100} = \frac{1}{\sqrt{\pi a_0^3}} e^{-r/a_0} \quad \text{(1s, spherically symmetric)} $$

$$ \psi_{200} = \frac{1}{\sqrt{32\pi a_0^3}}\left(2 - \frac{r}{a_0}\right) e^{-r/(2a_0)} \quad \text{(2s, radial node at } r = 2a_0\text{)} $$

$$ \psi_{210} = \frac{1}{\sqrt{32\pi a_0^3}} \frac{r}{a_0} e^{-r/(2a_0)} \cos\theta \quad \text{(2p}_z\text{, angular node in xy-plane)} $$

$$ \psi_{21\pm 1} = \mp\frac{1}{\sqrt{64\pi a_0^3}} \frac{r}{a_0} e^{-r/(2a_0)} \sin\theta \, e^{\pm i\phi} \quad \text{(2p}_{\pm 1}\text{, complex)} $$

[Normalizations from Griffiths §4.2, verify Table 4.7 of the adopted edition.]

A useful node-counting rule emerges: the total number of nodes is $n - 1$, partitioned into $n - \ell - 1$ radial nodes and $\ell$ angular nodes. The 1s state (n=1, ℓ=0) has zero nodes. The 2s state has one radial node (at $r = 2a_0$) and zero angular nodes. The 2p states have zero radial nodes and one angular node. The 3d states have zero radial nodes and two angular nodes. The simulation displays the node count for every state.

### 5.2 The chemistry orbitals vs. the $L_z$ eigenstates

Chemistry textbooks draw three "p orbitals" labeled $p_x, p_y, p_z$, as orthogonal dumbbells along the coordinate axes. These are *real* linear combinations of the complex $L_z$ eigenstates $\psi_{21,\pm 1}$ and $\psi_{210}$:

$$ p_z \equiv Y_{10} \propto \cos\theta, $$
$$ p_x \equiv -\frac{Y_{11} - Y_{1,-1}}{\sqrt{2}} \propto \sin\theta \cos\phi, $$
$$ p_y \equiv i\frac{Y_{11} + Y_{1,-1}}{\sqrt{2}} \propto \sin\theta \sin\phi. $$

The $p_z$ state *is* an $L_z$ eigenstate (with $m = 0$). The $p_x$ and $p_y$ states are not — they are superpositions of $m = +1$ and $m = -1$. Both descriptions are correct; they answer different questions. Chemists working with bonding geometries want the real dumbbells. Physicists working with magnetic fields or spectroscopy want the $L_z$ eigenstates because they diagonalize $L_z$. Knowing both lets you move between the two pictures fluently.

---

## 6. The hidden symmetry — why energy depends only on $n$

For a generic central potential $V(r)$, the energy depends on both $n$ (the radial quantum number) and $\ell$ (the angular quantum number). Hydrogen is special: $E$ depends only on $n$. The 2s and 2p states are degenerate even though they have different angular structure. The 3s, 3p, and 3d are all degenerate. This "extra" degeneracy is called the **Coulomb degeneracy** and it has a deeper origin.

The Coulomb potential $-1/r$ is unique among central potentials in admitting a *second* conserved vector beyond angular momentum: the **Laplace–Runge–Lenz vector**

$$ \vec{M} = \frac{1}{2m_e}(\vec{p} \times \vec{L} - \vec{L} \times \vec{p}) - \frac{e^2}{4\pi\epsilon_0}\hat{r}. $$

In classical mechanics, $\vec{M}$ points along the major axis of the Kepler ellipse and is conserved because $1/r$ orbits do not precess. In quantum mechanics, the commutators of the six components $\{\vec{L}, \vec{M}\}$ close on each other, forming the Lie algebra $\mathfrak{so}(4)$ — the symmetry algebra of rotations in four dimensions. Wolfgang Pauli used this algebra in 1926 (*Zeitschrift für Physik* 36, 336 [verify]) to solve hydrogen *algebraically* — before Schrödinger published the wave-mechanical solution.

The chapter does not derive the $\mathfrak{so}(4)$ machinery; that is a graduate-level topic. But I want you to know that the $n^2$-degeneracy of hydrogen is not generic to "rotational symmetry." It is rotational symmetry plus an extra conserved vector that exists *only* because the potential is exactly $1/r$. The moment the potential departs from $1/r$ — for instance, in a multi-electron atom where inner electrons partially screen the nucleus — the LRL symmetry is broken and the $\ell$-degeneracy splits. In sodium (Z = 11), the 3s lies below 3p lies below 3d. The "sodium D lines" (the bright yellow doublet at 589 nm) are the 3p → 3s transitions, and their existence is direct evidence that sodium's effective single-electron potential is no longer pure $1/r$. The chapter on identical particles (Ch. 8) sets up the machinery to handle this.

---

## 7. The hydrogen spectrum and selection rules

### 7.1 The spectral series

Transitions $\psi_{n_i \ell_i m_i} \to \psi_{n_f \ell_f m_f}$ emit (or absorb) a photon whose energy is the difference of the initial and final levels:

$$ \hbar\omega = E_{n_i} - E_{n_f} = 13.6 \text{ eV}\left(\frac{1}{n_f^2} - \frac{1}{n_i^2}\right). $$

Named series, by final state:

| Series | $n_f$ | Wavelength range |
|---|---|---|
| Lyman | 1 | UV |
| Balmer | 2 | Visible |
| Paschen | 3 | Near IR |
| Brackett | 4 | IR |
| Pfund | 5 | IR |

**Balmer** $\alpha$ (the 3 → 2 transition) sits at 656.281 nm [verify NIST] — the red line of the hydrogen Balmer spectrum, the one you see in the H II emission nebulae photographed by every observatory. **Lyman** $\alpha$ (2 → 1) sits at 121.567 nm in the vacuum UV. These two lines are workhorses of astrophysics: redshifted Lyman $\alpha$ traces hydrogen out to the highest-redshift galaxies; Balmer $\alpha$ traces star-forming regions.

### 7.2 Selection rules

Not every transition is allowed. The electric-dipole matrix element $\langle\psi_f | \vec{r} | \psi_i\rangle$ governs the rate of single-photon emission. Computing the angular part of this integral (using the spherical harmonic algebra from Ch. 5) shows that the integral is nonzero only when

$$ \boxed{ \Delta\ell = \pm 1, \qquad \Delta m_\ell = 0, \pm 1. } $$

The $\Delta\ell = \pm 1$ rule comes from parity: the photon carries angular momentum 1, and the angular integrand has definite parity, so $\ell$ must change by an odd integer; the algebra forces this to be exactly $\pm 1$. The $\Delta m_\ell$ rule comes from the azimuthal symmetry.

A transition that violates these rules is *electric-dipole forbidden*. It can still occur, but at vastly reduced rate via higher-order processes (magnetic dipole, electric quadrupole, two-photon emission). The 2s → 1s transition in hydrogen has $\Delta\ell = 0$ — forbidden in the dipole approximation — and proceeds via two-photon emission with a lifetime of about 0.12 s [verify], compared to the ~$10^{-9}$ s lifetime of allowed transitions. This eight-order-of-magnitude difference is what makes the 2s state metastable, and it is the basis of precision hydrogen spectroscopy (the Lamb shift, hyperfine measurements, and antihydrogen tests of CPT).

### 7.3 Worked transition: Balmer $\alpha$

The 3 → 2 transition energy is

$$ \Delta E = 13.6 \text{ eV}\left(\frac{1}{4} - \frac{1}{9}\right) = 13.6 \times \frac{5}{36} \approx 1.889 \text{ eV}. $$

The photon wavelength:

$$ \lambda = \frac{hc}{\Delta E} = \frac{1240 \text{ eV nm}}{1.889 \text{ eV}} \approx 656.3 \text{ nm}. $$

Compare to the experimental value 656.281 nm [verify NIST]. Agreement to better than 0.05%, with no fudge factors. This is what Balmer's empirical 1885 formula was missing: an explanation.

---

## 8. Three misconceptions to dismantle

**Misconception 1: "Orbitals are paths the electron travels."** This is the picture from intro chemistry — "the 1s orbital is a spherical orbit." It is wrong. $|\psi_{n\ell m}|^2$ is a probability density: integrate it over a region and you get the probability of finding the electron in that region on a single position measurement. The "dumbbell" pictures chemists draw are *isosurfaces* of $|\psi|^2$ — surfaces enclosing some fixed fraction (usually 90%) of the total probability. The electron does not orbit. The most-probable-radius vs. $\langle r \rangle$ comparison in §4.3 is the empirical evidence: a path has one radius; a probability distribution has many summary statistics.

**Misconception 2: "The Bohr model is essentially correct."** Bohr's model gets $E_n = -13.6 \text{ eV}/n^2$ right and gets the Balmer wavelengths right. It gets these answers right by a numerical accident: hydrogen's hidden $\mathfrak{so}(4)$ symmetry makes the energy depend on a single quantum number, and Bohr's quantization rule $L = n\hbar$ correctly identifies that quantum number for circular orbits. But Bohr's model has no machinery for:

- Wave functions (so no probability density, no node structure).
- Angular momentum quantum numbers other than $\ell = n$ (Bohr orbits have $L = n\hbar$ always; Schrödinger says $\ell$ can range from 0 to $n-1$).
- Multi-electron atoms (helium binding energy is off by 30 eV in Bohr's picture; see §A.4 below).
- Spectral fine structure (relativistic corrections, spin-orbit coupling).
- Selection rules.
- Anything quantum-mechanical about the electron's spatial distribution.

The Bohr model is a pre-Schrödinger numerology that worked once. It is not "essentially correct"; it is a special case that the full theory has long since superseded.

**Misconception 3: "$|\psi|^2$ is the electron's charge distribution."** This shows up in chemistry texts that smear the electron's charge over the orbital. It is closer to right than the orbit picture — at least there is no path — but it is still wrong. $|\psi|^2$ is the *probability density* for finding the electron at a point on a single position measurement. The electron is a point particle whose location is governed by a probability distribution, not a continuous fluid of charge. The distinction matters in scattering experiments: when you fire something at hydrogen and measure where it bounces, you get a probability distribution of scattering events, not the result of a single fluidic charge density. Run enough scattering events and the histogram converges to $|\psi|^2$.

---

## 9. LLM Exercise — Building the Hydrogen Orbital Visualizer

This is the headline simulation of the book. You are going to render $|\psi_{n\ell m}(x, 0, z)|^2$ as a 2D heat map, the radial probability density $P(r) = r^2|R_{n\ell}|^2$ as a line plot beneath it, and an interactive energy-level diagram. Drag the $(n, \ell, m)$ sliders and watch the orbital reorganize. Click a state to highlight it on the energy diagram. Toggle into transition mode and pick an initial and final state to compute the emitted photon's wavelength.

### 9.1 The CLAUDE.md prompt

Append this to your existing project's `CLAUDE.md`:

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

### 9.2 The simulation prompt — four-move structure

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

### 9.3 Exploration tasks

1. **Confirm the 1s headline numbers.** Set (n, ℓ, m) = (1, 0, 0). Read off $r_{mp}$ and $\langle r \rangle$. Confirm $r_{mp} \approx 1.00 a_0$ and $\langle r \rangle \approx 1.50 a_0$. These two different numbers describe the same probability distribution. Stop and look at the heat map: it is a spherical blob. There is no "ring" at $a_0$.

2. **Count nodes.** Set (2, 0, 0) — the 2s state. The radial probability plot should show two peaks separated by a zero at $r = 2a_0$. That zero is the radial node. The heat map shows two concentric shells with a dark ring between them. Now set (3, 1, 0) — the 3p$_z$ state. Predict the node count using $n - 1 = 2$ total, partitioned into $n - \ell - 1 = 1$ radial and $\ell = 1$ angular. Verify on the simulation.

3. **The $n^2$ degeneracy.** Switch among (2, 0, 0), (2, 1, 0), (2, 1, +1), (2, 1, -1). All four have $E = -3.4$ eV — they sit on the same horizontal line in the energy diagram. The shapes differ dramatically. The energy diagram makes the degeneracy visible as the lines that *don't split*. Same energy, different geometry.

4. **Compute the Balmer $\alpha$ wavelength.** Enter transition mode. Set initial state $(n_i, \ell_i, m_i) = (3, 1, 0)$ and final $(n_f, \ell_f, m_f) = (2, 0, 0)$. Read the wavelength. Confirm $\lambda \approx 656$ nm. Verify the transition is ALLOWED ($\Delta\ell = -1$).

5. **A forbidden transition.** Set $(n_i, \ell_i, m_i) = (2, 0, 0)$ and $(n_f, \ell_f, m_f) = (1, 0, 0)$ — the 2s → 1s transition. Read the simulation's verdict. It should flag this as FORBIDDEN ($\Delta\ell = 0$). This is the metastable 2s state.

6. **Real vs. complex orbitals.** Switch the orbital-set dropdown from "complex $Y_{\ell m}$" to "real chemistry orbitals." Set ($n$, sub-shell) = (2, p). Cycle through $p_x, p_y, p_z$ and watch the dumbbells rotate. Switch back to complex; cycle through $m = -1, 0, +1$. The $m = 0$ case is the same as $p_z$; the $m = \pm 1$ cases are azimuthally symmetric blobs (with nontrivial complex phase that the magnitude plot does not show).

### 9.4 Extension prompt — Time evolution in a superposition

A stationary state has a time-independent probability density. To see something move, you build a coherent superposition:

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

This is the simulation that makes "atomic transitions are coherent superpositions evolving in time" finally visible. Most undergraduate treatments stop at "the electron jumps from one orbital to another." That picture is wrong: the electron's wave function continuously sloshes between configurations, and the photon emission is the dipole-radiation tail of the oscillation.

### 9.5 Six failure modes to watch for

1. **Color-scale domain not reset on state change.** If you set the Viridis domain once at $n = 1$ and then switch to $n = 4$ (where peak density is hundreds of times smaller), the high-$n$ orbital will look uniformly dark. Recompute the domain at every state change.

2. **Forgetting the $r^2$ Jacobian in $P(r)$.** A common bug: students plot $|R_{n\ell}|^2$ instead of $r^2 |R_{n\ell}|^2$. The former peaks at $r = 0$ for 1s; the latter peaks at $r = a_0$. The visible difference is dramatic: the radial probability plot for 1s should have its peak at $r = a_0$, not at the origin.

3. **Energy formula off by a sign.** $E_n = -13.6/n^2$, *negative* (bound states). If your energy diagram shows positive values, you dropped a sign somewhere.

4. **Selection rule logic too strict.** $\Delta m_\ell$ must be $0, +1,$ or $-1$. Some students implement this as exactly $0$. Allow all three.

5. **Quantum number ranges not enforced.** If sliders allow (n, ℓ, m) = (1, 1, 0), the simulation will try to evaluate a Laguerre polynomial of degree $-1$ and produce garbage. Constrain the sliders: $\ell$ slider's max is $n - 1$; $m$ slider's range is $-\ell$ to $+\ell$.

6. **Heat-map coordinate confusion.** The xz-plane has $\phi = 0$, but $x > 0$ corresponds to $\phi = 0$ and $x < 0$ to $\phi = \pi$. Some students use $\phi = 0$ everywhere and get a half-orbital. Correctly handle the sign of $x$ when computing the azimuthal angle.

---

## 10. Synthesis and the path forward

This chapter is the central triumph of single-particle quantum mechanics. You started with the 1885 Balmer formula — an empirical fit with no theory — and ended with a closed-form solution of the bound-state Schrödinger equation that reproduces Balmer's wavelengths to better than 0.05%, predicts every line of the Lyman and Paschen and higher series, and produces a complete probability-density description of the electron in hydrogen.

You can now:

- Reduce two bodies (proton + electron) to one body (reduced mass + Coulomb potential).
- Separate variables in spherical coordinates and write the radial equation with its centrifugal barrier.
- Solve the radial equation for 1s explicitly, recovering the Bohr radius and the ground-state energy from one ansatz.
- Compute most-probable and expectation-value radii and explain why they differ — the geometric fingerprint of "orbital is not a path."
- State the quantum-number constraints and explain their origins (normalizability, polynomial degree, angular operator inequality).
- Compute Rydberg-formula transitions and identify spectral series.
- Apply the dipole selection rules and distinguish allowed from forbidden transitions.
- Render and manipulate the full family of orbitals up to $n = 4$ with your own simulation.

What this chapter does *not* address, and what is coming:

- **Multi-electron atoms.** Helium, lithium, and the rest of the periodic table involve electron-electron Coulomb repulsion, which breaks the $\mathfrak{so}(4)$ symmetry and splits the $\ell$-degeneracy. Chapter 8 sets up the indistinguishability and antisymmetry machinery.
- **Fine structure.** The 2p$_{1/2}$ and 2p$_{3/2}$ levels split by about $10^{-4}$ eV due to relativistic corrections and spin-orbit coupling. Chapter 9 (perturbation theory) computes this from first principles.
- **Lamb shift.** The 2s$_{1/2}$ and 2p$_{1/2}$ levels are degenerate in non-relativistic Schrödinger theory, in Dirac theory, but split by about 1058 MHz [verify] in experiment — the first observational evidence for the radiative corrections of QED (Lamb & Retherford 1947, *Physical Review* 72, 241 [verify]). This is a Ch. 13 topic.
- **The proton radius puzzle.** Spectroscopy of muonic hydrogen — where a muon replaces the electron and sits 200 times closer to the proton — gave a proton charge radius about 4% smaller than electronic measurements were yielding around 2010 (Pohl et al. 2010, *Nature* 466, 213 [verify]). The discrepancy drove a decade of precision experiments and largely converged to the smaller value by 2018 (CODATA 2018 adopted 0.8414 fm [verify]). Hydrogen spectroscopy is still where new physics gets tested.
- **Antihydrogen.** The ALPHA collaboration at CERN has trapped antihydrogen ($\bar{p} + e^+$) and measured the 1S–2S transition, finding agreement with hydrogen at the parts-per-trillion level (Ahmadi et al. 2018, *Nature* 557, 71 [verify]). A direct test of CPT symmetry.

Hydrogen is the foundation. Every multi-electron atom is built from hydrogen-like single-particle orbitals plus the antisymmetry of Chapter 8. The visualizer you built will travel forward: in Chapter 8 you will extend it to handle two-electron products and Slater determinants; in Chapter 9 you will see how perturbations split the levels you computed here.

---

**What would change my mind:** a precision measurement of a hydrogen transition that disagrees with the Schrödinger + Dirac + QED prediction at a level larger than current theoretical uncertainty, after all known systematic effects are accounted for.

**Still puzzling:** the $\mathfrak{so}(4)$ symmetry of the Coulomb problem — the existence of the Laplace–Runge–Lenz vector — is a fact about the specific potential $-1/r$ that I can state and use, but I do not have a deep explanation for why this potential, of all central potentials, admits the extra conserved vector. The standard answer ("it's algebraically what falls out") leaves me unsatisfied.

**Tags:** hydrogen atom, Coulomb potential, radial equation, Bohr radius, Rydberg formula, spherical harmonics, orbital visualizer, Balmer series, selection rules, D3.js
