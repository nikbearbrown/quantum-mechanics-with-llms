# Research Notes: Chapter 09 — Time-Independent Perturbation Theory
**Source:** TIKTOC.md chapter entry (lines 497–542)
**Notes file:** 09-time-independent-perturbation-theory_notes.md
**Corresponding chapter:** chapters/09-perturbation-theory.md (not yet written)
**Generated:** 2026-05-13

---

## Chapter summary (from TIKTOC.md) [verbatim paste]

**Filename:** `09-perturbation-theory.md`
**Arc position:** Act Two → Act Three transition, Chapter 9

**One-line:** Students learn to compute energy corrections and state corrections for systems close to an exactly solvable model, building a visualizer that shows how energy levels split and shift under a perturbation.

**Chapter description:**
Almost no realistic quantum system is exactly solvable. Perturbation theory is the workhorse approximation method: start with a solvable Hamiltonian H₀, add a small perturbation H', and compute corrections to the energies and states order by order. This chapter covers non-degenerate perturbation theory (first and second order) and degenerate perturbation theory (essential when unperturbed states share an energy). Applications include the fine structure of hydrogen (spin-orbit coupling, relativistic correction), the Stark effect (hydrogen in an electric field), and the Zeeman effect (hydrogen in a magnetic field). The simulation shows energy levels splitting and shifting in real time as a perturbation strength slider is moved.

**Core concepts:**
- The perturbation expansion: H = H₀ + λH'; expand Eₙ and |ψₙ⟩ in powers of λ
- First-order energy correction: Eₙ⁽¹⁾ = ⟨ψₙ⁰|H'|ψₙ⁰⟩ — the expectation value of the perturbation
- First-order state correction: |ψₙ⁽¹⁾⟩ = Σₘ≠ₙ [⟨ψₘ⁰|H'|ψₙ⁰⟩/(Eₙ⁰ - Eₘ⁰)] |ψₘ⁰⟩
- Second-order energy correction: Eₙ⁽²⁾ = Σₘ≠ₙ |⟨ψₘ⁰|H'|ψₙ⁰⟩|²/(Eₙ⁰ - Eₘ⁰)
- Degenerate perturbation theory: diagonalize H' in the degenerate subspace
- Applications:
  - Fine structure of hydrogen: relativistic correction + spin-orbit coupling → good quantum numbers (n,l,j,mⱼ)
  - Stark effect: hydrogen in an electric field; quadratic Stark effect for ground state
  - Zeeman effect: hydrogen in a magnetic field; normal and anomalous Zeeman

**Key vocabulary:** perturbation theory, non-degenerate, degenerate, secular equation, fine structure, spin-orbit coupling, Stark effect, Zeeman effect, good quantum numbers

**Common misconceptions:**
- "Perturbation theory always converges" — it is an asymptotic expansion; the series may diverge even when individual terms are small
- "First-order is always sufficient" — near-degenerate states require degenerate perturbation theory even at first order

---

## A. Conceptual foundations

The chapter rests on five conceptual moves. Each must be specified before it can be used.

**1. The perturbation expansion is a formal device, not a guaranteed truth.** Write the full Hamiltonian as $\hat{H} = \hat{H}_0 + \lambda \hat{H}'$ where $\lambda$ is a bookkeeping parameter (small and dimensionless in practice). Then expand both energy and state as power series in $\lambda$:

$$E_n = E_n^{(0)} + \lambda E_n^{(1)} + \lambda^2 E_n^{(2)} + \cdots$$
$$|n\rangle = |n^{(0)}\rangle + \lambda |n^{(1)}\rangle + \lambda^2 |n^{(2)}\rangle + \cdots$$

Substitute into $\hat{H}|n\rangle = E_n |n\rangle$ and demand equality at each order of $\lambda$. The whole machine drops out of that one move. The key catch: convergence is not automatic, and most physically interesting perturbation series in QED and QM are *asymptotic*, not convergent. Dyson 1952 made this explicit for QED; the same logic — analytic continuation breaks at $\lambda < 0$ — bites textbook problems too.

**2. First-order energy correction is the expectation value of $\hat{H}'$ in the unperturbed state.** Collecting first-order terms in $\lambda$ from the substitution and using $\hat{H}_0 |n^{(0)}\rangle = E_n^{(0)} |n^{(0)}\rangle$:

$$E_n^{(1)} = \langle n^{(0)} | \hat{H}' | n^{(0)} \rangle$$

This is the single most useful result in the entire chapter. It says: if you have an exact solution to a nearby problem, the first correction to the energy is just the average of the perturbation in the unperturbed state. No new diagonalization required.

**3. First-order state correction is a sum over all other unperturbed states weighted by matrix elements and energy denominators.**

$$|n^{(1)}\rangle = \sum_{m \neq n} \frac{\langle m^{(0)} | \hat{H}' | n^{(0)} \rangle}{E_n^{(0)} - E_m^{(0)}} |m^{(0)}\rangle$$

The energy denominator carries the bad news: when $E_n^{(0)} \to E_m^{(0)}$ (degeneracy or near-degeneracy), the formula explodes. This is the signal that the chosen basis is wrong for the problem and you must move to degenerate perturbation theory.

**4. Second-order energy correction is always negative for the ground state.** From the same expansion:

$$E_n^{(2)} = \sum_{m \neq n} \frac{|\langle m^{(0)} | \hat{H}' | n^{(0)} \rangle|^2}{E_n^{(0)} - E_m^{(0)}}$$

For $n$ = ground state, every $E_m^{(0)} > E_n^{(0)}$, so every term is negative. The ground state is always pushed *down* by perturbation. This is a small theorem worth showing.

**5. When the unperturbed Hamiltonian has degeneracies, the basis is not unique and the naive formulas fail.** The fix: within each degenerate subspace, diagonalize $\hat{H}'$ first. The eigenvalues of $\hat{H}'$ restricted to that subspace are the first-order energy corrections. The eigenvectors are the "good" zeroth-order states — the ones that smoothly connect to the perturbed eigenstates as $\lambda \to 0$. This is not a "special case" — it is the general case; non-degenerate perturbation theory is what you get when the degenerate subspace is one-dimensional.

## B. Domain examples and cases

**Case 1: Anharmonic oscillator with $\hat{H}' = \lambda \hat{x}^4$.** Start with the 1D harmonic oscillator (Griffiths Ch. 2, well-known eigenstates). The perturbation $\hat{x}^4$ is what makes the Morse potential and most realistic potential wells deviate from quadratic. Using ladder operators $\hat{x} = \sqrt{\hbar/(2m\omega)}(\hat{a} + \hat{a}^\dagger)$, expand $\hat{x}^4$ and pick out the diagonal contributions to get $E_n^{(1)} = \lambda (3\hbar^2 / 4 m^2 \omega^2)(2n^2 + 2n + 1)$ [verify exact prefactor against Griffiths Problem 6.2 / Liboff §13.1]. This worked example shows the machinery transparently — no degeneracy, clean ladder algebra, a result that grows with $n$ (so perturbation theory works worst for highly excited states). The simulation will let students dial $\lambda$ and watch this growth, then compare to exact numerical diagonalization to see where it breaks down.

**Case 2: Hydrogen fine structure (relativistic kinetic + spin-orbit + Darwin).** Three perturbations enter at order $(v/c)^2 \sim \alpha^2 \sim 5 \times 10^{-5}$, where $\alpha \approx 1/137$ is the fine-structure constant.
- Relativistic kinetic correction: $\hat{H}'_{rel} = -\hat{p}^4/(8m^3 c^2)$, from expanding $\sqrt{p^2 c^2 + m^2 c^4} - mc^2$ to next order beyond $p^2/2m$.
- Spin-orbit coupling: $\hat{H}'_{SO} = \frac{1}{2m^2 c^2} \frac{1}{r} \frac{dV}{dr} \vec{L} \cdot \vec{S}$, from the electron seeing a magnetic field in its rest frame as it orbits the proton; includes the Thomas-precession factor of 1/2.
- Darwin term: $\hat{H}'_{Darwin} = \frac{\pi \hbar^2}{2 m^2 c^2} (Ze^2/4\pi\epsilon_0) \delta^3(\vec{r})$, affects only $s$-states.

Net result: degeneracy in $\ell$ at fixed $n$ is lifted; "good quantum numbers" become $(n, \ell, j, m_j)$ instead of $(n, \ell, m_\ell, m_s)$. The 2p level splits into $2p_{1/2}$ and $2p_{3/2}$ with a gap of order $\alpha^2 \cdot$ Rydberg $\sim 10^{-4}$ eV — measurable in 1947 by Lamb (the Lamb shift itself is a QED correction beyond fine structure). Cite Griffiths §6.3 (3e: §7.3; 2e: §6.3) — [verify edition mapping].

**Case 3: Stark effect (hydrogen in uniform E-field).** Discovered simultaneously by Stark (Aachen, fall 1913, modified canal-ray discharge tube) and Lo Surdo (Italy, accidentally, on classical theory). $\hat{H}' = e E z$ (electron charge $-e$, field along $+z$).
- Ground state ($n=1$): non-degenerate; $\langle 1s | z | 1s \rangle = 0$ by parity, so $E_1^{(1)} = 0$. The leading correction is *second-order quadratic* in $E$: $E_1^{(2)} = -\frac{1}{2} \alpha_{pol} E^2$ where $\alpha_{pol}$ is the polarizability.
- First excited state ($n=2$): fourfold degenerate (ignoring spin) — $2s$, $2p_0$, $2p_{\pm 1}$. Apply degenerate perturbation theory: diagonalize $eEz$ in the four-dimensional subspace. Only $\langle 2s | z | 2p_0 \rangle$ is nonzero (by parity and $m$-selection); the matrix has two zero eigenvalues and two of magnitude $3 e a_0 E$ [verify prefactor]. The $n=2$ level splits into three: one shifted up by $3 e a_0 E$, one shifted down by the same amount, and one (degenerate pair) unshifted. **This is the perfect simulation centerpiece.**

**Case 4: Zeeman effect.** Hydrogen in a uniform B-field, $\hat{H}' = -\vec{\mu} \cdot \vec{B} = \mu_B B (L_z + 2 S_z)/\hbar$. Two regimes set by relative strength of Zeeman to fine-structure perturbations:
- Weak field (anomalous Zeeman): fine structure dominates; $(n, \ell, j, m_j)$ are good; $E^{(1)} = g_J \mu_B B m_j$ with Landé $g$-factor $g_J = 1 + [j(j+1) + s(s+1) - \ell(\ell+1)]/[2 j(j+1)]$.
- Strong field (Paschen-Back): Zeeman dominates; $(n, \ell, m_\ell, m_s)$ are good; $E^{(1)} = \mu_B B (m_\ell + 2 m_s)$.
- Intermediate field: must diagonalize the full $\hat{H}'_{SO} + \hat{H}'_{Zeeman}$ in the degenerate subspace.

**Failure case: the anharmonic oscillator $\hat{H}' = \lambda \hat{x}^4$ at large $\lambda$.** Bender & Wu 1969 showed that the perturbation series for the quartic oscillator has zero radius of convergence — every term grows like $n!$ and the series is asymptotic, not convergent [verify Bender-Wu citation]. Yet the series is *useful*: truncating at the optimal order gives an exponentially good approximation. This is the canonical example to break the "perturbation theory always converges" misconception in the simulation: the student watches the truncated series diverge from the exact diagonalization at finite $\lambda$, and sees that adding more terms actually makes the approximation worse past a critical order.

## C. Connections and dependencies

**Backward (Acts One and Two):**
- Chapter 2 (Schrödinger equation): the eigenvalue problem $\hat{H}|n\rangle = E_n|n\rangle$ is the structure the entire chapter perturbs.
- Chapter 4 (Dirac notation): bras, kets, matrix elements $\langle m | \hat{H}' | n \rangle$ — perturbation theory is unreadable without this.
- Chapter 5 (operators, expectation values): $E_n^{(1)} = \langle n | \hat{H}' | n \rangle$ is literally an expectation value.
- Chapter 6 (harmonic oscillator): the anharmonic example uses ladder operators directly.
- Chapter 8 (hydrogen atom): every application in this chapter perturbs hydrogen.

**Forward:**
- Chapter 10 (time-dependent perturbation theory): same expansion strategy applied to time-dependent $\hat{H}'(t)$; transition amplitudes replace energy corrections.
- Chapter 12 (entanglement): degenerate perturbation theory's diagonalization is structurally identical to choosing the right basis for entangled states.
- Chapter 13 (modern applications): variational method as the complement to perturbation theory; quantum chemistry uses both throughout.

**Cross-discipline:**
- Quantum chemistry: Møller-Plesset perturbation theory (MP2, MP4) is non-degenerate perturbation theory applied to the Hartree-Fock reference. Pillar method in computational chemistry.
- Solid state: $\vec{k} \cdot \vec{p}$ perturbation theory near band extrema is the textbook way to compute effective masses.
- Atomic physics: precision spectroscopy (Rydberg states, optical clocks) lives or dies by fourth-order perturbation theory and QED corrections.

## D. Current state of the field

Time-independent perturbation theory is over a century old and structurally settled. What is alive now is the *failure modes* and the *extensions*.

- **Resurgence and resummation.** Perturbation series in QM and QFT are typically asymptotic with $n!$-growing coefficients. Borel summation, transseries, and resurgent analysis (Écalle, Costin, Mariño) recover information from the divergent tail. Active area in mathematical physics; relevant when the student asks "what do we *do* with an asymptotic series?"
- **Strong-coupling and non-perturbative methods.** When $\lambda$ is not small, perturbation theory fails entirely. Variational methods (Ritz), tensor networks (DMRG, MPS), quantum Monte Carlo, and exact diagonalization fill the gap. The chapter should mention these by name as where the student will go next.
- **Open-system perturbation theory.** Lindblad master equations, Bloch-Redfield equations — perturbative treatments of system-environment coupling. Backbone of decoherence and noise modeling in qubits.
- **Effective field theory.** A unification of perturbative reasoning: separate scales, expand in a small ratio, throw away terms with the right Wilsonian justification. Connects this chapter to particle physics and condensed-matter low-energy descriptions.

## E. Teaching considerations

**Why students fail at this chapter:**
1. **Index gymnastics.** The sums over $m \neq n$, the matrix elements with two state labels and one operator label, the energy denominators — they hide the simple machinery. Spend explicit time on the bookkeeping. Show one example, all the way through, with every index expanded.
2. **Asymmetry of treatment.** Most textbooks present the non-degenerate case as primary and the degenerate case as an exception. This is pedagogically wrong: real systems are riddled with degeneracies (hydrogen, harmonic oscillator in 2D and 3D, spin systems). Teach the degenerate case as the general one and present non-degenerate as the limit.
3. **The convergence question.** Students assume perturbation series converge because Taylor series converge. They don't. The simulation must let students *see* the divergence — push $\lambda$ until the perturbation-theory curve and the exact-diagonalization curve separate, then keep pushing.
4. **"Why is the formula symmetric in $m$ and $n$ but the denominator isn't?"** Because we're computing the correction to state $n$, not to state $m$. Make this explicit; it confuses everyone the first time.

**Pedagogical sequencing:**
1. Hook with the anharmonic oscillator: a problem that looks innocent and isn't exactly solvable.
2. Derive first-order energy correction explicitly from the expansion — show the algebra, do not assert.
3. Apply to hydrogen Stark effect on $n=2$ as the worked example. The degeneracy *forces* the move to degenerate PT, which makes the lesson stick.
4. Show the fine structure as the application that explains the spectroscopy the student already knows.
5. Close with the simulation: dial $\lambda$, watch levels move, see the approximation break.

## F. Library files relevant to this chapter

- `pantry/436681929-Introductory-Quantum-Mechanics-by-Richard-L-Liboff-pdf.txt` — Liboff Chapter 13 covers time-independent perturbation theory (§13.1 non-degenerate; §13.2 degenerate; §§13.3–13.4 fine structure / Zeeman). Lines 34956–37000+ in the pantry file. Good companion to Griffiths.
- `pantry/993201189-Solution-Manual-Introduction-to-Quantum-Mechanics-3e-Griffiths.txt` — preview only; flagged not actually a usable solution manual in the pantry. [verify availability of full solutions elsewhere]
- Griffiths' *Introduction to Quantum Mechanics* (3rd ed., 2018, Cambridge University Press) — Chapter 7 in 3e is time-independent perturbation theory; in 2e it was Chapter 6. The brief cites Ch. 6, consistent with 2e. [verify which edition the course uses; flag both.]
- `pantry/01-what-is-anthropology.md` — unrelated; ignore.

**Notably missing from the pantry:** Cohen-Tannoudji *Quantum Mechanics* Vol. II Chapter XI (the most thorough textbook treatment of degenerate PT and Stark effect for the n=2 hydrogen level); Sakurai *Modern Quantum Mechanics* Chapter 5 (cleaner notation for the formal expansion). Both should be cited in the chapter; neither needs to be in the pantry to write the chapter.

## F.5 Simulation pedagogy and D3 specifics

**What the student should *see*, not just compute.** The anharmonic-oscillator and Stark-effect simulations are pedagogical sweet spots for one reason: both make a hidden mathematical structure (the perturbation series, the matrix diagonalization) immediately visible as motion on the screen. A static plot in Griffiths labels the $n=2$ Stark splitting "$3 e a_0 \mathcal{E}$." A simulation with a slider lets the student see that splitting come into existence from zero, watch the three-fold structure emerge, observe that two of the four states do not shift, and ask "why?" — at which point the parity argument lands instead of glancing off.

**Two simulations, two pedagogical purposes:**

*Simulation A: Anharmonic oscillator energy levels vs. perturbation strength.* Controls: $\lambda$ slider for the strength of the $\hat{x}^4$ term, integer selector for which level $n$ to plot, toggle between first-order PT / second-order PT / exact diagonalization. Display: energy-level diagram on the left (horizontal lines for the first 5–8 levels at the current $\lambda$); plot on the right of $E_n(\lambda)$ vs. $\lambda$ with three curves overlaid (first-order, second-order, exact). Pedagogical move: dial $\lambda$ from 0 to large values. The student watches first-order PT diverge from exact, second-order improve, and *both* eventually fail. This is the moment "asymptotic" becomes physical, not jargon.

*Simulation B: Hydrogen Stark effect on $n=2$ manifold.* Controls: electric field strength $\mathcal{E}$ slider (in units of $E_0 = e/(4\pi\epsilon_0 a_0^2)$ — atomic units, so values from 0 to ~0.01 are pre-ionization). Display: four horizontal lines starting at the unperturbed $n=2$ energy on the left; as $\mathcal{E}$ increases, two split symmetrically with slope $\pm 3 e a_0$, two stay flat. Annotate the eigenstates: the shifting ones are $|2s\rangle \pm |2p_0\rangle / \sqrt{2}$, the flat ones are $|2p_{\pm 1}\rangle$. Show wave function plots (radial, schematic) for each as the field turns on — the shifting states are *polarized* (electron cloud asymmetric along $\hat{z}$); the flat states have $m \neq 0$ and cannot polarize along $\hat{z}$.

**D3 v7 specifics:**
- Use `d3.scaleLinear` for both the slider value and the y-axis (energy). Pin the y-axis so levels stay in view as they move; do not auto-rescale (defeats the pedagogy of "watch this line move").
- Animate level positions with `transition().duration(150)` — fast enough to feel responsive when dragging the slider, slow enough that the eye can track each level.
- Use `d3-simple-slider` (`johnwalley/d3-simple-slider` library, MIT) for the $\lambda$ slider; it integrates cleanly with D3 v7.
- Color: distinguish PT (first-order) from PT (second-order) from exact via a consistent palette declared in `DESIGN.md`. Suggested: first-order = teal dashed, second-order = orange dashed, exact = black solid. (PhET's quantum simulations use a similar convention.)
- Computation: do the diagonalization in-browser. For the anharmonic oscillator, build the matrix of $\hat{x}^4$ in the first 30 harmonic-oscillator eigenstates, then diagonalize using `numeric.js` or a small custom Jacobi rotation routine. For Stark $n=2$, the 4×4 matrix is hand-codable.

**Failure mode to anticipate:** students will increase $\lambda$ very large and the PT curve will go to infinity, possibly off-screen. Build in a y-axis auto-clip or a graceful "PT no longer reliable" warning when $|E_n^{(2)}| > |E_n^{(0)} - E_{n\pm 1}^{(0)}|/4$ — the regime where second-order corrections exceed the level spacing of the unperturbed problem. This warning is pedagogy; it tells the student what convergence failure *looks like*.

**Extension prompts:**
1. Add the $\hat{x}^3$ cubic perturbation; show that $E_n^{(1)} = 0$ by parity but $E_n^{(2)} \neq 0$ — second-order matters even at first nonzero order.
2. Add the Zeeman effect to the $n=2$ Stark simulation: add a magnetic field slider; watch the $m_\ell = \pm 1$ degeneracy lift as well.
3. Switch the base system from harmonic oscillator to infinite square well; show that the $\hat{x}^4$ matrix elements are entirely different and the corrections behave differently.

## G. Gaps and flags

- [verify] Griffiths edition numbering — chapter is "Ch. 6" in 2e, "Ch. 7" in 3e. Brief says Ch. 6. Confirm which edition the course uses before final write.
- [verify] Exact prefactor on $E_n^{(1)}$ for the $\lambda x^4$ perturbation — Griffiths Problem 6.2 (2e) / 7.2 (3e) works it out. Compute, do not assert.
- [verify] Bender & Wu 1969 reference for divergence of the quartic-oscillator perturbation series — *Phys. Rev.* 184, 1231 (1969); subsequent paper *Phys. Rev. D* 7, 1620 (1973). Confirm exact citations.
- [verify] Spin-orbit prefactor and Thomas factor 1/2 derivation — standard but easy to flub. Cross-check Griffiths §6.3 and Cohen-Tannoudji Complement A_XII.
- [verify] Dyson 1952 reference — *Phys. Rev.* 85, 631 (1952), "Divergence of perturbation theory in quantum electrodynamics." Used as the canonical citation for the "asymptotic, not convergent" point.
- [flag] The chapter is dense; word count budget should plan for the derivation of $E_n^{(1)}$ in full, one worked example of degenerate PT, and the simulation block — likely pushing toward the 7,500–8,000 word upper limit.
- [flag] Stark vs. Lo Surdo attribution — most physics textbooks cite only Stark. The 2004 paper by Leone, Paoletti, and Robotti (*Physics in Perspective* 6, 271) documents the simultaneous independent discovery. Mention; do not litigate.
- [flag] "Fine structure" without QED feels incomplete; the Lamb shift requires field quantization which the book has not introduced. Acknowledge the limit ("classical field, no Lamb shift, no anomalous magnetic moment") and point forward.
- [open question] Should the chapter include the variational method as a one-page side-by-side comparison? Griffiths puts it in the same chapter (3e Ch. 8); pedagogically it's the natural complement. Brief doesn't say. Default: brief mention, defer full treatment.
