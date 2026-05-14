# Research Notes: Chapter 11 — The WKB Approximation and Tunneling
**Source:** TIKTOC.md chapter entry (lines 591–638)
**Notes file:** 11-the-wkb-approximation-and-tunneling_notes.md
**Corresponding chapter:** chapters/11-wkb-tunneling.md (not yet written)
**Generated:** 2026-05-13

---

## Chapter summary (from TIKTOC.md) [verbatim paste]

**Filename:** `11-wkb-tunneling.md`
**Arc position:** Act Three, Chapter 11

**One-line:** Students learn the WKB semiclassical approximation and apply it to quantum tunneling — computing transmission coefficients for barriers that would be classically impenetrable — and build a tunneling simulator showing barrier penetration.

**Chapter description:**
The WKB (Wentzel-Kramers-Brillouin) approximation applies when the potential varies slowly compared to the de Broglie wavelength — the semiclassical regime. It gives approximate wave functions for classically allowed and forbidden regions and, most importantly, a simple formula for tunneling transmission coefficients. Quantum tunneling is one of the most physically consequential quantum phenomena: it underlies nuclear fusion in stars, radioactive decay, scanning tunneling microscopy, tunnel diodes, and DNA mutation. The simulation lets students tune barrier height and width and watch the transmission coefficient change — making viscerally clear how exponentially sensitive tunneling is to barrier parameters.

**Core concepts:**
- The semiclassical regime: potential varies slowly; de Broglie wavelength locally defined
- WKB wave functions:
  - Classically allowed (E > V): ψ ≈ A/√p(x) × e^(±i∫p(x)dx/ℏ)
  - Classically forbidden (E < V): ψ ≈ A/√|p(x)| × e^(±∫|p(x)|dx/ℏ)
- Connection formulas at turning points
- Tunneling through a rectangular barrier: exact solution for comparison
- WKB tunneling probability: T ≈ e^(-2γ) where γ = (1/ℏ)∫√(2m(V-E))dx
- Applications:
  - Gamow's theory of alpha decay: derive the Geiger-Nuttall law
  - Scanning tunneling microscopy: exponential sensitivity to tip-sample distance
  - Nuclear fusion in stars: tunneling through the Coulomb barrier
- Bound states via WKB: Bohr-Sommerfeld quantization condition

**Key vocabulary:** WKB approximation, semiclassical, turning point, connection formulas, tunneling, transmission coefficient, Gamow factor, Geiger-Nuttall law, scanning tunneling microscopy

**Common misconceptions:**
- "Tunneling violates energy conservation" — the particle never exists at any point in the barrier with less than zero kinetic energy; the wave function has amplitude there but the measurement outcome is always E
- "Tunneling is rare and exotic" — it underlies nuclear fusion in every star, including the Sun

---

## A. Conceptual foundations

Five conceptual pillars. The first three build the approximation; the last two are physical interpretation.

**1. WKB is a controlled expansion in $\hbar$.** Write the wave function as $\psi(x) = \exp[(i/\hbar) S(x)]$ — exact for any $\psi$, since $S(x)$ is then a complex function determined by the equation. Substitute into the time-independent Schrödinger equation and you get a nonlinear equation for $S$:

$$\frac{(S')^2}{2m} - \frac{i\hbar}{2m} S'' = E - V(x)$$

Expand $S = S_0 + (\hbar/i) S_1 + (\hbar/i)^2 S_2 + \cdots$. Matching powers of $\hbar$: the leading order gives $(S_0')^2 = 2m(E - V) = p^2(x)$, so $S_0(x) = \pm \int p(x') dx'$. Next order gives $S_1 = -\frac{1}{2} \ln p(x)$. Combine:

$$\psi_{WKB}(x) \approx \frac{C}{\sqrt{p(x)}} \exp\!\left[\pm \frac{i}{\hbar} \int p(x') dx'\right]$$

The factor $1/\sqrt{p(x)}$ has a classical interpretation: where the classical particle moves slowly, the probability density $|\psi|^2 \propto 1/p$ is large. The wave function spends time in proportion to where the classical particle does. This is the *semi*-classical part of "semiclassical."

**2. The approximation is valid when the potential varies slowly on the scale of the local de Broglie wavelength.** The expansion parameter is $|\hbar S_0''/(S_0')^2| = |\hbar p'/p^2| = |d\lambda/dx|$ where $\lambda(x) = h/p(x)$. Validity: $|d\lambda/dx| \ll 1$. The wavelength must change slowly across one wavelength. This fails *exactly* at the classical turning points where $E = V(x)$ and $p \to 0$, $\lambda \to \infty$ — the very places we most want to use the approximation. Hence the next pillar.

**3. Connection formulas patch WKB through turning points via Airy functions.** Near a turning point $x_0$ where $E = V(x_0)$, linearize the potential: $V(x) \approx V(x_0) + V'(x_0) (x - x_0)$. The Schrödinger equation in this linear potential is the Airy equation; its exact solution is $\text{Ai}(z)$, which oscillates for $z < 0$ (classically allowed side) and decays for $z > 0$ (forbidden side). Match the Airy asymptotic forms to the WKB forms on each side, and you get the **connection formulas:**

For a turning point at $x = a$ with classically allowed region to the left, forbidden region to the right:
$$\frac{2}{\sqrt{p(x)}} \cos\!\left[\frac{1}{\hbar} \int_x^a p\, dx' - \frac{\pi}{4}\right] \;\longleftrightarrow\; \frac{1}{\sqrt{|p(x)|}} \exp\!\left[-\frac{1}{\hbar} \int_a^x |p|\, dx'\right]$$

The $\pi/4$ phase is the *Maslov index* contribution from one turning point. Bender & Orszag (*Advanced Mathematical Methods for Scientists and Engineers*, 1978) is the standard reference for the matched-asymptotics derivation. [verify chapter and edition.]

**4. Tunneling probability is exponentially suppressed in the action of the forbidden region.** For a barrier between turning points $a$ and $b$ with $V(x) > E$ in between:

$$T \approx \exp\!\left[-\frac{2}{\hbar} \int_a^b \sqrt{2m(V(x) - E)}\, dx\right] = e^{-2\gamma}$$

The integral is the *Gamow factor*. Two crucial features:
- **Exponential sensitivity:** the transmission depends *exponentially* on barrier height, width, and particle energy. A small change in any of these is amplified into a giant change in $T$. This is what makes alpha decay halflives span 24 orders of magnitude, and what makes STM atomically resolved.
- **The barrier shape *integrates* into the formula.** Square barriers, parabolic barriers, Coulomb barriers — all get the same treatment, you just compute the integral.

**5. Bohr-Sommerfeld quantization is the WKB version of bound states.** For a particle bound between two turning points $a$ and $b$, requiring a single-valued, normalizable wave function gives:

$$\oint p\, dx = 2 \int_a^b p(x)\, dx = \left(n + \frac{1}{2}\right) h, \quad n = 0, 1, 2, \ldots$$

The integer comes from counting wavefunction nodes; the $1/2$ comes from $\pi/4$ at each turning point (Maslov index). The factor was missed in the original Bohr-Sommerfeld 1913–1916 quantization condition (which had $nh$, not $(n+1/2)h$); the Maslov correction is the WKB upgrade. For the harmonic oscillator, $\oint p\, dx = (n+1/2)h$ is *exact*, not just leading order — a happy accident that bound generations of physicists to the formula.

## B. Domain examples and cases

**Case 1: Rectangular barrier — the exact-vs-WKB comparison.** Particle energy $E < V_0$, barrier from $x=0$ to $x=L$. The exact transmission coefficient (Griffiths Problem 2.33 / Example 2.7):

$$T_{exact} = \left[1 + \frac{V_0^2 \sinh^2(\kappa L)}{4 E (V_0 - E)}\right]^{-1}, \quad \kappa = \frac{\sqrt{2m(V_0 - E)}}{\hbar}$$

For $\kappa L \gg 1$ (thick or tall barrier), $\sinh(\kappa L) \approx e^{\kappa L}/2$ and:

$$T_{exact} \approx \frac{16 E (V_0 - E)}{V_0^2} \, e^{-2\kappa L}$$

The WKB prediction is $T_{WKB} = e^{-2\kappa L}$ (exact integral for constant $V_0$). So WKB gets the exponential right and misses the prefactor. The prefactor is a smooth function of order 1; the exponential carries the physics. **This is the most important fact in the chapter.** The simulation will let students dial $L$ and watch both $T_{exact}$ and $T_{WKB}$ on the same log plot — they will see the curves diverge by an O(1) factor and agree on the slope.

**Case 2: Gamow's theory of alpha decay (1928).** Gamow's paper (G. Gamow, "Zur Quantentheorie des Atomkernes," *Zeitschrift für Physik* 51, 204–212, submitted 29 July 1928) was one of the first applications of quantum mechanics to a nuclear problem. Independently and within a day, Gurney & Condon submitted to *Nature* (224, 439, 1928). Both showed that the enormous range of alpha-decay halflives — from $10^{-7}$ seconds for polonium-212 to $10^{17}$ years for thorium-232, **24 orders of magnitude** — could be explained by quantum tunneling through the Coulomb barrier.

Mechanism: model the alpha particle as a pre-formed cluster bouncing inside the nucleus (radius $R$). Outside the nucleus, the alpha sees a Coulomb potential $V(r) = 2(Z-2) e^2 / (4\pi\epsilon_0 r)$ (charges $+2e$ on the alpha and $+(Z-2)e$ on the daughter). The barrier extends from $r = R$ to $r = r_c$ where $V(r_c) = E$. The Gamow factor:

$$\gamma = \frac{1}{\hbar} \int_R^{r_c} \sqrt{2m\left[\frac{2(Z-2)e^2}{4\pi\epsilon_0 r} - E\right]} \, dr$$

This integral can be done analytically (substitute $r = r_c \sin^2\theta$). For $E \ll V_{max}$:

$$\gamma \approx \frac{2(Z-2) e^2}{4 \epsilon_0 \hbar v} \pi - \text{corrections}$$

where $v = \sqrt{2E/m}$. Decay rate $\Gamma \sim \nu_0 \cdot e^{-2\gamma}$ where $\nu_0$ is the attempt frequency ($\sim 10^{21}$ Hz from $v/2R$). Taking the log:

$$\log_{10}(\tau_{1/2}) \approx A(Z) + \frac{B(Z)}{\sqrt{E}}$$

This is the **Geiger-Nuttall law** (empirical from 1911–1912; H. Geiger & J. M. Nuttall, *Phil. Mag.* 22, 613, 1911 and 23, 439, 1912). The plot of $\log \tau_{1/2}$ vs. $1/\sqrt{E}$ for alpha emitters of fixed $Z$ is a straight line — a famous figure students should see. Gamow derived the line from first principles. The 24-decade range is the dynamic range of an exponential.

**Case 3: Scanning tunneling microscopy.** Binnig & Rohrer at IBM Zurich, first successful test 16 March 1981; published Binnig, Rohrer, Gerber & Weibel, *Appl. Phys. Lett.* 40, 178 (January 1982) for the first STM image of a vacuum-tunneling barrier modulation; *Phys. Rev. Lett.* 49, 57 (1982, submitted 30 April) for the first 7×7 silicon reconstruction. Nobel Prize 1986 (with Ruska for the electron microscope).

Mechanism: bring a metal tip within ~Å of a conducting sample, apply a small bias voltage ($\sim$ mV); electrons tunnel through the vacuum gap with current

$$I \propto e^{-2\kappa d}, \quad \kappa = \frac{\sqrt{2m \phi}}{\hbar} \approx 0.51 \, \text{Å}^{-1} \cdot \sqrt{\phi / \text{eV}}$$

where $\phi$ is the work function ($\sim$ 4–5 eV for most metals). With $\kappa \approx 1$ Å$^{-1}$, a 1 Å change in $d$ changes $I$ by a factor of $e^2 \approx 7.4$ — almost an order of magnitude per atomic radius. **This is what makes STM atomically resolved:** the exponential turns sub-angstrom topography into measurable current swings. Worked example for the chapter: estimate the current ratio for $d = 5$ Å vs. $d = 6$ Å with $\phi = 4$ eV.

**Case 4: Nuclear fusion in stars.** Eddington's 1920 conjecture that stellar energy comes from hydrogen fusion was rejected by classical physicists because two protons at stellar temperatures (~$10^7$ K, $kT \sim 1$ keV) have $\sim 10^{-3}$ of the energy needed to climb the Coulomb barrier ($V_{Coul}(R) \sim$ 1 MeV at $R \sim$ fm). Atkinson & Houtermans 1929 (*Z. Phys.* 54, 656) applied Gamow's tunneling formula and showed that the tail of the Maxwell-Boltzmann distribution, combined with the energetically rising Gamow penetration factor, gives a narrow energy window — the **Gamow peak** — where most fusion happens. Modern pp-chain rates in stars are still computed by integrating Maxwell-Boltzmann × Gamow factor × nuclear cross section over relative energies. Every star burns by tunneling.

**Case 5: Flash memory.** A floating-gate transistor stores a bit by trapping electrons on a polysilicon gate isolated by a thin (5–10 nm) oxide layer. Writing: high voltage drives electrons *into* the floating gate by Fowler-Nordheim tunneling through the oxide. Reading: charge state changes the threshold voltage of the transistor channel below. Erasing: reverse the voltage, tunnel them out. The whole device is engineered tunneling. Estimated tunneling current scales as $\exp(-K / \mathcal{E})$ where $\mathcal{E}$ is the oxide electric field (Fowler-Nordheim form, derived from WKB through a triangular barrier). [verify Fowler-Nordheim 1928 *Proc. R. Soc. A* 119, 173.]

**Possible biology — proton tunneling in DNA.** Löwdin 1963 (P.-O. Löwdin, "Proton tunneling in DNA and its biological implications," *Rev. Mod. Phys.* 35, 724) proposed that protons in the hydrogen bonds between Watson-Crick base pairs can tunnel between two tautomeric positions, occasionally flipping a base into a mismatched tautomeric form that causes a point mutation when DNA replicates. The proposal is over sixty years old and remains *contested*: open-system quantum simulations (Slocombe et al., *Comm. Phys.* 5, 109, 2022) suggest the mechanism is plausible for G:C base pairs but not for A:T. **Use this as the chapter's honest-about-uncertainty case:** the math is clean, the biological consequence is not yet settled.

**Failure case: cold-fusion claims.** Tunneling through the Coulomb barrier at room temperature in a metal lattice — claimed by Fleischmann & Pons 1989 to be enhanced enormously. Quantum mechanics constrains the tunneling rate: $e^{-2\gamma}$ for room-temperature deuterons in palladium gives a fusion rate so small ($\sim 10^{-75}$ events per pair per second) that no plausible enhancement can recover the claimed power output. This is the textbook example of "the exponential dominates" — chemistry cannot lower a nuclear-scale Gamow factor by 70 decades. Mention to make the WKB formula concrete and to teach students how to use a back-of-envelope tunneling estimate to falsify a claim.

## C. Connections and dependencies

**Backward:**
- Chapter 2 (Schrödinger equation): the rectangular-barrier exact solution is a standard 1D problem; WKB compares against it.
- Chapter 3 (probability and statistics): the exponential sensitivity of $T$ to barrier parameters is the kind of distribution students should be comfortable with after the Gaussian wave-packet chapter.
- Chapter 6 (harmonic oscillator): Bohr-Sommerfeld $(n + 1/2)h$ is *exact* for the harmonic oscillator; this is the calibration point.
- Chapter 8 (hydrogen atom): the Coulomb potential will reappear in the Gamow alpha-decay calculation.
- Chapter 9 (time-independent PT): both are approximation methods; perturbation theory works when something is small, WKB works when something is slow. Contrast explicitly.

**Forward:**
- Chapter 12 (entanglement/QI): not a direct connection; tunneling is single-particle physics. But Josephson junction qubits (superconducting qubits) live and die by Cooper-pair tunneling — a worked extension if time permits.
- Chapter 13 (modern connections): STM, qubits, topological systems all involve tunneling at some level.

**Cross-discipline:**
- Nuclear physics: alpha decay, fission, fusion — all tunneling.
- Solid state: tunnel diodes (Esaki 1958, Nobel 1973), Josephson effect (1962, Nobel 1973), STM, AFM, tunnel junctions.
- Chemistry: kinetic isotope effects, proton-coupled electron transfer, enzyme catalysis [contested — Klinman group claims tunneling contributions in alcohol dehydrogenase, Hammes-Schiffer's calculations support; not all reactions show it].
- Biology: proton tunneling in DNA (Löwdin 1963), electron tunneling in respiratory chain (Marcus theory hits tunneling regime at low temperatures), [verify] tryptophan-tryptophan electron transfer in photolyase.
- Astrophysics: hydrogen burning, helium flash, carbon-oxygen detonation in supernovae.
- Technology: flash memory, EEPROM, single-electron transistors, Esaki diodes, Josephson voltage standards.

## D. Current state of the field

WKB itself is mature mathematics — Wentzel, Kramers, Brillouin all in 1926, with Jeffreys 1924 the British precursor (sometimes the method is called JWKB). What's alive now:

- **Beyond-WKB and exact WKB.** Voros, Delabaere, Pham developed the *exact WKB* method: Borel summation of the formal WKB series, giving exact results from a divergent expansion. Active in mathematical physics and conformal field theory.
- **Instanton methods.** WKB-style tunneling in field theory: false-vacuum decay (Coleman 1977, *Phys. Rev. D* 15, 2929; with de Luccia 1980 *Phys. Rev. D* 21, 3305). Bounce solutions to the Euclidean equations of motion are the "tunneling trajectories" of a field. Same exponential suppression formula, different setting.
- **Dynamical tunneling and chaos-assisted tunneling.** In quasi-integrable systems, tunneling rates between symmetry-related classical regions can be enhanced by chaotic manifolds. Active in atomic physics (cold-atom experiments by Raizen group).
- **STM as a working laboratory tool.** Routine atomic-resolution imaging of surfaces; manipulation of individual atoms (Eigler 1989 IBM logo; positioned Xe atoms one by one). Spin-polarized STM, scanning tunneling spectroscopy. Atomic-scale physics is *experimental* now.
- **Tunneling in quantum biology.** A real subfield, not crackpot anymore: McFadden & Al-Khalili *Life on the Edge* (2014); ongoing work on enzyme catalysis (Klinman, Schwartz), photosynthesis (Engel et al. 2007 *Nature* 446, 782 on FMO complex — contested), olfaction (Turin 1996 — speculative, mostly rejected). The chapter should be honest: some claims hold up, others don't; the methodology for telling them apart is exactly the tunneling-rate estimate from this chapter.
- **Macroscopic quantum tunneling.** Caldeira-Leggett model for tunneling of a macroscopic degree of freedom (e.g., flux in a SQUID) coupled to a bath. Foundation of superconducting qubits.

## E. Teaching considerations

**Why students fail at this chapter:**
1. **WKB derivation is opaque.** Many students never internalize the $\hbar$ expansion; they memorize the formula. The remedy: actually do the substitution and the matching of powers. Showing the algebra is the teaching.
2. **The "connection formula sign" trap.** The matching at turning points has a directionality (incoming vs. outgoing): you can only connect *from* the classically allowed side *to* the forbidden side, not vice versa. Reversing causes spurious exponentially growing solutions. Bender & Orszag spend a chapter on this; Griffiths summarizes; students still get it backwards.
3. **"Tunneling violates energy conservation."** Address head-on. The wave function has amplitude inside the barrier, but *measuring* the energy gives $E$ (no measurement gives $E < V$). The classically forbidden region is forbidden *classically* — quantum mechanically, the particle just has an exponentially damped wave function there. Energy is conserved at every step.
4. **"Tunneling is rare."** No. Every star is tunneling right now. Every flash drive stores data via tunneling. Every STM scan is tunneling. The chapter should hammer this in the opening.
5. **The exponential is everything.** Students compute a Gamow factor and reach for the answer in linear units. The whole point is that small changes in the exponent are giant changes in $T$. Always plot $\log T$, not $T$.

**Pedagogical sequencing:**
1. Hook: alpha decay halflives span 24 decades. *Why*? (The exponential.) Or: how does an STM see atoms? (Same exponential.) Open in a specific puzzle.
2. The rectangular barrier — exact solution. Compute $T$, plot $\log T$ vs. $L$ and $V_0$. Students see the exponential.
3. WKB derivation: $\hbar$ expansion, oscillating vs. decaying forms, $1/\sqrt{p}$ prefactor. Show the algebra.
4. Connection formulas (sketch the Airy matching, don't grind through it; cite Bender & Orszag for the proof).
5. The general tunneling formula $T \approx e^{-2\gamma}$. Apply to Gamow alpha decay.
6. Bohr-Sommerfeld quantization as the bound-state version. Calibrate against harmonic oscillator (exact result).
7. Simulation: rectangular barrier first; then general WKB; then animated wave packet.

## F. Library files relevant to this chapter

- `pantry/436681929-Introductory-Quantum-Mechanics-by-Richard-L-Liboff-pdf.txt` — Liboff §7.7 (rectangular barrier and tunneling, lines 11941–12300), §7.10 (WKB approximation, lines 12746–13100). Very thorough; Liboff carefully separates the "oscillatory in I" / "exponential in II" / "oscillatory in III" cases. Better introductory treatment than Griffiths in some respects.
- Griffiths *Introduction to Quantum Mechanics* 3e Chapter 9 (WKB; in 2e it was Chapter 8). Brief mentions "Ch. 8" for WKB — consistent with 2e. Brief also mentions "Chapter 2" for the rectangular-barrier exact solution — consistent with both editions. [verify edition.]
- `pantry/993201189-Solution-Manual-Introduction-to-Quantum-Mechanics-3e-Griffiths.txt` — preview only.

**Notably missing from the pantry:**
- Bender & Orszag, *Advanced Mathematical Methods for Scientists and Engineers* (Springer/McGraw-Hill, 1978/1999). The canonical reference for WKB, connection formulas, and matched asymptotic expansions. Chapter 10 on WKB. Cited universally.
- Berry & Mount, "Semiclassical approximations in wave mechanics," *Reports on Progress in Physics* 35, 315 (1972). The review of WKB done right.
- Razavy, *Quantum Theory of Tunneling*, 2nd ed., World Scientific (2014) — encyclopedic.
- Krane *Introductory Nuclear Physics* (Wiley, 1988) Chapter 8 for the cleanest pedagogical alpha-decay treatment.
- Chen *Introduction to Scanning Tunneling Microscopy*, 2nd ed., Oxford (2008) — the standard STM reference.

## F.5 Simulation pedagogy and D3 specifics

**Why tunneling wave packet is *the* pedagogical sweet spot.** Tunneling is impossible to picture from a static figure. Griffiths shows three panels: incident wave, exponential decay inside, transmitted wave. The student looks at it, nods, and walks away with no intuition. **An animated Gaussian wave packet hitting a barrier and partially transmitting / partially reflecting is the single most effective visualization in all of undergraduate QM.** It cannot be replicated in print. It must be built.

PhET's *Quantum Tunneling and Wave Packets* (McKagan, Perkins, Wieman et al., 2008, *Am. J. Phys.* 76, 406) is the gold standard for this; build on its lessons, do not duplicate it.

**Three nested simulations, one HTML file:**

*Simulation A: Stationary scattering — $T(E)$ for a rectangular barrier.* Inputs: barrier height $V_0$, width $L$, mass $m$ (with $\hbar = 1$ in atomic units). Sweep energy $E$ from 0 to $2 V_0$. Plot $T(E)$ both exactly and via WKB ($T_{WKB} = e^{-2\kappa L}$ valid for $E < V_0$; transmission resonances for $E > V_0$ from the exact formula). On a *log* y-axis: the WKB and exact curves are parallel (same slope!) but offset by an O(1) prefactor. This is the teaching: WKB nails the slope, misses the prefactor by a constant of order unity. Lesson sticks.

*Simulation B: General WKB — $T$ for arbitrary barrier shape.* Barrier shape selector (rectangular, triangular, parabolic, double-barrier). Numerically integrate the Gamow integral $\int \sqrt{2m(V(x) - E)}\, dx$ over the classically forbidden region. Show: $T_{WKB}$ as a function of $E$. For the **parabolic barrier**, an exact result (Kemble's formula, $T = 1/(1 + e^{2\pi \epsilon})$) interpolates smoothly through $E = V_{max}$, where WKB diverges — this is a teachable failure of WKB at the top of the barrier.

*Simulation C: The animated wave packet — the pedagogical centerpiece.* A Gaussian wave packet with center momentum $p_0$ and width $\sigma_x$ initiated to the left of the barrier. Evolve the time-dependent Schrödinger equation using **Crank-Nicolson** (unconditionally stable, second-order accurate in time and space; standard reference for educational use). Show $|\psi(x,t)|^2$ as a filled area chart sliding right. When it hits the barrier:
- Part reflects (heads left).
- Part decays exponentially inside the barrier.
- Part emerges on the right with reduced amplitude.

The student sees the wave packet *split* into a transmitted piece and a reflected piece. Sliders: $V_0$, $L$, $E$ (via $p_0$). At $E \ll V_0$: nearly all reflection, vanishing transmitted bump. At $E \approx V_0$: roughly half-and-half. At $E > V_0$: mostly transmitted, with small reflection from the barrier edges (interference fringes). **This is the visualization that makes tunneling permanent in the student's intuition.**

**Controls (combined):**
- Barrier shape: rectangular / triangular / parabolic / double barrier
- $V_0$ slider
- $L$ (width) slider
- $E$ (energy) slider — drives both stationary curves and the wave-packet $p_0$
- Toggle: stationary view (Panel A/B) vs. wave-packet view (Panel C)
- Time-play button + time slider (for wave-packet view)
- Toggle: log y-axis vs. linear (force students to compare)

**D3 v7 specifics:**
- Wave-packet animation: pre-compute the full $(x, t)$ grid of $|\psi(x,t)|^2$ when the user releases a slider; play back via `requestAnimationFrame`. Crank-Nicolson on a 500×500 grid takes O(seconds) in JavaScript; this is a one-time cost, scrubbing is instant after.
- Use `d3.scaleLog` for the y-axis when displaying $T(E)$ — flag this in axis labels. Most introductory students have never seen a log plot; the chapter must teach them.
- Highlight the classically forbidden region with a translucent fill ($V(x) > E$, light red). Color the wave function: real part vs. imaginary part in two colors, or $|\psi|^2$ as a single filled curve. PhET uses both; this book should default to $|\psi|^2$ but offer a toggle to show real/imag for the curious.
- Use `d3-simple-slider` for the parameter sliders; integrate cleanly with v7.
- Boundary conditions for Crank-Nicolson: absorbing boundary conditions at the edges of the computational domain are necessary to prevent reflection artifacts from the box walls. Use the standard imaginary-potential absorber at the left/right 10% of the grid.
- Computational watch-out: the Crank-Nicolson tridiagonal solve in JS is straightforward (Thomas algorithm); avoid hauling in `numeric.js` for this — write 30 lines.

**The pedagogical move that nothing in print can do:** *show the wave packet incident on the barrier in slow motion.* The student watches a piece *go through.* They cannot un-see it. Every classical intuition they had about barriers is gone. This is the simulation Griffiths' figures cannot replicate, and it is the reason the +1 chapter format exists.

**Extension prompts:**
1. Add a **double barrier** and watch resonant tunneling — at certain energies, $T \to 1$ even though both individual barriers are highly opaque. This is the principle behind the resonant tunneling diode (Esaki & Tsu 1970, *IBM J. Res. Dev.* 14, 61).
2. Compute the **Gamow factor for alpha decay** explicitly: integrate the Coulomb-barrier penetration for $^{238}$U decay; reproduce the experimental halflife of $4.5 \times 10^9$ years to within an order of magnitude. (The fact that you can hit a number spanning 24 decades of dynamic range from a back-of-envelope quantum-mechanical estimate is the high-water mark of this chapter.)
3. Add a **Coulomb barrier shape** (1/r outside a nuclear radius). Compute $T$ vs. $E$ near the Gamow peak temperature for the pp chain. Show the convolution with Maxwell-Boltzmann that gives the fusion rate in stars.
4. **STM mode:** simulate the current $I \propto e^{-2\kappa d}$ as a function of tip-sample distance $d$. Add a 1-Å step on the sample surface and watch the current change as the tip scans across.

## G. Gaps and flags

- [verify] Griffiths edition mapping. Brief says Ch. 8 for WKB and Ch. 2 for rectangular tunneling. In 3e: WKB is Ch. 9, tunneling is Ch. 2. Confirm which edition the course uses.
- [verify] Gamow 1928 *Z. Phys.* 51, 204–212, submission date 29 July 1928. Web search confirmed; cite directly.
- [verify] Gurney & Condon 1928 *Nature* 122, 439 (independent simultaneous derivation); fuller paper *Phys. Rev.* 33, 127 (1929). Both should be cited if alpha-decay history is treated honestly.
- [verify] Binnig & Rohrer citations: first STM image of vacuum tunneling — *Appl. Phys. Lett.* 40, 178 (January 1982); first Si(111)-7×7 image — *Phys. Rev. Lett.* 49, 57 (1982). Helvetica Physica Acta 55 (1982), 726–735 is the longer Swiss-society paper. Nobel 1986.
- [verify] Atkinson & Houtermans 1929 *Z. Phys.* 54, 656 — first application of Gamow tunneling to stellar fusion.
- [verify] Löwdin 1963 *Rev. Mod. Phys.* 35, 724 — proton tunneling in DNA. Confirmed in web search.
- [verify] Fowler-Nordheim 1928 *Proc. R. Soc. A* 119, 173 — cold field-electron emission via tunneling. Connection to flash memory needs cited.
- [verify] McKagan, Perkins, Dubson, Malley, Reid, LeMaster, Wieman, "Developing and researching PhET simulations for teaching quantum mechanics," *Am. J. Phys.* 76, 406 (2008) — PhET's design principles; reference in F.5.
- [flag] Bohr-Sommerfeld $(n+1/2)h$ vs. $nh$ — the Maslov index is a 1970s upgrade (V. P. Maslov, *Théorie des perturbations et méthodes asymptotiques*, 1972 French translation of his 1965 Russian text). The chapter can mention without full treatment.
- [flag] Connection formula derivation via Airy functions is technically demanding; the chapter should *sketch* and cite Bender & Orszag, not derive.
- [flag] "Tunneling time" — a notorious subtle topic (Hauge-Støvneng, Büttiker, Larmor clock, attosecond delay measurements). Out of scope for this chapter but interesting enough to mention as a "still open" problem. Honest Feynman move: name the puzzle, don't resolve it.
- [flag] Cold fusion: a deliberately controversial example. The point is to show how to use tunneling estimates to falsify a claim, not to litigate Fleischmann-Pons. Frame as "what a quick back-of-envelope says" and move on.
- [open question] Should the chapter include the Esaki tunnel diode? Historically important (Nobel 1973), pedagogically clean (negative differential resistance via resonant tunneling). Default: brief mention; defer full treatment to a possible solid-state appendix.
- [open question] How much QFT-flavored "instanton" language to include? Tempting because it's beautiful, but the chapter is about undergraduate QM. Default: one-sentence forward pointer in the synthesis section.
