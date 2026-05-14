# TIKTOC.md — Quantum Mechanics+1
## A Simulation-First Undergraduate Textbook

**Working title:** Quantum Mechanics+1: Interactive Simulations with Claude and D3
**Series:** +1 Series — AI-Augmented Undergraduate STEM
**Author:** Nik Bear Brown · ni.brown@neu.edu · Bear Brown & Company
**Repo:** quantum-mechanics-with-llms
**Version:** 1.0
**Status:** TIKTOC complete — ready for research gathering and chapter drafting

---

## Book Concept

This book teaches the standard undergraduate quantum mechanics curriculum — wave functions, operators, the hydrogen atom, perturbation theory — to physics majors who have completed one semester of QM, by pairing each conceptual chapter with LLM-generated D3.js simulations that let students see, manipulate, and explore the physics directly. It fills the gap left by Griffiths (rigorous but static) and YouTube (visual but non-rigorous) by giving students a third option: a simulation they built themselves, governed by physics they understand, that they can modify at 11pm without asking anyone.

**The +1 is the simulation layer.** Every chapter ends with copy-paste-ready Claude prompts that produce interactive D3 visualizations students can modify by changing parameters, boundary conditions, or physical constants and watching what happens. The simulations are not decoration — they are the primary tool for building physical intuition.

**Central thesis:** Quantum mechanics is not hard because the math is hard. It is hard because the objects have no classical analogues and students have no way to develop intuition for them. Interactive simulation closes that gap. An undergraduate who has watched a wave packet spread, tuned a potential well, and seen a probability density collapse has physical intuition that no amount of lecture can supply.

---

## Book Type and Deployment

**Primary type:** Course textbook — adopted for a semester, chapter = week, read in sequence.

**Target course:** Second undergraduate course in quantum mechanics (after modern physics or intro QM). Junior or senior year physics major. Can also serve as a simulation-enriched first course for strong students.

**Semester format:** 15 weeks. Chapter 0 is assigned Week 1 alongside Chapter 1. Chapters 1–13 map to Weeks 1–13. Weeks 14–15 are review, project, and exam.

**Prerequisites assumed:** Calculus through differential equations, introductory physics (waves, electromagnetism), one semester of modern physics or intro QM (photoelectric effect, Bohr model, de Broglie). Linear algebra helpful but not required — introduced as needed.

**What this book is not:** A first exposure to calculus or classical mechanics. A graduate quantum mechanics text. A pure computation course. A physics-free simulation course.

---

## The +1 System: How Simulations Work in This Book

Each chapter ends with an **LLM Exercise** block containing:

1. **The CLAUDE.md prompt** — establishes the coding constitution for QM simulations (D3 v7, SVG canvas, parameter sliders, real-time redraw)
2. **The simulation prompt** — a copy-paste-ready four-move prompt that produces a working D3 simulation for that chapter's core concept
3. **Exploration tasks** — specific parameter changes students make and questions they answer by watching the simulation
4. **Extension prompt** — a follow-up prompt that adds one feature or connects to the next chapter

The Brutalist system governs all simulation code: `CLAUDE.md` (coding constitution), `DESIGN.md` (visual constitution), `PROJECT.md` (project state). These are generated in Chapter 0 and travel with the student through the entire book.

---

## Three-Act Learning Arc

**ACT ONE — The Quantum World (Chapters 1–4)**
*From "I passed modern physics" to "I understand what a wave function is and how it evolves."*
The foundational layer. Wave functions, the Schrödinger equation, probability, and the infinite square well. The student builds their first simulations and develops physical intuition for quantum states before encountering the full operator formalism.

**ACT TWO — The Formalism and Standard Systems (Chapters 5–10)**
*From "I can solve the particle in a box" to "I can solve any central-force problem."*
The technical core. Dirac notation, operators, the harmonic oscillator, angular momentum, spin, and the hydrogen atom. Each chapter's simulation makes an abstract mathematical structure physically visible.

**ACT THREE — Methods and Modern Connections (Chapters 11–13)**
*From "I can solve textbook problems" to "I can attack real physics."*
Perturbation theory, identical particles, and a capstone chapter connecting QM to the research problems students will encounter — quantum information, decoherence, topological systems. Each simulation connects the formalism to something a researcher actually cares about.

---

## Chapter List

---

### CHAPTER 00 — How to Use the Simulations
**Filename:** `00-how-to-use-the-simulations.md`
**Arc position:** Pre-chapter / setup

**One-line:** Students build the three Brutalist governing files and produce their first QM simulation — a free particle wave packet — before reading any physics content.

**Chapter description:**
This chapter has one job: get the student from zero to a working, modifiable D3 quantum mechanics simulation before they encounter any new physics. It introduces Claude, the Brutalist system, and the four-move prompt structure through the lens of a free particle wave packet — the simplest quantum object that shows something interesting. By the end, the student has `CLAUDE.md`, `DESIGN.md`, and `PROJECT.md` in their working directory, a working simulation they can modify, and a mental model of how the LLM exercises in every subsequent chapter will work.

**Core concepts:**
- The Brutalist system: CLAUDE.md (coding constitution), DESIGN.md (visual constitution), PROJECT.md (project state)
- The four-move prompt structure: Show / Say / Constrain / Verify
- D3 v7 for physics simulation: SVG canvas, parameter sliders, requestAnimationFrame, real-time redraw
- The free particle wave packet as first simulation object: Gaussian envelope, plane wave carrier, group vs. phase velocity
- The verification stack: format check, physics check (does the wave packet spread?), browser test
- The instruction budget: why CLAUDE.md and DESIGN.md are separate files

**Key vocabulary:** wave packet, group velocity, phase velocity, Gaussian envelope, D3, SVG, CLAUDE.md, DESIGN.md, PROJECT.md, four-move prompt, verification stack

**What the student builds:**
- `CLAUDE.md` — QM simulation coding constitution (D3 v7, SVG canvas, parameter sliders, normalization display, real-time physics)
- `DESIGN.md` — visual constitution (probability density in blue, wave function real part in orange, imaginary part in gray, dark-mode support)
- `PROJECT.md` — project state file (tracks simulations built, current chapter)
- `00-wave-packet.html` — free particle Gaussian wave packet with sliders for k₀ (central wavenumber), σ (initial width), and time evolution speed; shows spreading in real time

**Simulation physics:**
Free particle Gaussian wave packet: ψ(x,0) = A exp(ik₀x) exp(-x²/4σ²). Time evolution via dispersion relation ω(k) = ℏk²/2m. Show |ψ(x,t)|² spreading. Sliders: initial width σ, central momentum k₀, time step. Display: real part, imaginary part, probability density on three stacked SVG panels.

**LLM Exercise structure:**
Part 1: Generate CLAUDE.md (prompt provided)
Part 2: Generate DESIGN.md (prompt provided)
Part 3: Generate PROJECT.md (prompt provided)
Part 4: Build the wave packet simulation (four-move prompt provided)
Part 5: Exploration tasks — change σ, change k₀, observe spreading rate
Part 6: Extension — add momentum-space representation |φ(k)|²

**Connection to Chapter 1:** The wave packet spreading is the physical motivation for Chapter 1's question: what does the wave function mean?

---

### CHAPTER 01 — The Wave Function
**Filename:** `01-the-wave-function.md`
**Arc position:** Act One, Chapter 1

**One-line:** Students learn what the wave function is, what it means physically, and how to extract probability information from it — building a probability density visualizer as the chapter simulation.

**Chapter description:**
The first physics chapter. It does not assume the student knows what a wave function is beyond the name. It establishes the Born rule, normalization, probability density, expectation values, and the uncertainty principle — not as abstract postulates but as answers to the question the Chapter 0 wave packet raised: what is |ψ|² actually measuring? The simulation makes the probability interpretation concrete: students see probability density, compute ⟨x⟩ and ⟨p⟩ from their simulation, and watch the uncertainty principle emerge as a numerical fact before it is stated as a theorem.

**Core concepts:**
- The wave function ψ(x,t) as a complex-valued function; what it is and is not
- The Born rule: P(x,t)dx = |ψ(x,t)|²dx — probability of finding the particle between x and x+dx
- Normalization: ∫|ψ|²dx = 1 — the total probability must be 1; normalization as a physical requirement
- Expectation values: ⟨x⟩ = ∫x|ψ|²dx; ⟨p⟩ = ∫ψ*(-iℏ∂/∂x)ψ dx — average results of many measurements
- The uncertainty principle: σxσp ≥ ℏ/2 — where it comes from, what it means physically
- Quantum probability vs. classical ignorance: the deep conceptual distinction
- Stationary states and time dependence: ψ(x,t) = ψ(x)e^(-iEt/ℏ)
- The time-dependent Schrödinger equation: iℏ∂ψ/∂t = Ĥψ

**Key vocabulary:** wave function, Born rule, probability density, normalization, expectation value, standard deviation, uncertainty principle, stationary state, Schrödinger equation

**Common misconceptions to address:**
- "The wave function is a physical wave like a water wave" — it is a probability amplitude, not a physical disturbance
- "The uncertainty principle is about measurement disturbance" — it is a property of wave-like objects, not an engineering limitation
- "A normalized wave function stays normalized" — it does, under Schrödinger evolution, but this needs to be shown
- "⟨x⟩ is where the particle is" — it is the average of many measurements, not a prediction for a single measurement

**Worked examples:**
1. Gaussian wave packet: compute ⟨x⟩, ⟨x²⟩, σx explicitly
2. Infinite square well ground state (preview): ψ₁(x) = √(2/L)sin(πx/L) — compute ⟨x⟩, check normalization
3. Uncertainty product for the Gaussian: σxσp = ℏ/2 (minimum uncertainty state)

**What the student builds:**
`01-probability-explorer.html` — interactive probability density visualizer. Input: choose from a gallery of wave functions (Gaussian, sinusoidal, step-function superposition). Display: |ψ(x)|², real and imaginary parts of ψ(x). Computed quantities shown live: ⟨x⟩, ⟨p⟩, σx, σp, σxσp. Slider: time evolution. Students can verify the uncertainty principle numerically for any wave function in the gallery.

**Simulation physics:** For a given ψ(x), compute |ψ(x)|² numerically on a grid. Compute ⟨x⟩ = Σ xᵢ|ψ(xᵢ)|²Δx and ⟨x²⟩ similarly. Compute σx = √(⟨x²⟩ - ⟨x⟩²). For ⟨p⟩ and σp, use Fourier transform to momentum space. Display all quantities live as student adjusts sliders.

**Key references for research agent:**
- Griffiths, *Introduction to Quantum Mechanics*, Chapter 1
- Shankar, *Principles of Quantum Mechanics*, Chapter 4
- Research on student misconceptions about the wave function and Born rule
- History of Born's probability interpretation (1926) and its reception

**Bridge to Chapter 2:** The Schrödinger equation determines how ψ evolves in time. But what determines ψ in the first place? The answer is the time-independent Schrödinger equation — which requires a potential V(x).

---

### CHAPTER 02 — The Time-Independent Schrödinger Equation
**Filename:** `02-time-independent-schrodinger.md`
**Arc position:** Act One, Chapter 2

**One-line:** Students learn to solve the time-independent Schrödinger equation for simple potentials, building an infinite square well visualizer that shows all energy eigenstates and their superpositions.

**Chapter description:**
The central technical chapter of Act One. Separation of variables converts the time-dependent Schrödinger equation into the time-independent version Ĥψ = Eψ — an eigenvalue problem. The infinite square well is solved exactly, giving discrete energy levels and standing wave solutions. The student sees quantization emerge naturally from boundary conditions, not from an ad hoc assumption. Superposition of stationary states produces time-dependent behavior. The simulation makes all of this visible: every eigenstate, their energies, and the time evolution of arbitrary superpositions.

**Core concepts:**
- Separation of variables: ψ(x,t) = ψ(x)φ(t); φ(t) = e^(-iEt/ℏ)
- The time-independent Schrödinger equation: (-ℏ²/2m)d²ψ/dx² + V(x)ψ = Eψ
- Stationary states: |ψ(x,t)|² is time-independent for energy eigenstates
- The infinite square well: V=0 for 0<x<L, V=∞ elsewhere
  - Boundary conditions: ψ(0) = ψ(L) = 0
  - Solutions: ψₙ(x) = √(2/L)sin(nπx/L)
  - Energy levels: Eₙ = n²π²ℏ²/2mL² — quantization from boundary conditions
- Superposition of stationary states: Ψ(x,t) = Σ cₙψₙ(x)e^(-iEₙt/ℏ)
- Orthonormality of eigenstates: ⟨ψₘ|ψₙ⟩ = δₘₙ
- Completeness: any normalizable function can be expanded in the energy eigenbasis
- The finite square well (brief): bound states, tunneling preview

**Key vocabulary:** stationary state, eigenstate, eigenvalue, energy quantization, boundary conditions, orthonormality, completeness, superposition, infinite square well

**Common misconceptions:**
- "Quantization is assumed, not derived" — it emerges from boundary conditions in the square well
- "The particle is standing still in a stationary state" — the probability density is static but the wave function is oscillating in time (the phase e^(-iEt/ℏ))
- "Higher energy means the particle is in a larger region" — the wave function has more nodes, not more space

**Worked examples:**
1. Complete solution of the infinite square well: boundary conditions → sinusoidal solutions → energy quantization
2. Computing expansion coefficients cₙ for an arbitrary initial state ψ(x,0)
3. Time evolution of a superposition of n=1 and n=2 states: the "sloshing" motion

**What the student builds:**
`02-infinite-well.html` — infinite square well explorer. Sliders: well width L, particle mass m, initial state (choose energy levels and their coefficients). Display: energy level diagram, wave functions ψₙ(x) for each level, probability density |Ψ(x,t)|², time evolution animation. Shows how adding more energy levels to a superposition makes the wave packet more localized.

**Simulation physics:** Compute ψₙ(x) = √(2/L)sin(nπx/L) for n = 1..10 on a grid. Allow student to set coefficients c₁..c₅. Compute Ψ(x,t) = Σcₙψₙ(x)e^(-iEₙt/ℏ) at each time step. Display |Ψ|² animated. Show energy level diagram with horizontal lines at Eₙ ∝ n².

**Key references for research agent:**
- Griffiths, Chapter 2
- Cohen-Tannoudji, *Quantum Mechanics*, Chapter II
- Research on the conceptual difficulty of energy quantization — why students think it is an assumption
- Historical development: Schrödinger's 1926 paper

**Bridge to Chapter 3:** The infinite square well is exactly solvable because the potential is piecewise constant. What about continuous potentials — specifically the harmonic oscillator? That requires a new technique: ladder operators.

---

### CHAPTER 03 — The Harmonic Oscillator
**Filename:** `03-harmonic-oscillator.md`
**Arc position:** Act One, Chapter 3

**One-line:** Students solve the quantum harmonic oscillator using ladder operators — the algebraic method — and build a simulation showing the energy eigenstates, coherent states, and their time evolution.

**Chapter description:**
The harmonic oscillator is the most important exactly solvable system in quantum mechanics. It appears everywhere — molecular vibrations, photons in a cavity, phonons, quantum field theory. This chapter teaches two approaches: the power series (analytic) method and the ladder operator (algebraic) method. The algebraic method is emphasized because it introduces the notation and thinking that carries forward to angular momentum and quantum field theory. Coherent states — the quantum states that most resemble classical oscillation — are introduced as the physically interesting superpositions. The simulation shows Gaussian wave packets sloshing back and forth without spreading (coherent states) versus spreading (other superpositions).

**Core concepts:**
- The harmonic oscillator Hamiltonian: Ĥ = p̂²/2m + mω²x̂²/2
- The algebraic method: ladder operators â± = (1/√(2mℏω))(∓ip̂ + mωx̂)
  - [â₋, â₊] = 1
  - Ĥ = ℏω(â₊â₋ + 1/2)
  - â₊|n⟩ = √(n+1)|n+1⟩; â₋|n⟩ = √n|n-1⟩
- Energy levels: Eₙ = (n + 1/2)ℏω — zero-point energy is real and physical
- Wave functions: Hermite polynomials times Gaussian
- The analytic method (brief): Hermite polynomials as confirmation
- Coherent states: eigenstates of â₋; minimum-uncertainty states; classical behavior
- The quantum-classical correspondence: large-n eigenstates peak at classical turning points

**Key vocabulary:** harmonic oscillator, ladder operators, raising operator, lowering operator, ground state, zero-point energy, Hermite polynomials, coherent state, quantum-classical correspondence

**Common misconceptions:**
- "Zero-point energy is a mathematical artifact" — it has measurable consequences (Casimir effect, liquid helium never freezes at atmospheric pressure)
- "Coherent states are just classical states" — they are quantum states with classical-like behavior, still subject to the uncertainty principle
- "The ladder operators are tricks" — they are the foundation of quantum field theory

**Worked examples:**
1. Deriving the energy spectrum from [â₋, â₊] = 1 alone — no differential equations
2. Computing ⟨x⟩ and ⟨x²⟩ for the nth eigenstate using ladder operators
3. The coherent state as a displaced Gaussian that oscillates without spreading

**What the student builds:**
`03-harmonic-oscillator.html` — harmonic oscillator explorer. Sliders: ω (frequency), initial state selector (eigenstate n, or coherent state with amplitude α, or custom superposition). Display: potential V(x) = mω²x²/2 as background, wave function ψ(x,t), probability density |ψ(x,t)|², energy level lines, classical turning points. Time evolution animation. Shows coherent state sloshing vs. eigenstate static probability density.

**Simulation physics:** Compute ψₙ(x) using Hermite polynomials Hₙ and Gaussian: ψₙ(x) = (mω/πℏ)^(1/4) / √(2ⁿn!) Hₙ(√(mω/ℏ)x) exp(-mωx²/2ℏ). For coherent state: α-displaced Gaussian, oscillating at frequency ω without spreading. Animate using e^(-iEₙt/ℏ) phases.

**Key references for research agent:**
- Griffiths, Chapter 2 (sections 2.3–2.4)
- Shankar, Chapter 7
- History and significance of coherent states (Glauber, 1963 Nobel Prize 2005)
- The role of the harmonic oscillator in quantum field theory
- Zero-point energy: Casimir effect experimental measurements

**Bridge to Chapter 4:** The harmonic oscillator and the square well are both one-dimensional, time-independent problems. Chapter 4 introduces the full mathematical framework — Dirac notation and the operator formalism — that makes all QM calculations systematic.

---

### CHAPTER 04 — Formalism: Dirac Notation and Operators
**Filename:** `04-formalism-dirac-notation.md`
**Arc position:** Act One → Act Two transition, Chapter 4

**One-line:** Students learn Dirac notation, Hermitian operators, and the spectral theorem — the abstract language that makes all of quantum mechanics a unified system — and build a two-level system simulator (a qubit).

**Chapter description:**
The formalism chapter. Everything done concretely in Chapters 1–3 is now placed in a general framework. Hilbert space, inner products, Hermitian operators, eigenvalues, eigenvectors, the spectral decomposition. The chapter introduces Dirac bra-ket notation as a language, not a new physics — it is a cleaner way to write everything already learned. The two-level system (qubit) is the pedagogical anchor: small enough to compute everything explicitly, rich enough to illustrate every abstract concept. The simulation is a Bloch sphere visualizer — the geometric representation of all qubit states.

**Core concepts:**
- Hilbert space: complete inner product space; state vectors |ψ⟩; dual vectors ⟨ψ|
- Dirac notation: bra-ket; inner product ⟨φ|ψ⟩; outer product |ψ⟩⟨φ|
- Hermitian operators: Â† = Â; real eigenvalues; orthogonal eigenstates
- The spectral theorem: Â = Σ aₙ|aₙ⟩⟨aₙ|
- Commutators [Â,B̂] = ÂB̂ - B̂Â; compatible observables; simultaneous eigenstates
- The generalized uncertainty principle: σAσB ≥ |⟨[Â,B̂]⟩|/2
- The two-level system: |0⟩, |1⟩ basis; Pauli matrices σx, σy, σz
- The Bloch sphere: geometric representation of all qubit states
- Time evolution operator: Û(t) = e^(-iĤt/ℏ); unitary evolution

**Key vocabulary:** Hilbert space, ket, bra, inner product, Hermitian operator, eigenvalue, eigenvector, spectral decomposition, commutator, uncertainty principle, Pauli matrices, Bloch sphere, unitary operator

**Common misconceptions:**
- "Dirac notation is new physics" — it is notation for the same mathematics already encountered
- "All observables commute with each other" — only compatible observables do; [x̂,p̂] = iℏ is the canonical non-commuting pair
- "The uncertainty principle is about simultaneous measurement" — it is about the statistical spread of outcomes in identically prepared states

**Worked examples:**
1. Two-level system: computing expectation values of σx, σy, σz for an arbitrary state |ψ⟩ = α|0⟩ + β|1⟩
2. The commutator [x̂,p̂] = iℏ derived from position and momentum operators in position representation
3. Time evolution of a two-level system under Ĥ = (ℏω/2)σz — Larmor precession on the Bloch sphere

**What the student builds:**
`04-bloch-sphere.html` — Bloch sphere visualizer for qubit states. Input: θ and φ (spherical coordinates on the Bloch sphere), or α and β (complex amplitudes). Display: 3D Bloch sphere rendered in D3/SVG with projection; state vector as arrow; ⟨σx⟩, ⟨σy⟩, ⟨σz⟩ shown numerically; time evolution under a chosen Hamiltonian animates precession. Sliders: Hamiltonian parameters, time.

**Simulation physics:** Bloch vector: r = (⟨σx⟩, ⟨σy⟩, ⟨σz⟩) = (sin θ cos φ, sin θ sin φ, cos θ). Time evolution under Ĥ = (ℏω/2)(Bx σx + By σy + Bz σz): precession around the B-field axis at frequency ω. Project 3D sphere onto 2D SVG using isometric or perspective projection.

**Key references for research agent:**
- Griffiths, Chapter 3
- Shankar, Chapters 1–2
- Sakurai & Napolitano, *Modern Quantum Mechanics*, Chapter 1
- Bloch sphere: history, application in NMR and quantum computing
- Research on student difficulties with the abstract formalism layer

**Bridge to Chapter 5:** The formalism of Chapter 4 applies to any quantum system. Chapter 5 applies it to the quantum mechanics of a particle in three dimensions — specifically the central force problem, which requires angular momentum operators.

---

### CHAPTER 05 — Quantum Mechanics in Three Dimensions
**Filename:** `05-three-dimensions.md`
**Arc position:** Act Two, Chapter 5

**One-line:** Students extend quantum mechanics to three dimensions, solve the central force problem using separation of variables, and build a 3D probability density visualizer for the first few hydrogen-like orbitals.

**Chapter description:**
Three-dimensional quantum mechanics introduces spherical coordinates, the separation of the Schrödinger equation for central potentials into radial and angular parts, and the spherical harmonics as the universal solutions to the angular equation. This chapter is a prerequisite for the hydrogen atom (Chapter 7) but focuses on the mathematics of 3D: separation of variables, the angular equation, spherical harmonics Yₗᵐ(θ,φ), and the radial equation for a general central potential. The simulation visualizes the angular probability distributions |Yₗᵐ|² as 3D surface plots projected onto 2D — giving students their first visual sense of orbital shapes.

**Core concepts:**
- The 3D Schrödinger equation in Cartesian and spherical coordinates
- Separation of variables for central potentials V(r): ψ(r,θ,φ) = R(r)Y(θ,φ)
- The angular equation: Ĺ²Y = ℏ²l(l+1)Y; separation into θ and φ parts
- Spherical harmonics Yₗᵐ(θ,φ): the universal angular eigenfunctions
  - Quantum numbers l (orbital angular momentum) and m (magnetic quantum number)
  - l = 0,1,2,... and m = -l,-l+1,...,l
  - Orthonormality and completeness
- The radial equation: depends on V(r); effective potential with centrifugal barrier
- Angular momentum operator L̂: L̂x, L̂y, L̂z; [L̂x, L̂y] = iℏL̂z and cyclic
- L̂² and L̂z as compatible observables: simultaneous eigenstates

**Key vocabulary:** spherical coordinates, central potential, separation of variables, spherical harmonics, orbital angular momentum, quantum numbers l and m, effective potential, centrifugal barrier

**Common misconceptions:**
- "The orbital shapes are the wave function" — they are |Yₗᵐ|², the angular probability density; the full orbital includes the radial part
- "Higher l means higher energy" — energy depends on the specific potential V(r); for hydrogen, energy depends only on n

**Worked examples:**
1. Y₀⁰, Y₁⁰, Y₁±¹ written out explicitly; their node structures
2. The centrifugal barrier in the effective potential: why l>0 states have zero probability at r=0
3. Computing ⟨L̂z⟩ and ⟨L̂²⟩ for a given angular state

**What the student builds:**
`05-spherical-harmonics.html` — spherical harmonic visualizer. Controls: l selector (0–4), m selector (-l to l). Display: 2D polar plot of |Yₗᵐ(θ,φ)|² as a function of θ at fixed φ=0, plus a projected 3D-like surface using D3 radial plots. Color encodes the sign of the real part of Yₗᵐ. Shows nodal planes and nodal cones.

**Simulation physics:** Compute Yₗᵐ(θ,φ) using associated Legendre polynomials Pₗᵐ(cos θ). Render |Yₗᵐ(θ,φ)|² as radial distance from origin in polar coordinates for a sweep of θ at φ=0. Use D3 line generators for the polar plot.

**Key references for research agent:**
- Griffiths, Chapter 4 (sections 4.1–4.3)
- Arfken & Weber, *Mathematical Methods for Physicists* — spherical harmonics chapter
- Visualizations of atomic orbitals in chemistry education literature
- Historical development of spherical harmonics (Laplace, Legendre)

**Bridge to Chapter 6:** Chapter 5 solved the angular equation universally. Chapter 6 solves it for spin — an angular momentum with no classical analogue, requiring half-integer quantum numbers.

---

### CHAPTER 06 — Spin
**Filename:** `06-spin.md`
**Arc position:** Act Two, Chapter 6

**One-line:** Students learn that spin is an intrinsically quantum mechanical angular momentum, solve the spin-1/2 system completely using Pauli matrices, and build a Stern-Gerlach simulation showing spin measurement outcomes.

**Chapter description:**
Spin is the most distinctively quantum mechanical concept in the standard curriculum. It has no classical analogue, it cannot be visualized as rotation, and yet it is essential for understanding atoms, magnetic resonance, and quantum computing. This chapter treats spin-1/2 completely: the two-state Hilbert space, Pauli matrices, spin operators, measurement probabilities, and the addition of spin to orbital angular momentum. The Stern-Gerlach experiment is the historical anchor — students see spin quantization as a direct experimental result before the formalism. The simulation recreates the Stern-Gerlach experiment interactively.

**Core concepts:**
- Experimental motivation: the Stern-Gerlach experiment (1922) — discrete deflection, not continuous
- Spin-1/2: two-dimensional Hilbert space; basis states |↑⟩ = |+⟩ and |↓⟩ = |-⟩
- Spin operators: Ŝ = (ℏ/2)σ where σ = (σx, σy, σz) are Pauli matrices
  - σx = [[0,1],[1,0]]; σy = [[0,-i],[i,0]]; σz = [[1,0],[0,-1]]
  - Eigenvalues ±ℏ/2 for each component
- General spin state: |ψ⟩ = α|↑⟩ + β|↓⟩ with |α|² + |β|² = 1
- Measurement probabilities: P(↑) = |α|², P(↓) = |β|²
- Sequential Stern-Gerlach: measuring Sz then Sx destroys Sz information
- The Bloch sphere for spin (connecting to Chapter 4)
- Spin-orbit coupling preview: J = L + S
- Addition of angular momenta: Clebsch-Gordan coefficients (brief)

**Key vocabulary:** spin, Pauli matrices, spinor, Stern-Gerlach experiment, spin-1/2, spin-orbit coupling, Clebsch-Gordan coefficients, singlet, triplet

**Common misconceptions:**
- "Spin is the particle rotating on its axis" — this is impossible for a point particle; spin is intrinsic angular momentum with no classical analogue
- "Measuring spin in one direction destroys information about other directions because of the measurement device" — it is a fundamental quantum property, not a measurement limitation

**Worked examples:**
1. Stern-Gerlach analysis: beam prepared in Sx eigenstate, measured along Sz — computing probabilities
2. Sequential measurements: prepare |↑z⟩, measure Sx (get |↑x⟩), measure Sz again — probabilities of outcomes
3. Spin precession in a magnetic field: Larmor precession via time-dependent Schrödinger equation for spin

**What the student builds:**
`06-stern-gerlach.html` — Stern-Gerlach simulator. Controls: initial spin state (θ, φ on Bloch sphere), measurement axis direction (azimuthal angle). Display: animated beam entering the magnet, splitting into two components with correct probabilities, deflection proportional to ±ℏ/2. Shows outcome probabilities as bar chart. Sequential measurement mode: add a second SG device with independent axis; shows how the first measurement affects the second.

**Simulation physics:** For state |ψ⟩ = cos(θ/2)|↑⟩ + e^(iφ)sin(θ/2)|↓⟩ and measurement along axis n̂ = (sin α cos β, sin α sin β, cos α): P(+) = cos²(γ/2) where γ is the angle between the state vector on the Bloch sphere and the measurement axis. Animate beam splitting with trajectory arcs proportional to deflection.

**Key references for research agent:**
- Griffiths, Chapter 4 (section 4.4)
- Sakurai, Chapter 1 (the spin-first approach)
- Original Stern-Gerlach paper (1922) and its historical context
- Pauli's introduction of spin matrices (1927)
- Modern use of spin in quantum computing and NMR

**Bridge to Chapter 7:** With angular momentum and spin both understood, Chapter 7 solves the hydrogen atom — the combination of the radial equation with a Coulomb potential and the full angular momentum structure.

---

### CHAPTER 07 — The Hydrogen Atom
**Filename:** `07-hydrogen-atom.md`
**Arc position:** Act Two, Chapter 7

**One-line:** Students solve the hydrogen atom exactly, derive the energy levels and wave functions, and build an orbital visualizer showing probability densities for all n,l,m combinations up to n=4.

**Chapter description:**
The hydrogen atom is the central triumph of quantum mechanics — the first system where the theory made precise predictions that matched experiment exactly. This chapter solves the Coulomb potential problem using the machinery of Chapters 5 and 6: separation into radial and angular parts, the angular part solved by spherical harmonics, the radial part solved for the Coulomb potential. The result is the hydrogen energy levels Eₙ = -13.6 eV/n², the wave functions ψₙₗₘ(r,θ,φ), and a complete picture of atomic structure. The simulation is the most visual in the book: a genuine orbital visualizer.

**Core concepts:**
- The Coulomb potential: V(r) = -e²/4πε₀r
- The radial equation for hydrogen: associated Laguerre polynomials
- Principal quantum number n: n = 1,2,3,...; l = 0,1,...,n-1; m = -l,...,l
- Energy levels: Eₙ = -13.6 eV/n² (Rydberg formula confirmed)
- Wave functions: ψₙₗₘ(r,θ,φ) = Rₙₗ(r)Yₗᵐ(θ,φ)
  - Radial functions Rₙₗ: Laguerre polynomials × exponential × power
  - Angular functions Yₗᵐ: from Chapter 5
- The Bohr radius a₀ = 0.529 Å as the natural length scale
- Spectroscopic notation: s (l=0), p (l=1), d (l=2), f (l=3)
- Degeneracy: n² states per energy level (without spin: n²; with spin: 2n²)
- Radial probability density: P(r) = r²|Rₙₗ(r)|² — most probable radius
- Selection rules for radiative transitions: Δl = ±1, Δm = 0,±1

**Key vocabulary:** hydrogen atom, Coulomb potential, principal quantum number, radial wave function, Laguerre polynomials, Bohr radius, spectroscopic notation, degeneracy, selection rules, Lyman series, Balmer series

**Common misconceptions:**
- "Electrons orbit the nucleus in circles" — they occupy probability distributions; only ⟨r⟩ can be computed
- "The 2s and 2p states have the same energy because they are the same shell" — they are degenerate in hydrogen but not in multi-electron atoms
- "The probability density |ψ|² is the electron's charge distribution" — it is the probability density for finding the electron at a point

**Worked examples:**
1. Complete solution for ψ₁₀₀ (1s ground state): show calculation of R₁₀, combine with Y₀⁰, verify normalization
2. Radial probability density P(r) for 1s, 2s, 2p: find most probable radius, compare to Bohr radius
3. Compute ⟨r⟩ for 1s state; compare to a₀

**What the student builds:**
`07-hydrogen-orbitals.html` — hydrogen orbital visualizer. Controls: n (1–4), l (0 to n-1), m (-l to l). Display: 2D cross-section of |ψₙₗₘ|² in the xz-plane as a heat map (color = probability density); radial probability distribution P(r) = r²|Rₙₗ|² as a line plot; energy level diagram with current state highlighted; numerical values of ⟨r⟩, ⟨r²⟩, most probable r. Shows nodal surfaces.

**Simulation physics:** Compute Rₙₗ(r) using associated Laguerre polynomials Lₙ₋ₗ₋₁^(2l+1)(2r/na₀) × r^l × e^(-r/na₀). Compute Yₗᵐ(θ,φ) from Chapter 5 code. For 2D cross-section: evaluate |ψₙₗₘ(x,0,z)|² on a grid in the xz-plane. Render as D3 heatmap with color scale.

**Key references for research agent:**
- Griffiths, Chapter 4 (sections 4.1–4.2, 4.7)
- Atkins & Friedman, *Molecular Quantum Mechanics* — hydrogen atom chapter
- Historical development: Bohr model → Schrödinger's solution (1926)
- Experimental confirmation: spectral lines of hydrogen (Balmer, Lyman, Paschen series)
- Modern applications: hydrogen as a test of QED corrections

**Bridge to Chapter 8:** The hydrogen atom has a remarkable degeneracy: energy depends only on n, not on l or m. Identical particles (Chapter 8 preview) will break this with exchange symmetry. But first, Chapter 8 addresses multi-particle systems and the Pauli exclusion principle.

---

### CHAPTER 08 — Identical Particles
**Filename:** `08-identical-particles.md`
**Arc position:** Act Two, Chapter 8

**One-line:** Students learn that identical particles are not just similar but fundamentally indistinguishable, derive the symmetry requirements for fermions and bosons, and build a two-particle simulation showing exchange symmetry and the Pauli exclusion principle.

**Chapter description:**
Identical particles are where quantum mechanics diverges most sharply from classical mechanics. In classical physics, identical objects can always be tracked individually — a label survives. In quantum mechanics, there is no label: two electrons are not "electron A and electron B" but one quantum state of a two-electron system. This leads to symmetrization (bosons) and antisymmetrization (fermions) requirements, the Pauli exclusion principle, and ultimately to the structure of the periodic table. The chapter is conceptually rich but mathematically accessible — the key mathematics is Slater determinants and the symmetrization postulate.

**Core concepts:**
- The indistinguishability principle: identical particles have no hidden labels
- Exchange operator P̂₁₂: P̂₁₂ψ(1,2) = ψ(2,1)
- Symmetrization postulate: bosons have symmetric states (eigenvalue +1); fermions have antisymmetric states (eigenvalue -1)
- Two-particle wave functions: ψ±(r₁,r₂) = (1/√2)[ψₐ(r₁)ψᵦ(r₂) ± ψᵦ(r₁)ψₐ(r₂)]
- The Pauli exclusion principle: two fermions cannot occupy the same single-particle state
- Slater determinants for N-fermion systems
- Exchange interaction: purely quantum mechanical; responsible for ferromagnetism
- Bosons: Bose-Einstein condensation preview; photons; phonons
- Connection to the periodic table: electron configurations from the Pauli principle

**Key vocabulary:** identical particles, indistinguishability, exchange operator, symmetrization postulate, bosons, fermions, Pauli exclusion principle, Slater determinant, exchange interaction, Bose-Einstein condensation

**Common misconceptions:**
- "Identical particles are just very similar particles" — they are fundamentally indistinguishable; no experiment can tell them apart
- "The Pauli exclusion principle is about repulsion" — it is a symmetry requirement, not a force; it has no classical analogue

**Worked examples:**
1. Two distinguishable particles vs. two identical particles in a box: counting states, computing probabilities at same location
2. Slater determinant for two electrons in 1s and 2s states of helium
3. The exchange energy: compute ⟨ψ-|1/r₁₂|ψ-⟩ - ⟨ψ+|1/r₁₂|ψ+⟩ for the helium ground state configuration

**What the student builds:**
`08-identical-particles.html` — two-particle symmetry explorer. Controls: choose particle type (bosons / fermions / distinguishable), choose single-particle states a and b (from infinite well or harmonic oscillator), choose superposition. Display: |ψ(x₁,x₂)|² as a 2D heatmap in the (x₁,x₂) plane; shows that fermions have zero probability at x₁=x₂ (Pauli exclusion diagonal); shows bunching for bosons. Toggle between symmetric, antisymmetric, and distinguishable to compare.

**Simulation physics:** Compute ψ±(x₁,x₂) = (1/√2)[ψₐ(x₁)ψᵦ(x₂) ± ψᵦ(x₁)ψₐ(x₂)] on a 2D grid. Render |ψ±(x₁,x₂)|² as D3 heatmap. For fermions: explicitly show zero on the diagonal x₁=x₂. Compare with |ψᵢₙdₑₓ(x₁,x₂)|² = |ψₐ(x₁)|²|ψᵦ(x₂)|² for distinguishable.

**Key references for research agent:**
- Griffiths, Chapter 5
- Landau & Lifshitz, *Quantum Mechanics*, Chapter IX
- History of the Pauli exclusion principle (1925) and Fermi-Dirac statistics (1926)
- Experimental evidence for exchange interaction: ferromagnetism, superconductivity
- Bose-Einstein condensation: first experimental realization (1995)

**Bridge to Chapter 9:** The hydrogen atom and many-electron atoms can be solved approximately using perturbation theory. Chapter 9 introduces time-independent perturbation theory — the most widely used approximation method in quantum mechanics.

---

### CHAPTER 09 — Time-Independent Perturbation Theory
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

**Worked examples:**
1. Harmonic oscillator with anharmonic perturbation H' = λx⁴: compute first and second-order energy corrections
2. Fine structure of hydrogen: compute the spin-orbit correction, show j = l±1/2 splitting
3. Stark effect on hydrogen ground state: quadratic correction using second-order theory

**What the student builds:**
`09-perturbation-explorer.html` — energy level splitting visualizer. Controls: choose base system (infinite well or harmonic oscillator), choose perturbation type (linear, quadratic, sinusoidal), perturbation strength λ slider. Display: energy level diagram; as λ increases from 0, levels shift (showing first and second order corrections). For degenerate case: show splitting of degenerate levels. Compare exact numerical solution to perturbation theory approximation to show where the approximation breaks down.

**Simulation physics:** For the harmonic oscillator with H' = λx^n: compute Eₙ⁽¹⁾ = λ⟨n|x^n|n⟩ and Eₙ⁽²⁾ numerically. Compare to exact numerical diagonalization. Plot Eₙ(λ) vs. λ for several levels, showing perturbation theory (linear + quadratic in λ) vs. exact. Animate as λ slider moves.

**Key references for research agent:**
- Griffiths, Chapter 6
- Cohen-Tannoudji, Chapter XI
- Fine structure of hydrogen: historical measurements and QED corrections
- Stark effect: original discovery (1913); precision measurements
- Zeeman effect: normal and anomalous; Paschen-Back effect at high fields

**Bridge to Chapter 10:** Perturbation theory handles static perturbations. Chapter 10 handles time-dependent perturbations — oscillating fields that drive transitions between energy levels.

---

### CHAPTER 10 — Time-Dependent Perturbation Theory and Transitions
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
  - Applies when final states form a continuum; constant transition rate
- Selection rules: H' matrix element vanishes by symmetry → forbidden transition
  - Electric dipole selection rules: Δl = ±1, Δm = 0,±1
- Spontaneous emission: Einstein A coefficient; lifetime of excited states
- Absorption and stimulated emission: Einstein B coefficients; the laser

**Key vocabulary:** interaction picture, transition probability, resonance, Fermi's Golden Rule, density of states, selection rules, electric dipole approximation, spontaneous emission, stimulated emission, Einstein coefficients

**Common misconceptions:**
- "Fermi's Golden Rule gives an exact transition probability" — it is a rate valid for continuous spectra and long times; discrete spectra require the full first-order formula
- "Selection rules are absolute" — they apply in the electric dipole approximation; magnetic dipole and quadrupole transitions are allowed but weaker

**Worked examples:**
1. Two-level system driven by oscillating field: exact solution showing Rabi oscillations; comparison with perturbation theory result
2. Fermi's Golden Rule for hydrogen: compute spontaneous emission rate for 2p→1s, get lifetime ~1 ns
3. Selection rules from symmetry: show that ⟨1s|x|2s⟩ = 0 but ⟨1s|x|2p, m=±1⟩ ≠ 0

**What the student builds:**
`10-rabi-fermi.html` — resonance and transition simulator. Controls: two-level system with energy gap ℏω₀; driving frequency ω; driving amplitude; time slider. Display: transition probability P(i→f) vs. time showing Rabi oscillations at resonance (ω=ω₀) and off-resonance oscillations with smaller amplitude; frequency sweep mode showing P vs. ω/ω₀ (the resonance peak and sinc² envelope). Fermi's Golden Rule panel: for a chosen continuum model, show the constant rate vs. the oscillatory short-time behavior.

**Simulation physics:** Compute P(t) = (Ω²/(Ω²+Δ²)) sin²(√(Ω²+Δ²)t/2) where Ω = ⟨f|H'|i⟩/ℏ (Rabi frequency) and Δ = ω - ω₀ (detuning). Plot vs. t and vs. Δ. For frequency sweep, plot P(T,Δ) vs. Δ at fixed T showing sinc² envelope.

**Key references for research agent:**
- Griffiths, Chapter 9
- Cohen-Tannoudji, Chapter XIII
- Rabi oscillations: original NMR experiments; modern qubit control
- Fermi's Golden Rule: derivation history; applications in nuclear physics
- Laser physics: stimulated emission and population inversion

**Bridge to Chapter 11:** Chapters 9 and 10 give approximation methods for realistic Hamiltonians. Chapter 11 addresses two specific and widely applicable phenomena: the WKB approximation for slowly varying potentials, and quantum tunneling — classically forbidden barrier penetration.

---

### CHAPTER 11 — The WKB Approximation and Tunneling
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

**Worked examples:**
1. Rectangular barrier: exact transmission coefficient T(E,V₀,L); compare to WKB result
2. Gamow's theory of alpha decay: compute decay constant for a realistic nuclear potential; reproduce the Geiger-Nuttall correlation
3. STM tip-sample tunneling: estimate how a 1 Å change in distance affects the current

**What the student builds:**
`11-tunneling.html` — quantum tunneling visualizer. Controls: barrier shape selector (rectangular, triangular, parabolic, double-barrier), barrier height V₀, barrier width L, particle energy E. Display: potential V(x) with energy line E; wave function |ψ(x)|² showing exponential decay inside the barrier and transmitted wave on the right; transmission coefficient T vs. E/V₀ curve; T vs. L curve showing exponential decay with barrier width. Shows classically forbidden region highlighted.

**Simulation physics:** For rectangular barrier: T = [1 + (V₀ sinh(κL))²/(4E(V₀-E))]⁻¹ where κ = √(2m(V₀-E))/ℏ. For WKB general barrier: T ≈ e^(-2γ) with γ computed numerically by integrating √(2m(V(x)-E)) over the classically forbidden region. Render ψ(x) as incident + reflected on left, decaying inside, transmitted on right.

**Key references for research agent:**
- Griffiths, Chapter 9 (WKB) and Chapter 2 (tunneling)
- Historical development: Gamow's tunneling theory of alpha decay (1928)
- Scanning tunneling microscopy Nobel Prize (Binnig and Rohrer, 1986)
- Nuclear fusion in stars: the proton-proton chain and tunneling
- Tunnel diodes and their applications

**Bridge to Chapter 12:** The preceding chapters focused on single particles or pairs. Chapter 12 addresses the quantum mechanics of many-body systems through the lens of entanglement — and connects to quantum information.

---

### CHAPTER 12 — Entanglement and Quantum Information
**Filename:** `12-entanglement-quantum-information.md`
**Arc position:** Act Three, Chapter 12

**One-line:** Students learn what quantum entanglement is precisely, why it has no classical explanation (Bell's theorem), and how it underlies quantum computation — building a Bell inequality simulator and a simple quantum circuit visualizer.

**Chapter description:**
Entanglement is the resource that distinguishes quantum information from classical information. This chapter builds on Chapter 8 (identical particles) and Chapter 4 (Dirac notation) to define entanglement precisely: a state is entangled if and only if it cannot be written as a product state. Bell's theorem shows that no local hidden variable theory can reproduce quantum correlations — entanglement is genuinely non-classical. The chapter introduces qubits, quantum gates, and the basic concepts of quantum computation, connecting the formalism to a rapidly developing field students will encounter in research. This is not a quantum computing course; the chapter gives enough to understand what is physically happening in a quantum circuit.

**Core concepts:**
- Entanglement defined: |ψ⟩ ≠ |ψ₁⟩ ⊗ |ψ₂⟩; Schmidt decomposition
- The four Bell states: |Φ±⟩ = (|00⟩ ± |11⟩)/√2; |Ψ±⟩ = (|01⟩ ± |10⟩)/√2
- EPR paradox: Einstein-Podolsky-Rosen argument for incompleteness
- Bell's theorem: CHSH inequality; no local hidden variable theory satisfies quantum predictions
- Experimental tests: Aspect's experiments; loophole-free Bell tests
- Quantum information basics:
  - Qubits and quantum gates: X, Y, Z (Pauli), H (Hadamard), CNOT
  - Quantum circuits: gate sequences; measurement at the end
  - No-cloning theorem: cannot copy an unknown quantum state
  - Quantum teleportation: transfer a quantum state using entanglement + classical communication
- Decoherence: entanglement with the environment destroys quantum information; T₁ and T₂ times

**Key vocabulary:** entanglement, Bell states, EPR, Bell inequality, CHSH, local hidden variables, qubit, quantum gate, quantum circuit, no-cloning theorem, teleportation, decoherence

**Common misconceptions:**
- "Entanglement allows faster-than-light communication" — measurement outcomes are random; only correlations are non-local, and they cannot transmit information
- "Quantum computers are just faster classical computers" — they exploit superposition and entanglement to solve specific problems exponentially faster

**Worked examples:**
1. Bell state creation: apply Hadamard then CNOT to |00⟩; show the result is entangled
2. CHSH inequality: compute quantum prediction for entangled state; show it exceeds the classical bound of 2 (quantum maximum: 2√2)
3. Quantum teleportation protocol: step by step with Alice, Bob, and the Bell measurement

**What the student builds:**
`12-bell-inequality.html` — Bell inequality simulator. Controls: choose measurement angles for Alice (θ_A) and Bob (θ_B); choose initial two-qubit state (product or Bell state). Display: joint measurement outcome probabilities as a 2×2 table; CHSH parameter S = E(a,b) - E(a,b') + E(a',b) + E(a',b') displayed numerically; show S vs. angle for optimal settings; highlight when |S| > 2 (classical bound violation). Second panel: simple quantum circuit visualizer with drag-and-drop gates (H, X, CNOT, Rz) applied to 1–2 qubits; compute and display output state and measurement probabilities.

**Simulation physics:** For two-qubit state |ψ⟩ and measurement axes â = (sin θ_A, 0, cos θ_A) and b̂ = (sin θ_B, 0, cos θ_B): E(a,b) = ⟨ψ|(â·σ)⊗(b̂·σ)|ψ⟩. For Bell state |Φ+⟩: E(a,b) = cos(θ_A - θ_B). Compute CHSH S for four angle settings. Show S as a function of relative angle; maximum at 45° offsets.

**Key references for research agent:**
- Griffiths, Chapter 12 (quantum mechanics and entanglement)
- Nielsen & Chuang, *Quantum Computation and Quantum Information*, Chapters 1–2
- Bell's original paper (1964); CHSH paper (1969)
- Aspect's experiments (1981–1982); loophole-free tests (2015)
- Quantum computing: IBM Q, Google Sycamore; current state of the field

**Bridge to Chapter 13:** The full formalism has been developed. Chapter 13 is the capstone: it connects everything to the research problems students will encounter, with emphasis on the systems most relevant to current quantum science and engineering.

---

### CHAPTER 13 — Capstone: Quantum Mechanics in Research
**Filename:** `13-capstone-research-connections.md`
**Arc position:** Act Three, Chapter 13

**One-line:** Students connect the full QM curriculum to active research areas — quantum computing hardware, NV centers, topological systems, and open quantum systems — building a decoherence simulator and a final integrative project.

**Chapter description:**
The capstone chapter does not introduce new formalism. It takes the formalism of Chapters 1–12 and shows where it appears in active research. The goal is for a student who has completed this book to sit in a research group meeting, read a paper introduction, and understand what problem is being solved and what tools are being used. Five research areas are covered: open quantum systems and the Lindblad master equation (generalizing Chapters 1 and 4), NV centers in diamond (Chapters 6, 9, 10 applied to a real defect qubit), topological systems and Berry phase (Chapter 4 formalism + topology), quantum error correction (Chapter 12 extended), and computational quantum mechanics (numerical methods for many-body systems). The simulation is a decoherence visualizer — watching a Bloch vector shrink from the surface toward the center as T₁ and T₂ processes act.

**Core concepts:**
- Open quantum systems: density matrix ρ = Σpᵢ|ψᵢ⟩⟨ψᵢ|; von Neumann equation
  - Lindblad master equation: dρ/dt = -i[H,ρ]/ℏ + Σ(LᵢρLᵢ† - {Lᵢ†Lᵢ,ρ}/2)
  - T₁ (energy relaxation) and T₂ (dephasing) times; Bloch equations
- NV centers in diamond:
  - Spin-1 ground state; zero-field splitting; Zeeman effect (Chapter 9)
  - Optical initialization and readout; ODMR spectroscopy
  - Coherent control with microwave pulses (Chapters 6, 10)
  - Applications: magnetometry, quantum memory
- Berry phase and topology:
  - Adiabatic evolution; geometric phase γ = i∮⟨n|∇_R|n⟩·dR
  - Topological insulators: bulk-boundary correspondence
  - Majorana zero modes in topological superconductors
- Quantum error correction:
  - Errors as unitary operations (bit flip, phase flip)
  - The three-qubit bit-flip code; syndrome measurement
  - Surface codes (conceptual)
- Numerical quantum mechanics:
  - Exact diagonalization for small systems
  - Density functional theory (DFT): conceptual overview
  - Tensor networks: matrix product states for 1D systems

**Key vocabulary:** density matrix, Lindblad equation, T₁, T₂, decoherence, NV center, ODMR, Berry phase, topological insulator, Majorana mode, quantum error correction, syndrome, surface code, exact diagonalization, DFT

**Worked examples:**
1. NV center magnetometry: compute the ODMR frequency splitting as a function of external magnetic field using perturbation theory from Chapter 9
2. Decoherence calculation: solve the Lindblad equation for a qubit with T₁ and T₂; show how the Bloch vector shrinks
3. Three-qubit error correction: encode a logical qubit, apply a bit-flip error, perform syndrome measurement, apply correction

**What the student builds:**
`13-decoherence-simulator.html` — open quantum system and decoherence visualizer. Controls: initial qubit state (Bloch sphere), T₁ and T₂ sliders, Hamiltonian (free precession frequency ω₀), time. Display: Bloch sphere with state vector; vector shrinks exponentially toward center as time increases; shows T₁ process (Bloch vector decaying to south pole) vs. T₂ process (Bloch vector decaying toward z-axis). Time series plots of ⟨σx⟩(t), ⟨σy⟩(t), ⟨σz⟩(t) showing oscillation with decay envelope. NV center panel: shows ODMR spectrum (transition frequencies vs. B field) using perturbation theory results from Chapter 9.

**Final project prompt:** Students produce one of the following: (A) a complete annotated simulation set for all 13 chapters with parameter exploration notes; (B) a simulation of a physical system from their research group or area of interest, with a written explanation connecting it to the formalism; (C) a simulation-based tutorial on one of the five research connections in this chapter, suitable for explaining the physics to a peer who has completed Chapter 12.

**Key references for research agent:**
- Lindblad master equation: original paper (Lindblad 1976); accessible treatment in Breuer & Petruccione
- NV centers: Doherty et al. (2013) review; Rondin et al. (2014) magnetometry review
- Berry phase: Berry's original paper (1984); Xiao, Chang, Niu (2010) review
- Topological insulators: Hasan & Kane (2010) review
- Quantum error correction: Shor's code; Kitaev's surface code
- Tensor networks: Schollwöck (2011) DMRG review

---

## Assessment Structure

| Component | Chapters | Notes |
|-----------|---------|-------|
| Weekly simulation builds (12 × 15 pts) | 1–12 | One simulation per chapter; graded on correctness and exploration documentation |
| Chapter 0 setup (25 pts) | 0 | CLAUDE.md, DESIGN.md, PROJECT.md all present and correct |
| Midterm: formalism and standard systems (100 pts) | 4–8 | Problem set covering Dirac notation, harmonic oscillator, hydrogen atom, spin |
| Simulation exploration reports (3 × 25 pts) | 3, 7, 11 | Short written report: what did you change, what did you observe, what does it mean physically |
| Final project (150 pts) | 13 | See Chapter 13 options above |

---

## Simulation Stack Reference

All simulations use D3 v7 loaded via CDN, single HTML files with inline CSS and JS.

**Standard QM simulation elements defined in CLAUDE.md:**
- SVG canvas: 700×400px for 1D systems; 500×500px for 2D probability densities
- Parameter sliders: HTML range inputs, live update on `input` event
- Animation: `requestAnimationFrame` loop, pause/play button
- Color conventions (from DESIGN.md):
  - Probability density |ψ|²: blue fill, opacity 0.7
  - Real part Re(ψ): orange line, 2px stroke
  - Imaginary part Im(ψ): gray line, 2px stroke, dashed
  - Potential V(x): red line, 2px stroke
  - Energy levels: horizontal green lines
  - Classical turning points: vertical dashed lines, purple
- Dark mode: `prefers-color-scheme` media query in all files
- Normalization indicator: always displayed; warns if |∫|ψ|²dx - 1| > 0.01
- Physics constants: use SI units internally; display in natural units

---

## Open Questions for Research Agent

1. What are the current best-reviewed undergraduate QM textbooks and how do their chapter structures compare to this one?
2. What are the most common student misconceptions at each stage, per PER (Physics Education Research) literature?
3. What D3 physics simulation examples currently exist online — what is the state of the art for browser-based QM visualization?
4. What research papers should each chapter's LLM exercises reference to connect formalism to current science?
5. What are the key historical primary sources (Schrödinger 1926, Heisenberg 1925, Dirac 1928, etc.) that should be cited in each chapter?
6. For the Chapter 13 research connections, what are the most accessible review papers in each area that an advanced undergraduate could read?

---

*TIKTOC.md v1.0 — 14 chapters (Chapter 0 + Chapters 1–13)*
*Ready for: research gathering (Cowork research prompt), chapter drafting*
*Repo: quantum-mechanics-with-llms*
