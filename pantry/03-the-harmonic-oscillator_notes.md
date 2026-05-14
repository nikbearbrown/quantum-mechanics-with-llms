# Research Notes: Chapter 03 — The Harmonic Oscillator
**Source:** TIKTOC.md chapter entry (lines 206–251)
**Notes file:** 03-the-harmonic-oscillator_notes.md
**Corresponding chapter:** chapters/03-harmonic-oscillator.md (not yet written)
**Generated:** 2026-05-13

---

## Chapter summary (from TIKTOC.md)

**One-line:** Students solve the quantum harmonic oscillator using ladder operators — the algebraic method — and build a simulation showing the energy eigenstates, coherent states, and their time evolution.

**Chapter description:** The harmonic oscillator is the most important exactly solvable system in quantum mechanics. It appears everywhere — molecular vibrations, photons in a cavity, phonons, quantum field theory. This chapter teaches two approaches: the power series (analytic) method and the ladder operator (algebraic) method. The algebraic method is emphasized because it introduces the notation and thinking that carries forward to angular momentum and quantum field theory. Coherent states — the quantum states that most resemble classical oscillation — are introduced as the physically interesting superpositions. The simulation shows Gaussian wave packets sloshing back and forth without spreading (coherent states) versus spreading (other superpositions).

**Core concepts (from TIKTOC):** Hamiltonian $\hat{H}=\hat{p}^2/2m + (1/2)m\omega^2\hat{x}^2$; ladder operators $\hat{a}_\pm = (1/\sqrt{2m\hbar\omega})(\mp i\hat{p} + m\omega\hat{x})$; commutator $[\hat{a}_-, \hat{a}_+] = 1$; energy levels $E_n = (n+1/2)\hbar\omega$; Hermite polynomial wave functions; coherent states; quantum-classical correspondence.

**Arc position:** Closes Act One — the second canonical exactly solvable system after the infinite square well, and the gateway to the operator formalism in Chapter 4.

---

## A. Conceptual foundations

### A.1 The Hamiltonian and why this system matters

The quantum harmonic oscillator (QHO) has the simplest non-trivial Hamiltonian in physics:
$$\hat{H} = \frac{\hat{p}^2}{2m} + \frac{1}{2}m\omega^2\hat{x}^2$$
Two terms. One kinetic. One quadratic in position. Nothing fancy. And yet this object appears in nearly every physical system we can write down, because any smooth potential $V(x)$ with a stable equilibrium at $x_0$ looks like a quadratic to leading order: $V(x) \approx V(x_0) + (1/2)V''(x_0)(x-x_0)^2$. The linear term vanishes at the minimum. The quadratic term is what is left. Drop the constant, identify $V''(x_0)$ as $m\omega^2$, and a generic small-oscillation problem becomes the harmonic oscillator. That is why molecular vibrations, lattice phonons, and the modes of the electromagnetic field all reduce — at the lowest level of approximation — to this same Hamiltonian.

The classical analogue is a mass on a spring obeying $F = -kx$ with $\omega = \sqrt{k/m}$ (Liboff §7.2, p. 191). Classically the energy is continuous: any amplitude is allowed and $E = (1/2)kx_0^2$ for turning points at $\pm x_0$. The quantum version forces two changes. First, the energy is quantized: $E_n = (n+1/2)\hbar\omega$ with $n = 0, 1, 2, \ldots$. Second, the ground state is not at rest — it has energy $E_0 = \hbar\omega/2$. This is the **zero-point energy**, and it is not an accounting artifact.

**Why specify?** "Harmonic oscillator" is a phrase that hides two different objects. The *classical* HO is a trajectory $x(t) = A\cos(\omega t + \phi)$ with continuous $A$. The *quantum* HO is a discrete energy spectrum and a set of eigenfunctions whose probability densities are *static* — they do not oscillate at all (Griffiths §2.3). The chapter has to keep these straight from the first paragraph or students will spend the rest of the semester confusing eigenstates with classical motion.

**Misconception:** *"$E_0 = \hbar\omega/2$ is a mathematical artifact — you can subtract it off."* No. It is forced by the uncertainty principle. A state localized at $x = 0$ with $p = 0$ would have $\sigma_x = \sigma_p = 0$, violating $\sigma_x\sigma_p \geq \hbar/2$. The ground state is the *minimum-uncertainty* compromise: a Gaussian wide enough in $x$ to spread $p$ just enough to satisfy the bound, with $\langle\hat{H}\rangle = \hbar\omega/2$ as the price (Griffiths §2.3.2, Problem 2.11). Measurable consequences include the **Casimir force** between conducting plates, [demonstrated experimentally by Lamoreaux in 1997](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.78.5) to within 5% of theory, and the fact that liquid helium does not freeze at atmospheric pressure even at $T = 0$ — zero-point motion is enough to keep it liquid.

**Worked example:** Write down $\hat{H}$, identify $\omega$ from $V''(x_0)$ for a generic potential, estimate the ground-state energy for a diatomic molecule (e.g., HCl, $\omega \approx 5.4 \times 10^{14}$ rad/s [verify against NIST WebBook]).

**Sources:** Griffiths §2.3; Liboff §7.2 (p. 190–198); pantry text confirms (lines 9992–10090).

### A.2 Ladder operators — the algebraic move

The clever trick is to factor the Hamiltonian. Define:
$$\hat{a}_\pm = \frac{1}{\sqrt{2\hbar m\omega}}\left(\mp i\hat{p} + m\omega\hat{x}\right)$$
Then a short calculation using $[\hat{x}, \hat{p}] = i\hbar$ gives:
$$[\hat{a}_-, \hat{a}_+] = 1 \qquad \hat{H} = \hbar\omega\left(\hat{a}_+\hat{a}_- + \tfrac{1}{2}\right)$$
And from $[\hat{H}, \hat{a}_\pm] = \pm\hbar\omega\,\hat{a}_\pm$, if $|n\rangle$ is an eigenstate with energy $E_n$, then $\hat{a}_+|n\rangle$ is an eigenstate with energy $E_n + \hbar\omega$ and $\hat{a}_-|n\rangle$ with energy $E_n - \hbar\omega$. The operators climb and descend the energy ladder. The descent has to stop somewhere — the energies cannot go below zero because $\hat{H} = \hat{p}^2/2m + (1/2)m\omega^2\hat{x}^2$ is manifestly non-negative — so there exists a ground state $|0\rangle$ with $\hat{a}_-|0\rangle = 0$. From this single condition and the algebra:
$$E_n = \left(n + \tfrac{1}{2}\right)\hbar\omega, \qquad \hat{a}_+|n\rangle = \sqrt{n+1}\,|n+1\rangle, \qquad \hat{a}_-|n\rangle = \sqrt{n}\,|n-1\rangle$$
No differential equations. The entire spectrum drops out of the commutator $[\hat{a}_-, \hat{a}_+] = 1$.

**Misconception:** *"Ladder operators are a trick — a slick shortcut to the same answer the analytic method gives."* No. They generalize. In quantum field theory, $\hat{a}_+$ and $\hat{a}_-$ are the **creation and annihilation operators** for photons: a state with $n$ excitations of a single mode of the EM field is a state with $n$ photons. The Hamiltonian $\hbar\omega(\hat{a}_+\hat{a}_- + 1/2)$ is the energy of $n$ photons of frequency $\omega$ plus the zero-point $\hbar\omega/2$. Lahiri & Pal's *First Book of QFT* (pantry) makes this connection explicit — the harmonic oscillator is the building block of every free quantum field. Chapter 6 will use the same algebra for angular momentum: $\hat{J}_\pm = \hat{J}_x \pm i\hat{J}_y$ raise and lower $m$. The "trick" is the structure.

**Worked example:** Derive the spectrum from $[\hat{a}_-, \hat{a}_+] = 1$ alone, using the non-negativity of $\hat{H}$ to terminate the ladder downward. (Griffiths §2.3.1.)

**Sources:** Griffiths §2.3.1 (algebraic method); Lahiri & Pal, *A First Book of Quantum Field Theory* (pantry).

### A.3 Hermite polynomials — the analytic confirmation

The same problem solved by power series. Substitute $\psi(x) = h(\xi)e^{-\xi^2/2}$ with $\xi = \sqrt{m\omega/\hbar}\,x$ into the time-independent Schrödinger equation and require polynomial solutions for normalizability. The condition that the series terminates fixes the energy: same $E_n = (n+1/2)\hbar\omega$, no surprise. The polynomial that drops out is the **Hermite polynomial** $H_n(\xi)$:
$$\psi_n(x) = \left(\frac{m\omega}{\pi\hbar}\right)^{1/4}\frac{1}{\sqrt{2^n n!}}\,H_n\!\left(\sqrt{\tfrac{m\omega}{\hbar}}\,x\right)e^{-m\omega x^2/(2\hbar)}$$
with $H_0 = 1$, $H_1 = 2\xi$, $H_2 = 4\xi^2 - 2$, $H_3 = 8\xi^3 - 12\xi$, etc., generated by the Rodrigues formula or the recursion $H_{n+1} = 2\xi H_n - 2n H_{n-1}$.

Two facts students need to internalize. (1) Each eigenstate has $n$ nodes (zeros, not counting $\pm\infty$). The ground state has none, the first excited state crosses zero once, and so on. (2) The classical turning points are at $\xi_n = \sqrt{2n+1}$. For large $n$, $|\psi_n|^2$ piles up *near* the turning points where the classical particle spends the most time — the **correspondence principle** in action. For small $n$, it does the opposite: the ground state is *most likely* to be found at the center where the classical particle moves fastest.

**Misconception:** *"The wave functions look like oscillating bell curves."* Half right. They are oscillating *and* damped by a Gaussian envelope. The Gaussian dominates outside the turning points; the Hermite polynomial dominates inside. Tunneling into the classically forbidden region — $|x| > \xi_n\sqrt{\hbar/m\omega}$ — is real and finite. For the ground state, about 16% of the probability is outside the classical turning points [verify exact number from Griffiths Problem 2.15].

**Worked example:** Compute $\langle\hat{x}\rangle$, $\langle\hat{x}^2\rangle$, $\langle\hat{p}\rangle$, $\langle\hat{p}^2\rangle$ for $|n\rangle$ using $\hat{x} = \sqrt{\hbar/2m\omega}(\hat{a}_+ + \hat{a}_-)$ and $\hat{p} = i\sqrt{m\omega\hbar/2}(\hat{a}_+ - \hat{a}_-)$ — no integrals needed. Result: $\sigma_x\sigma_p = (n+1/2)\hbar$, saturating Heisenberg only for $n=0$.

**Sources:** Griffiths §2.3.2; Liboff §7.3 (p. 198–211); Arfken & Weber, *Mathematical Methods*, Hermite polynomial chapter [verify section number].

### A.4 Coherent states — the bridge to classical behavior

Eigenstates of $\hat{H}$ have static probability densities. They do not slosh. So what *does* slosh? The answer: eigenstates of $\hat{a}_-$, not of $\hat{H}$.

A **coherent state** $|\alpha\rangle$ is defined by $\hat{a}_-|\alpha\rangle = \alpha|\alpha\rangle$ for any complex $\alpha$. Expanded in the energy basis:
$$|\alpha\rangle = e^{-|\alpha|^2/2}\sum_{n=0}^\infty \frac{\alpha^n}{\sqrt{n!}}|n\rangle$$
The probability of finding $n$ excitations is Poisson with mean $\langle n\rangle = |\alpha|^2$. The expectation value of position oscillates classically: $\langle\hat{x}(t)\rangle = \sqrt{2\hbar/m\omega}\,|\alpha|\cos(\omega t - \arg\alpha)$. The wave packet is Gaussian, has the *same width as the ground state for all time*, and saturates the uncertainty principle. It is the quantum state that most resembles a classical oscillating particle.

[Glauber's 1963 paper](https://journals.aps.org/pr/abstract/10.1103/PhysRev.131.2766) (*Physical Review* 131, 2766) introduced these in the context of the radiation field — coherent states describe the output of an ideal laser. Glauber shared the 2005 Nobel for this work. The pedagogical point: coherent states are not a curiosity. They are the *physical* states of the electromagnetic field that interact with classical detectors.

**Misconception:** *"Coherent states are classical states."* They are quantum states with classical-like *expectation values* and minimum uncertainty. They still have non-trivial quantum noise — the Poisson distribution of photon number is a quantum signature, distinguishable from thermal or squeezed light.

**Worked example:** Show that $|\alpha(t)\rangle = e^{-i\omega t/2}|\alpha e^{-i\omega t}\rangle$ — the coherent state evolves into another coherent state with a rotated $\alpha$. The Gaussian wave packet just orbits in phase space without distortion.

**Sources:** [Glauber 1963](https://journals.aps.org/pr/abstract/10.1103/PhysRev.131.2766); Griffiths §3.6 [verify in 3rd ed. — coherent states sometimes appear in problem sets only].

---

## B. Domain examples and cases

### B.1 Diatomic molecule vibrations
Carbon monoxide, hydrogen chloride, nitrogen — each diatomic gas absorbs infrared light at frequencies that match the harmonic-oscillator spectrum (with small anharmonic corrections). The bond is modeled as a spring with reduced mass $\mu = m_1m_2/(m_1+m_2)$ and effective spring constant from $V''$ at equilibrium. Infrared absorption spectroscopy is the experimental confirmation: $E_n - E_0 = n\hbar\omega$ means transitions $|0\rangle \to |1\rangle$ absorb a photon of energy exactly $\hbar\omega$. CO vibrates at about $2143\text{ cm}^{-1}$ — that is a directly measured value [verify NIST WebBook].

### B.2 Lattice phonons
A crystal of $N$ atoms in 3D has $3N$ vibrational modes. Each normal mode, at lowest order, is a harmonic oscillator. The collective excitations — **phonons** — have energy $\hbar\omega_k$ for wavevector $k$. Einstein's 1907 model of specific heat treated each atom as an independent oscillator; Debye refined to a spectrum of modes. The QHO ground-state energy summed over modes gives the zero-point lattice energy of a solid, measurable through neutron scattering.

### B.3 Photons in a cavity (preview of QFT)
The free electromagnetic field in a box decomposes into independent oscillator modes labeled by wavevector and polarization. Quantize each mode as a QHO and the excitations are photons. The vacuum has zero-point energy $\sum_k \hbar\omega_k/2$, formally infinite, regularized in calculations — the Casimir force between conducting plates is the *difference* between vacuum energies with and without plates and is finite and measurable.

### B.4 Failure mode: anharmonicity at large amplitude
The QHO is a leading-order approximation. Real molecules bonds break — the potential is not quadratic forever. The Morse potential $V(r) = D_e(1-e^{-a(r-r_0)})^2$ is bounded above and gives a spectrum that converges to a finite dissociation energy. Highly excited vibrational states deviate measurably from $E_n = (n+1/2)\hbar\omega$; the deviation is the **anharmonicity constant**, tabulated in spectroscopy handbooks. The textbook lesson: the harmonic oscillator is exact for *the harmonic potential*. Whether any physical system is *actually* harmonic is an experimental question, and the answer is "approximately, near the minimum."

---

## C. Connections and dependencies

**Backward:**
- Chapter 1 (wave function, probability density, expectation values) — the QHO eigenstates are a concrete arena to compute these.
- Chapter 2 (infinite square well, Schrödinger equation) — the QHO is the second exactly solvable system. Contrast: ISW has discontinuous walls and oscillating-only solutions; QHO has smooth walls and Gaussian-damped oscillations that penetrate the classically forbidden region.
- Heisenberg uncertainty (Ch 1 or 2 sidebar) — needed to motivate zero-point energy.

**Forward:**
- Chapter 4 (Dirac notation, operators) — the QHO is rewritten in $|n\rangle$ notation and becomes the canonical example. The chapter sets up the algebraic move that Chapter 4 generalizes.
- Chapter 6 (angular momentum) — ladder operators $\hat{J}_\pm$ are direct analogues of $\hat{a}_\pm$.
- Chapter 8 (time-dependent perturbation theory) — transitions between $|n\rangle$ states driven by an external field use the matrix elements $\langle n|\hat{x}|m\rangle$ that ladder operators compute trivially.
- A future QFT chapter (or capstone in Ch 13) — second quantization is the QHO algebra applied to every mode of a field.

---

## D. Current state of the field

The QHO is not a research frontier — it is one of the bedrock solved problems. But its *applications* are active research:

- **Trapped ions** (Wineland group at NIST, 2012 Nobel for Wineland and Haroche) — single ions in harmonic traps prepared in arbitrary $|n\rangle$ states, used as qubits and as oscillator-cavity hybrids.
- **Optomechanics** — micromechanical resonators cooled to their motional ground state (first achieved by O'Connell *et al.* 2010, *Nature* [verify]). The QHO ground state is now a routine experimental object, not a calculation.
- **Squeezed light** — non-coherent states of the EM field with reduced quantum noise in one quadrature at the cost of increased noise in the other. LIGO uses squeezed light to push below the standard quantum limit for gravitational-wave detection ([verify in 2019 *Physical Review Letters* upgrade paper]).
- **Casimir physics** — precision tests of zero-point energy continue; recent work on the dynamical Casimir effect (motion of mirrors creating photons from vacuum) has been observed in superconducting circuits.

The undergraduate point: every modern quantum technology that traps something — atoms, ions, photons, mechanical modes — uses the QHO as its model and the ladder operators as its language.

---

## E. Teaching considerations

**Hardest concepts to teach:**

1. **Eigenstates do not oscillate.** Students fresh from classical mechanics expect $|\psi_n(x,t)|^2$ to slosh. It does not — $|\psi_n(x,t)|^2 = |\psi_n(x)|^2$ for an energy eigenstate. The time-dependent phase $e^{-iE_n t/\hbar}$ cancels in $|\psi|^2$. Superpositions oscillate; eigenstates do not. This is the single biggest source of confusion and the simulation must make it visible immediately.

2. **Zero-point energy is forced, not chosen.** Students often think $E_0 = \hbar\omega/2$ is a convention. Show explicitly: a Gaussian with $\sigma_x \to 0$ has $\langle\hat{H}\rangle \to \infty$ from the kinetic term. There is a *minimum* of $\langle\hat{H}\rangle$ over Gaussian widths, and it is exactly $\hbar\omega/2$. This is a calculation, not a definition.

3. **Ladder operators feel like magic.** The remedy is to *do* the algebra. Have the student verify $[\hat{a}_-, \hat{a}_+] = 1$ from $[\hat{x}, \hat{p}] = i\hbar$ explicitly. Once the commutator is in hand, the rest follows mechanically. Mystery dissolves into bookkeeping.

4. **Coherent states are the bridge.** Without coherent states, students believe quantum eigenstates are "what really exists" and classical motion is "an emergent illusion." Coherent states show that classical-like motion is *also* a quantum state — just a particular superposition. The simulation must show a coherent state sloshing next to an eigenstate sitting still.

**Prerequisite calibration:** Students arriving from a first QM course typically have $E_n = (n+1/2)\hbar\omega$ memorized but cannot derive it. This chapter is where the derivation lives. Expect to spend more time than feels reasonable on the algebraic derivation — it pays off in Chapter 4 and Chapter 6.

**Singh and collaborators** ([arXiv 1510.01296](https://arxiv.org/abs/1510.01296), [Marshman & Singh 2017](https://iopscience.iop.org/article/10.1088/1361-6404/aa8e73)) document that even graduate students struggle to translate between Dirac notation and position-representation wave functions for the QHO. The chapter should write the *same* state both ways — as $|n\rangle$ *and* as $\psi_n(x)$ — and switch back and forth deliberately.

---

## F. Library files relevant to this chapter

- `pantry/436681929-Introductory-Quantum-Mechanics-by-Richard-L-Liboff-pdf.txt` — §7.2 (classical setup and QM Hamiltonian, p. 190+), §7.3 (eigenfunctions and Hermite polynomials, p. 198+), §7.4 (HO in momentum space, p. 211+). Direct text quotes available at lines 9992–10090 and 9807+.
- `pantry/993201189-Solution-Manual-Introduction-to-Quantum-Mechanics-3e-Griffiths.txt` — solutions to Griffiths Ch. 2 problems, useful for worked-example calibration.
- `pantry/290663862-A-First-Book-of-Quantum-Field-Theory-Lahiri-Pal.txt` — uses the QHO ladder algebra to construct second quantization; pull the "harmonic oscillator as building block of QFT" framing for the §A.2 misconception sidebar.
- Pantry files labeled "Quantum Physics for Beginners" (multiple): conceptual prose only — useful for analogies and student-facing language, not as primary sources.
- `pantry/_lib_QM-Into-the-Light-Beginners.md` — likely contains pedagogical framing for zero-point energy [verify by reading].
- **External:** Griffiths, *Introduction to Quantum Mechanics*, 3rd ed., §2.3 (the primary reference — the pantry .txt labeled as Griffiths is mislabeled and contains a nanotech book, so Griffiths must be cited from the print edition or library access).

---

## F.5 Simulation pedagogy and D3 specifics

**Target deliverable:** `03-harmonic-oscillator.html` — a single-page D3 v7 SVG simulation. Following Bear's Brutalist system: governed by `CLAUDE.md` (coding constitution), `DESIGN.md` (visual), `PROJECT.md` (state).

**Visual layout (single SVG canvas, ~900×600):**

1. **Background:** parabolic potential $V(x) = (1/2)m\omega^2 x^2$ drawn as a smooth curve (path with `d3.curveBasis` or `curveMonotoneX`).
2. **Energy levels:** horizontal lines at $E_n = (n+1/2)\hbar\omega$ for $n = 0, \ldots, 6$, with the line *shifted* vertically to its energy. Each line is also the $\psi = 0$ axis for the wave function plotted at that level — a Griffiths-style display where the wave functions stack inside the potential well.
3. **Classical turning points:** small vertical tick marks at $\pm\sqrt{(2n+1)\hbar/m\omega}$ for the active state, dashed.
4. **Wave function plot:** $\psi_n(x)$ for the active $n$, or the real part of the time-evolving $\psi(x,t)$ for a coherent state or superposition. Plotted as a continuous line.
5. **Probability density plot:** $|\psi(x,t)|^2$ as a filled area underneath the wave function, animated in real time for superpositions.
6. **Phase-space inset (optional, top-right):** Wigner-function or simple $\langle x\rangle$-vs-$\langle p\rangle$ trajectory showing the coherent state orbiting in phase space.

**Controls (sliders and buttons):**

- $\omega$ slider (frequency) — from $0.5$ to $5.0$ in natural units.
- Mode selector: "Eigenstate $n$" (integer slider $0$–$8$), "Coherent state $\alpha$" (complex magnitude and phase sliders), "Two-state superposition" ($n_1, n_2$ and coefficients $c_1, c_2$).
- Time animation: play/pause/reset. Default frame rate 60 fps via `requestAnimationFrame`.
- Toggle: show/hide classical turning points; show/hide energy levels.

**Physics computation (in JavaScript):**

- **Hermite polynomials:** compute via recursion $H_{n+1}(\xi) = 2\xi H_n - 2nH_{n-1}$ with $H_0 = 1$, $H_1 = 2\xi$. Cache values across the spatial grid for each chosen $n$.
- **Normalization:** $N_n = (m\omega/\pi\hbar)^{1/4}/\sqrt{2^n n!}$ — precompute $n!$ via lookup for $n \leq 20$ (above that, switch to log-gamma or numerical normalization).
- **Time evolution:** $\psi(x,t) = \sum_n c_n \psi_n(x) e^{-iE_n t/\hbar}$ — store complex coefficients, multiply by phase, sum. For coherent states use $c_n = e^{-|\alpha|^2/2}\alpha^n/\sqrt{n!}$ — but **truncate** at $n_{\max} \approx |\alpha|^2 + 5\sqrt{|\alpha|^2}$ for accuracy.
- **Natural units:** set $\hbar = m = 1$, $\omega$ in user units. Energies in units of $\hbar\omega$. Lengths in units of $\sqrt{\hbar/m\omega}$.

**D3 v7 patterns to use:**

- `d3.scaleLinear()` for x-axis (position) and y-axis (energy/amplitude).
- `d3.line()` with `.x(d => xScale(d.x))` and `.y(d => yScale(d.y))` and `.curve(d3.curveMonotoneX)` for smooth plots ([D3 line generator docs](https://d3js.org/d3-shape/line)).
- `d3.area()` for the filled probability-density region.
- Update pattern: bind data to a single path element per layer, use `.transition().duration(0)` (or no transition) in the animation loop for direct re-rendering.
- Sliders: HTML `<input type="range">` outside the SVG, with `input` event listeners that call a `redraw(state)` function.

**Animation loop sketch:**
```javascript
let t = 0;
function tick() {
  t += dt;
  const psi = computeWavefunction(state, t); // returns array of {x, re, im, prob}
  wavePath.attr('d', lineGen(psi.map(d => ({x: d.x, y: d.re}))));
  probArea.attr('d', areaGen(psi.map(d => ({x: d.x, y: d.prob}))));
  if (state.playing) requestAnimationFrame(tick);
}
```

**Known LLM-generated physics-code failure modes to anticipate (and warn the student about in the prompt):**

1. **Hermite polynomial overflow at large $n$.** Naively computing $H_n(\xi)$ for $n > 30$ with the standard recursion overflows double precision near the turning points. Mitigation: use scaled Hermite functions (multiply by $e^{-\xi^2/2}$ as you go) or cap $n$ at 15.
2. **Forgetting to renormalize after parameter changes.** When $\omega$ changes, the natural length unit changes. Without renormalizing the wave function on the *new* spatial grid, the plot will look wrong.
3. **Phase convention errors.** $\psi_n(x)$ has a real overall phase by convention. LLMs sometimes generate a Hermite that is off by a sign for odd $n$. Verify against the known forms $H_1 = 2\xi$, $H_3 = 8\xi^3 - 12\xi$.
4. **Coherent state truncation.** Summing the series to $n = 50$ for $|\alpha| = 0.5$ wastes cycles; summing only to $n = 5$ for $|\alpha| = 4$ misses the peak. The truncation rule must scale with $|\alpha|^2$.
5. **Time step too large.** $\hbar\omega \cdot dt / \hbar = \omega\,dt$ should be $\ll 1$ per frame for smooth animation. If $\omega$ slides to 5 and $dt = 0.1$, the phases jump by 0.5 radians per frame and the wave packet looks like it teleports.
6. **Animating $\psi$ instead of $|\psi|^2$ and confusing students.** Both should be shown — animate the real part *or* probability density, but label which is which. PhET's bound-states sim ([JILA tutorial](https://jila.colorado.edu/sites/default/files/uploads/Tutorial%20for%20Quantum%20Bound%20States.pdf)) does this well.

**What the simulation must show that no textbook figure can:** the *contrast* between a static eigenstate probability density (boring, fixed pattern) and a sloshing coherent state (Gaussian bouncing back and forth without spreading), side-by-side, with the same $\omega$. This is the visual that closes the "but doesn't the quantum particle oscillate?" gap.

**Comparison anchor:** PhET's "Quantum Bound States" simulation ([phet.colorado.edu/en/simulations/bound-states](https://phet.colorado.edu/en/simulations/bound-states)) does the eigenstate visualization well but does not foreground coherent states. The +1 simulation's distinctive contribution is the coherent-state mode.

---

## G. Gaps and flags

- **[verify]** Exact fraction of probability outside classical turning points for the ground state (cited as ~16% — should pull from Griffiths Problem 2.15 or compute directly).
- **[verify]** Carbon monoxide vibrational frequency $\omega \approx 2143\text{ cm}^{-1}$ — NIST WebBook citation needed.
- **[verify]** Section number for Hermite polynomials in Arfken & Weber (cited generically; should be specific).
- **[verify]** Whether Griffiths 3rd ed. covers coherent states in main text or only in problems (different editions place it differently).
- **[verify]** O'Connell *et al.* 2010 *Nature* paper on the mechanical-resonator ground state — need the exact DOI before claim of "first achieved."
- **[verify]** LIGO squeezed-light upgrade reference — date and journal.
- **Pantry gap:** The pantry file labeled "Griffiths" (`822531304-...`) is in fact a nanotech book. The actual Griffiths text is not in the pantry. The chapter author needs library or print access to Griffiths §2.3 and Problems 2.10–2.20. Flag for Nik.
- **Voice anchor:** Both `style/` and `books/quantum-mechanics-with-llms/style/` need to be checked. If empty, flag draft as `voice-unanchored`.
- **Pedagogy gap:** No physics-education-research citation has been confirmed *specifically* for the QHO (Singh's work is on Dirac notation and probability distributions, not the QHO eigenstates). The hardest-concepts-to-teach section is currently based on instructor experience, not PER literature. Worth a focused search before chapter draft.
- **Math density:** The chapter as outlined makes the algebraic method the *primary* derivation. Some second-QM textbooks (e.g., Townsend) introduce it more gently after the Hermite method. Decision: stay with TIKTOC's preference (algebra first) — it sets up Chapter 4 cleanly. But be ready for student pushback that the algebra looks like a black box on first encounter.

**Word count target:** ~2,800 words for this notes file. Reached.
