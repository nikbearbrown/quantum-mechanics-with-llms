# Research Notes: Chapter 02 — The Time-Independent Schrödinger Equation
**Source:** TIKTOC.md chapter entry (lines 157–202)
**Notes file:** 02-the-time-independent-schrodinger-equation_notes.md
**Corresponding chapter:** chapters/02-time-independent-schrodinger.md (not yet written)
**Generated:** 2026-05-13

---

## Chapter summary (from TIKTOC.md)

**One-line:** Students learn to solve the time-independent Schrödinger equation for simple potentials, building an infinite square well visualizer that shows all energy eigenstates and their superpositions.

**Chapter description:** The central technical chapter of Act One. Separation of variables converts the time-dependent Schrödinger equation into the time-independent version Ĥψ = Eψ — an eigenvalue problem. The infinite square well is solved exactly, giving discrete energy levels and standing wave solutions. The student sees quantization emerge naturally from boundary conditions, not from an ad hoc assumption. Superposition of stationary states produces time-dependent behavior. The simulation makes all of this visible: every eigenstate, their energies, and the time evolution of arbitrary superpositions.

**Core concepts:**
- Separation of variables: ψ(x,t) = ψ(x)φ(t); φ(t) = e^(-iEt/ℏ)
- TISE: (-ℏ²/2m)d²ψ/dx² + V(x)ψ = Eψ
- Stationary states: |ψ(x,t)|² time-independent
- Infinite square well: V = 0 on (0,L), V = ∞ outside; ψ_n(x) = √(2/L)sin(nπx/L); E_n = n²π²ℏ²/(2mL²)
- Superposition of stationary states; orthonormality; completeness
- Finite square well (brief): tunneling preview

**Key vocabulary:** stationary state, eigenstate, eigenvalue, energy quantization, boundary conditions, orthonormality, completeness, superposition, infinite square well.

**Common misconceptions:**
- "Quantization is assumed, not derived" — emerges from boundary conditions.
- "The particle is standing still in a stationary state" — probability density is static but ψ oscillates in time via e^(-iEt/ℏ).
- "Higher energy means larger region" — more nodes, not more space.

**Worked examples:** complete solution of the infinite square well; expansion coefficients for an arbitrary ψ(x, 0); time evolution of ψ_1 + ψ_2 superposition (the "sloshing").

**Simulation:** `02-infinite-well.html` — energy levels, ψ_n(x), |Ψ(x,t)|² with coefficient sliders.

**Bridge:** Chapter 3 introduces ladder operators for the harmonic oscillator.

---

## A. Conceptual foundations

### 1. Separation of variables

The time-dependent Schrödinger equation (TDSE) is iℏ ∂ψ/∂t = Ĥψ. When the Hamiltonian Ĥ does not depend on t (which it doesn't, for the systems in this chapter), an *ansatz* solves it:

ψ(x, t) = ψ(x) · φ(t).

Substituting: iℏ ψ(x) φ′(t) = (Ĥψ(x)) · φ(t). Dividing both sides by ψ(x)φ(t): iℏ φ′(t)/φ(t) = (Ĥψ(x))/ψ(x). The left depends only on t; the right only on x; they are equal; therefore both equal a constant. Call the constant E. Two ODEs result:

- φ′(t) = −(iE/ℏ) φ(t) → φ(t) = exp(−iEt/ℏ).
- Ĥψ(x) = E ψ(x) — the time-independent Schrödinger equation.

This is a *gift*. The full PDE (TDSE) reduces to an algebraic eigenvalue problem (TISE) plus a trivial time phase. Any solution of the TISE, multiplied by the universal phase exp(−iEt/ℏ), is a solution of the TDSE. The eigenvalue E is the *energy* of that state.

The trick — "separate the variables" — is one of the most reused techniques in physics. It works whenever Ĥ has no explicit time dependence. (Griffiths *Introduction to Quantum Mechanics* 3rd ed., §2.1, makes this point.)

### 2. The TISE in 1D

(−ℏ²/(2m)) d²ψ/dx² + V(x) ψ(x) = E ψ(x).

A second-order linear ODE for ψ(x). Given V(x), the equation is a *constrained* problem: not every E admits a normalizable solution. Boundary conditions (or normalizability at infinity) select a *discrete* set of allowed energies for bound states, and a *continuous* set for unbound states.

The whole edifice of one-dimensional QM is reading off this equation for various V(x):
- V = 0 (free particle, Chapter 0).
- V = ∞ outside (0, L) (infinite well, this chapter).
- V finite well (this chapter, brief).
- V = (1/2) m ω² x² (harmonic oscillator, Chapter 3).
- V central, 3D (hydrogen, Chapter 7).

### 3. Stationary states

A state of the form ψ(x, t) = ψ_E(x) exp(−iEt/ℏ) is called a *stationary state*. The reason is the probability density:

|ψ(x, t)|² = |ψ_E(x)|² · |exp(−iEt/ℏ)|² = |ψ_E(x)|² · 1 = |ψ_E(x)|².

Time-independent. The probability density of finding the particle does not change. *But the wave function itself is not static* — it carries the phase exp(−iEt/ℏ), and that phase is invisible only as long as you stay in a single eigenstate. The moment you take a *superposition* of two stationary states with different energies, the relative phase becomes physical:

|c_1 ψ_1 e^{−iE_1 t/ℏ} + c_2 ψ_2 e^{−iE_2 t/ℏ}|² = |c_1|² |ψ_1|² + |c_2|² |ψ_2|² + 2 Re(c_1* c_2 ψ_1* ψ_2 e^{−i(E_2 − E_1) t/ℏ}).

The cross term oscillates at angular frequency ω = (E_2 − E_1)/ℏ. *That* is where time-dependence comes back. The point the chapter must land hard: stationary states are *building blocks*. Real time evolution lives in their superpositions.

### 4. The infinite square well — boundary conditions force quantization

V(x) = 0 for 0 < x < L; V = ∞ elsewhere. Inside the well, TISE becomes

ψ″(x) = −(2mE/ℏ²) ψ(x).

Define k² = 2mE/ℏ². Solutions: ψ(x) = A sin(kx) + B cos(kx).

Boundary conditions: ψ(0) = 0 (because ψ must be continuous and ψ is forced to zero outside the well by V = ∞). Therefore B = 0. ψ(L) = 0 → A sin(kL) = 0 → kL = nπ, n = 1, 2, 3, ...

**This is where quantization is born.** It does not come from a postulate. It comes from requiring ψ to satisfy the boundary conditions of a confining potential. *Continuity of the wave function* — a regularity condition — *forces discrete k, therefore discrete E*.

The energies are E_n = (ℏ k_n)²/(2m) = n² π² ℏ²/(2 m L²).

Normalize: ∫_0^L A² sin²(nπx/L) dx = A² · L/2 = 1 → A = √(2/L).

So:
- **ψ_n(x) = √(2/L) sin(nπx/L)** for n = 1, 2, 3, ...
- **E_n = n² π² ℏ²/(2 m L²)** — energies scale as n².

n = 0 is excluded: ψ_0(x) ≡ 0, which is the *trivial* solution, not a physical state. (No particle at all.)

This is the chapter's deep-dive. The full path: ansatz → ODE → general solution → boundary conditions → discrete spectrum → normalization → labeled eigenstates. Every step visible. (Griffiths §2.2.)

### 5. Orthonormality and completeness

The eigenstates ψ_n are *orthonormal*: ⟨ψ_m | ψ_n⟩ = ∫_0^L ψ_m*(x) ψ_n(x) dx = δ_{mn}. Direct computation using sin(mπx/L) sin(nπx/L) = (1/2)[cos((m−n)πx/L) − cos((m+n)πx/L)] and integrating from 0 to L gives δ_{mn} after multiplying by 2/L.

They are also *complete*: any L²(0, L) function vanishing at the boundaries can be expanded as

ψ(x, 0) = Σ_n c_n ψ_n(x), with c_n = ⟨ψ_n | ψ(x, 0)⟩ = ∫_0^L ψ_n*(x) ψ(x, 0) dx.

This is the Fourier sine series, a result older than QM (Fourier 1822, *Théorie analytique de la chaleur*). The physical content: *any* initial state in the well is a sum of energy eigenstates. Once you know the c_n's, the full time evolution is determined:

ψ(x, t) = Σ_n c_n ψ_n(x) exp(−i E_n t/ℏ).

This is the chapter's *operational* result. Solve the TISE once; superpose; evolve in time via the phase factors. No need to integrate the TDSE numerically. The expansion-coefficient method is the dominant tool for the rest of the book.

### 6. The finite square well (brief)

V(x) = −V_0 for |x| < a/2; V = 0 outside. Differential equation has *two* regions; solutions are sinusoids inside, exponential decays outside. Matching ψ and ψ′ at the boundaries gives a transcendental equation for E that has only *finitely many* solutions for bound states. The wave function has *tails* in the classically forbidden region (V > E) — the preview of tunneling.

Important point: at least one bound state exists in any 1D finite well, no matter how shallow. (Griffiths §2.6 Problem 2.27.) This is a deep result that goes against classical intuition. The simulation should let the student verify it numerically.

---

## B. Domain examples and cases

### Example 1: The infinite-well ground state
ψ_1(x) = √(2/L) sin(πx/L). E_1 = π² ℏ²/(2 m L²).

For an electron (m = 9.11 × 10⁻³¹ kg) in a well of width L = 1 nm:
E_1 = π² · (1.055 × 10⁻³⁴ J·s)² / (2 · 9.11 × 10⁻³¹ · (10⁻⁹)² ) ≈ 6.0 × 10⁻²⁰ J ≈ 0.376 eV.
[Need to verify numerical value — recompute carefully in the chapter draft.]

This is comparable to thermal energy at room temperature (kT ≈ 0.025 eV). A particle in a 1 nm box is *quantum-energetic*; the same particle in a 1 μm box has E_1 ~ 10⁻⁶ eV, which is classically negligible. The scale of the well matters.

### Example 2: A 50/50 superposition ψ_1 + ψ_2 (sloshing)
ψ(x, 0) = (1/√2) [ψ_1(x) + ψ_2(x)]. Time evolution:

ψ(x, t) = (1/√2) [ψ_1(x) e^{−iE_1 t/ℏ} + ψ_2(x) e^{−iE_2 t/ℏ}].

|ψ(x, t)|² = (1/2)[|ψ_1|² + |ψ_2|² + 2 ψ_1 ψ_2 cos((E_2 − E_1) t/ℏ)] (using ψ_n real).

The cross term oscillates at frequency (E_2 − E_1)/ℏ = 3 π² ℏ/(2 m L²). The probability density *sloshes* between the left and right halves of the well at this frequency. The period is T = 2π ℏ · 2 m L²/(3 π² ℏ²) = 4 m L²/(3 π ℏ). For the 1 nm electron well: T ≈ [verify numerical value].

### Example 3: A localized initial state expanded in eigenstates
ψ(x, 0) = Gaussian centered at L/4, narrow. Compute c_n = ∫ ψ_n(x) ψ(x, 0) dx for n = 1, 2, ..., 20. The Gaussian's center is reflected in which c_n's are large. The student can watch how truncation at n_max = 5 vs. n_max = 20 affects the localization in the visualization. Truncation kills localization — *more eigenstates make the packet narrower*. This is the chapter's intuition payoff: a localized particle is a superposition of many energies.

### Failure case: A student writes ψ(x, t) = ψ_1(x) cos(E_1 t/ℏ)
Common error: students drop the imaginary part of the time phase. ψ_1(x) cos(...) is *not* a solution of the TDSE. The correct phase is exp(−iE_1 t/ℏ), which has both real and imaginary parts. If you take only the cosine, you have a real wave function whose time derivative is sin(E_1 t/ℏ) — and Ĥψ has no factor of i in its result, so the TDSE iℏ ∂ψ/∂t = Ĥψ is violated. The simulation must enforce complex storage and let the student verify numerically that the TDSE is satisfied.

---

## C. Connections and dependencies

- **Backward:** Chapter 1's machinery (Born rule, normalization, expectation values, ψ-vs-|ψ|²).
- **Within chapter:** Separation of variables → TISE → infinite well → orthonormality → expansion → time evolution as phase sum.
- **Forward (Chapter 3):** the harmonic oscillator. V(x) is now continuous; the analogous bound-state problem requires ladder operators. The student should leave Chapter 2 ready to see *one* algebraic alternative to the differential-equation method.
- **Forward (Chapter 4):** Dirac notation. The orthonormality ⟨ψ_m | ψ_n⟩ = δ_{mn} and completeness Σ |ψ_n⟩⟨ψ_n| = 1̂ are rewritten as the standard tools of operator algebra.
- **Forward (Chapter 8/9 — perturbation):** the eigenstate expansion is the starting point for perturbation theory.

---

## D. Current state of the field

### Historical primary sources
- **Schrödinger, E. (1926), "[Quantisierung als Eigenwertproblem](https://onlinelibrary.wiley.com/doi/10.1002/andp.19263840404)" (Quantization as an Eigenvalue Problem), *Annalen der Physik* 384, 361–376** — first paper of four. Schrödinger derived the time-independent equation, solved it for the hydrogen atom, and showed that the discrete spectrum was a *natural* consequence of requiring single-valuedness, finiteness, and continuity of ψ.
- The series ran through *Annalen der Physik* 384 and 385 in 1926. The fourth paper introduced the time-dependent form. Schrödinger received the Nobel Prize in Physics in 1933 with Dirac ([nobelprize.org](https://www.nobelprize.org/prizes/physics/1933/summary/)).
- Schrödinger's framing — quantization as the natural eigenvalue spectrum of a differential operator — is what this chapter inherits. The historical contrast with Heisenberg's matrix mechanics (published 1925) is worth a paragraph because the two formulations were proved equivalent within a year (Schrödinger 1926, Pauli 1926, Eckart 1926).

### Quantum wells in the real world
The infinite square well is a pedagogical idealization. Finite square wells are real:
- **Semiconductor quantum wells.** Layered semiconductor heterostructures (GaAs/AlGaAs) confine electrons in 1D wells of width 5–50 nm. The bound-state spectrum is measured optically. (Esaki & Tsu 1970, "Superlattice and negative differential conductivity in semiconductors," *IBM J. Res. Dev.* 14, 61–65 — foundational paper. Esaki shared the 1973 Nobel Prize.) These devices are inside every laser diode in a CD player or laser pointer.
- **Quantum dots.** 3D confinement; "artificial atoms." Used in biological imaging and in QLED displays.
- **Optical lattices.** Atoms in periodic potential created by interfering laser beams. The infinite well is the unit cell of the simplest possible lattice.

A chapter that ends with "and here is where this exactly-solvable toy model actually lives in real devices" is doing the +1 program. The simulation can include a *finite-well mode* with realistic numbers.

### Physics Education Research on quantization
- **McKagan, Perkins, & Wieman (2008), "Why we should teach the Bohr model and how to teach it effectively,"** [*Phys. Rev. Spec. Topics — PER* 4, 010103](https://journals.aps.org/prper/abstract/10.1103/PhysRevSTPER.4.010103). Argument: most students see quantization as an *ad hoc* assumption inherited from Bohr. The infinite-well derivation is the first time many of them see quantization *emerging* from a structural requirement. The chapter should explicitly contrast Bohr's postulated quantization with Schrödinger's derived quantization.
- **Singh, C. (2008), "Student understanding of quantum mechanics at the beginning of graduate instruction,"** [*Am. J. Phys.* 76, 277–287](https://aapt.scitation.org/doi/10.1119/1.2825387). Documents student difficulty with stationary states — specifically the "stationary means motionless" misconception. The simulation directly attacks this by showing the phase factor visualizable as a color (Re ψ rotating in time at each x).

---

## E. Teaching considerations

### Where students stick
- **"Stationary means the particle isn't moving."** No — the *probability density* is time-independent. The wave function itself rotates in the complex plane at angular frequency E/ℏ. The simulation must show this: the Re ψ panel should oscillate in time even when |ψ|² is static.
- **"n is the number of nodes" vs. "n is the energy level."** ψ_n has n − 1 internal nodes (not counting boundary zeros). The relationship is structural: more nodes ↔ more curvature ↔ more kinetic energy.
- **"Why isn't n = 0 allowed?"** Because ψ_0 ≡ 0 is the zero function — not a physical state, just the absence of a particle. This needs to be said clearly.
- **"Completeness" feels like magic.** That an arbitrary function can be written as a sum of sines is a *theorem* (Fourier 1822), not a postulate. The chapter should at least name this provenance so the student doesn't treat it as quantum mysticism.
- **"How do I compute c_n?"** Students see Σ c_n ψ_n and don't know how to invert. The trick is to take the inner product: ⟨ψ_m | ψ⟩ = Σ_n c_n ⟨ψ_m | ψ_n⟩ = c_m by orthonormality. The orthonormality is the *engine* of the expansion. State it explicitly.

### Voice notes
This is a technical chapter — more proofs, fewer scenes. The Feynman voice keeps it grounded by showing the *moves* visibly: "Here's the trick — we just substituted ψ = ψ(x)φ(t) and let the math sort itself out. Look what happens next." The discovery quality of separation of variables is worth celebrating. Same for quantization-from-boundary-conditions: the student should feel the "oh!" moment.

### Pacing
Long chapter (5,000+ words). Sections:
1. Cold open with the infinite well question: *why are the energies of a confined particle discrete?*
2. Separation of variables — the technique, then the application.
3. The TISE as eigenvalue problem.
4. Infinite well — full derivation, deep-dive.
5. Orthonormality, completeness, expansion.
6. Time evolution of superpositions — the "sloshing."
7. Brief: finite well, tunneling preview.
8. Hand to the simulation: now build it and verify.

---

## F. Library files relevant to this chapter

- **Griffiths, *Introduction to Quantum Mechanics* (3rd ed.), Chapter 2.** Primary source. §§2.1 (stationary states), 2.2 (infinite well), 2.6 (finite well). This is the closest match in language and pedagogical sequence to what the chapter does.
- **Griffiths Solution Manual (3rd ed.), Problems 2.1–2.10.** Detailed worked solutions for the infinite-well eigenstates, the expansion coefficient calculations, the sloshing superposition.
- **Liboff, *Introductory Quantum Mechanics* (4th ed.), Chapters 4–5.** Alternative derivation of the TISE and separation of variables; useful for cross-checking.
- **Cohen-Tannoudji, Diu & Laloë, *Quantum Mechanics*, Chapter II.** More mathematical; useful for the careful student or for the rigorous treatment of completeness.
- **Shankar, Chapter 5.** The eigenvalue problem treated abstractly; supports the Chapter 4 transition.
- **`_lib_QM-Into-the-Light-Beginners.md`** — pantry bookmap; useful for register check (how does popular language differ from technical?).
- **`_lib_Davies-Demon-in-the-Machine.md`** — pantry bookmap; Davies's "quantum measurement and information" framing could supply one analogy in the section on stationary states.
- **`_lib_Significant-Figures-Stewart.md`** — pantry bookmap; Stewart's profile of Fourier might supply a one-line historical aside ("the same Fourier series this chapter relies on is from a 1822 treatise on heat conduction") — verify Stewart covers Fourier.

## F.5 Simulation pedagogy and D3 specifics

### What the simulation must show
`02-infinite-well.html` — the infinite square well explorer.

Layout:
- **Top panel.** Energy level diagram. Horizontal green lines at E_n = n² π² ℏ²/(2 m L²) for n = 1..10 inside a "well drawing" (vertical red lines at x = 0 and x = L). Each level labeled with E_n in eV. Each level shows the corresponding ψ_n(x) drawn on top, with the zero line of the eigenfunction *at the energy of that level* (a standard textbook convention — Griffiths Fig. 2.2).
- **Middle panel.** Probability density |Ψ(x, t)|², the dynamical display. Updates in real time as the coefficients c_n and the time slider change.
- **Bottom panel.** Coefficient sliders. c_1, c_2, c_3, c_4, c_5 (real) plus phase sliders θ_n for the complex phases. Σ |c_n|² renormalized live so the wave function stays normalized.
- **Side panel.** Numerical display: ⟨x⟩(t), ⟨H⟩ = Σ |c_n|² E_n (time-independent), expansion-coefficient bar chart |c_n|², and a "draw your own ψ(x, 0)" canvas in the extension version. The "draw your own" canvas computes the c_n's by numerical projection and displays the bar chart.

The key chapter-specific feature: a *time slider* that animates the superposition. The student watches |Ψ(x, t)|² slosh, watches ⟨x⟩(t) oscillate, and watches ⟨H⟩ stay constant. The Hamiltonian expectation value is *exactly* constant — energy conservation as a numerical fact.

### D3 v7 patterns and SVG elements
- Multi-panel SVG layout. `d3.line()` for the eigenfunction curves and the dynamical |Ψ|² curve.
- For the energy level diagram: draw horizontal `<line>` elements at y = yScale(E_n). Use a parallel xScale for x ∈ [0, L]. The well boundary at x = 0 and x = L is drawn with vertical red lines. Each ψ_n curve drawn with its zero offset to its energy level (yScale(E_n) + ψ_n(x) · amplitudeScale). This is the *standard textbook visualization*.
- HTML range inputs for c_1..c_5 (range −1 to +1) and θ_1..θ_5 (range 0 to 2π).
- A `d3.bar()` (or just plain `<rect>` elements) chart for |c_n|².
- A time slider for animation.

The "draw your own" feature: use `<svg>` mouse events to capture a hand-drawn curve, sample it on the x grid, project onto each ψ_n via numerical integration. This is the *coolest* feature of the chapter simulation — the student draws a localized Gaussian-ish shape and watches it disperse over time.

### Real-time redraw approach
- For the eigenstate plots: static, drawn once on L change.
- For the dynamical |Ψ(x, t)|² plot: requestAnimationFrame loop, updates every 16 ms. At each frame, recompute Ψ(x, t) = Σ_n c_n ψ_n(x) exp(−i E_n t/ℏ) on the grid (N ≈ 200 points, n_max = 5 to 10), then |Ψ|², then update the SVG `<path>`.
- For the expansion-coefficient bar chart: updates only when sliders change or "draw your own" is invoked.
- Performance: 200 × 10 = 2000 multiply-adds per frame; trivial on any laptop.

### Parameter sliders and the surfaces they expose
- Well width L: 0.1 nm to 10 nm. Watch E_n scale as 1/L².
- Mass: electron, proton (dropdown). Watch E_n scale as 1/m.
- c_1..c_5: real coefficients, [−1, 1].
- θ_1..θ_5: phase offsets, [0, 2π]. Watch what happens when θ changes — the |Ψ|² shape shifts.
- Time slider: linear, 0 to T_period (computed automatically).
- Pause/play.

### Pedagogical research on simulations as a teaching tool (chapter-specific applications)
- **PhET *Quantum Bound States* simulation** ([phet.colorado.edu/en/simulation/legacy/bound-states](https://phet.colorado.edu/en/simulation/legacy/bound-states)). The closest existing analogue to what this chapter builds. McKagan, Perkins & Wieman documented its design and student outcomes. Findings: students who used the PhET bound-states sim with a guided activity sheet scored significantly higher on conceptual questions about energy quantization than students who only saw the textbook derivation.
- **McKagan, S. B., Perkins, K. K., Dubson, M., Malley, C., Reid, S., LeMaster, R., & Wieman, C. E. (2008), "Developing and researching PhET simulations for teaching quantum mechanics,"** [*Am. J. Phys.* 76, 406–417](https://aapt.scitation.org/doi/10.1119/1.2885199). Specifically discusses the bound-states sim. The key design lesson: *let the student draw their own potential* and see the eigenstates appear. This is the chapter's extension target and the *bookmark feature* for the +1 system.
- **Singh & Marshman 2015** PER review — calls out energy quantization as the second-most-persistent misconception (after wave-function-vs-probability-density). The simulation's energy-level diagram with horizontal lines is the direct visual response.
- **Wittmann, M. C., Steinberg, R. N., & Redish, E. F. (2002),** [*The Physics Teacher*](https://www.physport.org/recommendations/Entry.cfm?ID=92989) ASAP article on student difficulties with quantization. [verify exact citation — I recall the authors and topic but should confirm against PhysPort.]

### Four-move Claude prompt structure (chapter-specific)
- **Show:** paste ψ_n(x) = √(2/L) sin(nπx/L), E_n = n²π²ℏ²/(2mL²), the superposition formula Σ c_n ψ_n exp(−iE_n t/ℏ); paste CLAUDE.md and DESIGN.md.
- **Say:** "Produce `02-infinite-well.html`. Energy level diagram (top), |Ψ(x, t)|² animation (middle), coefficient sliders (bottom). Allow the student to set c_1..c_5 and θ_1..θ_5 and watch the time evolution. Display ⟨x⟩(t) and ⟨H⟩ live. Include a 'draw your own ψ(x, 0)' canvas in a separate tab."
- **Constrain:** "D3 v7. Complex-valued storage for Ψ. requestAnimationFrame for the time evolution. Normalization indicator. Energy levels drawn at the correct n²-scaling so the n=2 level is exactly 4× the n=1 level. ⟨H⟩ must be constant in time to numerical precision (any drift > 10⁻³ is a bug). Time period auto-scaled to the lowest beat frequency among non-zero c_n's."
- **Verify:** "Tell me four things to check: (a) ψ_n has n−1 internal nodes. (b) E_n scales as n² — for L = 1 nm electron, E_1 ≈ 0.376 eV, E_2 ≈ 1.50 eV, E_3 ≈ 3.39 eV [verify these numbers in the chapter]. (c) For c_1 = c_2 = 1/√2 with θ_1 = θ_2 = 0, the sloshing period is T = 2πℏ/(E_2 − E_1) = h/(3 E_1). (d) ⟨H⟩ = |c_1|² E_1 + |c_2|² E_2 + ... should not drift in time."

### Known failure modes when an LLM generates physics simulation code
- **The TISE solver uses wrong boundary conditions.** Claude has been observed to apply Neumann (ψ′ = 0) instead of Dirichlet (ψ = 0) at the well edges for the infinite well. Verify: the n = 1 state should look like a single positive hump that *vanishes* at x = 0 and x = L, not a flat-topped curve.
- **Energy scaling drift.** If the LLM normalizes ψ in code units rather than SI, the displayed E_n values may not show the n² scaling. Verify: read E_2 and check it is 4 × E_1.
- **Phase factor sign error.** exp(−iE_n t/ℏ) vs. exp(+iE_n t/ℏ). The sign matters when watching ⟨x⟩(t): the sloshing direction flips. The chapter should not let this go uncaught.
- **"⟨H⟩ drifts in time."** A symptom of either (a) using explicit Euler for the time evolution (the chapter's correct method is analytic exp(−iE_n t/ℏ) per eigenstate), or (b) recomputing the c_n's at every step (they should be set at t = 0 and held). The CLAUDE.md constraint must specify analytic time evolution.
- **Eigenfunction overlap = 0 for adjacent n's.** Sometimes Claude implements orthogonality by *force* (Gram-Schmidt) when it should arise naturally from sin(mπx/L) and sin(nπx/L). The latter is the *point*; the former hides the physics. Mitigation: CLAUDE.md says *use the closed-form ψ_n(x) = √(2/L) sin(nπx/L) directly; do not Gram-Schmidt.*
- **Finite well: missing the requirement that ψ′/ψ matches at the boundary.** When the chapter extends to the finite well (brief), the matching condition is the *technical* heart. Claude often forgets the continuity of ψ′ and produces unphysical solutions with kinks. Verify: ψ′ at the well boundary should be continuous.
- **"Draw your own ψ(x, 0)" doesn't show convergence as n_max grows.** A localized hand-drawn pulse should look progressively sharper as n_max increases from 5 to 20. If Claude truncates at a fixed n_max and the student sees no change, the feature is dead. Mitigation: expose n_max as a slider with range [1, 30].

---

## G. Gaps and flags

- **[verify]** Numerical value E_1 ≈ 0.376 eV for an electron in a 1 nm well. I have computed this from memory; should be re-verified in the chapter with a careful unit conversion.
- **[verify]** Schrödinger 1926 *Annalen der Physik* volume number — I have given 384 but should confirm; the 1926 volume is sometimes cited as vol. 79 or vol. 80 of the *fourth series*. The DOI link will resolve this.
- **[verify]** Esaki & Tsu 1970 *IBM J. Res. Dev.* pagination — given from memory.
- **[verify]** Wittmann, Steinberg & Redish citation — author list and topic are remembered but I haven't pulled up the paper.
- **[verify]** Cohen-Tannoudji chapter numbering — the book has been republished in multiple editions; chapter II is correct for the standard 2-volume French edition translated to English.
- **Gap:** the chapter has a brief finite-well section but doesn't go all the way to tunneling. The TIKTOC bridge says Chapter 3 introduces ladder operators. *Where does tunneling formally land?* — Possibly in a sidebar in this chapter, or in Chapter 8 (perturbation/scattering). Worth confirming with the chapter outline.
- **Gap:** I have not located a clean primary source for "the sloshing period of ψ_1 + ψ_2." This is undergraduate textbook material (Griffiths Example 2.2 / Problem 2.5 in 3rd ed.) but should be cited specifically.
- **Flag for Nik:** the simulation's "draw your own ψ(x, 0)" feature is the most compelling chapter exercise. It is also the riskiest to LLM-generate — the SVG mouse-tracking + projection + redraw is non-trivial. Consider whether this is the *base* simulation or the *extension* prompt. I have it as the extension in F.5, which seems right.
- **Flag:** the chapter should explicitly contrast the empirical Bohr quantization rule (mvr = nℏ for the hydrogen atom) with the Schrödinger derivation here. Most students arrive expecting quantization to be assumed. The "quantization emerges from boundary conditions" framing is the chapter's intellectual payoff and should be set up against the Bohr expectation. Worth one paragraph minimum.
- **Flag:** ⟨H⟩ should be *exactly* constant. If the simulation shows it drifting, that is a teachable moment about numerical precision. The chapter could turn it into an exercise: "What does the drift tell you about Claude's implementation?" — which is the +1 system's reflexive move applied to the simulation itself.
