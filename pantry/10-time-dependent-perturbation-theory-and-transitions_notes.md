# Research Notes: Chapter 10 — Time-Dependent Perturbation Theory and Transitions
**Source:** TIKTOC.md chapter entry (lines 544–589)
**Notes file:** 10-time-dependent-perturbation-theory-and-transitions_notes.md
**Corresponding chapter:** chapters/10-time-dependent-perturbation.md (not yet written)
**Generated:** 2026-05-13

---

## Chapter summary (from TIKTOC.md) [verbatim paste]

**Filename:** `10-time-dependent-perturbation.md`
**Arc position:** Act Three, Chapter 10

**One-line:** Students learn how time-varying perturbations drive transitions between quantum states, derive Fermi's Golden Rule, and build a simulation showing transition probabilities as a function of driving frequency.

**Chapter description:**
Time-dependent perturbation theory answers the question: if a system is in state |i⟩ and a time-varying perturbation is applied, what is the probability of finding it in state |f⟩ at a later time? This is the theory behind spectroscopy, laser-atom interactions, nuclear decay, and semiconductor physics. Fermi's Golden Rule gives the transition rate for a monochromatic perturbation near resonance. Selection rules emerge naturally as conditions under which the transition matrix element ⟨f|H'|i⟩ vanishes by symmetry. The simulation shows resonance: as the driving frequency sweeps through the transition frequency, the transition probability peaks sharply.

**Core concepts:**
- The interaction picture: time evolution separated into free and perturbative parts
- First-order transition probability: P(i→f,t) = |⟨f|H'|i⟩|² × |1-e^(i(ωfi-ω)t)/(ωfi-ω)|²
- Resonance: transition probability maximized when driving frequency ω = ωfi = (Ef-Ei)/ℏ
- Fermi's Golden Rule: Γi→f = (2π/ℏ)|⟨f|H'|i⟩|² ρ(Ef)
- Selection rules: H' matrix element vanishes by symmetry → forbidden transition
- Spontaneous emission: Einstein A coefficient; lifetime of excited states
- Absorption and stimulated emission: Einstein B coefficients; the laser

**Key vocabulary:** interaction picture, transition probability, resonance, Fermi's Golden Rule, density of states, selection rules, electric dipole approximation, spontaneous emission, stimulated emission, Einstein coefficients

**Common misconceptions:**
- "Fermi's Golden Rule gives an exact transition probability" — it is a rate valid for continuous spectra and long times; discrete spectra require the full first-order formula
- "Selection rules are absolute" — they apply in the electric dipole approximation; magnetic dipole and quadrupole transitions are allowed but weaker

---

## A. Conceptual foundations

The chapter has five conceptual pillars. The first three are mechanical; the last two are interpretive.

**1. The interaction picture separates trivial evolution from interesting evolution.** Start with $\hat{H} = \hat{H}_0 + \hat{H}'(t)$. In the Schrödinger picture, both parts evolve the state vector. Trade out the "trivial" $\hat{H}_0$ evolution by defining $|\tilde\psi(t)\rangle = e^{i\hat{H}_0 t/\hbar} |\psi(t)\rangle$. Then $i\hbar \partial_t |\tilde\psi\rangle = \tilde{H}'(t) |\tilde\psi\rangle$ where $\tilde{H}'(t) = e^{i\hat{H}_0 t/\hbar} \hat{H}'(t) e^{-i\hat{H}_0 t/\hbar}$. The state stops evolving when $\hat{H}'$ is off; all the dynamics is in the perturbation. This is the cleanest setting in which to do perturbation theory in time.

**2. First-order transition amplitude is a Fourier integral.** Expand the interaction-picture state in the unperturbed eigenbasis: $|\tilde\psi(t)\rangle = \sum_n c_n(t) |n\rangle$, with $c_n(0) = \delta_{ni}$ (system starts in state $|i\rangle$). To first order in $\hat{H}'$:

$$c_f(t) = \frac{1}{i\hbar} \int_0^t \langle f | \hat{H}'(t') | i \rangle \, e^{i\omega_{fi} t'} \, dt'$$

where $\omega_{fi} = (E_f - E_i)/\hbar$. **Read this carefully:** the transition amplitude is the Fourier component of the matrix element $\langle f | \hat{H}'(t) | i \rangle$ at frequency $\omega_{fi}$. Resonance is Fourier resonance.

**3. For a monochromatic perturbation $\hat{H}'(t) = \hat{V} \cos(\omega t)$, the transition probability has the canonical $\sin^2$/Δω² form.** Carrying out the integral (rotating-wave approximation: keep the resonant term, drop the rapidly oscillating counter-rotating one):

$$P_{i \to f}(t) = \frac{|\langle f | \hat{V} | i \rangle|^2}{4\hbar^2} \cdot \frac{\sin^2[(\omega_{fi} - \omega) t / 2]}{[(\omega_{fi} - \omega)/2]^2}$$

The right-hand factor is the diffraction-pattern-in-time profile. Its peak height grows as $t^2$, its width narrows as $1/t$, and the area under it grows as $t$ — the signature of a delta function emerging at long times.

**4. Fermi's Golden Rule emerges in the long-time + continuum limit.** When final states form a continuum with density $\rho(E_f)$, integrate $P_{i\to f}(t)$ over final states near $E_i + \hbar\omega$. The sinc² becomes a delta function $2\pi t \, \delta(\omega_{fi} - \omega)$, and the *rate* (probability per unit time) is:

$$W_{i \to f} = \frac{2\pi}{\hbar} |\langle f | \hat{H}' | i \rangle|^2 \rho(E_f)$$

This is **the** workhorse formula of atomic, nuclear, and solid-state transition theory. Note the conditions: (a) continuum of final states, (b) long times compared to $1/\omega_{fi}$ but short compared to the inverse Rabi frequency. Outside these limits the full $\sin^2$ formula applies. Cite Dirac 1927 (*Proc. R. Soc. A* 114, 243) as the original derivation; Fermi 1950 (*Nuclear Physics*, Chicago lecture notes compiled by Orear-Rosenfeld-Schluter) for the name "golden rule no. 2."

**5. Selection rules are zeroes of the matrix element.** When $\langle f | \hat{H}' | i \rangle = 0$ by symmetry, no first-order transition. For the electric-dipole interaction $\hat{H}' = -e \hat{\vec{r}} \cdot \vec{\mathcal{E}}(t)$, the angular integrals over hydrogenic states give:
- $\Delta \ell = \pm 1$ (parity flip plus angular-momentum addition triangle)
- $\Delta m_\ell = 0, \pm 1$ (depending on polarization of $\vec{\mathcal{E}}$: $\pi$ for $\hat{z}$, $\sigma^\pm$ for circular)
- $\Delta s = 0$ (spin doesn't couple to the electric field in the dipole approximation)

When dipole forbidden, magnetic-dipole or electric-quadrupole transitions take over — much weaker, governed by selection rules that involve different angular operators. The 21-cm hydrogen line is a magnetic-dipole transition, "forbidden" in the dipole sense, and it lights up the entire universe in radio astronomy.

## B. Domain examples and cases

**Case 1: Two-level Rabi oscillations (the simulation centerpiece).** A two-level atom with energies $E_g$ and $E_e = E_g + \hbar\omega_0$, driven by $\hat{H}'(t) = \hbar\Omega \cos(\omega t) (|e\rangle\langle g| + |g\rangle\langle e|)$ where $\Omega$ is the bare Rabi frequency. In the rotating frame:

$$P_{g \to e}(t) = \frac{\Omega^2}{\Omega^2 + \Delta^2} \sin^2\!\left(\frac{\sqrt{\Omega^2 + \Delta^2}}{2} t\right)$$

with detuning $\Delta = \omega - \omega_0$. At resonance ($\Delta = 0$): full population transfer at $t = \pi/\Omega$ (a "$\pi$-pulse"). Off resonance: oscillations are smaller in amplitude and faster in generalized frequency. **This solution is exact** — not perturbative. Comparing it to first-order perturbation theory is the lesson: PT captures the small-amplitude oscillations but misses the saturation. The simulation must show this collision.

Historical anchor: Rabi's molecular-beam magnetic-resonance experiments at Columbia (group with Zacharias, Millman, Kusch), first resonance observed January 1938, published in *Phys. Rev.* 53, 318 (1938) and *Phys. Rev.* 55, 526 (1939). Nobel 1944. The two-level driven system is the *quantum* model of every NMR, ESR, and qubit-control experiment. Modern relevance: a transmon qubit driven by microwave is literally this problem.

**Case 2: Spontaneous emission and Einstein A coefficient.** A textbook subtlety: $\hat{H}_0$ for the atom alone cannot produce spontaneous emission — the excited eigenstate of an isolated atom is stationary. Spontaneous emission requires the *quantized* electromagnetic field; the perturbation is the coupling to vacuum fluctuations. Einstein 1916/1917 (*Mitt. Phys. Ges. Zürich* 16, 47, 1916; revised *Physikalische Zeitschrift* 18, 121, 1917 — "Zur Quantentheorie der Strahlung" / "On the Quantum Theory of Radiation") derived the relation between $A$ and $B$ coefficients without ever quantizing the field, using thermodynamic equilibrium with blackbody radiation:

$$\frac{A_{21}}{B_{21}} = \frac{8\pi h \nu^3}{c^3}$$

For hydrogen 2p → 1s: $A_{2p \to 1s} \approx 6.27 \times 10^8 \, \text{s}^{-1}$, lifetime $\tau \approx 1.6$ ns. [verify exact value from Griffiths Example 9.x / NIST atomic spectra database.] The student should see this as a chained calculation: compute $\langle 1s | \hat{x} | 2p \rangle$, plug into the dipole-emission rate formula, get nanoseconds. This is what spectroscopists use every day.

**Case 3: Laser physics — population inversion + stimulated emission.** Maiman 1960 (*Nature* 187, 493–494, 6 August 1960, "Stimulated Optical Radiation in Ruby" — under 300 words, two figures, rejected twice by *Phys. Rev. Lett.* before going to *Nature*). Ruby contains $\text{Cr}^{3+}$ ions with three relevant levels: ground, a metastable upper state, and a fast-decaying pump level. Pumping via flashlamp populates the pump level; fast non-radiative decay accumulates atoms in the metastable level (microsecond lifetime); when population inversion exceeds threshold, stimulated emission cascades into a coherent pulse at 694.3 nm. The chapter does not need to teach laser engineering — it needs to show how Einstein's B coefficient + population inversion produce *amplification*, which is the lock-and-key explanation for the existence of lasers.

**Case 4: Selection rules in action — why $1s \to 2s$ is forbidden but $1s \to 2p$ is not.** Worked example: compute $\langle 2s | z | 1s \rangle$ (zero, by parity — both states are even, $z$ is odd) and $\langle 2p_0 | z | 1s \rangle$ (nonzero). Direct demonstration. Then compute $\langle 2p_{\pm 1} | z | 1s \rangle$ (zero, by $\Delta m = 0$ for $z$-polarization) and $\langle 2p_{\pm 1} | x \pm iy | 1s \rangle$ (nonzero, $\sigma^\pm$ polarization). This is the moment selection rules stop being a recipe and start being a calculation.

**Failure case: applying Fermi's Golden Rule to a discrete two-level system.** A common student error. The Golden Rule assumes a continuum density of states; for a two-level atom there is one final state, not a continuum, so the delta-function step fails and you must keep the $\sin^2$/Δω² formula. The Rabi simulation makes this visible: at fixed time, the transition probability does *not* increase linearly with time near resonance (the Rabi flop is sinusoidal). If you naively applied Golden Rule you'd predict linear-in-time probability and get population > 1 at long times. The simulation can show both regimes side by side.

## C. Connections and dependencies

**Backward:**
- Chapter 9 (time-independent PT): same Dyson-series expansion strategy applied with explicit time dependence; the algebra is parallel.
- Chapter 4 (Dirac notation): the formal apparatus of interaction picture requires unitary operators applied to kets.
- Chapter 8 (hydrogen atom): every spectroscopy application needs hydrogenic states.
- Chapter 6 (harmonic oscillator): the dipole-coupling formula for emission/absorption reuses ladder operators when you quantize the field.

**Forward:**
- Chapter 11 (WKB/tunneling): different approximation, different regime; mention the contrast — PT is for "small effect over time," WKB is for "smooth potential at any time."
- Chapter 12 (entanglement and quantum information): qubit control *is* two-level Rabi physics; the gates of a quantum computer are pulse-shape engineering on this formula.
- Chapter 13 (modern connections): laser cooling, optical clocks, NMR, ESR, quantum sensing — all built on this chapter's machinery.

**Cross-discipline:**
- Atomic, molecular, optical (AMO) physics: Fermi's Golden Rule is the lingua franca.
- Solid-state spectroscopy: absorption, photoluminescence, photoemission — same formula, different density of states.
- Nuclear physics: beta decay (Fermi's original 1934 application — Fermi 1934, *Z. Phys.* 88, 161).
- Quantum chemistry: vibrational and electronic spectroscopy, time-dependent density functional theory.
- Quantum information: gate fidelity, decoherence rates via Lindblad — all rooted in time-dependent PT.

## D. Current state of the field

- **Ultrafast spectroscopy.** Sub-femtosecond pulses (attosecond science, Nobel 2023 to L'Huillier, Krausz, Agostini) probe electronic dynamics on the timescale of one optical cycle. Linear-response PT extends to nonlinear-response PT: two-photon absorption, sum-frequency generation, third-order responses underlying pump-probe spectroscopy.
- **Coherent control.** Shaped optical pulses (Tannor, Rice 1985, *J. Chem. Phys.* 83, 5013) drive molecules into specific final states by exploiting interference of multiple PT pathways. The mathematical structure is the same first-order transition amplitude — what changes is the time-dependence of $\hat{H}'(t)$.
- **Quantum optimal control.** GRAPE, Krotov, CRAB algorithms shape pulses to maximize gate fidelity on qubits. Industrial-scale relevance: IBM, Google, IonQ all use optimal-control derivatives of the Rabi physics to calibrate gates.
- **Beyond rotating-wave approximation.** Bloch-Siegert shift, counter-rotating term effects in strong-field regimes. The RWA fails when $\Omega \sim \omega_0$ — increasingly relevant in superconducting qubit physics and strong-field laser-atom interaction.
- **Open-system extensions.** Lindblad master equation captures decoherence and dissipation perturbatively in system-environment coupling. The Born-Markov approximation is structurally a Fermi's Golden Rule for the system+bath.

## E. Teaching considerations

**Why students fail at this chapter:**
1. **Algebraic density of the first-order amplitude derivation.** Three different time-dependent objects (the Schrödinger ket, the interaction-picture ket, the coefficient $c_f$) confuse everyone. Slow down at the picture-change; show explicitly how the operator becomes time-dependent.
2. **The leap from $\sin^2$/Δω² to the delta function.** This is the long-time limit, and it's not obvious to students that "integrating against a peaky function that gets peakier and peakier" is mathematically the same move as a delta function. Show the integral with a finite Lorentzian or sinc² and take the limit graphically — the simulation can do this directly.
3. **Resonance vs. detuning vs. Rabi frequency vs. driving amplitude.** Four parameters, students get them tangled. Define each precisely, then *vary one at a time* in the simulation.
4. **Selection rules as a black box.** Students memorize $\Delta \ell = \pm 1$ without ever computing a matrix element. Demand they compute $\langle 2s | z | 1s \rangle = 0$ at least once in their lives. The forbidden becomes a calculation, not a rule.
5. **Spontaneous emission as a separate phenomenon.** Without quantum electrodynamics, spontaneous emission is mysterious — the unperturbed eigenstate $|e\rangle$ should be stationary forever. Acknowledge: Einstein's thermodynamic argument gives the relation between $A$ and $B$ without quantizing the field; *deriving* $A$ from first principles requires field quantization (out of scope for this book).

**Pedagogical sequencing:**
1. Hook with the question: "an electron is in $|1s\rangle$, you shine light at it. What happens?" Make sure they understand this is the question all of spectroscopy answers.
2. Derive $c_f(t)$ from the interaction picture. Show every step.
3. Specialize to monochromatic perturbation, derive the $\sin^2$/Δω² profile, plot it for fixed $t$ — the resonance lineshape.
4. Take the long-time / continuum limit; derive Fermi's Golden Rule.
5. Apply to hydrogen $2p \to 1s$: compute $\langle 1s | z | 2p_0 \rangle$, get the lifetime.
6. Two-level Rabi exact solution as the failure mode of PT: it works for short times, breaks at long times when population approaches 1.
7. Simulation: dial the detuning, watch the resonance peak.

## F. Library files relevant to this chapter

- `pantry/436681929-Introductory-Quantum-Mechanics-by-Richard-L-Liboff-pdf.txt` — Liboff §13.5 (Time-Dependent Perturbation Theory), §13.7 (Harmonic Perturbation Theory). Pantry lines 34964–34966 and following. Liboff's derivation of Fermi's Golden Rule is more leisurely than Griffiths'; useful for students who want a second pass.
- Griffiths, *Introduction to Quantum Mechanics* 3e, Chapter 11 (or 2e, Chapter 9) — primary textbook reference. Brief cites Ch. 9, consistent with 2e. [verify edition.]
- `pantry/993201189-Solution-Manual-Introduction-to-Quantum-Mechanics-3e-Griffiths.txt` — preview only; not usable as a working solution manual.

**Notably missing from the pantry:**
- Cohen-Tannoudji, Diu, Laloë *Quantum Mechanics* Vol. II Chapter XIII — the most thorough textbook derivation of the Golden Rule with explicit attention to validity conditions.
- Sakurai *Modern Quantum Mechanics* Chapter 5 — cleanest interaction-picture derivation, with the Dyson series spelled out as a time-ordered product.
- Loudon *The Quantum Theory of Light* — best textbook reference for Einstein A/B coefficients connected to dipole matrix elements.
- Allen & Eberly *Optical Resonance and Two-Level Atoms* (Dover reprint) — the Rabi physics reference.

## F.5 Simulation pedagogy and D3 specifics

**Why two-level Rabi is *the* pedagogical sweet spot for time-dependent PT.** The two-level driven system has an exact closed-form solution. It also has a clean perturbative limit. So the simulation can show *both at once*, side by side, and the student sees with their eyes the regime where perturbation theory works and the regime where it fails. No other simulation in the chapter has this property as cleanly. Build this one well; the rest are bonus.

**Three nested visualizations, one simulation file:**

*Panel A: Population vs. time at fixed detuning.* Two lines on the same plot: $|c_e(t)|^2$ from exact two-level solution (thick solid), $|c_e(t)|^2$ from first-order PT (dashed). At resonance ($\Delta = 0$), exact oscillates fully between 0 and 1; PT predicts $(\Omega t / 2)^2$ which agrees only for $\Omega t \ll 1$. Off resonance, both oscillate at the generalized Rabi frequency $\sqrt{\Omega^2 + \Delta^2}$, but with different amplitudes. **The teaching moment:** dial the time slider out; the dashed curve goes to infinity, the solid curve stays bounded. Perturbation theory's failure is visual.

*Panel B: Transition probability vs. detuning at fixed time.* Plot $P_{g \to e}(\Delta)$ at a chosen $t$. The exact curve is a Lorentzian-like saturating shape; the PT curve is the diffraction-pattern $\sin^2(\Delta t/2)/(\Delta/2)^2$ — sharp central peak with sinc² sidelobes. **Teaching moment:** the sidelobes are PT artifacts; the exact solution smooths them away as $\Omega t$ grows.

*Panel C: Fermi's Golden Rule regime (optional, advanced).* A "continuum" toggle: replace the single final state $|e\rangle$ with a band of states $|e_k\rangle$ with closely spaced energies. Show that the *total* probability summed over the band grows *linearly* in time after a short transient — the Golden Rule rate $W = (2\pi/\hbar) |\langle V \rangle|^2 \rho(E)$. Compare to the bare two-level Rabi flopping. This is the moment "continuum + long time = Golden Rule" lands as a calculation, not a recipe.

**Controls:**
- Bare Rabi frequency $\Omega$ slider (0 to $\sim 0.5 \omega_0$).
- Detuning $\Delta = \omega - \omega_0$ slider (centered on zero, range $\pm \Omega$ × 5).
- Time slider $t$ (range 0 to a few periods of the generalized Rabi frequency).
- Toggle: "show PT" / "show exact" / "both."
- Toggle: "two-level" / "continuum" (for Panel C).

**D3 v7 specifics:**
- Compute $P_{g \to e}(t, \Delta, \Omega)$ analytically; no numerical Schrödinger integration needed for the two-level case. Vectorize over $t$ or over $\Delta$ depending on which panel is active.
- Use `requestAnimationFrame` for smooth time-slider scrubbing; pre-compute a table of values at slider build time and look up.
- For Panel C, sum over a chosen number of band states (10–50); compute each amplitude analytically and add them. Population grows linearly only after $t \gtrsim 2\pi / \Delta_{band}$ where $\Delta_{band}$ is the level spacing — show this transient explicitly.
- Use `d3-shape` line generators; do not animate with `transition()` for the time evolution (too slow at 60fps); use direct attribute updates via `attr("d", linegen(data))`.
- Color: detuning axis should use a diverging palette (blue for $\omega < \omega_0$, red for $\omega > \omega_0$). PhET's "quantum tunneling" sim uses a similar visual convention for energy vs. potential.

**The Bloch-sphere companion (extension).** If time permits, add a Bloch-sphere panel: the two-level state on the unit sphere, with $\hat{z}$ as the energy axis. At resonance with a $\pi$-pulse, the state rotates from south pole to north pole. Off resonance, the rotation axis tilts and the trajectory is a circle off the north pole. This is the *geometric* picture of Rabi physics; once a student has both — population-vs-time AND Bloch sphere — they have what every working AMO physicist has.

**Pedagogical anti-pattern to avoid:** do not let the student vary the driving amplitude ($\Omega$) by orders of magnitude without also varying the time axis. The Rabi period scales as $1/\Omega$; if you crank $\Omega$ way up without rescaling time, the oscillations vanish off the right edge of the plot. Either pin the time axis to "number of Rabi periods" or auto-rescale.

**Extension prompts for the chapter:**
1. Add a pulse-shape selector: square pulse, Gaussian pulse, hyperbolic-secant pulse. Show that a hyperbolic-secant pulse can drive a perfect $\pi$-rotation even off resonance (Rosen-Zener problem; cite Rosen & Zener 1932, *Phys. Rev.* 40, 502).
2. Add a decoherence rate $T_1$ (energy relaxation) and $T_2$ (dephasing). Watch the Rabi oscillations damp; connect to NMR and qubit physics.
3. Switch from sinusoidal drive to a "chirp" — frequency that sweeps through resonance. Demonstrate adiabatic rapid passage.

## G. Gaps and flags

- [verify] Griffiths edition mapping: 3e Ch. 11 vs 2e Ch. 9. Brief says Ch. 9. Confirm before drafting.
- [verify] Exact lifetime of hydrogen 2p state — Griffiths Example 9.4 (2e) gives $\tau \approx 1.6$ ns; NIST atomic spectra database has the experimental value. Cross-check.
- [verify] Dirac 1927 citation: *Proc. R. Soc. London A* 114, 243 (1927), "The quantum theory of the emission and absorption of radiation." Contains the original time-dependent PT derivation that became Fermi's Golden Rule.
- [verify] Fermi 1950 textbook: "Nuclear Physics: A Course Given by Enrico Fermi at the University of Chicago," compiled by Orear, Rosenfeld, Schluter, University of Chicago Press. Confirm exact pagination of "Golden Rule No. 2."
- [verify] Einstein 1916/1917 citations: original 1916 paper *Mitteilungen der Physikalischen Gesellschaft Zürich* 16, 47; expanded 1917 *Physikalische Zeitschrift* 18, 121, "Zur Quantentheorie der Strahlung." English translation widely available; the 1917 paper is canonical.
- [verify] Maiman 1960 ruby laser citation: *Nature* 187, 493–494 (6 Aug 1960). Confirmed in web search.
- [verify] Rabi 1938/1939 citations: *Phys. Rev.* 53, 318 (1938) and *Phys. Rev.* 55, 526 (1939). Cross-check the exact volume/page for the first published resonance signal.
- [flag] The chapter's discussion of spontaneous emission necessarily steps outside semiclassical PT. Be honest: Einstein's argument is thermodynamic; the *derivation* of $A$ requires field quantization. The chapter can present $A/B$ relation without QED; flag the gap for Chapter 13 (modern connections) or a future quantum-optics elective.
- [flag] Rotating-wave approximation is used silently in every two-level derivation. Mention it explicitly; it's the standard approximation but it has a name and a regime of validity.
- [flag] "Fermi's Golden Rule" is misattributed — Dirac derived it twenty years earlier. The chapter should acknowledge this honestly (per the workshop's "the method applies to the method" rule); naming a thing for the wrong person is the kind of historical sloppiness Feynman would have called out.
- [open question] Should the chapter introduce the Bloch-sphere picture? It's the natural geometric language and dominates modern qubit-control literature. Brief is silent. Default: introduce as an extension simulation; do not require it in the main derivation.
- [open question] Where does laser cooling fit? It's the most beautiful and consequential modern application of time-dependent PT. Could be a half-page sidebar; could be deferred to Chapter 13. Default: brief paragraph in the synthesis section, full treatment in Ch. 13.
