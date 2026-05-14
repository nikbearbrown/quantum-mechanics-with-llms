# Research Notes: Chapter 08 — Identical Particles
**Source:** TIKTOC.md Chapter 08 entry (lines 450–493)
**Notes file:** 08-identical-particles_notes.md
**Corresponding chapter:** chapters/08-identical-particles.md (not yet written)
**Generated:** 2026-05-13

---

## Chapter summary (from TIKTOC.md)

> Identical particles are where quantum mechanics diverges most sharply from classical mechanics. In classical physics, identical objects can always be tracked individually — a label survives. In quantum mechanics, there is no label: two electrons are not "electron A and electron B" but one quantum state of a two-electron system. This leads to symmetrization (bosons) and antisymmetrization (fermions) requirements, the Pauli exclusion principle, and ultimately to the structure of the periodic table. The chapter is conceptually rich but mathematically accessible — the key mathematics is Slater determinants and the symmetrization postulate.

Core concepts named in TIKTOC: indistinguishability; exchange operator P̂₁₂; symmetrization postulate (bosons +1, fermions −1); two-particle wave functions ψ_±(r₁, r₂) = (1/√2)[ψ_a(r₁)ψ_b(r₂) ± ψ_b(r₁)ψ_a(r₂)]; Pauli exclusion as a consequence of antisymmetry; Slater determinants for N fermions; exchange interaction (responsible for ferromagnetism); bosons → Bose-Einstein condensation, photons, phonons; periodic table via Aufbau + Pauli + Hund. Common misconceptions: "identical = very similar" (no — fundamentally indistinguishable); "Pauli is a force / repulsion" (no — a symmetry of the wave function). Worked examples: distinguishable vs. identical particles in a box; Slater determinant for helium 1s 2s; exchange energy from ⟨ψ_−|1/r_12|ψ_−⟩ − ⟨ψ_+|1/r_12|ψ_+⟩.

What the student builds: a two-particle symmetry explorer with three modes (bosons, fermions, distinguishable), choice of single-particle states a and b from an infinite well or harmonic oscillator basis, and a 2D heat map of |ψ(x₁, x₂)|² showing the bosonic bunching, fermionic Pauli node along x₁ = x₂, and the contrast with distinguishable particles.

---

## A. Conceptual foundations

### 1. Indistinguishability is not a measurement limitation

In classical mechanics, two identical billiard balls are still individually trackable. You paint a dot on one at t = 0, follow its trajectory through time, and the dot survives every collision. Identity is preserved by *worldlines*: the function "which particle was this" is continuous along a path, and even if the balls are spectrally identical, an arbitrarily careful observer can keep them sorted.

In quantum mechanics the move is no longer available. The wave function ψ(r⃗₁, r⃗₂) for two particles spreads each over a region of space; the regions overlap; and there is no procedure — even in principle — that can tell you, when a detector clicks at some location, which of the two particles registered. The "labels" 1 and 2 are mathematical bookkeeping for the formalism; they do not correspond to physical identities. The chapter must make this distinction precise: indistinguishability is a statement about *which observables exist*, not about *how well our detectors work*.

Define the **exchange operator** P̂₁₂ on the two-particle Hilbert space by

P̂₁₂ ψ(r⃗₁, r⃗₂) = ψ(r⃗₂, r⃗₁).

Two facts follow immediately:

(a) P̂₁₂² = 𝟙. Swap twice and you are back where you started. So the eigenvalues of P̂₁₂ are ±1.
(b) If the two particles are physically identical, the Hamiltonian Ĥ must be symmetric under their exchange: [Ĥ, P̂₁₂] = 0. So Ĥ and P̂₁₂ share a common eigenbasis. Any energy eigenstate can be chosen to be either symmetric (P̂₁₂ ψ = +ψ) or antisymmetric (P̂₁₂ ψ = −ψ) under exchange.

The chapter must be honest that the symmetric/antisymmetric dichotomy is *postulated* in non-relativistic QM. Why every particle in nature falls into one of those two slots — and which slot — is the **spin-statistics theorem**, proved by Pauli (1940) in relativistic quantum field theory from the requirement that field operators at spacelike separation either commute (integer-spin bosons) or anticommute (half-integer-spin fermions). The undergraduate student should know the theorem exists, that it requires QFT, and that within their current toolkit it is a postulate.

(One-paragraph aside the chapter should include: the ±1 dichotomy is specific to 3+1 dimensions. In 2D systems — fractional quantum Hall fluids, certain topological superconductors — exchange phases other than ±1 are possible, giving rise to *anyons* with statistics that depend continuously on a parameter. Leinaas & Myrheim (1977) first analyzed this; Wilczek (1982) named anyons; direct experimental evidence appeared in Bartolomei et al. (2020) *Science* 368, 173 [verify]. This is a flag, not a section. Our postulate is 3+1-dimensional.)

**Common misconception to correct.** "Two electrons in distant atoms can be told apart because they are localized in different atoms." The correct statement: the exchange symmetry still applies; the multi-electron wave function is still antisymmetric across all labels. The reason exchange effects between distant electrons are *negligible* is that the overlap integral ⟨φ_atom A | φ_atom B⟩ is exponentially small, not that the symmetry stops applying. Indistinguishability is universal; what varies is whether it produces measurable consequences.

**Source anchors:** Griffiths, D. J. (2018). *Introduction to Quantum Mechanics*, 3rd ed., Ch. 5.1 "Two-Particle Systems." Pauli, W. (1940). "The Connection Between Spin and Statistics." *Physical Review* 58, 716–722. Leinaas, J. M. & Myrheim, J. (1977). "On the Theory of Identical Particles." *Il Nuovo Cimento B* 37, 1–23. Wilczek, F. (1982). "Quantum Mechanics of Fractional-Spin Particles." *Physical Review Letters* 49, 957–959 [verify].

### 2. Bosons and fermions — the dichotomy and its statistics

Particles whose multi-particle wave function is symmetric under exchange are **bosons**; particles whose wave function is antisymmetric are **fermions**. Empirically (and provably in QFT):

- **Integer spin** (s = 0, 1, 2, …) → bosons. Photons (s = 1), gluons (s = 1), W and Z (s = 1), Higgs (s = 0), and composite particles built from an even number of fermions (helium-4 = 2 protons + 2 neutrons + 2 electrons = 6 fermions; behaves as a boson).
- **Half-integer spin** (s = 1/2, 3/2, …) → fermions. Electrons (s = 1/2), protons, neutrons, quarks, neutrinos. Composite particles built from an odd number of fermions (helium-3 = 2 protons + 1 neutron + 2 electrons = 5 fermions; behaves as a fermion).

The thermodynamic statistics that follow are different in kind. For an ensemble of N non-interacting indistinguishable particles in thermal equilibrium at temperature T, the average occupation of a single-particle state of energy E_i is

⟨n_i⟩_BE = 1 / (e^((E_i − µ)/k_B T) − 1)    (bosons)

⟨n_i⟩_FD = 1 / (e^((E_i − µ)/k_B T) + 1)    (fermions)

The sign in the denominator is the whole story. At low temperature and high density, bosons crowd into the lowest-energy single-particle state (Bose-Einstein condensation, observed in dilute rubidium-87 vapor by Anderson, Ensher, Matthews, Wieman, Cornell 1995 *Science* 269, 198–201 — Nobel 2001). Fermions stack up one per state, all the way to the Fermi level — electron degeneracy pressure supports white dwarfs (Chandrasekhar 1931 *Astrophysical Journal* 74, 81, "The Maximum Mass of Ideal White Dwarfs" — Nobel 1983); neutron degeneracy pressure supports neutron stars.

The chapter should run the (n_i) formula derivations briefly and connect each to one observable physical consequence: BEC condensation as a Bose-Einstein signature, the Fermi sea + degeneracy pressure as the fermion signature.

**Common misconception to correct.** "Bosons attract; fermions repel." No. There is no *statistical force* — no term in the Hamiltonian that couples to particle identity. What there is, is a correlation in the joint probability density |ψ(r⃗₁, r⃗₂)|² that emerges from the (anti)symmetrization. For two identical fermions in a symmetric spin state, the spatial wave function must be antisymmetric, so |ψ(r⃗₁, r⃗₂)|² → 0 as r⃗₁ → r⃗₂. For two identical bosons, the symmetric spatial wave function makes |ψ|² larger at coincidence than for distinguishable particles. The chapter should name this an **exchange correlation**, not an exchange force. The distinction matters: a student who pictures Pauli as a force will be unable to do the helium calculation (§A.4) cleanly, where the exchange "effect" arises through the Coulomb integral, not through any new term.

**Source anchors:** Griffiths §5.1.2 (statistics). Anderson, M. H. et al. (1995). "Observation of Bose-Einstein Condensation in a Dilute Atomic Vapor." *Science* 269, 198–201. Chandrasekhar, S. (1931). *Astrophysical Journal* 74, 81 [verify exact pages]. Davis, K. B. et al. (1995). "Bose-Einstein Condensation in a Gas of Sodium Atoms." *Physical Review Letters* 75, 3969 [verify].

### 3. Slater determinants — antisymmetry built in

For two identical fermions in single-particle orbitals φ_a and φ_b, the antisymmetric wave function is

ψ_−(1, 2) = (1/√2) [φ_a(1) φ_b(2) − φ_b(1) φ_a(2)].

This is a 2×2 determinant in disguise:

ψ_−(1, 2) = (1/√2) det[ [φ_a(1), φ_b(1)], [φ_a(2), φ_b(2)] ].

For N identical fermions, the generalization is the **Slater determinant** (Slater 1929 *Physical Review* 34, 1293–1322, "The Theory of Complex Spectra"):

ψ(1, 2, …, N) = (1/√N!) det[ φ_i(j) ],

an N×N matrix whose (i, j) entry is the i-th single-particle orbital evaluated at the j-th particle coordinate (including spin). The construction has two pedagogical virtues that the chapter must exploit:

(1) **Antisymmetry is built in.** Swap two particles (two columns of the determinant) → determinant flips sign. The wave function automatically satisfies P̂_ij ψ = −ψ for any pair (i, j). Antisymmetry is a *property of determinants*, not an extra rule.

(2) **Pauli exclusion as a property of determinants.** If two orbitals are identical (two rows of the determinant identical), the determinant is zero. Two fermions cannot occupy the same single-particle state, because the wave function constructed to represent that situation is identically zero — a wave function that is everywhere zero is not a state at all. **Pauli exclusion is a corollary of antisymmetry, not a separate postulate.**

This is the most important pedagogical move in the chapter. Many students have learned Pauli exclusion as "no two electrons can have the same four quantum numbers (n, ℓ, m_ℓ, m_s)" — a rule about labels, with no machinery underneath. The chapter must deliver the deeper version: the wave function is antisymmetric, the Slater determinant enforces this, and putting two fermions in identical states makes the determinant zero. Students who learn Pauli as a rule about quantum numbers stumble in solid-state physics, where the "quantum numbers" are band indices and crystal momenta and the rule has to be re-derived from antisymmetry anyway. Better to deliver it once, correctly, here.

**Where Slater determinants live in real practice.** The Hartree–Fock approximation, the workhorse of computational quantum chemistry, is exactly: "assume the N-electron ground state is a single Slater determinant; minimize ⟨ψ|Ĥ|ψ⟩ variationally over the choice of orbitals φ_i." Every subsequent quantum-chemistry method — configuration interaction, coupled cluster, density functional theory in some readings — is a correction to or generalization of the single-Slater-determinant ansatz. The chapter should name Hartree–Fock without deriving it.

**Source anchors:** Slater, J. C. (1929). "The Theory of Complex Spectra." *Physical Review* 34, 1293–1322. Griffiths §5.2.1 (helium and the Slater determinant). Szabo, A. & Ostlund, N. S. (1996). *Modern Quantum Chemistry*. Dover — the standard Hartree-Fock reference.

### 4. Helium, exchange integrals, and singlet–triplet splitting — the earned deep-dive

Two electrons in the helium atom is the simplest non-trivial multi-fermion problem and the cleanest place to see exchange effects produce a measurable energy splitting. The total electron wave function is a product of a spatial part and a spin part. For two spin-1/2 particles, the spin-state space (4 states total: |↑↑⟩, |↑↓⟩, |↓↑⟩, |↓↓⟩) decomposes by total spin S:

- **Spin singlet** (antisymmetric, S = 0, one state): χ_singlet = (1/√2) (|↑↓⟩ − |↓↑⟩).
- **Spin triplet** (symmetric, S = 1, three states): χ_triplet = |↑↑⟩, (1/√2)(|↑↓⟩ + |↓↑⟩), |↓↓⟩.

The total electron wave function must be antisymmetric under exchange. So:

- Spin singlet (antisymmetric) ⊗ Spatial symmetric → **parahelium**, total wave function antisymmetric. ✓
- Spin triplet (symmetric) ⊗ Spatial antisymmetric → **orthohelium**, total wave function antisymmetric. ✓

The two cases are real, both observed spectroscopically. Helium I (parahelium) and helium II (orthohelium) lines were classified empirically before the antisymmetry framework existed.

**The helium ground state.** Take both electrons in the 1s orbital: φ_a = φ_b = φ_1s. The spatial product φ_1s(r⃗₁) φ_1s(r⃗₂) is symmetric. The antisymmetric counterpart vanishes (Slater determinant with two identical rows). So both electrons can be in 1s *only* via the spin-singlet, spatial-symmetric combination:

ψ_GS(1, 2) = φ_1s(r⃗₁) φ_1s(r⃗₂) × (1/√2)(|↑↓⟩ − |↓↑⟩).

The ground state of helium is parahelium. No orthohelium ground state exists with both electrons in 1s — Pauli forbids it. The lowest orthohelium state must have one electron in 1s and one in 2s (or higher): 1s 2s ³S.

**Zeroth-order energy.** Treat the electrons as non-interacting (drop the e²/(4πε₀ r_12) term). Two hydrogen-like electrons at Z = 2 in 1s each have E_1s = −Z² × 13.6 eV = −54.4 eV. Sum: E₀ = −108.8 eV. The experimental ground-state energy of helium is approximately −79.0 eV. The zeroth-order prediction is off by ≈ +29.8 eV — the electron-electron Coulomb repulsion energy, which we ignored.

**First-order correction: direct and exchange integrals.** Treat V_12 = e²/(4πε₀ |r⃗₁ − r⃗₂|) as a perturbation on the non-interacting Hamiltonian. The first-order energy shift is

ΔE^(1) = ⟨ψ_GS | V_12 | ψ_GS⟩.

For the ground state (both in 1s), the spin part is irrelevant (1/r_12 doesn't act on spin) and we get the single integral

ΔE_GS = ∫∫ |φ_1s(r⃗₁)|² (e²/(4πε₀ r_12)) |φ_1s(r⃗₂)|² d³r₁ d³r₂.

This integral evaluates to (5/8) Z × (e²/(4πε₀ a₀)) = (5/8) × 2 × 27.2 eV = 34.0 eV [verify the 5/8 factor; Griffiths §5.2.1 derives it]. So the first-order corrected energy is E₀ + ΔE_GS ≈ −108.8 + 34.0 = −74.8 eV. Closer to experiment (−79.0), still ≈ 5 eV off. The remaining gap closes with the variational principle (Ch. 9 in this book, or Griffiths Ch. 7) using an effective Z as the variational parameter, giving Z_eff ≈ 27/16 and E ≈ −77.5 eV [verify Griffiths exact value].

**The split for excited states (1s 2s).** Take one electron in 1s, one in 2s. The spatial wave function can be symmetric (parahelium 1s 2s ¹S) or antisymmetric (orthohelium 1s 2s ³S):

ψ_±(r⃗₁, r⃗₂) = (1/√2) [φ_1s(r⃗₁) φ_2s(r⃗₂) ± φ_2s(r⃗₁) φ_1s(r⃗₂)].

The first-order Coulomb correction is

⟨ψ_± | V_12 | ψ_±⟩ = J ± K,

where

J = ∫∫ |φ_1s(r⃗₁)|² (e²/(4πε₀ r_12)) |φ_2s(r⃗₂)|² d³r₁ d³r₂   (**direct / Coulomb integral**)

K = ∫∫ φ_1s*(r⃗₁) φ_2s*(r⃗₂) (e²/(4πε₀ r_12)) φ_2s(r⃗₁) φ_1s(r⃗₂) d³r₁ d³r₂   (**exchange integral**)

J has a classical interpretation: the average Coulomb energy between two charge clouds, one shaped like |φ_1s|² and one like |φ_2s|². The exchange integral K has no classical analog — it arises purely from the antisymmetrization (or symmetrization) of the wave function. For φ_1s and φ_2s real and the Coulomb kernel positive, K > 0. So:

- Spatial-symmetric (parahelium, ¹S): E = E₀ + J + K (higher).
- Spatial-antisymmetric (orthohelium, ³S): E = E₀ + J − K (lower).

**Orthohelium 1s 2s lies below parahelium 1s 2s by 2K.** Experimentally, the 1s 2s ³S state of helium is about 0.80 eV below the 1s 2s ¹S state, both ~ 20 eV above the parahelium ground state [verify exact numbers from NIST atomic spectra database]. The splitting is real, measured, and historically anomalous — at the time of its observation it suggested that "parallel-spin" states were lower in energy, which seemed to imply a spin-dependent force. The post-1925 explanation: there is no spin-dependent force (at this level of approximation); the spins control the spatial symmetry of the orbital part, which controls the Coulomb energy. The chapter should emphasize this. **Spin acts on the spatial geometry, which acts on the Coulomb energy.** That is the chain.

**Hund's first rule** (Hund 1925 *Zeitschrift für Physik* 33, 345–371): for a given configuration, the term with the highest total S has the lowest energy. The chapter should derive Hund's rule for the 1s 2s case as a corollary of antisymmetry: higher spin → symmetric spin state → antisymmetric spatial state → electrons avoid coincidence → lower Coulomb energy. The rule that gets quoted in chemistry is a *consequence* of the symmetry, not a separate physical principle.

**Source anchors:** Griffiths §5.2.1 (helium calculation) and §7.2 (helium variational). Hund, F. (1925). "Zur Deutung verwickelter Spektren, insbesondere der Elemente Scandium bis Nickel." *Zeitschrift für Physik* 33, 345–371. NIST atomic spectra database for helium 1s 2s ¹S − ³S splitting [verify URL].

### 5. The periodic table — antisymmetry + Coulomb + Hund

The architecture of the periodic table — why noble gases are inert, why alkali metals are reactive, why the d-block sits where it does — is the synthesis of three ingredients:

1. **Hydrogenic energy ordering, modified by screening.** Inner electrons screen the nuclear charge, so the effective potential seen by an outer electron is no longer pure 1/r. The screening is weakest for low-ℓ orbitals (which penetrate close to the nucleus) and strongest for high-ℓ orbitals. So at fixed n, low-ℓ states lie below high-ℓ — the n²-degeneracy of pure hydrogen splits. For sodium (Z = 11): 3s lies below 3p lies below 3d; the 3s is the chemically active "valence" orbital. The chapter should plot this splitting.

2. **Pauli exclusion** (antisymmetry → at most one electron per spin-orbital): two electrons per spatial orbital (one m_s = +1/2, one m_s = −1/2). Without Pauli, every electron in every atom would collapse into 1s and chemistry would not exist.

3. **Hund's rule** (from §A.4): for a partially filled subshell, fill different m_ℓ orbitals with parallel spins before pairing. This minimizes Coulomb repulsion through the exchange-integral mechanism.

The **Aufbau** ("building-up") principle compiles these: fill orbitals in order of increasing energy, respecting Pauli, with Hund's rule resolving ties. The **Madelung rule** (Madelung 1936; independently Klechkovskii 1962) gives the empirical filling order — lowest n + ℓ first, ties broken by lowest n: 1s, 2s, 2p, 3s, 3p, 4s, 3d, 4p, 5s, 4d, 5p, 6s, 4f, 5d, 6p, 7s, 5f, 6d, 7p. The chapter should not ask students to memorize Madelung; it should show that screening flips the 4s/3d ordering for low-Z atoms and that the n + ℓ rule is an empirical summary.

**Madelung exceptions.** The rule is not exact. Chromium (3d⁵ 4s¹ instead of the Madelung-predicted 3d⁴ 4s²) and copper (3d¹⁰ 4s¹ instead of 3d⁹ 4s²) are the classic exceptions: the stability of half-filled and fully-filled d-shells outweighs the 4s/3d energy gap. There are roughly twenty such exceptions across the table, mostly in the d- and f-blocks where orbital energies are near-degenerate. The chapter should name a few of these as evidence that Madelung is an empirical rule, not a derived law.

**Intellectual move worth making explicit.** Chemistry is the low-energy effective theory of atoms whose ground states are dictated by fermionic antisymmetry plus Coulomb plus relativistic corrections (for the heaviest atoms; gold's color and mercury's liquid state at room temperature both involve relativistic shifts of valence orbitals). Without antisymmetry, every electron crashes to 1s and there is no periodic table — just N copies of helium with increasing nuclear charge. The chapter is not making a poetic claim; the formal structure of the table really is determined by exchange symmetry + Coulomb.

**Source anchors:** Griffiths §5.2.2 (periodic table). Madelung, E. (1936). *Die mathematischen Hilfsmittel des Physikers*. Berlin: Springer. NIST atomic spectra database for ground-state electron configurations of all elements [verify URL: `nist.gov/pml/atomic-spectra-database`].

---

## B. Domain examples and cases

### Example 1: Two non-interacting particles in a 1D infinite well — distinguishable, boson, fermion

Single-particle eigenstates: φ_n(x) = √(2/L) sin(n π x / L), with E_n = n² π² ℏ² / (2 m L²). Put two particles in states a = 1 and b = 2.

- **Distinguishable particles:** ψ_dist(x₁, x₂) = φ_1(x₁) φ_2(x₂). |ψ_dist|² = |φ_1(x₁)|² |φ_2(x₂)|². No interference.

- **Bosons (symmetric):** ψ_+(x₁, x₂) = (1/√2) [φ_1(x₁) φ_2(x₂) + φ_2(x₁) φ_1(x₂)]. |ψ_+|² peaks along the diagonal x₁ = x₂.

- **Fermions (antisymmetric):** ψ_−(x₁, x₂) = (1/√2) [φ_1(x₁) φ_2(x₂) − φ_2(x₁) φ_1(x₂)]. |ψ_−(x₁, x₁)|² = 0 — the Pauli node. The probability of finding both fermions at the same place vanishes.

A direct calculation (Griffiths §5.1.2, problem set) gives ⟨(x₁ − x₂)²⟩ for each case:

⟨(x₁ − x₂)²⟩_dist = ⟨x²⟩_1 + ⟨x²⟩_2 − 2 ⟨x⟩_1 ⟨x⟩_2,

⟨(x₁ − x₂)²⟩_± = ⟨(x₁ − x₂)²⟩_dist ∓ 2 |⟨x⟩_12|²,

where ⟨x⟩_12 = ⟨φ_1 | x | φ_2⟩. The fermion average squared separation exceeds the distinguishable case; the boson average squared separation falls short. Bosons "bunch," fermions "spread" — without any potential coupling them. Pure exchange correlation, made quantitative.

This calculation is the chapter's cleanest hands-on demonstration of exchange correlation. The simulation will show |ψ_±|² and |ψ_dist|² side-by-side as 2D heat maps in (x₁, x₂) and let the student watch the Pauli node appear, disappear, and become bosonic bunching.

**Source anchors:** Griffiths §5.1.2.

### Example 2: Bose-Einstein condensation in dilute alkali gases

In June 1995 Eric Cornell, Carl Wieman, and collaborators at JILA cooled ~ 2,000 rubidium-87 atoms in a magnetic trap to about 170 nK using laser cooling followed by evaporative cooling, and observed a sharp peak in the time-of-flight momentum distribution — the macroscopic occupation of a single quantum state predicted by Bose-Einstein statistics. The Anderson et al. *Science* paper (269, 198–201) is the canonical reference. Wolfgang Ketterle at MIT produced the second BEC in sodium weeks later (Davis et al. 1995 *PRL* 75, 3969). Nobel 2001 to Cornell, Wieman, Ketterle.

The chapter should walk the composite-particle counting. Rubidium-87: 37 protons + 50 neutrons + 37 electrons = 124 fermions, even, so the composite atom is a boson. (Helium-4: 2 + 2 + 2 = 6 fermions, even, boson. Helium-3: 2 + 1 + 2 = 5 fermions, odd, fermion. The rule.) The simplicity of this counting hides a subtlety: the "composite particle is a boson" statement is exact only when the constituents can be treated as a single inseparable object — at temperatures or densities where individual proton, neutron, and electron exchanges become accessible, the composite picture breaks. At BEC temperatures (10⁻⁷ K), this is overwhelmingly satisfied. At Big-Bang-nucleosynthesis temperatures (10⁹ K), it is not.

### Example 3 (failure case): Pauli exclusion as "repulsion"

A persistent misreading: "Pauli exclusion is what keeps electrons from collapsing into the nucleus / keeps atoms from interpenetrating." The chapter must dismantle this carefully because there is a true statement in the neighborhood and a wrong one.

The wrong statement: "Pauli is a repulsive force between fermions." There is no such force. The Hamiltonian for two non-interacting electrons in a box has no exchange term. The two-electron probability density |ψ_−|² has a node at x₁ = x₂ because of the symmetry of the wave function, not because of any potential energy term.

The right statement: in a many-fermion system, antisymmetry forces the wave function to occupy distinct single-particle states, and the energetic cost of "compressing" the system (squeezing the wave function into smaller spatial volume) rises faster than for distinguishable or bosonic systems because more single-particle modes must be populated. This is **degeneracy pressure** — kinetic in origin, not from any direct exchange potential. Degeneracy pressure is what holds up a white dwarf (electron degeneracy) or a neutron star (neutron degeneracy). Chandrasekhar (1931 *ApJ* 74, 81) showed that this pressure has a relativistic limit: above M ≈ 1.4 M_☉, electron degeneracy fails and the white dwarf collapses. This is the Chandrasekhar limit — a direct astrophysical consequence of the structure of fermionic antisymmetry.

The chapter should be careful: "Pauli prevents collapse" is correct in the degeneracy-pressure sense. "Pauli is a repulsive force" is wrong. They differ in whether there is a term in the Hamiltonian that couples directly to particle identity (there is not) vs. an emergent kinetic-energy cost of compressing antisymmetric wave functions (there is). Make this distinction and the student will never confuse the two again.

**Source anchors:** Chandrasekhar (1931). Lieb, E. H. (1990). "The Stability of Matter: From Atoms to Stars." *Bulletin of the AMS* 22, 1–49 — the rigorous statement of why fermionic antisymmetry is necessary for the stability of bulk matter.

---

## C. Connections and dependencies

**Depends on (earlier chapters):**
- Ch. 1–4: wave functions, Born rule, Hilbert spaces.
- Ch. 5 (3D QM, harmonic oscillator): single-particle eigenstates that get assembled into multi-particle products.
- Ch. 6 (spin): the two-spin singlet/triplet decomposition is the algebraic input that combines with antisymmetry to give the helium spatial-symmetry structure. The chapter cannot start until the student has S = 1/2 and the operator algebra on a two-particle spin Hilbert space.
- Ch. 7 (hydrogen): single-particle hydrogen orbitals are the building blocks for the helium calculation; the chapter assumes fluency with ψ_nℓm and their energies.

**Enables (later chapters):**
- Ch. 9 (perturbation theory): the helium first-order calculation (Example A.4) is the canonical worked example of degenerate perturbation theory. The chapter sets this up; Ch. 9 runs it formally.
- Ch. 10 (variational methods, if present): helium ground state with effective Z as a variational parameter. The chapter motivates this as the obvious next step after first-order is shown to be ≈ 5 eV off.
- Ch. 11+ (multi-electron atoms, molecules, solids): the Slater determinant + Coulomb + exchange machinery is what extends quantum mechanics from one atom to all of chemistry and condensed-matter physics. Hartree-Fock, configuration interaction, DFT — all built on this foundation.
- Ch. 13 (modern topics): Bose-Einstein condensation (Cornell/Wieman/Ketterle), superconductivity (Cooper pairs as composite bosons in the BCS framework), quantum computing on neutral-atom platforms, fractional quantum Hall fluids and anyons.

**Pop-sci linkage:**
- `_lib_QM-Into-the-Light-Beginners.md`: pop-sci treatments of "Pauli says no two electrons can be in the same state" usually omit the antisymmetry derivation. Useful as a reference for what students have already (incompletely) absorbed.
- `_lib_Davies-Demon-in-the-Machine.md`: Davies on collective quantum effects, BEC, and superfluidity — usable as one paragraph of motivation for §A.2.

---

## D. Current state of the field

**Settled:** The spin-statistics theorem is one of the most secure predictions of relativistic QFT. Experimental searches for Pauli-violating transitions (e.g., the VIP and VIP-2 experiments at Gran Sasso, using copper X-ray emission spectra) place limits on the probability of an electron undergoing a Pauli-violating transition at the level of 10⁻²⁹ or better (Curceanu et al. 2017 *Symmetry* 9, 13; Marton et al. 2024 *Physical Review Letters* [verify recent citation]). The fermion/boson dichotomy is universal in 3+1 dimensions, with experimental support spanning many orders of magnitude.

**Active fronts the chapter may flag, not develop:**

- **Anyons in 2D.** Direct evidence for anyonic exchange statistics in the fractional quantum Hall regime: Bartolomei et al. (2020) *Science* 368, 173, "Fractional statistics in anyon collisions"; Nakamura et al. (2020) *Nature Physics* 16, 931, an independent demonstration. The chapter should name these in §A.1's aside, not develop them.

- **Majorana zero modes.** Fermionic excitations predicted at the boundaries of topological superconductors that are their own antiparticles, with non-abelian exchange statistics. Experimental claims have been contentious; Microsoft retracted a major 2018 *Nature* paper in 2022; the field's status in 2026 is unsettled [verify].

- **Topological qubits.** Building on anyons or Majoranas, the goal is a qubit whose error rate is suppressed by topology rather than by error correction. Microsoft Station Q has pursued this for over a decade; no working topological qubit has been demonstrated as of 2026 [verify].

- **Quantum gas microscopes.** Single-site, single-atom imaging of ultracold fermions and bosons in optical lattices (Bakr et al. 2009; Sherson et al. 2010; Cheuk et al. 2015; Parsons et al. 2015) lets experimentalists *directly observe* exchange correlations in real space — anti-bunching for fermions, bunching for bosons — without indirect inference. This is the modern experimental setting where the chapter's textbook claims about |ψ(r⃗₁, r⃗₂)|² become directly measurable. [verify all citations.]

**Source anchors:** Curceanu, C. et al. (2017). *Symmetry* 9, 13 [verify]. Bakr, W. S. et al. (2009). "A quantum gas microscope for detecting single atoms in a Hubbard-regime optical lattice." *Nature* 462, 74–77 [verify].

---

## E. Teaching considerations

**Where students stick:**

1. **"Why does antisymmetry imply Pauli exclusion?"** Many students arrive having learned Pauli as a quantum-number rule and have never been shown the Slater-determinant move. The chapter should make this single algebraic fact — putting two electrons in the same spin-orbital makes the determinant identically zero — the pedagogical center of gravity. Run the 2×2 case explicitly: ψ_−(1, 2) = (1/√2)[φ_a(1)φ_a(2) − φ_a(2)φ_a(1)] = 0.

2. **"What's the difference between Pauli exclusion and Coulomb repulsion?"** Pauli is a statement about the wave function (symmetric/antisymmetric structure); Coulomb is a term in the Hamiltonian (a real potential energy between charges). They are *distinct*, and they *combine* to produce Hund's rule. The helium calculation separates them cleanly: zeroth-order energies are degenerate (no Coulomb); first-order correction with Coulomb splits singlet from triplet; the size of the splitting is 2K (the exchange integral). Most introductory treatments blur these. The chapter must not.

3. **"Why doesn't the periodic table fill 1s, 2s, 2p, 3s, 3p, 3d, 4s, … in straight order?"** Because screening makes high-ℓ orbitals less stable than low-ℓ at the same n: 4s lies below 3d in atoms with low Z. Madelung encodes this empirically. Students should not memorize Madelung; they should understand that screening shifts orbital energies and that the n + ℓ rule is a useful summary.

4. **"Are 'bosons attract' and 'fermions repel' wrong or right?"** Wrong in the literal force sense; cute as a memory aid. Replace with "the joint probability density is enhanced at coincidence for bosons, vanishes at coincidence for fermions — exchange correlation, not exchange force." If students remember only one thing from this chapter, this distinction is the right thing.

5. **"What's the spin-statistics theorem and why doesn't it appear in the chapter as a derivation?"** Because the proof requires QFT (Pauli 1940). The chapter should state the theorem, name Pauli's paper, and assert it as a postulate. Honesty about scope > false confidence.

**Recommended pedagogical moves:**

- Open with the helium spectrum as scene. Before 1925, the singlet–triplet splitting of helium was a phenomenological mystery — "parahelium" and "orthohelium" looked like two different elements. The 1925–1929 development (Heisenberg's 1926 paper on helium as a two-electron exchange problem; Pauli's 1925 exclusion principle; Heitler-London 1927 on the H₂ molecule; Slater 1929 on the determinant) is one of the cleanest historical arcs in physics — a known anomaly, an inventive postulate, a quantitative confirmation. Use it as the chapter's puzzle.

- Run the 2×2 Slater determinant on the page. The chapter's earned deep-dive is the helium calculation: ground state (Pauli forces parahelium), excited state (singlet vs. triplet splitting via the exchange integral). Show the integrals symbolically; quote the numerical values from Griffiths.

- Use the simulation (F.5) for the exchange-correlation visualization. Static figures of |ψ_±(x₁, x₂)|² do not communicate the contrast as well as dragging a slider between "boson," "fermion," "distinguishable" and watching the Pauli node form and vanish.

- End with the periodic-table preview. The chapter is the explanation chemistry students were never given for why the periodic table looks the way it does. Run noble gases, alkali metals, the d-block. Name the Madelung exceptions.

**Exercises to embed:**

- Construct the 2×2 Slater determinant for two electrons in 1s and 2s of helium. Verify antisymmetry under exchange.
- Construct the 3×3 Slater determinant for lithium 1s² 2s¹ (orbitals: 1s↑, 1s↓, 2s↑). Expand explicitly. Verify that swapping any two columns flips the sign.
- For two non-interacting fermions in a 1D infinite well in states n = 1 and n = 2, compute ⟨(x₁ − x₂)²⟩. Compare to distinguishable and bosonic cases.
- For helium 1s 2s, set up the integrals J and K symbolically; identify which one has no classical analog.
- Predict the ground-state electron configuration of carbon. Apply Aufbau, then Hund's rule. Predict the term symbol ³P. Verify against NIST atomic spectra database.
- Why is liquid helium-4 a superfluid below 2.17 K, while liquid helium-3 only becomes superfluid below 2.5 mK? Answer in terms of composite-particle statistics.

---

## F. Library files relevant to this chapter

- **Griffiths, *Introduction to Quantum Mechanics*, 3rd ed.** (`822531304-David-J-Griffiths-Introduction-to-Quantum-Mechanics-Prentice-Hall-1994.txt` — pantry transcript is 1994 1st edition; cross-check §5 numbering against the 3rd edition). Ch. 5 is the spine. §5.1 (two-particle systems, exchange operator), §5.2.1 (helium), §5.2.2 (periodic table). The chapter follows Griffiths' organization.
- **Griffiths Solution Manual** (`993201189-Solution-Manual-Introduction-to-Quantum-Mechanics-3e-Griffiths.txt`) — the helium integrals, the 5/8 factor, and the Hund's-rule application are worked.
- **Liboff, *Introductory Quantum Mechanics*** (`436681929-Introductory-Quantum-Mechanics-by-Richard-L-Liboff-pdf.txt`) — Liboff's Ch. 12 treats identical particles with more explicit construction of the symmetrizer S and antisymmetrizer A operators; useful for students who want the formalism made concrete.
- **Lahiri & Pal, *A First Book of Quantum Field Theory*** (`290663862-A-First-Book-of-Quantum-Field-Theory-Lahiri-Pal.txt`) — useful for the spin-statistics theorem statement and the QFT context. The chapter should not derive it from here, but can point students who want to see it.
- **`_lib_QM-Into-the-Light-Beginners.md`** — pop-sci framing for the periodic-table narrative (assignable motivational reading; the chapter must add the math).
- **`_lib_Davies-Demon-in-the-Machine.md`** — Davies on collective quantum effects (BEC, superfluidity), useful as one-paragraph motivation.
- **`_lib_Penrose-Emperors-New-Mind.md`** — Penrose on spinor exchange under rotation; useful for connecting to the spin-statistics framing.
- **Pop-sci pantry texts** — usually state Pauli as a rule about quantum numbers without deriving from antisymmetry. Reference for what students have read.

---

## F.5 Simulation pedagogy and D3 specifics

**What the simulation must show that prose cannot.** The headline pedagogical fact of this chapter is that exchange correlation is a structure in the *joint* probability density |ψ(x₁, x₂)|², and a structure in a 2D function is invisible in 1D plots. A static rendering in a textbook can show one |ψ_±|² heat map; the simulation must let the student switch between symmetric, antisymmetric, and distinguishable cases — and switch between single-particle state choices — and watch the structure transform. The Pauli node along x₁ = x₂ must appear and vanish under the student's hand.

**Layout (single SVG canvas, multiple panels):**

1. **Primary: 2D heat map of |ψ(x₁, x₂)|² in the (x₁, x₂) plane.** A square grid, say 200 × 200 pixels covering x₁, x₂ ∈ [0, L] for an infinite well or x₁, x₂ ∈ [−5, 5] (in units of the oscillator length) for a harmonic oscillator. Pixel color = |ψ(x₁, x₂)|² via a perceptually uniform color scale (Viridis or Cividis). The diagonal x₁ = x₂ is drawn as a thin overlay line — students can see the Pauli node (zero density) for fermions or the bunching (peak density) for bosons.

2. **Secondary: one-particle reduced density |ρ(x₁)|² = ∫ |ψ(x₁, x₂)|² dx₂.** Plotted as a line plot below the heat map. This is what a single-particle detector would see. Bosons and fermions give the *same* one-particle density (assuming the same single-particle states a, b) — the exchange correlation lives in the *joint* density, not the marginal. The chapter should run this surprise explicitly. The simulation shows the joint heat maps differing dramatically while the marginal line plots are identical. That contrast is itself a pedagogical headline.

3. **Tertiary: control panel.**
   - Particle type: radio buttons for **boson** (symmetric), **fermion** (antisymmetric), **distinguishable**.
   - Single-particle basis: dropdown for **infinite well** or **harmonic oscillator**.
   - State a: slider for n_a ∈ {1, 2, 3, 4, 5}.
   - State b: slider for n_b ∈ {1, 2, 3, 4, 5}.
   - When n_a = n_b and fermion is selected, the simulation must display the *vanishing* wave function and a status note: "ψ_− = 0: Pauli forbidden."

4. **Quaternary: numerical readouts.**
   - ⟨(x₁ − x₂)²⟩ (computed from the wave function on the grid).
   - The maximum value of |ψ(x₁, x₂)|² and where it occurs.
   - The probability of finding both particles in the left half of the box: ∫∫_{x₁, x₂ < L/2} |ψ|² dx₁ dx₂.
   - All to ≤ 3 significant figures, monospaced, no animation.

**Spin extension toggle.** A second mode adds the spin part. For two spin-1/2 particles, the user selects spin singlet (antisymmetric spin) or spin triplet (symmetric spin). The simulation then enforces total antisymmetry: singlet ⊗ symmetric-spatial or triplet ⊗ antisymmetric-spatial. Pick singlet with n_a = n_b: both electrons can occupy the same spatial state because the spin part is antisymmetric — and the simulation shows the (symmetric-spatial) heat map. Pick triplet with n_a = n_b: the spatial part must be antisymmetric and identical, hence zero. The status note tells the student: "Triplet with both electrons in the same orbital is Pauli-forbidden." This is the chapter's deepest demonstration — antisymmetry on the *combined* wave function, with the spin and spatial parts trading symmetry.

**D3 idioms appropriate to this chapter:**

- `d3.scaleSequential(d3.interpolateViridis)` for the heat map. Recompute domain on every state change.
- SVG `<rect>` elements for the heat map (200 × 200 = 40,000 rects — D3 handles it but a `<canvas>` would be faster; brutalist principle prefers SVG for clarity).
- `d3.line()` for the marginal density plot.
- Radio buttons and dropdowns as plain HTML form elements positioned absolutely over the SVG (do not try to build form controls inside SVG).
- `d3.format(".3g")` for numeric readouts.

**Honesty about what the simulation does not show:**

- **Three-or-more particle Slater determinants.** The simulation handles N = 2 cleanly. For N = 3 (lithium ground state), the wave function lives in a 3D space (x₁, x₂, x₃) which is hard to visualize as a heat map. The chapter should run the 3×3 Slater determinant as a worked example in prose; the simulation stays at N = 2.

- **Realistic Coulomb interaction.** The simulation visualizes the *non-interacting* two-particle wave function. The helium calculation (§A.4) involves the Coulomb integral and the exchange integral; these are computed in the chapter prose, not in the simulation. An extension prompt could add a slider for an interaction strength λ and let the student watch the wave function deform; this is recommended but optional.

- **Composite-particle counting.** The chapter discusses helium-4 vs. helium-3 as composite boson vs. composite fermion. The simulation does not model this; the rule (count constituent fermions, even → boson, odd → fermion) is asserted in prose.

**Why this simulation matters more than text.** Three things only become natural by doing them:

- **The Pauli node.** Set particle type = fermion, n_a = 1, n_b = 2. The diagonal x₁ = x₂ is a stripe of zero. Now set n_a = n_b = 1. The wave function vanishes entirely (the simulation displays "ψ = 0"). Then switch to boson: now both electrons in the same state is fine and the wave function has its maximum on the diagonal. The student sees Pauli emerge as a property of the antisymmetric construction, not as a separate rule.

- **Marginals don't reveal exchange.** Compare boson, fermion, distinguishable cases at the same (a, b). The marginal line plot at the bottom is identical across all three; the joint heat map at the top differs dramatically. This is the chapter's "what is and is not a single-particle observable" lesson, made visible.

- **Singlet vs. triplet for helium.** In spin-extension mode, the student selects singlet + (1s, 2s) and sees a symmetric spatial wave function — electrons can be close together. Then triplet + (1s, 2s): antisymmetric spatial — electrons avoid each other, lower Coulomb energy if they were interacting. The triplet's spatial separation is the geometric origin of Hund's rule.

**Prompt scaffolding (preview of chapter-end LLM exercise):**

1. CLAUDE.md prompt: extend the Brutalist QM coding constitution with rules for this chapter (single SVG primary panel, marginal line plot underneath, control panel as plain HTML to the side, no DOM mutation outside redraw, status text for "ψ = 0" cases, recompute color domain per state change).
2. Simulation prompt (four-move):
   - hook: "render |ψ_±(x₁, x₂)|² for two particles in a 1D infinite well";
   - unfold: "build ψ_±(x₁, x₂) = (1/√2)[φ_a(x₁) φ_b(x₂) ± φ_b(x₁) φ_a(x₂)] from infinite-well eigenstates φ_n(x) = √(2/L) sin(n π x / L)";
   - mechanism: "let the user select particle type (boson, fermion, distinguishable), state quantum numbers n_a and n_b, and watch the heat map and marginal plot update";
   - synthesize: "add the spin-extension mode that combines singlet/triplet spin with symmetric/antisymmetric spatial."
3. Exploration tasks: (a) verify the Pauli node along x₁ = x₂ for fermions with n_a ≠ n_b; (b) verify ψ = 0 for fermions with n_a = n_b; (c) compare the joint heat maps and marginal line plots for boson, fermion, distinguishable at fixed (n_a, n_b) — confirm marginals are identical; (d) compute ⟨(x₁ − x₂)²⟩ for the three cases and confirm ⟨...⟩_fermion > ⟨...⟩_dist > ⟨...⟩_boson.
4. Extension prompts: (a) add an interaction term V_int = λ δ(x₁ − x₂) and diagonalize the two-particle Hamiltonian numerically; (b) extend to N = 3 by computing the 3×3 Slater determinant for three particles in n = 1, 2, 3 and visualizing pair-correlation cuts; (c) add a Hartree-Fock mode for the helium ground state that minimizes the energy over Slater-determinant orbitals (this is more ambitious; recommended for advanced students).

**Pedagogical-design references:** No widely-known PhET simulation covers this material directly; this chapter's visualization is more original than the Stern-Gerlach simulator (Ch. 6) or the hydrogen visualizer (Ch. 7). Closest references: the "Quantum Bound States" PhET simulation (single-particle, but shows wave-function structure) and various Jupyter notebooks from the Quantum Optics & Quantum Information Toolbox (QuTiP) tutorials [verify URL]. PhET research findings on simulation-based learning of multi-particle quantum mechanics are thin; the field has good single-particle visualizations and few two-particle ones. This chapter's simulation is a contribution to the genre.

---

## G. Gaps and flags

**Confidence anchors (high):** The non-relativistic identical-particles formalism is 1925–1929 physics. The exchange operator, the symmetrization postulate, the Slater determinant, the helium first-order calculation, the Hund's-rule derivation can be cited from Griffiths §5 without hedging. The spin-statistics theorem (Pauli 1940) is one of the most well-tested predictions in physics, but its proof requires QFT and the chapter must postulate the bosons/fermions correspondence rather than derive it.

**Items flagged `[verify]`:**

- The 5/8 factor in the helium first-order direct integral — verify against Griffiths §5.2.1. `[verify]`
- Helium 1s 2s ¹S − ³S splitting numerical value (≈ 0.80 eV) — verify against NIST atomic spectra database. `[verify]`
- VIP-2 collaboration upper bound on Pauli violation probability — pull most recent published limit (likely 2023 or 2024). `[verify]`
- Bartolomei et al. 2020 *Science* and Nakamura et al. 2020 *Nature Physics* on anyon experiments — verify exact volume/page. `[verify]`
- Anderson et al. 1995 *Science* on rubidium BEC — verify pages (198–201). `[verify]`
- Chandrasekhar 1931 *ApJ* — verify exact pages. `[verify]`
- Bakr et al. 2009 quantum gas microscope — verify *Nature* citation. `[verify]`
- Pauli 1940 *Physical Review* — verify pages 716–722. `[verify]`
- Madelung 1936 — verify primary citation in *Die mathematischen Hilfsmittel*. `[verify]`
- Slater 1929 *Physical Review* 34 — verify pages 1293–1322. `[verify]`

**Thinnest section:** the "current state of the field" subsection. Anyons, Majoranas, and topological qubits are hot topics with rapidly shifting status. The chapter should name them as pointers, give one primary citation each, and resist surveying. Recommendation: one paragraph total for §D's "active fronts" block, not three.

**Open pedagogical question 1.** Should the chapter introduce second quantization (creation and annihilation operators a†_i, a_i with anticommutators {a_i, a_j†} = δ_ij for fermions, commutators for bosons)? Recommendation: no. Second quantization is the next natural step but belongs in a graduate QM course or a many-body course. The chapter stays in first quantization with Slater determinants. Flag for Nik's review.

**Open pedagogical question 2.** How much Hartree-Fock to introduce? Recommendation: name it ("the single-Slater-determinant variational ansatz, when minimized over orbitals, is the Hartree-Fock approximation") but do not develop the equations. The chapter is QM, not computational chemistry.

**Open pedagogical question 3.** Should the chapter include the explicit derivation of the singlet/triplet decomposition of two spin-1/2 particles? Or should it cite Ch. 6 and proceed? Recommendation: include a brief recap, two paragraphs, because the singlet/triplet decomposition is the algebraic input the helium calculation directly uses. Students may have studied Ch. 6 weeks ago.

**What is *not* in this chapter (defer to later):**

- Second quantization, creation/annihilation operators — beyond this book or in Ch. 13.
- Hartree-Fock equations and self-consistent field methods — computational chemistry, beyond this book.
- The full spin-statistics theorem proof — requires QFT.
- Fractional statistics, anyons, braid-group representations — Ch. 13 pointer only.
- BCS theory of superconductivity, BEC-BCS crossover — Ch. 13.
- Quantum Hall effect, topological band theory — Ch. 13 or graduate-level.

**Mechanism the chapter deep-dives on:** the helium singlet–triplet splitting calculation. From the antisymmetry requirement on the total wave function, decompose into spin singlet × spatial symmetric (parahelium) and spin triplet × spatial antisymmetric (orthohelium). Compute the first-order Coulomb correction in both cases and extract the direct integral J and the exchange integral K. Show that the singlet–triplet energy splitting is 2K. From this single calculation the student sees (a) why Pauli forces parahelium for the helium ground state, (b) why orthohelium 1s 2s lies below parahelium 1s 2s (Hund's rule), and (c) how spin acts on the spatial geometry to control Coulomb energy — the conceptual headline that makes all of chemistry work.

**Voice posture:** the chapter that resists the temptation to call Pauli a "force." Make the antisymmetry-vs.-Hamiltonian distinction in body paragraphs and reinforce it through the simulation. The chapter is the place where students learn what a *symmetry* of the wave function does — and what it does not do.

**Word count target for chapter:** 6,000–7,500. Identical-particles arguments require careful definitional work (what's the exchange operator, why ±1, why is Pauli a corollary), and the helium calculation is the chapter's earned deep-dive. Hund's rule and the periodic-table preview deserve real space.

**Connection forward (Ch. 9):** the chapter ends having set up the apparatus (antisymmetric wave functions, Slater determinants, Coulomb integrals, exchange integrals) but having only run first-order perturbation on it. Ch. 9 introduces time-independent perturbation theory formally and applies it to the helium calculation more carefully, to the fine structure of hydrogen, and to the Stark and Zeeman effects. The visualizer travels forward: in Ch. 9 the student extends it to handle the variational ground state of helium with an effective Z parameter.
