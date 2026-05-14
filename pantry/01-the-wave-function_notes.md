# Research Notes: Chapter 01 — The Wave Function
**Source:** TIKTOC.md chapter entry (lines 110–153)
**Notes file:** 01-the-wave-function_notes.md
**Corresponding chapter:** chapters/01-the-wave-function.md (not yet written)
**Generated:** 2026-05-13

---

## Chapter summary (from TIKTOC.md)

**One-line:** Students learn what the wave function is, what it means physically, and how to extract probability information from it — building a probability density visualizer as the chapter simulation.

**Chapter description:** The first physics chapter. It does not assume the student knows what a wave function is beyond the name. It establishes the Born rule, normalization, probability density, expectation values, and the uncertainty principle — not as abstract postulates but as answers to the question the Chapter 0 wave packet raised: what is |ψ|² actually measuring? The simulation makes the probability interpretation concrete: students see probability density, compute ⟨x⟩ and ⟨p⟩ from their simulation, and watch the uncertainty principle emerge as a numerical fact before it is stated as a theorem.

**Core concepts:**
- The wave function ψ(x,t) as a complex-valued function
- The Born rule: P(x,t)dx = |ψ(x,t)|²dx
- Normalization: ∫|ψ|²dx = 1
- Expectation values: ⟨x⟩ = ∫x|ψ|²dx; ⟨p⟩ = ∫ψ*(-iℏ∂/∂x)ψ dx
- The uncertainty principle: σ_x σ_p ≥ ℏ/2
- Quantum probability vs. classical ignorance
- Stationary states and time dependence: ψ(x,t) = ψ(x)e^(-iEt/ℏ)
- The time-dependent Schrödinger equation: iℏ∂ψ/∂t = Ĥψ

**Key vocabulary:** wave function, Born rule, probability density, normalization, expectation value, standard deviation, uncertainty principle, stationary state, Schrödinger equation.

**Common misconceptions:**
- "The wave function is a physical wave like a water wave" — it is a probability amplitude.
- "The uncertainty principle is about measurement disturbance" — it is a property of wave-like objects.
- "A normalized wave function stays normalized" — it does, under Schrödinger evolution, but needs to be shown.
- "⟨x⟩ is where the particle is" — it is the average of many measurements.

**Worked examples:** Gaussian wave packet ⟨x⟩, ⟨x²⟩, σ_x; infinite-well ground state preview; minimum uncertainty σ_x σ_p = ℏ/2 for the Gaussian.

**Simulation:** `01-probability-explorer.html` — interactive probability density visualizer with gallery of wave functions; live ⟨x⟩, ⟨p⟩, σ_x, σ_p, σ_x σ_p; time slider.

**Bridge:** Chapter 2 asks what determines ψ(x) in the first place — the time-independent Schrödinger equation.

---

## A. Conceptual foundations

### 1. The wave function as a complex probability amplitude

The wave function ψ(x, t) is a *complex-valued function* of position and time. It is not a wave in the sense of water or sound. It does not transport energy. It is not directly observable. What you observe is |ψ(x, t)|², the modulus squared. This is the single most important specification the chapter has to make: ψ itself is *amplitude*, not *quantity*.

The complex-valuedness is not optional. Real wave functions can describe stationary states, but the moment time evolution is introduced — iℏ ∂ψ/∂t = Ĥψ — the imaginary unit i appears in the dynamical law. A real-only ψ cannot evolve correctly. (Griffiths *Introduction to Quantum Mechanics* 3rd ed., §1.4, makes this point explicit.) Stripping away "the wave function is a wave" requires saying *clearly* what it is instead: a complex-valued device for computing probability densities.

### 2. The Born rule

Max Born introduced the probabilistic interpretation in 1926:

**P(x, t) dx = |ψ(x, t)|² dx** — the probability of finding the particle between x and x + dx at time t.

The historical primary source is Born, M. (1926), "[Zur Quantenmechanik der Stoßvorgänge](https://link.springer.com/article/10.1007/BF01397477)," *Zeitschrift für Physik* 37, 863–867 [verify exact pagination]. Born received the 1954 Nobel Prize in Physics ([nobelprize.org](https://www.nobelprize.org/prizes/physics/1954/born/facts/)) specifically for "his fundamental research in quantum mechanics, especially for his statistical interpretation of the wavefunction." The footnote in Born's 1926 paper added in proof — where he changes ψ to |ψ|² — is one of the most consequential footnotes in physics. (Pais, A. (1982), *Subtle Is the Lord*, ch. 14; [verify chapter]; the footnote story is well documented but should be checked against Pais for the chapter.)

The Born rule is *a postulate*. It is not derived; it is the bridge between the formalism and what you measure. Saying that out loud is part of intellectual honesty. There are research programs (Zurek's envariance, [arXiv:quant-ph/0405161](https://arxiv.org/abs/quant-ph/0405161); the many-worlds branch-counting arguments — Wallace, *The Emergent Multiverse*, 2012) that try to derive the Born rule from other axioms. They are not settled. The chapter should mention this in a paragraph, not as a controversy but as an honest note about the foundations.

### 3. Normalization

If |ψ|² is a probability density, then ∫_{-∞}^{∞} |ψ(x, t)|² dx = 1 — the probability of finding the particle *somewhere* is unity. This is *normalization*. Not every solution of the Schrödinger equation is normalizable (the plane wave exp(ikx) is not, which is why the Chapter 0 wave packet was a *superposition* of plane waves). For physical states, normalizability is a constraint.

**The key result the chapter must prove:** *if* ψ is normalized at t = 0, it stays normalized under Schrödinger evolution. The proof is short and beautiful:

d/dt ∫|ψ|² dx = ∫ (∂ψ*/∂t · ψ + ψ* · ∂ψ/∂t) dx
                = ∫ ((iℏ/2m) ψ ∂²ψ*/∂x² − (iℏ/2m) ψ* ∂²ψ/∂x²) dx (using the Schrödinger equation)
                = (iℏ/2m) ∫ ∂/∂x (ψ ∂ψ*/∂x − ψ* ∂ψ/∂x) dx
                = (iℏ/2m) [ψ ∂ψ*/∂x − ψ* ∂ψ/∂x]_{-∞}^{∞}
                = 0 (because ψ → 0 at infinity for normalizable states).

This is the deep-dive candidate for the chapter — the proof that normalization is preserved is *non-trivial*, uses integration by parts, the Schrödinger equation, and the boundary condition all at once, and produces a *conservation law*. (Griffiths §1.4.)

The clever part is the rearrangement into a total derivative — the integrand becomes ∂J/∂x where J = (iℏ/2m)(ψ ∂ψ*/∂x − ψ* ∂ψ/∂x) is the *probability current*. Continuity equation: ∂|ψ|²/∂t + ∂J/∂x = 0. Probability is *locally* conserved, not just globally. This is worth a footnote.

### 4. Expectation values

For an observable Q̂, the expectation value in state ψ is ⟨Q̂⟩ = ∫ ψ* Q̂ ψ dx.

- Position: ⟨x⟩ = ∫ x |ψ|² dx. (The position operator is multiplication by x.)
- Momentum: ⟨p⟩ = ∫ ψ* (−iℏ ∂/∂x) ψ dx. (The momentum operator is −iℏ ∂/∂x in position representation.)

The momentum form is the one that confuses students. Why ∂/∂x? Because the Fourier transform of ψ(x) is φ(p/ℏ), and ⟨p⟩ in momentum space is ∫ p |φ(p)|² dp, which by Parseval and integration by parts becomes the −iℏ ∂/∂x form in position space. The derivation belongs in the deep-dive section or an appendix; the *result* is what the student uses.

The variance: σ_Q² = ⟨Q̂²⟩ − ⟨Q̂⟩². The standard deviation σ_Q = √σ_Q² is the *spread* of measurements around the mean. The uncertainty principle is a statement about these spreads.

### 5. The uncertainty principle, properly stated

σ_x σ_p ≥ ℏ/2.

Heisenberg's original 1927 paper, "[Über den anschaulichen Inhalt der quantentheoretischen Kinematik und Mechanik](http://dx.doi.org/10.1007/BF01397280)," *Zeitschrift für Physik* 43, 172–198, derived a less-tight bound using a microscope thought experiment. The σ_x σ_p ≥ ℏ/2 form is from Kennard (1927), *Z. Phys.* 44, 326–352 [verify], and Robertson (1929), *Phys. Rev.* 34, 163 [verify], extended this to the generalized uncertainty σ_A σ_B ≥ |⟨[Â, B̂]⟩|/2.

The misconception to dismantle is *measurement disturbance*. Heisenberg's microscope thought experiment encouraged this reading. The modern understanding (Robertson, Kennard, every textbook from Griffiths to Sakurai) is that σ_x σ_p ≥ ℏ/2 is a *statistical* statement about identically prepared ensembles. If you prepare 10,000 copies of the same state ψ and measure x on half of them and p on the other half, the spreads obey the inequality. No single measurement disturbs anything; the inequality is about the *shape of ψ*. A narrow ψ in x is necessarily a broad ψ̃ in p, by the Fourier transform.

The Gaussian wave packet saturates the bound: σ_x σ_p = ℏ/2 exactly. (Griffiths Problem 1.9, 3rd ed.) This is the chapter's main worked example because the simulation can verify it numerically.

---

## B. Domain examples and cases

### Example 1: The Gaussian wave packet, explicit calculation
For ψ(x) = (1/(πa²))^{1/4} exp(−x²/(2a²)):

- ⟨x⟩ = 0 (odd integrand)
- ⟨x²⟩ = a²/2
- σ_x = a/√2
- In momentum space, φ(k) = (a²/π)^{1/4} exp(−a² k²/2), so ⟨p⟩ = 0, σ_p = ℏ/(a√2).
- σ_x σ_p = (a/√2)(ℏ/(a√2)) = ℏ/2. ✓

The Gaussian is the *minimum-uncertainty state*. Every other wave function gives σ_x σ_p > ℏ/2. The simulation lets the student verify this for non-Gaussian states (a square pulse, a double Gaussian, the n=2 infinite-well state).

### Example 2: Infinite square well ground state (preview for Chapter 2)
ψ_1(x) = √(2/L) sin(πx/L) for 0 ≤ x ≤ L, zero elsewhere.

- Normalization: ∫_0^L (2/L) sin²(πx/L) dx = 1. ✓
- ⟨x⟩ = L/2 by symmetry.
- ⟨x²⟩ = L²(1/3 − 1/(2π²)) (Griffiths Example 1.4 / Problem 2.4).
- σ_x = L · √(1/12 − 1/(2π²)) ≈ 0.181 L.
- σ_p computed in the same way; the product σ_x σ_p ≈ 0.568 ℏ > ℏ/2. (Approximately 14% above the minimum.)

### Example 3: A double-peaked superposition
ψ ∝ exp(−(x−a)²/2σ²) + exp(−(x+a)²/2σ²). |ψ|² has two peaks. ⟨x⟩ = 0 by symmetry. But the particle is *never* found near x = 0 — the probability density there is small. This dismantles "⟨x⟩ is where the particle is." The average is not the location.

### Failure case: a student computes ⟨p⟩ by ∫ p |ψ|² dx
Students often try to compute ⟨p⟩ by analogy with ⟨x⟩, treating p as a number to integrate against the probability density. This gives the wrong answer (and for real ψ, gives zero trivially). The fix: p is an *operator*, not a number; ⟨p⟩ = ∫ ψ* p̂ ψ dx with p̂ = −iℏ ∂/∂x. The simulation surfaces this: it computes ⟨p⟩ by FFT (Fourier transform to momentum space, then integrate p |φ(p)|² dp). The student sees that for a real ψ, ⟨p⟩ = 0 because φ(p) is even and p is odd. The mathematics enforces what the formalism requires.

---

## C. Connections and dependencies

- **Backward dependency:** Chapter 0's wave packet. The student already has a Gaussian in front of them; this chapter explains what they were looking at.
- **Within chapter:** the Born rule comes first; normalization is its consequence; expectation values are the next-level extraction; the uncertainty principle is the structural result that ties σ_x and σ_p together.
- **Forward dependency:** Chapter 2 uses the wave-function machinery to solve eigenvalue problems (TISE). Chapter 4 generalizes ψ to abstract |ψ⟩. The Born rule generalizes to P_n = |⟨a_n | ψ⟩|² for discrete measurements.
- **Side connection:** the time-dependent Schrödinger equation iℏ ∂ψ/∂t = Ĥψ is *stated* in this chapter and *derived*-as-postulate. The connection to classical Hamiltonian mechanics (Ĥ replacing H, with [x̂, p̂] = iℏ replacing Poisson brackets) is touched on but not unpacked here — Chapter 4 owns that.

---

## D. Current state of the field

### Foundational debates that remain active
The Born rule is universally accepted as the *operational* link between formalism and measurement. The *interpretation* of why it works is not settled.

- **Copenhagen** (Bohr, Heisenberg, 1920s–30s): the wave function describes the state of knowledge or the system; collapse upon measurement is fundamental. (Howard, D. (2004), "[Who Invented the Copenhagen Interpretation?](https://www.journals.uchicago.edu/doi/10.1086/425941)," *Phil. Sci.* 71, 669–682, argues the unified "Copenhagen interpretation" is partly a post-war construction.)
- **Many-worlds** (Everett, 1957, "[Relative State Formulation of Quantum Mechanics](https://journals.aps.org/rmp/abstract/10.1103/RevModPhys.29.454)," *Rev. Mod. Phys.* 29, 454): no collapse; the wave function evolves unitarily; all measurement outcomes are realized in branches.
- **Bohmian / pilot wave** (de Broglie 1927, Bohm 1952): ψ guides actual particle trajectories. The trajectories are hidden but deterministic.
- **GRW / spontaneous collapse** (Ghirardi, Rimini, Weber 1986, [*Phys. Rev. D* 34, 470](https://journals.aps.org/prd/abstract/10.1103/PhysRevD.34.470)): collapse is a real physical process, occurring at a small rate per particle.
- **QBism** (Fuchs, Mermin, Schack): ψ encodes an agent's personal probability assignments.

The chapter does not need to resolve this. It needs to tell the student: the formalism in this book uses the standard Born rule; the *interpretation* is unsettled; the experimentally testable predictions are the same across the live interpretations. This is the right place to introduce Feynman's "shut up and calculate" — and then point out that *some* physicists have not shut up, and the foundational program is a real research field.

### Physics Education Research on student misconceptions
- **McKagan, S. B., Perkins, K. K., & Wieman, C. E. (2010), "[Design and validation of the Quantum Mechanics Conceptual Survey](https://journals.aps.org/prper/abstract/10.1103/PhysRevSTPER.6.020121)," *Phys. Rev. Spec. Topics — PER* 6, 020121.** Documents the most common misconceptions: confusing ψ with |ψ|²; treating ψ as a classical wave; conflating probability density with probability.
- **Singh, C. (2001), "[Student understanding of quantum mechanics](https://aapt.scitation.org/doi/10.1119/1.1365404)," *Am. J. Phys.* 69, 885–895.** Foundational PER paper on QM misconceptions; documents the "wave function is the particle" error and the "uncertainty is about measurement" error.
- **Singh, C., & Marshman, E. (2015),** PER review cited in Chapter 0 notes — same source, relevant here.

The chapter should cite these and use the documented misconception list as the structural skeleton for the "what ψ is not" section.

---

## E. Teaching considerations

### Where students stick
- **ψ vs. |ψ|².** Students sketch ψ when asked for the probability density, and vice versa. The simulation should display both, color-coded (Re ψ orange, Im ψ gray-dashed, |ψ|² blue filled).
- **Complex values are unfamiliar.** Most physics majors have not used complex-valued functions outside of AC circuits. The chapter should pause and remind them how |z|² = z* z works, and what the magnitude and phase of a complex number look like graphically.
- **"Probability density" is not "probability."** P(x) dx is the probability; P(x) is a density (units of 1/length). Students forget the dx. The simulation should label units explicitly.
- **The uncertainty principle "should" be saturated by a localized state.** Students think narrow ψ in x means narrow ψ in p (because both feel "localized"). The Fourier inversion is non-intuitive; the simulation must show it in real time so the student can build the inverse-relation intuition.
- **Expectation values feel like predictions.** Students treat ⟨x⟩ as "where the particle is." The chapter must repeatedly hammer: *⟨x⟩ is the average of many measurements on identically prepared states.* The double-peaked superposition example (B.3) is the antidote.

### Voice notes
The chapter has more "I" sentences than most because the Born rule earns the author's first-person engagement: "I find the historical fact that Born's interpretation appeared in a footnote-added-in-proof more telling about the foundations than any modern argument." The voice should be inviting the student into a *strange* situation rather than smoothing over the strangeness.

### Sequencing
1. Open with the simulation from Chapter 0 — show the student the wave packet again. Ask: "What did you watch?" Force the realization that they don't yet know.
2. Born rule. State and motivate.
3. Normalization. Prove it is preserved (deep-dive).
4. Expectation values. Computation patterns.
5. Uncertainty principle. State, motivate, show the Gaussian saturates it.
6. Hand back to the simulation. Now compute ⟨x⟩, ⟨p⟩, σ_x σ_p in the visualizer.

---

## F. Library files relevant to this chapter

- **Griffiths, *Introduction to Quantum Mechanics* (3rd ed., 2018), Chapter 1.** The primary source. §§1.1–1.6 cover wave function, probability, normalization, momentum, uncertainty in the exact order the chapter needs.
- **Griffiths Solution Manual (3rd ed.), Problems 1.1–1.18.** Worked solutions for the Gaussian-packet expectation values, the minimum-uncertainty proof, the boundary-condition normalization integrals.
- **Liboff, *Introductory Quantum Mechanics* (4th ed.), Chapter 3.** Alternative derivation of the momentum operator and expectation value; secondary reference.
- **Shankar, *Principles of Quantum Mechanics* (2nd ed.), Chapter 4.** More mathematically rigorous treatment; useful for the careful student or for the appendix on operator notation.
- **`_lib_Penrose-Emperors-New-Mind.md`** — pantry bookmap; Penrose's framing of the measurement problem could feed a sentence in the interpretations section (used as instrument-under-test, not authority).
- **`_lib_The-Blind-Spot.md`** — pantry bookmap; relevant for the framing of "you see the probability density, not the particle." Could supply one well-chosen sentence in the opening.
- **Pop-sci pantry files (*QM for Beginners*, etc.)** — useful for *bad examples* of the "wave function is a wave" misconception. The chapter can cite one such phrasing and contrast it with the correct formulation.
- **`_lib_Davies-Demon-in-the-Machine.md`** — pantry bookmap; tangential, but Davies has clean popular language for the statistical interpretation that could be a comparison register.

## F.5 Simulation pedagogy and D3 specifics

### What the simulation must show
`01-probability-explorer.html` — a wave function gallery + live observable computation.

Layout:
- **Left panel.** Three stacked SVG plots: Re ψ(x), Im ψ(x), |ψ(x)|². Width 700 px, each 130 px tall.
- **Right panel.** Live numerical display: ⟨x⟩, ⟨p⟩, ⟨x²⟩, ⟨p²⟩, σ_x, σ_p, σ_x σ_p (in units of ℏ/2 — so the display shows 1.0 for the Gaussian, indicating the bound is saturated). Below: a normalization indicator (∫|ψ|² dx, should read 1.000).
- **Below.** Wave function selector — a dropdown or radio set: Gaussian (with σ slider, k₀ slider), infinite-well n-th state (with n selector, L slider), double Gaussian (with separation slider), square pulse, custom (with code editor in extension version).
- **Time slider.** Optional time evolution under free-particle Hamiltonian or under user-supplied V (for the gallery options where this is meaningful).

The σ_x σ_p / (ℏ/2) display is the chapter's punch — students watch it as they change wave functions. The Gaussian reads 1.000. Anything else reads > 1.000. The uncertainty principle becomes a number on screen.

### D3 v7 patterns and SVG elements
- Three `<svg>` panels stacked. Each with its own `xScale` and `yScale`. Shared `xScale` across the three panels so the x-axis lines up visually.
- `d3.line()` for each curve. `selection.datum(data).attr("d", line)` updates on change.
- For the live observable display, plain HTML `<span>` elements with text updated via D3 `.text(...)` on each input event.
- HTML range inputs for σ, k₀, n, L, separation; HTML select for wave function family.
- Numerical integration of ⟨x⟩, ⟨x²⟩ via Simpson's rule on N = 500 grid points. For ⟨p⟩, ⟨p²⟩: compute discrete FFT (use `fft-js` from CDN, or hand-roll a Cooley-Tukey routine — fft-js is simpler).
- Display unit conventions on the axes (x in nm, ψ in nm^{-1/2}, |ψ|² in nm^{-1}). The chapter teaches the student to check units; the simulation must model good practice.

### Parameter sliders and the surfaces they expose
- Gaussian σ ∈ [0.1 nm, 5 nm]. Pull σ small, watch σ_p grow; product stays ℏ/2.
- Infinite-well n ∈ [1, 10]. Watch σ_x grow slowly with n; watch σ_p grow with n; product grows with n.
- Custom: in the extension prompt, the student types a ψ(x) expression and the simulation parses it. (Use [Math.js](https://mathjs.org/) for parsing or just `Function("x", "return " + expr)`.)
- Time slider for free evolution: watch σ_x grow while σ_p stays constant (free particle conserves momentum spread).

### Real-time redraw approach
- Single `update()` function called on any input change. Recomputes ψ on the grid, |ψ|², the FFT, the expectation values, and triggers SVG path updates.
- N = 500 grid points: a single `update()` runs in < 5 ms on a modern laptop. No need for requestAnimationFrame except when time evolution is animating. Use `setInterval` or `requestAnimationFrame` for the time slider, but `oninput` (no animation) for the parameter sliders.
- Cache the FFT plan if using fft-js; recompute only when the grid changes.

### Pedagogical research on simulations as a teaching tool (chapter-specific applications)
- **McKagan et al. 2008, "Developing and researching PhET simulations for teaching quantum mechanics,"** [*Am. J. Phys.* 76, 406–417](https://aapt.scitation.org/doi/10.1119/1.2885199). Specifically about *quantum* simulations and what works. Findings: interactive sliders with live numerical readouts (exactly the format this chapter uses) produce larger learning gains than static visualizations or single-button "run experiment" buttons.
- **Wieman, C. E., & Perkins, K. K. (2005), "Transforming physics education,"** [*Physics Today* 58 (11), 36–41](https://physicstoday.scitation.org/doi/10.1063/1.2155756). The pedagogical argument for interactive engagement.
- **Hake 1998** (cited in Chapter 0 notes) — the 2σ effect size for interactive engagement vs. traditional lecture.
- **Singh & Marshman 2015** PER review for upper-division QM — specifically calls out the wave-function-vs-probability-density confusion as the most persistent misconception. The simulation's color-coded display directly addresses this.

### Four-move Claude prompt structure (chapter-specific)
- **Show:** paste the Born rule and expectation-value formulas; paste CLAUDE.md and DESIGN.md; paste the wave function gallery options (Gaussian, infinite-well, double-Gaussian, square pulse).
- **Say:** "Produce `01-probability-explorer.html` — three stacked SVG panels (Re ψ, Im ψ, |ψ|²), a live numerical panel showing ⟨x⟩, ⟨p⟩, σ_x, σ_p, σ_x σ_p / (ℏ/2), and a wave function selector with appropriate sliders for each family."
- **Constrain:** "D3 v7. Numerical integration via Simpson's rule on N = 500 points. Discrete FFT for momentum-space observables (use fft-js from CDN). Normalization indicator at top. The σ_x σ_p / (ℏ/2) display must read 1.000 for a Gaussian."
- **Verify:** "Tell me three predicted values: (a) for a Gaussian with σ = 1 nm, σ_x = 1/√2 nm = 0.707 nm and σ_p = ℏ/(√2 nm) [compute the number]. (b) for the n = 1 infinite-well state in L = 10 nm, ⟨x⟩ = 5 nm and σ_x = L · √(1/12 − 1/(2π²)) [compute the number]. (c) σ_x σ_p / (ℏ/2) must be ≥ 1 for any choice. Print all three in the UI so I can read them against the live values."

### Known failure modes when an LLM generates physics simulation code
- **Confusing ψ and |ψ|² in the rendered curve.** The most common failure: Claude plots |ψ|² where Re ψ should go, or plots ψ² (treating ψ as real). The verify step *must* require Re ψ to oscillate (positive and negative values visible) for a wave packet with k₀ ≠ 0.
- **Phase information lost in the imaginary part.** If Claude implements ψ as a real-valued function and adds an "imaginary part = 0" placeholder, the chapter's point collapses. The CLAUDE.md constraint must explicitly require complex storage (use `{re: number, im: number}` objects or two parallel arrays).
- **Wrong sign in the momentum operator.** p̂ = −iℏ ∂/∂x. The minus sign is easy for Claude to drop, which gives ⟨p⟩ = −⟨p⟩_true. Verify with the Gaussian wave packet at k₀ > 0: ⟨p⟩ should be positive.
- **Simpson's rule applied to a function with sign changes.** If the grid is too coarse near the zeros of ψ, ⟨x⟩ computations can drift. Mitigation: use a fine grid (N ≥ 500) and let the student watch the normalization indicator stay at 1.000.
- **FFT normalization conventions.** Claude has multiple conventions to choose from (NumPy, MATLAB, asymmetric, symmetric). The momentum-space σ_p depends on getting the convention right. Worth a one-paragraph caveat in CLAUDE.md.
- **"Probability" displayed without units.** Claude reports |ψ|² as a unitless number. The simulation must label units (nm^{-1} in 1D) to model good practice. Mitigation: CLAUDE.md says *every numerical display must include units.*
- **Numerical drift under time evolution.** If the LLM uses an explicit Euler step for the time-dependent Schrödinger equation, normalization drifts and the simulation lies. For Chapter 1 we mostly use analytic time evolution (Gaussian free-particle); when time evolution is needed, the chapter should constrain the LLM to use either analytic evolution or a *unitary* scheme (Crank-Nicolson) — not explicit Euler.
- **The σ_x σ_p / (ℏ/2) display reads exactly 0.5 (or 0.499...).** This means Claude divided by the wrong thing — ratio against ℏ instead of ℏ/2. The chapter's verify step catches this immediately.

---

## G. Gaps and flags

- **[verify]** Born 1926 *Zeitschrift für Physik* citation: vol. 37, 863–867 *or* the second 1926 paper at vol. 38, 803–827. There are two relevant 1926 Born papers; the footnote-added-in-proof is in the first. The chapter should cite both correctly. Nik should confirm.
- **[verify]** Kennard 1927 and Robertson 1929 page numbers above were given from memory; confirm against Reviews of Modern Physics or original journal volumes.
- **[verify]** Pais, *Subtle Is the Lord*, chapter number for the Born footnote anecdote.
- **[verify]** The exact phrasing of the Singh 2001 paper's title and pagination — I have given *Am. J. Phys.* 69, 885–895; this is from memory.
- **Gap:** the chapter does not yet have a clean treatment of *why* the probability current J appears. The deep-dive proof of normalization conservation produces it as a byproduct; the chapter should either own that or push it to Chapter 2. Recommend owning it here — the continuity equation is a beautiful side product of the chapter's main calculation.
- **Gap:** the interpretations paragraph (Copenhagen / MW / Bohm / GRW / QBism) is one of the trickiest in the book. I have framed it as "live research, settled operationally." Nik should decide whether to keep it brief or push to a sidebar.
- **Flag for Nik:** the simulation's reliance on a discrete FFT means the student will see momentum-space artifacts at the edges of the grid. Worth a short footnote in the chapter on *grid artifacts as a feature, not a bug* — they are the discrete analogue of the limit-related complications in continuous QM and a teachable moment.
- **Flag:** the chapter is foundational; its tone has to set the book's voice. The opening should not start with "the wave function is..." It should start with the Chapter 0 wave packet and a question: *what were you actually looking at?* This is the genuine puzzle Feynman's first move requires.
