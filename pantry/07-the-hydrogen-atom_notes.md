# Research Notes: Chapter 07 — The Hydrogen Atom
**Source:** TIKTOC.md Chapter 07 entry (lines 399–446)
**Notes file:** 07-the-hydrogen-atom_notes.md
**Corresponding chapter:** chapters/07-hydrogen-atom.md (not yet written)
**Generated:** 2026-05-13

---

## Chapter summary (from TIKTOC.md)

> The hydrogen atom is the central triumph of quantum mechanics — the first system where the theory made precise predictions that matched experiment exactly. This chapter solves the Coulomb potential problem using the machinery of Chapters 5 and 6: separation into radial and angular parts, the angular part solved by spherical harmonics, the radial part solved for the Coulomb potential. The result is the hydrogen energy levels Eₙ = -13.6 eV/n², the wave functions ψₙₗₘ(r,θ,φ), and a complete picture of atomic structure. The simulation is the most visual in the book: a genuine orbital visualizer.

Core concepts named in TIKTOC: Coulomb potential V(r) = −e²/(4πε₀ r); radial equation with associated Laguerre polynomials; quantum numbers (n, ℓ, m); energy levels E_n = −13.6 eV/n²; wave functions ψ_nℓm = R_nℓ(r) Y_ℓm(θ, φ); Bohr radius a₀ ≈ 0.529 Å as the natural length scale; spectroscopic notation s, p, d, f; degeneracy n² without spin, 2n² with; radial probability density P(r) = r² |R_nℓ|² and the distinction between most probable r and ⟨r⟩; selection rules Δℓ = ±1, Δm = 0, ±1 for radiative transitions; Lyman, Balmer, Paschen series.

What the student builds: an orbital visualizer with sliders for (n, ℓ, m), a 2D cross-section heat map of |ψ_nℓm|² in the xz-plane, a radial probability plot, an energy-level diagram with the current state highlighted, and numerical readouts ⟨r⟩, ⟨r²⟩, most-probable r.

---

## A. Conceptual foundations

### 1. Why hydrogen is the canonical worked example — and why "canonical" is doing two distinct jobs

Hydrogen is the only neutral atom for which the time-independent Schrödinger equation has a closed-form bound-state solution. Two electrons (helium) already requires approximation methods; the helium ground state is computed variationally or perturbatively, not exactly. Hydrogen is the boundary case where the full quantum apparatus produces a solved system whose spectrum can be checked against spectroscopy line-by-line.

The chapter must distinguish two senses of "canonical":

- **Canonical in the curriculum sense.** Hydrogen is the worked example physicists fold every subsequent atomic system into. The (n, ℓ, m_ℓ, m_s) labeling, the s/p/d/f spectroscopic letters, the radial-and-angular factorization — all of it generalizes immediately to alkali atoms (under screening corrections), to Rydberg atoms, and to multi-electron atoms via Hartree–Fock. Hydrogen sets the vocabulary.

- **Canonical in the symmetry sense.** Hydrogen has a hidden symmetry — the conserved Laplace–Runge–Lenz (LRL) vector M⃗ = (1/(2m_e)) (p⃗ × L⃗ − L⃗ × p⃗) − (e²/(4πε₀)) (r̂) — which is special to 1/r potentials. The Lie algebra of {L⃗, M⃗} is so(4), the algebra of rotations in 4D, and the bound-state spectrum decomposes into representations of so(4) rather than just so(3). This is why the energy depends only on n, not on ℓ — the "extra" degeneracy among states of different ℓ at the same n is the fingerprint of the LRL symmetry. Pauli (1926 *Zeitschrift für Physik* 36, 336–363) used this symmetry to solve hydrogen *algebraically*, before Schrödinger published the wave-mechanical solution. The chapter does not have to derive this, but should name it: hydrogen's energy spectrum E_n = −E₁/n² is not generic to central potentials. It is special to 1/r.

For a generic central potential — say a finite spherical well, or a 1/r² potential — the radial equation depends on ℓ explicitly and the (2ℓ+1)-fold m-degeneracy survives but the ℓ-degeneracy does not. The n²-degeneracy of hydrogen is not a tautology of "rotational symmetry"; it is rotational symmetry plus an extra conserved vector, which exists only because the Coulomb potential goes as 1/r.

**Source anchors:** Griffiths, D. J. (2018). *Introduction to Quantum Mechanics*, 3rd ed., §4.2 (hydrogen) and §4.2.2 footnote on the LRL connection. Pauli, W. (1926). "Über das Wasserstoffspektrum vom Standpunkt der neuen Quantenmechanik." *Zeitschrift für Physik* 36, 336–363. Schrödinger, E. (1926). "Quantisierung als Eigenwertproblem (Erste Mitteilung)." *Annalen der Physik* 79, 361–376 — the first of the four 1926 papers; the hydrogen wave-mechanics is in *Erste* and *Dritte Mitteilung*. [verify exact issue/page for the *Annalen* publication.]

### 2. Reduced mass and the two-body problem

Hydrogen is a two-body system: a proton (mass m_p ≈ 1.6726 × 10⁻²⁷ kg) and an electron (m_e ≈ 9.1094 × 10⁻³¹ kg), interacting through the Coulomb potential V(|r⃗_p − r⃗_e|) = −e²/(4πε₀ |r⃗_p − r⃗_e|). The chapter should run the two-body separation explicitly even if briefly. Introduce the center-of-mass coordinate R⃗ = (m_p r⃗_p + m_e r⃗_e)/(m_p + m_e) and the relative coordinate r⃗ = r⃗_e − r⃗_p. The Hamiltonian separates:

Ĥ = (P⃗²)/(2M) + (p⃗²)/(2µ) + V(r),

where M = m_p + m_e and µ = m_p m_e / (m_p + m_e) is the reduced mass. The center-of-mass motion is a free particle (drop it). The relative-motion Schrödinger equation is

[−(ℏ²/2µ) ∇² − e²/(4πε₀ r)] ψ(r⃗) = E ψ(r⃗).

This is identical to a single particle of mass µ in an external Coulomb potential. Because m_p ≫ m_e, µ ≈ m_e (correction is about 1 part in 1836); the chapter should use m_e in all the headline numbers but note that the difference appears in precision spectroscopy as the "isotope shift" — hydrogen vs. deuterium vs. tritium have slightly different reduced masses and slightly different line positions. Urey, Brickwedde & Murphy (1932) discovered deuterium by spotting the predicted isotope shift in the Balmer series (Nobel 1934 to Urey).

**Source anchors:** Griffiths §4.2.1 (statement of the radial equation; reduced-mass aside in a footnote). Urey, H. C., Brickwedde, F. G. & Murphy, G. M. (1932). "A Hydrogen Isotope of Mass 2." *Physical Review* 39, 164–165 [verify].

### 3. Separation of variables in spherical coordinates and the effective radial potential

Because V depends only on r, write ψ(r, θ, φ) = R(r) Y(θ, φ). The angular part is solved universally by spherical harmonics (Ch. 5): Y_ℓm with L² Y_ℓm = ℏ² ℓ(ℓ+1) Y_ℓm and L_z Y_ℓm = m ℏ Y_ℓm. ℓ ∈ {0, 1, 2, …}, m ∈ {−ℓ, …, +ℓ}.

The radial equation, after substituting u(r) = r R(r), takes the form of a 1D Schrödinger equation with an *effective potential*:

−(ℏ²/2µ) u''(r) + V_eff(r) u(r) = E u(r),

where

V_eff(r) = −e²/(4πε₀ r) + ℏ² ℓ(ℓ+1)/(2µ r²).

The second term is the **centrifugal barrier** — a repulsive 1/r² term proportional to ℓ(ℓ+1). It comes from the angular kinetic energy and is the quantum-mechanical analog of the classical centrifugal pseudo-potential. For ℓ = 0, no barrier — the electron can sit on top of the nucleus (in the probability-density sense). For ℓ ≥ 1, the barrier pushes the electron away from r = 0; this is why p, d, f orbitals all vanish at the origin and only s orbitals have nonzero density at r = 0.

The chapter should plot V_eff(r) for ℓ = 0, 1, 2 superimposed and let the student see the centrifugal barrier emerge as ℓ increases. This is one of the cleanest "where does that come from?" moments in QM — the radial equation looks like 1D, the (2ℓ+1) degeneracy is hidden in the angular factor, and the ℓ-dependence in V_eff is the only place the angular quantum number appears in the radial dynamics.

**Source anchors:** Griffiths §4.2.1 (full derivation). Liboff, R. L. *Introductory Quantum Mechanics*, Ch. 10 — Liboff is more explicit about the centrifugal barrier and its semiclassical interpretation.

### 4. Solving the radial equation — Laguerre polynomials, the energy spectrum, the quantum number n

For the Coulomb potential, the radial equation can be reduced (via Frobenius / power-series method) to the differential equation for the **associated Laguerre polynomials** L_{n−ℓ−1}^{2ℓ+1}. The chapter does not need to derive the full Frobenius solution; what it must do is name the moves and run them on the ground state.

The radial wave functions take the form

R_nℓ(r) = (normalization) × r^ℓ × e^(−r/(n a₀)) × L_{n−ℓ−1}^{2ℓ+1}(2r/(n a₀))

with the **Bohr radius**

a₀ = (4πε₀ ℏ²)/(m_e e²) ≈ 5.29177 × 10⁻¹¹ m ≈ 0.529 Å

as the natural length scale (using m_e rather than µ; the reduced-mass correction shifts a₀ by ≈ 0.05%). The principal quantum number n = 1, 2, 3, … indexes the energy spectrum:

E_n = −(µ e⁴)/(2 (4πε₀)² ℏ² n²) = −(13.606 eV)/n².

The constant −13.606 eV is the Rydberg unit of energy (more precisely, the Rydberg constant times hc; CODATA value 13.605693 122994(26) eV [verify current value]).

The allowed quantum numbers: n ∈ {1, 2, 3, …}, ℓ ∈ {0, 1, …, n−1}, m ∈ {−ℓ, …, +ℓ}. Add spin: m_s ∈ {+1/2, −1/2}. The degeneracy per energy level (ignoring spin) is Σ_{ℓ=0}^{n−1} (2ℓ+1) = n². With spin, 2n².

Where do the ranges come from? The chapter should name this honestly:
- The ℓ ≤ n − 1 constraint comes from the radial equation: the polynomial L_{n−ℓ−1}^{2ℓ+1} has degree n − ℓ − 1, which must be ≥ 0 for a normalizable solution.
- The |m| ≤ ℓ constraint comes from the angular operator algebra (L² ≥ L_z²), derived in Ch. 5.
- The n = 1, 2, 3, … quantization comes from the requirement of normalizability of u(r) at both r = 0 and r → ∞.

These three constraints are independent. They are not "rules" — they are consequences of demanding that |ψ|² integrate to 1.

**Source anchors:** Griffiths §4.2.1 (the radial equation, Laguerre polynomials, Table 4.7 lists R_nℓ for n ≤ 3). Schrödinger 1926 *Annalen der Physik* (first paper of the *Quantisierung als Eigenwertproblem* series) — the original derivation. Bethe, H. A. & Salpeter, E. E. (1957). *Quantum Mechanics of One- and Two-Electron Atoms*. Springer — the canonical advanced reference. CODATA 2018 / 2022 values for a₀ and Ry [verify].

### 5. Wave functions and orbitals: |ψ|² as probability density, not path

The lowest few wave functions, explicitly:

ψ_100 = (1/√(π a₀³)) e^(−r/a₀) — the 1s ground state, spherically symmetric.

ψ_200 = (1/√(32 π a₀³)) (2 − r/a₀) e^(−r/(2 a₀)) — the 2s state, with a radial node at r = 2 a₀.

ψ_210 = (1/√(32 π a₀³)) (r/a₀) e^(−r/(2 a₀)) cos θ — the 2p_z state (m = 0), with an angular node in the xy-plane.

ψ_21±1 = ∓(1/√(64 π a₀³)) (r/a₀) e^(−r/(2 a₀)) sin θ e^(±iφ) — the 2p_{±1} states, complex.

(All forms verified against Griffiths Table 4.7 [verify exact table number and 3rd-edition normalizations].)

**Where students get confused: the m_ℓ eigenstates vs. the "chemistry" orbitals.** The chemistry textbook pictures of p_x, p_y, p_z as three orthogonal dumbbells along the coordinate axes are the *real* combinations:

p_x = −(Y_11 − Y_1,−1)/√2 ∝ sin θ cos φ,
p_y = i (Y_11 + Y_1,−1)/√2 ∝ sin θ sin φ,
p_z = Y_10 ∝ cos θ.

The p_z state is an L_z eigenstate (m = 0); p_x and p_y are not — they are superpositions of m = +1 and m = −1. Chemists draw the real forms because they are real-valued and easy to render; physicists working out spectra need the complex eigenstates because they diagonalize L_z. Both descriptions are correct; they answer different questions ("what does the electron density look like?" vs. "what's the z-component of orbital angular momentum?"). The chapter should show the transformation explicitly so the student can move between them.

**The misconception that costs the most.** Many students arrive (from intro chemistry or modern physics) believing that an orbital is a path the electron traces — perhaps a fast, smeared-out path. It is not. |ψ_nℓm(r, θ, φ)|² is a probability density: integrate it over a region and you get the probability of finding the electron in that region on a single position measurement. The familiar "dumbbell" pictures are isosurfaces of |ψ|² — surfaces enclosing some fixed fraction (often 90%) of the probability. The electron does not orbit. The chapter must say this in plain language; the visualizer makes it visible.

**Source anchors:** Griffiths §4.2 Table 4.7 (wave functions) and §4.4.3 (real combinations of spherical harmonics). NIST Physical Reference Data, atomic spectra, `physics.nist.gov/PhysRefData/ASD` [verify URL].

### 6. The Rydberg series and selection rules

The transitions ψ_{n_i ℓ_i m_i} → ψ_{n_f ℓ_f m_f} emit (or absorb) a photon of energy

ℏω = E_{n_i} − E_{n_f} = 13.6 eV × (1/n_f² − 1/n_i²).

Named spectral series, by final state:

- **Lyman series** (n_f = 1): UV. Lyman α = 1s ↔ 2p at 121.567 nm [verify CODATA].
- **Balmer series** (n_f = 2): visible. H_α (2 → 3) at 656.281 nm (red), H_β at 486.135 nm (blue-green), H_γ at 434.05 nm (violet) [verify]. The visible Balmer lines were the empirical anchor — Balmer wrote down λ = B · n²/(n²−4) for them in 1885 without any theory; Bohr's 1913 model was the first explanation; Schrödinger's 1926 solution was the first explanation that required no unjustified postulates.
- **Paschen series** (n_f = 3): near IR.
- **Brackett, Pfund** (n_f = 4, 5): IR.

**Selection rules.** Not every transition is allowed in the dipole approximation. The electric-dipole selection rules are

Δℓ = ±1,   Δm_ℓ = 0, ±1.

These come from evaluating ⟨ψ_f | r⃗ | ψ_i⟩ — the matrix element of the position operator between the two states. The angular integrals impose the Δℓ and Δm rules. Transitions that violate them (called "forbidden") are not strictly impossible, but they proceed through higher-order processes (magnetic dipole, electric quadrupole) with rates orders of magnitude lower. The 2s → 1s transition in hydrogen is electric-dipole-forbidden (Δℓ = 0); it occurs through a two-photon process with a lifetime of about 0.12 seconds, against ~ 10⁻⁹ s for typical allowed transitions [verify].

The chapter should derive the Δℓ = ±1 rule for one case (e.g., compute ⟨ψ_100 | z | ψ_210⟩ vs. ⟨ψ_100 | z | ψ_200⟩) to show how the parity of the integrand controls whether the integral vanishes.

**Source anchors:** Griffiths §11.2 (radiative transitions and selection rules — deferred to the perturbation theory chapter in Griffiths; the hydrogen chapter cites them). NIST Atomic Spectra Database for hydrogen line wavelengths. Balmer, J. J. (1885). "Notiz über die Spectrallinien des Wasserstoffs." *Annalen der Physik* 261, 80–87 [verify volume].

---

## B. Domain examples and cases

### Example 1: The 1s ground state — the chapter's earned deep-dive

Set n = 1, ℓ = 0, m = 0. The radial equation, with V_eff = V (no centrifugal barrier for ℓ = 0):

[−(ℏ²/2µ) (1/r) (d²/dr²)(r R) − e²/(4πε₀ r)] R = E R.

Substitute u(r) = r R(r):

−(ℏ²/2µ) u'' − (e²/(4πε₀ r)) u = E u.

Try the ansatz u(r) = A r e^(−r/a₀). Compute u'' = A e^(−r/a₀) (1/a₀² · r − 2/a₀) = (r/a₀² − 2/a₀) e^(−r/a₀) A. Substitute back, divide by A e^(−r/a₀):

−(ℏ²/2µ) (r/a₀² − 2/a₀) − (e²/(4πε₀)) = E r.

This must hold for all r, so the coefficient of r and the constant term must each balance:

Coefficient of r: −ℏ²/(2µ a₀²) = E, so E = −ℏ²/(2µ a₀²).
Constant: −2·(−ℏ²)/(2µ a₀) − e²/(4πε₀) = 0, so ℏ²/(µ a₀) = e²/(4πε₀), giving a₀ = (4πε₀ ℏ²)/(µ e²).

Substitute a₀ back into E: E = −ℏ²/(2µ a₀²) = −(µ e⁴)/(2 (4πε₀)² ℏ²) = −13.6 eV (using m_e for µ).

So the ground-state energy and the Bohr radius fall out of a single ansatz. The chapter can run this calculation explicitly — it takes half a page, it gives the two headline numbers of atomic physics, and it shows the machinery working.

**Normalize:** Set ψ_100 = R_10(r) Y_00(θ, φ) where Y_00 = 1/√(4π) and R_10 = (2/a₀^(3/2)) e^(−r/a₀). Check ∫|ψ_100|² d³r = ∫₀^∞ |R_10|² r² dr · ∫ |Y_00|² dΩ = (4/a₀³) ∫₀^∞ r² e^(−2r/a₀) dr · 1 = (4/a₀³) · (a₀/2)³ · 2 = 1. ✓

**Most probable radius.** The radial probability density is P(r) dr = |R_10|² r² dr = (4 r²/a₀³) e^(−2r/a₀) dr. Maximize: dP/dr = (4/a₀³) [2r − 2r²/a₀] e^(−2r/a₀) = 0 at r = a₀. The most probable radius equals the Bohr radius exactly. Bohr's 1913 model put the electron in a *circular orbit* at radius a₀; the wave-mechanical solution puts the *peak of the probability distribution* at a₀. Same number, different meaning.

**Expectation value.** ⟨r⟩_1s = ∫₀^∞ r |R_10|² r² dr · ∫|Y_00|² dΩ = (4/a₀³) ∫₀^∞ r³ e^(−2r/a₀) dr = (4/a₀³) · (3! a₀⁴/16) = (3/2) a₀.

So ⟨r⟩ = 1.5 a₀ while the most probable radius is a₀. These two numbers are different because |R|² r² is a skewed distribution — long tail to large r. The chapter must make this explicit. Students who conflate "average" and "most likely" are not yet thinking probabilistically.

**Source anchors:** Griffiths §4.2.1 Example 4.2 (the 1s integrals; verify problem number against the 3rd edition). Solution Manual (`993201189-Solution-Manual-Introduction-to-Quantum-Mechanics-3e-Griffiths.txt`) for the worked normalization and ⟨r⟩.

### Example 2: 2s vs. 2p — same energy, different geometry

n = 2 admits ℓ = 0 (2s, one state) and ℓ = 1 (2p, three states: m = −1, 0, +1). All four have E_2 = −13.6/4 = −3.4 eV. They are degenerate. They are *not* the same wave function.

The 2s state has a radial node — a sphere where R_20 = 0. Specifically, R_20 ∝ (2 − r/a₀) e^(−r/(2a₀)), zero at r = 2 a₀. Inside this sphere the wave function is positive; outside, negative. (The probability density is positive everywhere, of course; the wave function changes sign.)

The 2p_z state has an angular node — the xy-plane is a nodal plane (Y_10 ∝ cos θ vanishes at θ = π/2). No radial node.

So same energy, different spatial structure. The chapter should plot |ψ_200|² and |ψ_210|² side-by-side as radial cuts and contour plots, and note that "same eigenvalue of Ĥ" does not mean "same shape" — it means "same one number." The degeneracy is an algebraic fact about the energy operator; it is not a statement about geometry.

This is also where the LRL symmetry pays off: 2s and 2p have the same energy because the LRL vector connects them within a representation of so(4). Without that symmetry — say in a multi-electron atom where the effective potential isn't exactly 1/r — the degeneracy is broken and 2s and 2p split apart. The 2s/2p splitting in alkali atoms (sodium D lines) is a direct measurement of the departure from 1/r in the effective single-electron potential. The chapter should mention this as the bridge to Ch. 8 (multi-electron atoms).

### Example 3 (failure case): The Bohr model applied to anything other than hydrogen

The Bohr model gets E_n = −13.6 Z²/n² eV for a hydrogen-like ion (one electron, nuclear charge +Ze). For He⁺ (Z = 2), this predicts E_1 = −54.4 eV. The experimental first ionization energy of He⁺ is 54.4 eV. Bohr is right.

For neutral helium (Z = 2, two electrons), the Bohr model has no machinery for electron-electron repulsion. The naïve "fill the n = 1 shell with two electrons, each at energy −Z² × 13.6 eV" gives a total ground-state energy of −108.8 eV. The experimental binding energy of helium (first + second ionization energies summed) is −79.0 eV. Bohr's prediction is off by 30 eV — the electron-electron Coulomb repulsion contributes a real, positive energy that the Bohr model cannot represent.

This is the canonical demonstration that Bohr's success was specific to hydrogen. The chapter should run the comparison explicitly:

- He⁺ (one electron): Bohr gets the energy right.
- He neutral (two electrons): Bohr misses by ≈ 27%.

The deeper reason: hydrogen has the LRL symmetry only because it has one electron in a 1/r potential. Add a second electron and the potential is no longer 1/r (the second electron screens the nucleus); the symmetry is broken; Bohr's quantization condition becomes a numerical accident that worked once. The full apparatus (antisymmetric wave functions, exchange integrals, variational methods) of Ch. 8 and Ch. 9 is built to handle exactly this failure.

**Source anchors:** NIST Atomic Spectra Database for the He⁺ ionization (54.418 eV) and He neutral ionization energies (24.587 eV + 54.418 eV = 79.005 eV) [verify URL]. Griffiths §7.2 (variational calculation of the helium ground state).

---

## C. Connections and dependencies

**Depends on (earlier chapters):**
- Ch. 1–2 (wave function, Schrödinger equation): the time-independent equation with a central potential.
- Ch. 4 (Hilbert space, operators, the Born rule): the meaning of |ψ|² as probability density.
- Ch. 5 (3D quantum mechanics, angular momentum, spherical harmonics): the angular part of the hydrogen wave function is recycled from Ch. 5; the chapter only needs to solve the *radial* equation.
- Ch. 6 (spin): the fourth quantum number m_s comes from spin. Energy levels in pure Schrödinger hydrogen do not depend on m_s, but the 2n² degeneracy and the periodic-table electron count do.

**Enables (later chapters):**
- Ch. 8 (Identical particles): helium and heavier atoms require multi-electron wave functions built from hydrogenic-like single-particle orbitals plus antisymmetry. The periodic table is the synthesis.
- Ch. 9 (Time-independent perturbation theory): the fine structure of hydrogen (relativistic correction + spin-orbit + Darwin term) is the canonical worked example of degenerate perturbation theory. The Stark effect (hydrogen in an electric field) and the Zeeman effect (in a magnetic field) are the next worked examples. All of these are perturbations on top of the Schrödinger hydrogen spectrum the chapter solves.
- Ch. 10 (variational methods, if present in the book — placement depends on TIKTOC): helium ground state.
- Ch. 13 (modern applications): Rydberg atoms in quantum computing; hyperfine structure as the basis for the cesium-133 atomic clock and the SI second; antihydrogen spectroscopy at CERN as a CPT test; the 21 cm hydrogen line in radio astronomy (a hyperfine transition).

**Pop-sci linkage:**
- `_lib_QM-Into-the-Light-Beginners.md`: pop-sci Ch. 5 covers the Bohr model and shows the "shapes" of orbitals without ever stating what an orbital mathematically is. Assignable as motivational reading before the chapter; the chapter must correct the orbital-as-path picture explicitly.
- `_lib_Significant-Figures-Stewart.md`: Stewart on Schrödinger's biographical context, the 1926 winter, and the hydrogen solution; useful for the historical opening.

---

## D. Current state of the field

The Schrödinger solution of hydrogen is mature 1926 physics. What has moved since:

- **QED corrections.** The Lamb shift — discovered by Lamb & Retherford 1947 (*Physical Review* 72, 241) measuring a small splitting between the 2s_{1/2} and 2p_{1/2} levels that Dirac theory predicts to be exactly degenerate — was the first experimental confirmation that virtual photons (the vacuum polarization and self-energy of QED) make measurable corrections to atomic energies. The current theoretical prediction agrees with experiment to about 10 parts per million [verify].

- **The proton radius puzzle.** Around 2010, Pohl et al. (*Nature* 466, 213–216) measured the proton charge radius from muonic hydrogen spectroscopy (a muon replaces the electron, sitting ~ 200× closer to the proton and so probing finite-size effects strongly) and got 0.84184 fm, about 4% smaller and 7σ away from the CODATA 2010 value (0.8775 fm) from electronic hydrogen and electron scattering. A decade of work followed. New electronic hydrogen measurements — Bezginov et al. 2019 *Science* 365, 1007 (2S–2P), Fleurbaey et al. 2018 (1S–3S), CREMA collaboration extensions — have largely converged to the smaller (muonic) value; CODATA 2018 adopted 0.8414 fm [verify exact value and source]. The chapter should mention this as a place where hydrogen spectroscopy still tests the foundations.

- **Antihydrogen.** The ALPHA collaboration at CERN has trapped antihydrogen (ē⁺ + p̄) and measured the 1S–2S transition, finding agreement with hydrogen at the parts-per-trillion level (Ahmadi et al. 2018 *Nature* 557, 71–75 [verify]). The hyperfine splitting and the gravitational behavior of antihydrogen are active fronts.

- **Rydberg atoms in quantum simulation.** Highly excited (n ~ 50–100) hydrogenic states of alkali atoms have large dipole moments (~ n² a₀) and long lifetimes (~ n³); chains of Rydberg-blockaded atoms are the basis for the analog quantum simulators built by groups at Harvard (Lukin) and Caltech (Endres), and for commercial neutral-atom quantum computers from Atom Computing, QuEra, and Pasqal.

The chapter should mention 2–3 of these as "where the story continues" and resist surveying them.

**Source anchors:** Lamb, W. E. & Retherford, R. C. (1947). *Physical Review* 72, 241 [verify]. Pohl, R. et al. (2010). *Nature* 466, 213–216 [verify]. Bezginov, N. et al. (2019). *Science* 365, 1007 [verify]. Ahmadi, M. et al. (2018). *Nature* 557, 71–75 [verify]. CODATA 2018 recommended values, NIST.

---

## E. Teaching considerations

**Where students stick:**

1. **Orbital as path.** This is the single most damaging picture in introductory chemistry. The chapter must reset it with the most-probable-radius vs. expectation-value comparison (r_mp = a₀ vs. ⟨r⟩ = 1.5 a₀ for 1s). If those two numbers are different, the orbital cannot be a path — a path has one radius. The visualizer (F.5) makes the probability cloud directly visible.

2. **"Why does energy depend only on n?"** Most central potentials give energies depending on both n and ℓ. Hydrogen's energy-depends-only-on-n behavior is the LRL symmetry (the hidden so(4)). The chapter should name this — call it the *Coulomb degeneracy* — and note that as soon as the potential departs from 1/r (e.g., screening in multi-electron atoms), the degeneracy splits.

3. **Quantum-number ranges.** Students memorize "n ≥ 1, 0 ≤ ℓ ≤ n−1, |m| ≤ ℓ" without seeing where the constraints come from. The chapter should at least name each: ℓ ≤ n−1 from the radial polynomial degree, |m| ≤ ℓ from the operator inequality L² ≥ L_z², n from normalizability.

4. **The chemistry orbitals vs. the L_z eigenstates.** The dumbbells drawn in chemistry are the real combinations p_x, p_y, p_z. Two of them (p_x, p_y) are not L_z eigenstates — they are superpositions of m = ±1. The chapter should show the transformation. Students moving on to spectroscopy or magnetic-field problems will need the complex Y_ℓm; students staying in chemistry will use the real combinations. Both are correct; they answer different questions.

5. **Why the Bohr radius is the right length scale.** The chapter should derive a₀ from the 1s ansatz (Example 1) rather than asserting it. Students who see the calculation, including the cancellation that fixes a₀, understand the meaning of "natural length scale" better than those who just see the formula.

**Recommended pedagogical moves:**

- Open with the 1885 Balmer formula and its 28-year wait for explanation. Concrete, dated, specific. The puzzle: a Swiss math teacher wrote down a formula for the hydrogen spectrum that worked, with no theory. What was the theory?
- Run the 1s solution on the page. This is the chapter's earned deep-dive. Show the ansatz, the cancellation, the Bohr-radius identification, the energy. Do not relegate it to an appendix.
- Compare 1s, 2s, 2p, 3d wave functions side-by-side. The visualizer is the right way to do this; the prose should show two or three explicit plots.
- Be explicit about "orbital is not a path" and use the simulation as evidence — drag the n slider and watch the radial extent grow; drag the ℓ slider and watch angular structure appear.
- End with the periodic-table preview as synthesis. The whole apparatus (n, ℓ, m_ℓ, m_s + Pauli) will be used in Ch. 8 to derive the periodic table from antisymmetry. Hydrogen is the foundation that supports the rest.

**Exercises to embed:**

- Compute ⟨r⟩ for the 2s and 2p states; show they are different even though E is the same.
- Show ⟨1/r⟩ = 1/(n² a₀) for hydrogenic states (the chapter should at least quote the result; the derivation is Griffiths Problem 4.13 or thereabouts [verify]).
- Compute the Lyman α wavelength (2p → 1s) and compare to the experimental value 121.567 nm.
- Verify that ψ_200 has a radial node at r = 2 a₀.
- Estimate the hydrogen ionization energy using the uncertainty principle: take r ≈ a₀, then p ≈ ℏ/a₀, then KE ≈ p²/(2m_e) ≈ 13.6 eV; the Coulomb PE at r = a₀ is −27.2 eV; total E ≈ −13.6 eV. The chapter should run this back-of-envelope argument as a "look at where the number comes from" moment.

---

## F. Library files relevant to this chapter

- **Griffiths, *Introduction to Quantum Mechanics*, 3rd ed.** (`822531304-David-J-Griffiths-Introduction-to-Quantum-Mechanics-Prentice-Hall-1994.txt` — the pantry transcript is the 1994 1st edition; cross-check §4.2 numbering against the 3rd edition if that is the adopted text). §4.2 is home base: the radial equation, the Laguerre polynomial solution, the energy spectrum, the wave function table. The chapter follows Griffiths' organization closely.
- **Griffiths Solution Manual** (`993201189-Solution-Manual-Introduction-to-Quantum-Mechanics-3e-Griffiths.txt`) — worked integrals for ⟨r⟩, ⟨r²⟩, ⟨1/r⟩ in the 1s, 2s, 2p states; the chapter borrows directly for exercise solutions.
- **Liboff, *Introductory Quantum Mechanics*** (`436681929-Introductory-Quantum-Mechanics-by-Richard-L-Liboff-pdf.txt`) — Ch. 10. Liboff is more explicit about the Laguerre polynomial machinery and the Frobenius method than Griffiths; useful for students who want to see the polynomials derived rather than quoted.
- **`_lib_QM-Into-the-Light-Beginners.md`** — pop-sci framing for the orbital pictures and the Bohr-model narrative; useful as assignable motivational reading but mathematically rough.
- **`_lib_Penrose-Emperors-New-Mind.md`** — Penrose's discussion of hydrogen as the model atom and the role of angular momentum.
- **`_lib_Significant-Figures-Stewart.md`** — Stewart on Schrödinger's biographical context, the Christmas-in-Arosa hydrogen-solution episode; useful color for the opening.
- **Pop-sci pantry texts** (`556121095-…`, `701622316-…`, `687452060-…`, `698476853-…`) — all of these describe orbitals as "shapes" or "regions" without specifying probability density. Useful as a reference for what students arrive having read.

---

## F.5 Simulation pedagogy and D3 specifics

**The headline visualization of the book.** TIKTOC describes this as "the most visual in the book" and is right. The hydrogen orbital visualizer is the chapter where a simulation does what no static figure can: lets the student dial (n, ℓ, m) and watch the probability cloud reorganize. Every previous static figure in chemistry textbooks is a frozen snapshot of one orbital; here the student sees the family.

**Layout (single SVG canvas, multiple panels):**

1. **Primary: 2D cross-section heat map.** A grid in the xz-plane (y = 0), say 200 × 200 pixels covering ±20 a₀ in each direction. At each pixel compute |ψ_nℓm(x, 0, z)|² and color-map it. Use a perceptually uniform color scale (Viridis or Cividis), not a rainbow. Brutalist principle: one color scale, one legend. The cross-section is in the xz-plane because most orbitals with m ≠ 0 have azimuthal phase that integrates to azimuthal symmetry of |ψ|² around z, so a single xz cut captures the full angular structure with no rotation needed. (For real orbitals like p_x or p_y, the xz cut would miss the lobe — handle this by offering a toggle between "complex Y_ℓm eigenstates" and "real chemistry orbitals" and rotating the cut plane accordingly.)

2. **Secondary: radial probability density P(r) = r² |R_nℓ(r)|² as a line plot.** Same panel underneath the heat map. Shows the radial distribution, with vertical lines marking r_mp (most probable) and ⟨r⟩. The contrast between these two numbers is one of the chapter's pedagogical headlines; the simulation must show both.

3. **Tertiary: energy-level diagram.** A vertical axis showing E_n = −13.6/n² for n = 1, 2, 3, 4, 5. Horizontal lines at each E_n. The currently selected state lights up. Spectroscopic labels (1s, 2s, 2p, 3s, 3p, 3d, 4f, …) annotate the lines. Clicking on a different state moves the (n, ℓ, m) sliders to that state. The diagram makes the n²-degeneracy visible: 2s and 2p sit on the same horizontal line; 3s, 3p, 3d on another.

4. **Quaternary: numeric readouts.** ⟨r⟩, ⟨r²⟩, r_mp, the energy E_n, the number of radial nodes (n − ℓ − 1), the number of angular nodes (ℓ), the total nodes (n − 1). Monospaced. Three significant figures. No animation on numbers.

**Transition mode.** A toggle adds a second state selector. The student picks |ψ_{n_i ℓ_i m_i}⟩ and |ψ_{n_f ℓ_f m_f}⟩. The simulation computes ΔE = E_{n_i} − E_{n_f}, identifies the spectral series (Lyman if n_f = 1, Balmer if n_f = 2, etc.), displays the photon wavelength in nm, and flags whether the transition satisfies the dipole selection rules (Δℓ = ±1, Δm = 0, ±1). Forbidden transitions are shown in a different color with a note: "electric-dipole forbidden — proceeds via higher-order processes."

**D3 idioms appropriate to this chapter:**

- `d3.scaleSequential(d3.interpolateViridis)` for the heat map color scale, with the domain set to [0, max(|ψ|²)] (recompute on every state change so the contrast is consistent across orbitals of different normalization).
- `d3.contour` (the `d3-contour` module) to draw isocontour lines on top of the heat map — useful for the 90%-probability isosurface that chemistry textbooks call "the orbital shape."
- `d3.line()` for the radial probability plot.
- Plain SVG `<rect>` elements for the heat map (one rect per pixel — D3 handles this well at 200 × 200; for larger grids, switch to a `<canvas>` element).
- `d3.scaleLog()` *not* used for the probability scale — students need to see relative density linearly to compare regions.

**Honesty about what the simulation does not show.**

- **Phase.** The simulation displays |ψ|², not ψ. The phase information (the e^(imφ) factor, the sign change across a radial node) is invisible in the standard view. A toggle could show a *phase* visualization (color by arg(ψ) instead of magnitude), which is essential for understanding why the real p_x/p_y combinations look different from the complex p_{±1} eigenstates. Recommended as an extension prompt.

- **3D structure.** A 2D xz cross-section captures the full structure for m = 0 states (azimuthally symmetric) but misses the rotation for m ≠ 0. A toggle to view xy and xz simultaneously, or to rotate the cut plane around z, addresses this. Full 3D rendering (isosurface in a WebGL view) is possible but breaks brutalist single-SVG simplicity; recommended only as an advanced extension.

- **Time evolution.** Hydrogen energy eigenstates ψ_nℓm e^(−i E_n t/ℏ) have time-independent |ψ|². The simulation is static in time once a state is selected. A superposition mode — let the student build a coherent superposition of, say, 1s and 2p_z and watch the probability density slosh — is a powerful extension prompt; it shows time evolution and gives a feel for what "atomic transitions" look like dynamically.

**Why this simulation matters more than text.** Three things only become natural by doing them:

- **The orbital is not a path.** Drag the (n, ℓ, m) sliders. The shape changes continuously across the family. The electron is not "in" any of these shapes; the shape is the probability density. A path has one position at one time; |ψ|² has no time and shows everywhere the electron *could be*.

- **r_mp vs. ⟨r⟩.** The radial probability plot shows P(r) and marks both r_mp (the peak) and ⟨r⟩ (the area-weighted center). They are visibly different. The student sees the skewness directly.

- **The n² degeneracy.** Click between 2s (1s²2s¹ — no, sorry, 2s means n=2, ℓ=0) and 2p — same energy, different shape. Click between 3s, 3p, 3d — same energy, different shape. The energy-level diagram makes the degeneracy visible as horizontal lines that don't split. The shapes don't have to be the same just because the energy is.

**Prompt scaffolding (preview of chapter-end LLM exercise):**

1. CLAUDE.md prompt: extend the Brutalist QM coding constitution with rules for this chapter (single SVG primary panel, secondary radial plot underneath, color scale legend top right, sliders to the left, no DOM mutation outside the redraw function, recompute the color domain on every state change, ≤ 3 significant figures on readouts).
2. Simulation prompt (four-move):
   - hook: "render |ψ_nℓm(x, 0, z)|² for the hydrogen atom as a 2D heat map";
   - unfold: "the wave function is R_nℓ(r) Y_ℓm(θ, φ) where R_nℓ involves associated Laguerre polynomials and Y_ℓm involves associated Legendre polynomials; use a numerical library or compute by recursion";
   - mechanism: "let the user dial n, ℓ, m with sliders; show the radial probability P(r) = r² |R_nℓ|² alongside";
   - synthesize: "add an energy-level diagram and let the user click between states; mark ⟨r⟩ and r_mp on the radial plot."
3. Exploration tasks: (a) confirm that the 1s most-probable radius equals a₀ and ⟨r⟩ = 1.5 a₀; (b) count radial and angular nodes for several states and verify n − 1 total; (c) compare 2s and 2p shapes at the same energy; (d) compute the Balmer α wavelength from E_3 − E_2 and confirm against 656.281 nm.
4. Extension prompts: (a) add a transition mode that flags allowed vs. forbidden by the dipole selection rules; (b) add a superposition mode that shows time evolution of a 1s + 2p_z coherent state — the probability cloud oscillates between the two with frequency ω_{12} = (E_2 − E_1)/ℏ.

**Pedagogical-design references:** PhET Hydrogen Atom simulation (Java legacy; HTML5 version status [verify URL: `phet.colorado.edu`]). Falstad's *Hydrogen Atom Applet* (`falstad.com/qmatom`) is a venerable single-developer reference for this kind of visualization. PhET research literature on simulation-based learning in atomic physics (McKagan, Perkins, Wieman, and follow-ups in *American Journal of Physics* and *Physical Review Special Topics — PER*) [verify exact references at draft time].

---

## G. Gaps and flags

**Confidence anchors (high):** The Schrödinger solution of hydrogen is 1926 physics. The radial equation, the Laguerre polynomials, the energy spectrum E_n = −13.6/n² eV, the wave function table, and the Bohr radius a₀ = 0.529 Å can be cited from Griffiths §4.2 without hedging. CODATA values for a₀, the Rydberg constant, and the electron mass should be pulled at draft time for precision claims.

**Items flagged `[verify]`:**

- Schrödinger 1926 *Annalen der Physik* — four papers in the series; the hydrogen wave-mechanical solution is in *Erste* and *Dritte Mitteilung*. Exact volume and page numbers should be confirmed before publishing. `[verify]`
- CODATA 2022 recommended values for a₀, R_∞, R_∞ hc (Rydberg energy in eV), m_e — pull current values at draft time. `[verify]`
- Balmer α (H_α) wavelength 656.281 nm, Lyman α 121.567 nm — verify against NIST atomic spectra database. `[verify]`
- Lamb shift 2s_{1/2} − 2p_{1/2} ≈ 1058 MHz — verify exact value and current QED prediction. `[verify]`
- Proton radius: CODATA 2018 value 0.8414 fm. `[verify]`
- Bezginov et al. 2019 *Science* and Pohl et al. 2010 *Nature* — verify exact volume/page. `[verify]`
- Ahmadi et al. 2018 *Nature* on antihydrogen — same. `[verify]`
- 2s → 1s two-photon transition lifetime ≈ 0.12 s — verify against a primary atomic-physics source. `[verify]`
- PhET Hydrogen Atom simulation URL and current HTML5 / Java status. `[verify]`

**Thinnest section:** the "current state of the field" subsection. The proton radius puzzle, antihydrogen, and Rydberg quantum simulators are each fast-moving fields. The chapter should name two or three pointers and resist surveying. Recommendation: one sentence per pointer, with primary-source citations, and a clear note that the chapter is not the survey.

**Open pedagogical question.** How much of the radial-equation derivation belongs in the chapter body vs. an appendix? Griffiths puts the full Frobenius solution in §4.2.1 main text. The chapter is a second QM course; my reading is that the 1s ansatz (Example 1) belongs in the body as the earned deep-dive, but the general (n, ℓ) Laguerre-polynomial derivation can sit in a "if you want to see the full apparatus" subsection that students can skip. Flag for Nik's review.

**Open pedagogical question 2.** How explicit should the LRL/so(4) discussion be? Pauli's algebraic solution is beautiful and explains the n² degeneracy. But the full algebra is graduate-level. Recommendation: one paragraph in §A.1, framed as "the n² degeneracy has a hidden symmetry, and Pauli used it to solve hydrogen *before* Schrödinger; if you want to see the algebra, look at Pauli 1926." Don't derive it.

**What is *not* in this chapter (defer to later):**

- Fine structure (relativistic correction, spin-orbit, Darwin term) — Ch. 9 (perturbation theory).
- Hyperfine structure (proton-electron magnetic dipole interaction, the 21 cm line) — Ch. 9 or Ch. 13.
- Multi-electron atoms — Ch. 8 (identical particles).
- Lamb shift and QED corrections — Ch. 13 (modern topics) or mention only as a flag.
- Atomic transitions and selection rules — chapter mentions the rules and runs one example; full derivation belongs in Ch. 11 (time-dependent perturbation theory).

**Mechanism the chapter deep-dives on:** the explicit solution of the radial equation for the 1s ground state, including the ansatz u(r) = A r e^(−r/a₀), the consistency condition that fixes a₀, the recovery of E_1 = −13.6 eV, the normalization, and the most-probable-radius vs. expectation-value comparison. From this single worked example the student sees how the entire spectrum is built; the n ≥ 2 cases are quoted and visualized rather than re-derived.

**Voice posture:** the chapter that runs the calculation slowly and refuses to assert what it has not derived. The 1s computation is half a page; the chapter should run it line by line and resist the temptation to abbreviate. The most-probable-radius vs. ⟨r⟩ comparison is the chapter's "look at this trick" moment — same number, two different meanings, and the difference exposes the orbital-as-path picture as the misreading it is.

**Word count target for chapter:** 6,500–8,000. Hydrogen is dense, the misconceptions take real space to dismantle, and the chapter is the central triumph of single-particle QM — earned length.

**Connection forward (Ch. 8):** the chapter ends with the periodic-table preview. Hydrogen's single electron is the foundation; multi-electron atoms require antisymmetry (Ch. 8 setup), Coulomb repulsion (perturbation, Ch. 9), and screening (modifies the central potential and breaks the LRL degeneracy). The visualizer travels forward: in Ch. 8 the student extends it to handle two-electron orbital products and Slater determinants.
