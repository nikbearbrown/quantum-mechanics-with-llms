# Research Notes: Chapter 06 — Spin
**Source:** TIKTOC.md Chapter 06 entry (lines 350–395)
**Notes file:** 06-spin_notes.md
**Corresponding chapter:** chapters/06-spin.md (not yet written)
**Generated:** 2026-05-13

---

## Chapter summary (from TIKTOC.md)

> Spin is the most distinctively quantum mechanical concept in the standard curriculum. It has no classical analogue, it cannot be visualized as rotation, and yet it is essential for understanding atoms, magnetic resonance, and quantum computing. This chapter treats spin-1/2 completely: the two-state Hilbert space, Pauli matrices, spin operators, measurement probabilities, and the addition of spin to orbital angular momentum. The Stern-Gerlach experiment is the historical anchor — students see spin quantization as a direct experimental result before the formalism. The simulation recreates the Stern-Gerlach experiment interactively.

Core concepts named in TIKTOC: Stern-Gerlach (1922); spin-1/2 two-dim Hilbert space; basis |↑⟩, |↓⟩; spin operators Ŝ = (ℏ/2)σ with the three Pauli matrices; general state |ψ⟩ = α|↑⟩ + β|↓⟩; measurement probabilities; sequential Stern-Gerlach; Bloch sphere; spin-orbit coupling preview; Clebsch-Gordan briefly. Common misconceptions: "spin is rotation about an axis" (numerical takedown via equator speed > c); "measurement disturbance" framed as device limitation rather than as a fundamental incompatibility of observables. Worked examples named: SG analysis of Sx eigenstate measured along Sz; sequential SG; Larmor precession by time-dependent Schrödinger equation.

What the student builds: a Stern-Gerlach simulator with controls for initial state (θ, φ on Bloch sphere) and analyzer axis, beam-split animation with probabilities, and a sequential SG mode. The simulation physics formula given in TIKTOC: for state |ψ⟩ = cos(θ/2)|↑⟩ + e^(iφ) sin(θ/2)|↓⟩ measured along n̂, P(+) = cos²(γ/2) where γ is the angle between Bloch vector and measurement axis.

---

## A. Conceptual foundations

### 1. Stern-Gerlach as the experimental wedge

In February 1922 Otto Stern and Walther Gerlach, working in Frankfurt, sent a collimated beam of neutral silver atoms through the inhomogeneous magnetic field between a knife-edge pole piece and a flat pole piece, and onto a glass collector plate. The classical prediction, given a silver atom's magnetic moment µ at all angles to the field, was a continuous smear of deposition. What they got, after developing the plate (the developing was famously aided by Stern's cheap cigar — sulfur from the smoke reacted with the silver to make the deposit visible), was two discrete spots. The component of µ along the field direction takes only two values. The deflection is proportional to (∂B_z/∂z) · µ_z, so two values of µ_z give two beams.

A subtlety the chapter must honor: Stern and Gerlach in 1922 did *not* discover electron spin. Spin had not been proposed. They believed they were observing the space quantization of *orbital* angular momentum predicted by the old Bohr-Sommerfeld theory. Silver has the configuration [Kr] 4d¹⁰ 5s¹, so its single valence electron is in an s state with ℓ = 0 and contributes zero orbital angular momentum. The two-spot pattern is in fact the projection of the *spin* angular momentum of that single 5s¹ valence electron — but this interpretation only became available after Uhlenbeck and Goudsmit proposed spin in late 1925 (*Die Naturwissenschaften* 13, 953–954, "Ersetzung der Hypothese vom unmechanischen Zwang…"). The chapter should narrate this honestly: a 1922 experiment, a 1925 reinterpretation. The history is worth telling because it shows that the "obvious" outcome of an experiment can be ambiguous until the right concept is invented.

The experimental signature itself is robust. A beam prepared in any state will sort into two beams along whatever analyzer axis you point. Two values, always, with probabilities depending on the angle between the prepared state and the analyzer axis. That stubborn two-ness is the empirical fact spin-1/2 has to explain.

**Source anchors:** Stern, O. & Gerlach, W. (1922). "Der experimentelle Nachweis der Richtungsquantelung im Magnetfeld." *Zeitschrift für Physik* 9, 349–352. Friedrich, B. & Herschbach, D. (2003). "Stern and Gerlach: How a Bad Cigar Helped Reorient Atomic Physics." *Physics Today* 56(12), 53–59 [verify volume/issue]. Uhlenbeck, G. E. & Goudsmit, S. (1925). *Die Naturwissenschaften* 13, 953–954.

### 2. Spin is not rotation — the numerical takedown

Students arrive convinced spin is the electron physically spinning on an axis. The picture must be killed early, with a number, not a hand-wave. Treat the electron as a uniform sphere of "classical electron radius" r_e ≈ 2.82 × 10⁻¹⁵ m (this radius is defined by setting the electrostatic self-energy equal to mc², so it is the most generous radius you can give the electron; modern bounds put the actual size below 10⁻¹⁸ m). Demand angular momentum ℏ/2. The moment of inertia of a uniform sphere is (2/5) m_e r_e², and L_classical = Iω, so the equatorial speed v = ω r_e is

v = (5 ℏ) / (4 m_e r_e) ≈ (5 × 1.055 × 10⁻³⁴) / (4 × 9.11 × 10⁻³¹ × 2.82 × 10⁻¹⁵)
  ≈ 5.1 × 10¹⁰ m/s,

roughly 170 times the speed of light. Give the electron a larger radius and the picture still fails (the angular momentum drops further); give it a smaller radius (truer to experiment) and it fails worse. The "spinning ball" picture is not a small approximation that breaks at second order. It is wrong by orders of magnitude at zeroth order.

What spin actually is: an internal degree of freedom that transforms as a representation of SU(2) under rotations. It is not a description of any motion in space. It is a label that an electron carries that takes two values in a single measurement, and that obeys the same operator algebra as orbital angular momentum (so it deserves the *name* "angular momentum" — but only in the operator-algebra sense). The deep reason a spin-1/2 representation exists is that the rotation group SO(3) has a double cover SU(2), and quantum mechanical states are rays in projective Hilbert space, so they can transform under the cover rather than the group. Dirac (1928) derived spin-1/2 specifically from the requirement that the wave equation be Lorentz-invariant and first-order in time derivatives; spin is what falls out.

**Source anchors:** Griffiths, D. J. (2018). *Introduction to Quantum Mechanics*, 3rd ed., footnote in §4.4 makes the "spinning electron" estimate. Dirac, P. A. M. (1928). "The Quantum Theory of the Electron." *Proceedings of the Royal Society A* 117, 610–624. Classical electron radius r_e = e²/(4πε₀ m_e c²) ≈ 2.8179 × 10⁻¹⁵ m, CODATA 2018 [verify exact recommended value at draft time].

### 3. The two-state Hilbert space, basis states, and Pauli matrices

For spin-1/2 the Hilbert space is C² — two-dimensional, complex. Choose a basis: the eigenstates of S_z, conventionally

|↑⟩ = (1, 0)ᵀ,   |↓⟩ = (0, 1)ᵀ.

The spin operators are S_i = (ℏ/2) σ_i where σ_x, σ_y, σ_z are the three Pauli matrices. Write them out — the chapter should render all three explicitly because every later identity depends on them:

σ_x = [[0, 1], [1, 0]],
σ_y = [[0, −i], [i, 0]],
σ_z = [[1, 0], [0, −1]].

Four algebraic facts about these matrices, all checkable by direct multiplication and worth committing to memory:

1. σ_i² = I (the 2×2 identity), for each i.
2. Tr(σ_i) = 0, for each i.
3. Anticommutation: {σ_i, σ_j} = σ_i σ_j + σ_j σ_i = 2 δ_ij I.
4. Commutation: [σ_i, σ_j] = 2i ε_ijk σ_k. Equivalently, [S_i, S_j] = iℏ ε_ijk S_k — the same angular-momentum algebra as orbital L.

Together (3) and (4) mean σ_i σ_j = δ_ij I + i ε_ijk σ_k. Combined with Tr = 0 and σ² = I, this identifies σ_x, σ_y, σ_z as a basis for the traceless Hermitian 2×2 matrices, equivalently as generators of SU(2) — the group of unitary 2×2 matrices with determinant 1. The chapter should call this out: the Pauli matrices are not arbitrary; they are forced by the requirement that the operators (a) be Hermitian, (b) be traceless (the ±ℏ/2 eigenvalues sum to zero), (c) square to (ℏ/2)² I, and (d) satisfy the angular-momentum commutator. Up to a unitary change of basis, no other 2×2 matrices do all four.

Eigenstates of S_z: S_z |↑⟩ = +(ℏ/2)|↑⟩, S_z |↓⟩ = −(ℏ/2)|↓⟩. The general spin state is

|ψ⟩ = α |↑⟩ + β |↓⟩,   |α|² + |β|² = 1.

Two complex amplitudes minus one normalization minus one overall phase = two real parameters, which is the dimension of the Bloch sphere.

**Source anchors:** Griffiths §4.4 (spin). Pauli, W. (1927). "Zur Quantenmechanik des magnetischen Elektrons." *Zeitschrift für Physik* 43, 601–623 — the paper that introduced the matrices and the Pauli equation for spin in a magnetic field. Sakurai, J. J. & Napolitano, J. (2017). *Modern Quantum Mechanics*, 2nd ed., Ch. 1–3 takes the "spin-first" pedagogical route.

### 4. Spin along an arbitrary direction and the Bloch sphere

Pick a unit vector n̂ = (sin θ cos φ, sin θ sin φ, cos θ). The spin operator along that direction is S_n̂ = (ℏ/2) (n̂ · σ⃗) = (ℏ/2) (n_x σ_x + n_y σ_y + n_z σ_z). Its matrix form is

(ℏ/2) [[cos θ, sin θ e^(−iφ)], [sin θ e^(iφ), −cos θ]].

This matrix has eigenvalues ±ℏ/2 (one can check (n̂·σ)² = I). The two eigenstates are

|n̂, +⟩ = cos(θ/2) |↑⟩ + e^(iφ) sin(θ/2) |↓⟩
|n̂, −⟩ = sin(θ/2) |↑⟩ − e^(iφ) cos(θ/2) |↓⟩.

Two things to flag here. First, the half-angles: a state pointing along the +x axis (θ = π/2, φ = 0) has α = β = 1/√2 — equal weights on |↑⟩ and |↓⟩. A state pointing along −z (θ = π) is |↓⟩, not −|↑⟩. This is the famous "rotate by 2π and pick up a minus sign" property of spinors — a full 360° spatial rotation of the analyzer brings the spin state to −|ψ⟩, not |ψ⟩. Only a 720° rotation returns the state to itself. Penrose's discussion of this in *The Emperor's New Mind* (`_lib_Penrose-Emperors-New-Mind.md`) is a useful narrative source.

Second, the parameterization (θ, φ) makes the state vector a point on a unit sphere: the Bloch sphere. The north pole is |↑⟩, the south pole is |↓⟩, the equator is the family of equal-superposition states with phase φ. Any two-state quantum system — spin, two-level atom, qubit — has its state space the Bloch sphere. The chapter should connect this to the qubit picture used in Chapter 13 (the modern-applications capstone).

**Born-rule application.** A state |ψ⟩ = cos(θ_ψ/2) |↑⟩ + e^(iφ_ψ) sin(θ_ψ/2) |↓⟩ measured along axis n̂ at angles (θ_n, φ_n) gives outcome +ℏ/2 with probability P(+) = |⟨n̂,+|ψ⟩|² = cos²(γ/2), where γ is the angle on the Bloch sphere between the state vector and the measurement axis: cos γ = cos θ_ψ cos θ_n + sin θ_ψ sin θ_n cos(φ_ψ − φ_n). This is the formula the simulation will animate.

**Source anchors:** Griffiths §4.4.2 (general spin states; this exact half-angle form is Equation 4.151 [verify edition/equation number]). Nielsen, M. A. & Chuang, I. L. (2010). *Quantum Computation and Quantum Information*, 10th anniversary ed. Ch. 1 introduces the Bloch sphere for qubits.

### 5. Larmor precession — spin in a uniform magnetic field

Magnetic moment of the electron is µ⃗ = −γ S⃗, where γ = g_e (e/2m_e) is the gyromagnetic ratio and g_e ≈ 2.00232 is the electron g-factor (the deviation from 2 is the famous (g−2) anomaly; QED predicts it to extraordinary precision). The Hamiltonian for spin in a magnetic field B⃗ is

Ĥ = −µ⃗ · B⃗ = γ S⃗ · B⃗.

For B⃗ along ẑ with magnitude B₀:

Ĥ = γ B₀ S_z = (γ B₀ ℏ / 2) σ_z.

This Hamiltonian is diagonal in the S_z basis with eigenvalues ±(ℏ ω_L / 2), where the **Larmor frequency** is

ω_L = γ B₀.

The time evolution of an arbitrary initial spin state under Ĥ is given by |ψ(t)⟩ = exp(−i Ĥ t / ℏ) |ψ(0)⟩. For an initial state in the xz-plane at polar angle θ₀ (φ₀ = 0):

|ψ(t)⟩ = cos(θ₀/2) e^(−iω_L t / 2) |↑⟩ + sin(θ₀/2) e^(+iω_L t / 2) |↓⟩
       ≡ cos(θ₀/2) |↑⟩ + e^(iω_L t) sin(θ₀/2) |↓⟩ × (overall phase),

so the Bloch vector keeps polar angle θ₀ fixed and precesses in azimuth at frequency ω_L. The expectation values:

⟨S_x⟩(t) = (ℏ/2) sin θ₀ cos(ω_L t)
⟨S_y⟩(t) = (ℏ/2) sin θ₀ sin(ω_L t)
⟨S_z⟩(t) = (ℏ/2) cos θ₀.

This is a clean classical-looking result from a fully quantum calculation: the expectation value of the spin precesses around the field axis like a classical magnetic moment, at the Larmor frequency ω_L = γ B. The chapter should make this point — the Ehrenfest-style correspondence — and then immediately note that the underlying state is *not* a precessing classical vector; what precesses is the *probability distribution* over measurement outcomes.

For protons in a 1 T field, γ_p / (2π) ≈ 42.58 MHz/T, so ω_L / (2π) ≈ 42.58 MHz — this is the resonance frequency exploited in nuclear magnetic resonance imaging. For electrons, γ_e / (2π) ≈ 28.025 GHz/T. These numbers are not decoration; they are why magnetic resonance technology exists.

**Source anchors:** Griffiths §4.4.2 (Larmor precession derivation). Levitt, M. H. (2008). *Spin Dynamics: Basics of Nuclear Magnetic Resonance*, 2nd ed. Wiley — the canonical NMR textbook; opens with exactly this calculation. Gyromagnetic ratios from CODATA [verify current values at draft time].

---

## B. Domain examples and cases

### Example 1: Sequential Stern-Gerlach — the chapter's measurement-incompatibility headline

Prepare a beam in |↑z⟩ (using one SG_z magnet and blocking the |↓z⟩ output). Send it through a second analyzer oriented along x̂ (SG_x). The state |↑z⟩ in the x basis is

|↑z⟩ = (1/√2)(|↑x⟩ + |↓x⟩),

so P(↑x) = P(↓x) = 1/2 — the beam splits evenly. Block the |↓x⟩ output. Now the beam is in |↑x⟩. Send it through a *third* SG_z analyzer. The state |↑x⟩ in the z basis is

|↑x⟩ = (1/√2)(|↑z⟩ + |↓z⟩),

so P(↑z) = P(↓z) = 1/2 again. The intermediate SG_x measurement has wiped out the original definite |↑z⟩ — even though we never touched the z component "directly."

This is the famous result, and it is not about disturbance from a clumsy device. It is about the operators S_x and S_z not commuting: [S_x, S_z] = −iℏ S_y ≠ 0. No state can be a simultaneous eigenstate of both. Measuring S_x prepares the system in an S_x eigenstate; that state is a superposition in the S_z basis; the subsequent S_z measurement gives a probabilistic outcome. Sakurai's Ch. 1 opens with exactly this sequence as the motivation for the Hilbert-space formalism, and his pedagogical instinct is correct — the sequential SG experiment is the cleanest argument that classical labels do not survive quantum measurement.

The simulation will animate this. The user prepares an initial state, sees the beam split at SG₁, blocks one output, sees it split again at SG₂ with different probabilities depending on the angle between the two analyzers, and watches the running probabilities.

**Source anchors:** Sakurai & Napolitano (2017) Ch. 1.1 (sequential Stern-Gerlach). Griffiths §4.4.1.

### Example 2: Larmor precession quantitatively — what the slider does

Prepare a spin in |↑x⟩ at t = 0 (Bloch vector along +x). Apply B = B₀ ẑ. The Larmor frequency is ω_L = γ B₀. After time t, the Bloch vector has rotated by angle ω_L t in the xy-plane. After a quarter-period t = π/(2 ω_L), the vector points along +y. After a half-period t = π/ω_L, along −x. After a full period t = 2π/ω_L, back to +x.

Real numbers: electron in B = 1 mT. γ_e = 2π × 28.025 × 10⁹ rad/(s·T), so ω_L = 2π × 28.025 × 10⁶ rad/s, period T = 1/(28.025 MHz) ≈ 35.7 ns. This is fast — at radio frequencies — and is exploited in electron spin resonance (ESR) spectroscopy. Proton in B = 1 T: T ≈ 23.5 ns. In a clinical MRI scanner at B = 1.5 T, the proton Larmor frequency is ≈ 63.87 MHz. The chapter should run these numbers because they connect the abstract Hamiltonian to actual instruments students have seen.

The simulation lets the student dial B₀ on a slider and watch the precession speed change linearly. ω_L ∝ B is one of the cleanest visualizations of a quantum-mechanical proportionality.

### Example 3 (failure case): The "hidden-variable" reading of Stern-Gerlach

A naïve interpretation of two-spot Stern-Gerlach: each silver atom carries a hidden µ_z that is just ±µ_B (not continuously distributed), and the magnet sorts atoms by their pre-existing label. This explains the two spots without any quantum mechanics. The chapter must show why this story breaks at the next experimental step.

The hidden-variable model predicts that a beam already sorted to µ_z = +µ_B (the |↑z⟩ branch) carries that label intrinsically and would, by the same logic, also have a hidden µ_x = ±µ_B. So when sent through SG_x, it should sort cleanly by its pre-existing µ_x. Conditioning on µ_z = +µ_B and µ_x = +µ_B and then re-measuring µ_z, the hidden-variable model predicts you should get µ_z = +µ_B with probability 1 — the labels are stable. Experiment instead gives 50/50, the same as if you had never measured µ_z in the first place.

So the two-spot pattern is consistent with a hidden-variable model on its own, but the *full* set of sequential SG outcomes is not. The chapter should be specific: pre-existing definite labels for non-commuting observables are ruled out by the data, not by philosophical preference. (Bell-type arguments tighten this further by ruling out *any* local hidden-variable theory consistent with all measurement outcomes — that machinery belongs in Ch. 13.)

**Source anchors:** Sakurai & Napolitano (2017) Ch. 1.1.2; Bell, J. S. (1964). "On the Einstein-Podolsky-Rosen Paradox." *Physics* 1, 195–200 — for the deeper version of this argument.

---

## C. Connections and dependencies

**Depends on (earlier chapters):**
- Ch. 1–2 (wave functions, Schrödinger equation): the time evolution machinery used for Larmor precession.
- Ch. 4 (Dirac notation / Hilbert spaces): the algebra of operators on a finite-dimensional Hilbert space, the Born rule, Hermitian operators with real eigenvalues, projection onto eigenstates as the measurement postulate.
- Ch. 5 (3D QM and angular momentum): orbital L² and L_z with eigenvalues ℏ²ℓ(ℓ+1) and m_ℓ ℏ. Spin replays the algebra on a different (two-dim) Hilbert space.

**Enables (later chapters):**
- Ch. 7 (Hydrogen atom): the four-quantum-number description (n, ℓ, m_ℓ, m_s) requires spin to be available as a fourth label. Hydrogen energy levels at the Schrödinger level don't depend on m_s — but degeneracies and the electron capacity per orbital do.
- Ch. 8 (Identical particles): spin determines statistics. The singlet/triplet decomposition of two spin-1/2 particles is the algebraic content the helium calculation uses.
- Ch. 9 (Perturbation theory): the fine structure of hydrogen is the spin-orbit coupling H_SO = (1/(2 m_e² c²)) (1/r) (dV/dr) L⃗ · S⃗ applied as a perturbation to the Schrödinger Hamiltonian. The chapter should preview this without solving it.
- Ch. 13 (modern topics): qubits, NMR, ESR, the (g−2) anomaly as a QED test, NV centers, topological qubits.

**Pop-sci linkage:**
- `_lib_QM-Into-the-Light-Beginners.md`: pop-sci Ch. 5 mentions Stern-Gerlach verbally and gives the periodic-table consequence of the four quantum numbers, but does not introduce the matrix formalism. Useful as motivational reading, not as a math source.
- `_lib_Penrose-Emperors-New-Mind.md`: Penrose's discussion of spinors as objects that return to themselves only after 720° rotation is worth using as a side reference for the half-angle parameterization.

---

## D. Current state of the field

**Settled:** The non-relativistic spin-1/2 formalism (Pauli 1927) is a closed mature subject. The Pauli matrices, the half-angle parameterization, the Larmor precession formula — these are 1920s physics, untouched since.

**Active fronts the chapter may flag, not develop:**

- **The electron g-factor (g − 2).** The most precisely tested prediction of any physical theory. The Standard Model (QED + small hadronic and electroweak contributions) predicts g_e/2 to about 13 significant figures; the experimental measurement from a single electron in a Penning trap (Fan, Myers, Sukra, Gabrielse 2023 *Physical Review Letters* 130, 071801 [verify]) agrees to comparable precision. This is a striking confirmation that the Dirac/QED treatment of spin is correct — spin is not an ad hoc add-on.

- **Spintronics.** Manipulating electron spin (rather than charge) as the information-carrying degree of freedom in solid-state devices. The 2007 Nobel Prize (Fert and Grünberg) recognized giant magnetoresistance, used in hard-disk read heads, which depends on spin-dependent electron transport. Active engineering field.

- **Nitrogen-vacancy (NV) centers in diamond.** A nitrogen impurity adjacent to a vacancy in diamond gives a triplet ground state (S = 1) whose spin can be initialized, manipulated by microwaves, and read out optically at room temperature. NV centers are leading candidates for quantum magnetometry and quantum networks.

- **Topological qubits and Majorana modes** (cross-reference to Ch. 8 / Ch. 13). Microsoft's Station Q has pursued braided Majorana states as a topologically protected qubit; the field is contentious — multiple high-profile claims have been retracted or partially retracted [verify status at draft time, 2025–2026].

The chapter should name 1–2 of these as "where the story continues," not survey them.

**Source anchors:** Fan, X., Myers, T. G., Sukra, B. A. D., Gabrielse, G. (2023). "Measurement of the Electron Magnetic Moment." *Physical Review Letters* 130, 071801 [verify]. Fert, A. (2008). "Nobel Lecture: Origin, development, and future of spintronics." *Reviews of Modern Physics* 80, 1517 [verify].

---

## E. Teaching considerations

**Where students stick:**

1. **The half-angle.** A state at Bloch angle θ has amplitude cos(θ/2) on |↑⟩, not cos θ. The factor of 1/2 is structurally important (it is what makes spinors transform under SU(2) rather than SO(3)) but it surprises students every time. Worth pausing on with one concrete check: at θ = π/2 (equator), |α| = |β| = 1/√2 — equal weights, which makes physical sense (a spin pointing along x̂ has 50/50 probability for ±ẑ outcomes).

2. **What "measurement" means.** Many students hold an implicit "measurement disturbs the system" story that confuses two distinct facts: (a) the system was not in an eigenstate of the measured observable before the measurement, and (b) the measurement projects it into an eigenstate afterward. The disturbance language imports a classical picture where the system "had" a value all along. The cleaner statement: incompatible observables (non-commuting operators) cannot have simultaneous definite values; measurement chooses one observable to be definite at the cost of the others.

3. **Why spin behaves "like angular momentum" if it's not rotation.** Answer: because the Hilbert-space algebra is the same. Spin operators satisfy the same commutation relations as orbital L; they generate rotations of internal spinor space; the operator algebra inherits the geometric content of "angular momentum" even though the underlying degree of freedom has no spatial motion. The name is honest — same algebra, same conservation laws, same coupling to magnetic fields — but the picture is misleading.

4. **The (g − 2) anomaly.** Many students hear "the magnetic moment of the electron is exactly 2 in the right units" and then learn it's not quite 2 and assume something is wrong with Dirac. The truer story: Dirac's equation predicts g = 2 exactly; the deviation comes from QED radiative corrections (virtual photons dressing the electron). Each digit of g − 2 is a digit of agreement between theory and experiment. The chapter should flag this but not derive it.

**Recommended pedagogical moves:**

- Open with Stern-Gerlach as scene. The 1922 experiment with the cigar-developed plate is the canonical hook. Use the two-spot pattern as the empirical fact, then unfold to the formalism.
- Make the spinning-electron takedown a body paragraph with the number, not a footnote.
- Run the σ_x σ_y σ_z multiplication table on the page; do not relegate it to an exercise. The four identities (square to I, traceless, anticommute, commute to 2iε σ) are easier to internalize when seen computed than when seen quoted.
- Show the half-angle parameterization deriving the Bloch-sphere picture; do not import the Bloch sphere as a fait accompli.
- Run the Larmor precession calculation explicitly. The chapter's earned deep-dive is either (a) the derivation of the eigenstates of S_n̂ leading to the half-angle formula or (b) the Larmor precession solution from |ψ(t)⟩ = e^(−iĤt/ℏ) |ψ(0)⟩. My reading is (a) is the deeper one because it grounds the Bloch sphere, but (b) connects more directly to the simulation. Pick one and go deep; sketch the other.

**Exercises to embed:**

- Compute σ_x σ_y by hand and check that it equals i σ_z. Then verify (n̂ · σ⃗)² = I for arbitrary n̂.
- Show explicitly that |↑x⟩ = (|↑z⟩ + |↓z⟩)/√2 by diagonalizing σ_x.
- Compute ⟨S_x⟩, ⟨S_y⟩, ⟨S_z⟩ in the state cos(θ/2) |↑⟩ + e^(iφ) sin(θ/2) |↓⟩ and verify that the vector (⟨S_x⟩, ⟨S_y⟩, ⟨S_z⟩) has magnitude ℏ/2 and points in direction (θ, φ). This is the Bloch sphere derivation in disguise.
- For B = B₀ ẑ and initial state |↑x⟩, derive ⟨S_x⟩(t) = (ℏ/2) cos(ω_L t) and confirm the Larmor frequency.
- Sequential SG: prepare |↑z⟩, measure S_n̂ at angle θ, then measure S_z. Compute the joint probability of the (+, +) outcome as a function of θ.

---

## F. Library files relevant to this chapter

- **Griffiths, *Introduction to Quantum Mechanics*, 3rd ed.** (`822531304-David-J-Griffiths-Introduction-to-Quantum-Mechanics-Prentice-Hall-1994.txt` — note this is the 1994 1st-edition transcript; cross-check §4.4 numbering against the 3rd edition if that is the adopted text). §4.4 (Spin) is home base. Treats spin-1/2 cleanly with the Pauli matrices and includes Larmor precession.
- **Liboff, *Introductory Quantum Mechanics*** (`436681929-Introductory-Quantum-Mechanics-by-Richard-L-Liboff-pdf.txt`). Liboff's Ch. 11 (Spin) is more verbose and includes more explicit matrix manipulations; a useful alternative pass.
- **Griffiths Solution Manual** (`993201189-Solution-Manual-Introduction-to-Quantum-Mechanics-3e-Griffiths.txt`) — worked solutions for the §4.4 problems are the cleanest source of pre-tested calculations to adapt for the chapter's exercises.
- **`_lib_QM-Into-the-Light-Beginners.md`** — pop-sci framing for Stern-Gerlach as a narrative beat (not a formalism source).
- **`_lib_Penrose-Emperors-New-Mind.md`** — Penrose on spinor rotations and the 720° property.
- **`_lib_Davies-Demon-in-the-Machine.md`** — Davies on quantum measurement framing; potentially useful for the sequential-SG section's "measurement isn't disturbance" pivot.
- **Pop-sci pantry texts** (`556121095-QUANTUM-PHYSICS-FOR-BEGINNERS.txt`, `701622316-Quantum-Physics-for-Beginners…`, `687452060-Quantum-Physics-For-Beginners.txt`, `698476853-2022-THE-STRANGE-WORLD-OF-QUANTUM-PHYSICS.txt`) — these tend to assert "spin is intrinsic" without specifying what that means; usable as a reference for what students have probably heard and need corrected.

---

## F.5 Simulation pedagogy and D3 specifics

**What the simulation must show that the prose cannot.** The two empirical facts in this chapter — quantization (always two spots, never three or a continuum) and angle-dependent probability (P(+) = cos²(γ/2)) — are themselves easy to state but hard to *feel* without manipulating them. The simulation's job is to let the student vary (a) the initial spin direction on the Bloch sphere, (b) the analyzer axis, and (c) the magnetic field strength, and watch the consequences in real time.

**Layout (single SVG canvas, no separate windows).** Three coupled views, one above the other:

1. **Top: Bloch sphere widget.** A 3D-projected unit sphere rendered via D3 force-directed or simple spherical-to-Cartesian projection (no need for full WebGL — an isometric projection of latitude/longitude lines plus a draggable state vector is sufficient and brutalist-clean). Two arrows: one for the current state |ψ⟩, one for the analyzer axis n̂. Drag handles for both. The polar angle θ and azimuth φ of each are displayed as numbers next to the sphere.

2. **Middle: Stern-Gerlach apparatus, side view.** Beam entering from the left, splitting on encountering the SG magnet into two trajectories. The widths of the upper and lower beams are proportional to P(+) = cos²(γ/2) and P(−) = sin²(γ/2), where γ is the angle between the state vector and the analyzer axis (computed from the Bloch widget above). A bar chart at the right shows the same probabilities numerically.

3. **Bottom: Larmor precession panel.** When a B-field is enabled (slider for B₀ in the side panel), the state vector on the Bloch sphere precesses in real time at ω_L = γ B₀, where γ is set by a particle-species selector (electron, proton, default = electron). A digital readout shows ω_L / (2π) in MHz or GHz. The state arrow in the Bloch view animates; the SG output probabilities update live as the precessing state's angle to the analyzer axis sweeps.

**Sequential SG mode.** A toggle adds a second SG analyzer downstream of the first. The user picks the surviving branch from SG₁ (block one output) and sets the SG₂ axis independently. The simulation now shows the conditional probabilities P(SG₂ = + | SG₁ = +) and P(SG₂ = − | SG₁ = +) — the headline numbers for the sequential-measurement narrative.

**D3 idioms appropriate to this chapter:**

- `d3.scaleLinear()` for the (θ, φ) → screen coordinate mapping on the Bloch projection.
- `d3.drag()` for the state and analyzer arrows. Updates trigger re-computation of P(+) and re-render of beam widths.
- `d3.timer()` for the Larmor precession animation. Increment φ by ω_L · dt each frame.
- SVG `<line>` for beam segments, with `stroke-width` bound to probability (clamped to a minimum so zero-probability beams don't disappear from the visual budget — they fade to opacity 0.05 instead).
- Plain `<text>` for the numeric readouts. Brutalist styling: monospaced font, no animation on numbers, ≤ 3 significant figures.

**Honesty about what the simulation does not show.** The simulation displays *expectation values* and *probabilities*, not individual atom trajectories. A real Stern-Gerlach experiment produces one click per atom on one branch or the other — the cos²(γ/2) probability emerges as a frequency over many atoms. The simulation could be made more honest by adding a "Monte Carlo mode" toggle that fires individual atoms one at a time, each going up or down probabilistically, and tallies the running statistics. This is a useful extension prompt — the student builds the deterministic simulation first, then adds the Monte Carlo layer in the extension exercise. The deterministic version is the right pedagogical default because it makes the cos² law visible directly; the stochastic version is the right empirical default because it shows where that law comes from.

**Why this simulation matters more than text.** Three things only become natural by doing them:
- The half-angle: drag the state arrow to θ = π and watch the |↓⟩ probability go to 1 (not 0 — students forget the half-angle and predict P(−) = sin²(π/2) = 1 correctly only when they've seen it).
- Sequential incompatibility: prepare |↑z⟩, route through SG_x, route through SG_z. See the original z-information vanish — not described as "disturbance," but visible as the state vector being projected onto x̂ and then producing 50/50 for the next z measurement.
- Larmor precession: slide B₀ from 0 to its maximum and watch the precession frequency increase linearly. The student physically *sees* ω_L ∝ B, which is one of the cleanest visualizations of a quantum-mechanical proportionality in any chapter.

**Prompt scaffolding (preview of the chapter-end LLM exercise):**

1. CLAUDE.md prompt: extend the Brutalist QM coding constitution with rules specific to this chapter (single SVG, three coupled panels, no transitions on number readouts, parameter sliders only at the side panel, no DOM mutation outside the redraw function).
2. Simulation prompt (four-move): hook = "render the 1922 Stern-Gerlach experiment but let the user rotate the analyzer"; unfold = "the state is (θ, φ), the analyzer is (α, β), and the probability is cos²(γ/2)"; mechanism = "show the beam widths as a function of γ, animate the precession"; synthesize = "let the user run sequential SG."
3. Exploration tasks: (a) verify that rotating the analyzer by π flips P(+) and P(−); (b) measure the period of precession in 1 mT vs. 2 mT and verify ω_L ∝ B; (c) prepare |↑z⟩, route through SG_x, then SG_z, and confirm the 50/50 outcome.
4. Extension prompt: add a "Monte Carlo mode" that fires individual atoms one at a time and shows the running frequencies converging to the cos² law.

**Pedagogical-design references:** PhET Interactive Simulations (University of Colorado Boulder), `phet.colorado.edu` — their "Stern-Gerlach Experiment" simulation (HTML5) is the gold-standard reference for what this kind of widget looks like when done right [verify URL: `phet.colorado.edu/en/simulations/stern-gerlach`]. PhET research (Wieman, Adams, Perkins, Podolefsky 2010 *Science* 322, 682, and follow-ups in *Physical Review Special Topics — Physics Education Research*) demonstrates that students who manipulate simulation parameters retain mechanism understanding longer than students who passively watch demonstrations [verify exact citations at draft time].

---

## G. Gaps and flags

**Confidence anchors (high):** The non-relativistic spin-1/2 formalism is settled physics. The Pauli matrices, the Larmor precession formula, the half-angle parameterization, and the sequential-SG analysis can be cited from Griffiths §4.4 or Sakurai Ch. 3 without hedging.

**Items flagged `[verify]`:**

- Exact CODATA values for the electron g-factor (g_e ≈ 2.00232) and the gyromagnetic ratios (γ_p / 2π ≈ 42.58 MHz/T; γ_e / 2π ≈ 28.025 GHz/T) — pull current CODATA recommended values at draft time. `[verify]`
- Pauli 1927 *Zeitschrift für Physik* 43, 601–623 — volume and page numbers from secondary sources; confirm against a direct citation index before publishing. `[verify]`
- Dirac 1928 *Proceedings of the Royal Society A* 117, 610–624 — same. `[verify]`
- Friedrich & Herschbach 2003 *Physics Today* — issue/page should be checked. `[verify]`
- Fan et al. 2023 *PRL* on the electron g-factor measurement — verify exact volume/page. `[verify]`
- PhET Stern-Gerlach simulation URL — confirm at draft time; PhET has migrated several simulations to HTML5 from older Java versions. `[verify]`

**Thinnest section:** the "current state of the field" subsection. The (g−2) anomaly, spintronics, NV centers, and Majorana qubits are each book-length topics; the chapter must name them as pointers and resist surveying. Recommendation: one sentence per pointer, no more.

**Open pedagogical question:** does the chapter introduce Clebsch-Gordan coefficients (TIKTOC lists them as "brief"), or punt them to Ch. 8 / Ch. 9? My reading: introduce just the two-spin-1/2 singlet/triplet decomposition because Ch. 8 (Identical Particles) needs it for the helium calculation, and treat the general Clebsch-Gordan machinery as a flag, not a derivation. The chapter is already dense; full angular-momentum addition belongs in a separate section, not the spin chapter.

**What is *not* in this chapter (defer to later):**

- Spin-orbit coupling at the operator level — Ch. 9 (Perturbation theory).
- Spinor representation theory, SU(2) double-cover of SO(3) as a topological argument — beyond an undergraduate first course; mention as a flag, not derive.
- Full angular momentum addition with Clebsch-Gordan tables — Ch. 9 or a Ch. 8 sidebar.
- Density-matrix description of mixed spin states — Ch. 13 (modern topics).
- Bell inequalities and contextuality — Ch. 13.

**Mechanism the chapter deep-dives on:** the derivation of the eigenstates of S_n̂ = (ℏ/2) n̂·σ⃗, leading to the half-angle form |n̂, +⟩ = cos(θ/2)|↑⟩ + e^(iφ) sin(θ/2)|↓⟩ and thereby to the Bloch sphere parameterization. From this single derivation, the Born-rule probability P(+) = cos²(γ/2) and the Larmor precession follow as corollaries. The chapter spends its earned-explanation budget here, not on the σ-algebra (which is checkable but mechanical) or on the Stern-Gerlach narrative (which is the hook).

**Voice posture:** the chapter that is willing to be specific about a notoriously slippery topic. "Spin is intrinsic" is not enough — the chapter must say *what is intrinsic, in what space, satisfying what algebra*, and what numerical claim ("v_eq > c") rules out the picture students arrive with. Be willing to compute.

**Word count target for chapter:** 6,000–7,500. Stern-Gerlach narrative (1500 words), Pauli matrices and the algebra (1500), Bloch sphere derivation (1500), Larmor precession + simulation handoff (1500), exercises and synthesis (1500).

**Connection forward (Ch. 7):** the chapter ends having installed spin as a fourth quantum label. Ch. 7 (Hydrogen) is the first place this label does real work — the 2n² degeneracy, the periodic-table electron count, and the fine-structure splittings (deferred to Ch. 9) all use it.
