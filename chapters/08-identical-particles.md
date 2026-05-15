# Chapter 8 — Identical Particles
*One symmetry requirement, and the periodic table falls out.*

Helium has two electrons. Lithium has three. Carbon has six. You might think the important question, once you have solved hydrogen exactly, is how to handle the electron-electron Coulomb repulsion — the $e^2/(4\pi\epsilon_0|\vec{r}_1 - \vec{r}_2|)$ term that makes multi-electron atoms analytically intractable. That is a real difficulty, and we will meet it.

But there is a prior question, one that doesn't even appear in the hydrogen calculation because hydrogen has only one electron: when you write down a wave function for two electrons, what constraints does it have to satisfy? The answer to that question is what this chapter is about. And the constraints turn out to be more powerful than the Coulomb problem — they are what builds the periodic table.

---

## What "identical" means, and why it matters

In classical mechanics, two identical objects can always be tracked individually. Paint a dot on one billiard ball. Even without the dot, you could in principle follow both balls through every collision, because their trajectories are continuous and never disappear between observations. "Particle 1" and "particle 2" are labels you can always cash out by following the worldlines.

In quantum mechanics this fails. The wave function $\psi(\vec{r}_1, \vec{r}_2)$ for two electrons spreads each of them over a region of space. The regions overlap. When a detector fires at some location, there is no fact about which electron triggered it. The labels "1" and "2" we write into the wave function are mathematical bookkeeping. They cannot be cashed out by any measurement in principle, not just any measurement in practice. The Hamiltonian for two identical particles is symmetric under their exchange — it contains $\hat{p}_1^2/2m + \hat{p}_2^2/2m + V_{12}(|\vec{r}_1 - \vec{r}_2|)$, all unchanged if you swap the subscripts — so the physics literally does not distinguish the two labels.

This isn't a philosophical point about measurement. It's a structural constraint on which wave functions are physically allowed. Define the **exchange operator**:

$$\hat{P}_{12}\,\psi(\vec{r}_1, \vec{r}_2) = \psi(\vec{r}_2, \vec{r}_1).$$

Apply it twice: $\hat{P}_{12}^2 = \mathbb{1}$. So $\hat{P}_{12}$ has eigenvalues $\lambda$ satisfying $\lambda^2 = 1$: only $\lambda = +1$ or $\lambda = -1$. Since $[\hat{H}, \hat{P}_{12}] = 0$ for identical particles, every energy eigenstate can be chosen to have definite exchange symmetry — either symmetric ($+1$) or antisymmetric ($-1$). And once a state has definite exchange symmetry, it keeps it: the symmetry is conserved.

The empirical fact, elevated to a postulate in non-relativistic quantum mechanics: every species of particle in 3+1 dimensions is one or the other, permanently.

- **Bosons**: symmetric wave function under exchange, $\hat{P}_{12}\psi = +\psi$. Integer spin: photons, the Higgs boson, $^4$He atoms.
- **Fermions**: antisymmetric wave function under exchange, $\hat{P}_{12}\psi = -\psi$. Half-integer spin: electrons, protons, neutrons, quarks.

The connection between spin and statistics — why integer spin forces bosons and half-integer forces fermions — is the spin-statistics theorem, proven by Pauli in 1940 from relativistic quantum field theory. The proof is not available to us yet. We accept it as a postulate here and note where the deeper explanation lives.

<!-- → [TABLE: Particle statistics summary — rows: photon, electron, proton, neutron, ⁴He atom, ⁸⁷Rb atom; columns: spin, constituent fermion count, boson or fermion, key observable consequence (BEC, Pauli exclusion, superfluid transition temperature); student should see the composite-particle counting rule applied concretely] -->

Composite particles inherit their statistics by counting constituent fermions: even number → boson, odd number → fermion. $^4$He is 2 protons + 2 neutrons + 2 electrons = 6 fermions, even, so $^4$He is a boson. $^3$He has 5 fermions, odd, so $^3$He is a fermion. Below 2.17 K, $^4$He becomes a superfluid. $^3$He requires 2.5 mK and the formation of Cooper pairs before it superfluids. Three orders of magnitude in temperature, from a single parity. That is how much this symmetry matters.

---

## Antisymmetry built into the wave function

For two identical fermions occupying single-particle states $\phi_a$ and $\phi_b$, the antisymmetric wave function is:

$$\psi_-(1,2) = \frac{1}{\sqrt{2}}\bigl[\phi_a(1)\phi_b(2) - \phi_b(1)\phi_a(2)\bigr].$$

Check it: $\hat{P}_{12}\psi_-(1,2) = \psi_-(2,1) = -\psi_-(1,2)$. Antisymmetric by inspection. John Slater noticed in 1929 that this can be written as a determinant:

$$\psi_-(1,2) = \frac{1}{\sqrt{2}}\det\begin{pmatrix}\phi_a(1) & \phi_b(1) \\ \phi_a(2) & \phi_b(2)\end{pmatrix}.$$

Swapping particles swaps rows. Swapping rows flips the sign of a determinant. Antisymmetry is now a property of the matrix structure, not something you have to enforce by hand.

<!-- → [INFOGRAPHIC: Visual derivation of the 2×2 Slater determinant — show the matrix with labeled entries φ_a(1), φ_b(1), φ_a(2), φ_b(2); expansion into two terms with a minus sign; arrow showing that swapping rows 1↔2 (particles 1↔2) produces the negative; caption: "The antisymmetry is in the algebra of the matrix, not imposed on the wave function by hand"] -->

The construction extends to $N$ fermions. Write down an $N \times N$ matrix where entry $(i,j)$ is the $i$-th single-particle orbital evaluated at the $j$-th particle's coordinates. Take the determinant. Divide by $\sqrt{N!}$. The result is the **Slater determinant**:

$$\psi(1, 2, \ldots, N) = \frac{1}{\sqrt{N!}} \det\begin{pmatrix} \phi_1(1) & \phi_2(1) & \cdots & \phi_N(1) \\ \phi_1(2) & \phi_2(2) & \cdots & \phi_N(2) \\ \vdots & \vdots & \ddots & \vdots \\ \phi_1(N) & \phi_2(N) & \cdots & \phi_N(N) \end{pmatrix}.$$

Swapping any two particles swaps two rows and flips the sign — antisymmetric under any pairwise exchange. The $N = 3$ expansion is six terms with alternating signs, one for each permutation of the three particle labels weighted by the sign of that permutation.

This is the wave function ansatz on which all of computational quantum chemistry is built. Hartree-Fock theory — the workhorse of molecular quantum mechanics — minimizes $\langle\psi|\hat{H}|\psi\rangle$ over the choice of single-particle orbitals $\phi_i$, with the $N$-electron wave function constrained to be a single Slater determinant. Configuration interaction, coupled-cluster theory, and many density-functional approaches are all either corrections to or generalizations of this starting point. When a computational chemist reports the binding energy of a drug candidate to its target protein, the calculation rests on the construction in the equation above.

---

## Pauli exclusion as a corollary

Here is the move. Suppose two of the single-particle orbitals are identical: $\phi_i = \phi_j$ for some $i \neq j$. Then two columns of the Slater determinant are identical. A determinant with two identical columns is exactly zero. The wave function vanishes — not approximately, not in some limit — identically, everywhere in configuration space.

A wave function that is zero everywhere cannot be normalized: $\int 0\,d^Nr = 0 \neq 1$. It is not a state. So we cannot put two fermions in the same single-particle orbital, because the wave function we would write down to represent that situation doesn't exist.

This is the **Pauli exclusion principle**. Wolfgang Pauli stated it in 1925 as an empirical rule — no two electrons in an atom can share the same set of quantum numbers $(n, \ell, m_\ell, m_s)$ — because it explained the periodic table and he could not find a reason to reject it. He received the Nobel Prize in 1945 partly for it. But as he stated it, the rule was a phenomenological postulate with no derivation. Slater showed four years later that it isn't a postulate at all. It is a property of determinants. It follows from antisymmetry, which follows from the symmetrization postulate.

The reason to understand the deeper version — antisymmetry rather than quantum numbers — is that the quantum numbers $(n, \ell, m_\ell, m_s)$ are labels for single-particle hydrogenic orbitals, specific to atoms. When you move to a solid-state system, the relevant labels become band indices and crystal momenta. The rule derived from antisymmetry survives unchanged in both contexts. Understanding antisymmetry once is better than memorizing the atomic version and re-deriving it by analogy later.

---

## Helium and the exchange integral

The helium spectrum, by the early 1920s, had been catalogued in fine detail. There were two distinct families of spectral lines — one called parahelium, one called orthohelium — with different transition rates, different selection rules, different fine-structure patterns. They looked like spectra of two different elements. But helium is helium: one nuclear charge, two electrons, one element.

Werner Heisenberg resolved this in 1926. The two-electron wave function is a product of a spatial part and a spin part, and the total must be antisymmetric under exchange. From Chapter 6, the two-spin states decompose into a spin singlet (antisymmetric, $S = 0$) and a spin triplet (symmetric, $S = 1$). So there are exactly two ways to build an antisymmetric total wave function:

- **Parahelium**: symmetric spatial wave function $\times$ antisymmetric spin (singlet). $S = 0$.
- **Orthohelium**: antisymmetric spatial wave function $\times$ symmetric spin (triplet). $S = 1$.

Both are legitimate antisymmetric total wave functions. Both are physically realizable. Both produce distinct spectral families. The "two elements" are the same element in two different exchange-symmetry sectors.

<!-- → [INFOGRAPHIC: Helium symmetry sectors — two-column diagram; left column "Parahelium": spatial symmetric ψ₊ (blob + blob with equal lobes), spin singlet ↑↓−↓↑, S=0, ground state accessible; right column "Orthohelium": spatial antisymmetric ψ₋ (blob with node between lobes), spin triplet ↑↑/↑↓+↓↑/↓↓, S=1, no 1s² ground state; caption: "Not two elements — one element in two exchange-symmetry sectors, separated by the requirement that the total wave function be antisymmetric"] -->

The first consequence: the helium ground state is parahelium. Try to put both electrons in the 1s orbital — the antisymmetric spatial construction $\phi_{1s}(\vec{r}_1)\phi_{1s}(\vec{r}_2) - \phi_{1s}(\vec{r}_2)\phi_{1s}(\vec{r}_1)$ vanishes identically (Pauli). So the ground state must be the symmetric spatial construction paired with the spin singlet. The lowest orthohelium state requires one electron in 1s and one in 2s, at minimum. No orthohelium ground state exists.

Now the energy. Take the excited 1s2s configuration and ask what the Coulomb repulsion $V_{12} = e^2/(4\pi\epsilon_0|\vec{r}_1-\vec{r}_2|)$ does to the two symmetry sectors. At first order in perturbation theory:

$$\langle\psi_\pm|V_{12}|\psi_\pm\rangle = J \pm K,$$

where

$$J = \iint |\phi_{1s}(\vec{r}_1)|^2\frac{e^2/(4\pi\epsilon_0)}{|\vec{r}_1-\vec{r}_2|}|\phi_{2s}(\vec{r}_2)|^2\,d^3r_1\,d^3r_2$$

is the **direct integral** — the classical Coulomb interaction between two charge densities shaped like $|\phi_{1s}|^2$ and $|\phi_{2s}|^2$. A classical physicist could write this.

$$K = \iint \phi_{1s}^*(\vec{r}_1)\phi_{2s}^*(\vec{r}_2)\frac{e^2/(4\pi\epsilon_0)}{|\vec{r}_1-\vec{r}_2|}\phi_{2s}(\vec{r}_1)\phi_{1s}(\vec{r}_2)\,d^3r_1\,d^3r_2$$

is the **exchange integral**. It has no classical analog whatsoever. It comes entirely from the cross-terms generated by antisymmetrizing the wave function — terms that mix which electron is "in 1s" and which is "in 2s." For real orbitals and the positive Coulomb kernel, $K > 0$.

The result: parahelium 1s2s gets energy $E^{(0)} + J + K$; orthohelium 1s2s gets $E^{(0)} + J - K$. Since $K > 0$, orthohelium lies lower by $2K$. The experimental splitting is about 0.80 eV — a real, large, measurable energy difference that historically seemed to require a spin-dependent force, because before 1925 nobody knew about antisymmetry.

<!-- → [CHART: Helium 1s2s energy level diagram — horizontal lines for parahelium ¹S (higher, labeled E⁰+J+K) and orthohelium ³S (lower, labeled E⁰+J−K); vertical double-headed arrow labeled "2K ≈ 0.80 eV"; a second pair of lines below showing the 1s² ground state (parahelium only, spin singlet); caption: "The 2K splitting has no classical origin — it is the direct fingerprint of the exchange integral in the antisymmetrized wave function"] -->

There is no spin-dependent force. There is no exchange force of any kind. The Hamiltonian contains no term that distinguishes spin states at this order. The mechanism is purely geometric: the antisymmetric spatial wave function forces the two electrons to avoid coinciding in space (the wave function vanishes at $\vec{r}_1 = \vec{r}_2$). Electrons that avoid each other see less Coulomb repulsion. Less Coulomb repulsion means lower energy. Spin controls the symmetry of the spin part of the wave function, which forces the symmetry of the spatial part (because the total must be antisymmetric), which determines how close the electrons get, which sets the Coulomb energy. The chain runs through the spatial wave function, not through any spin interaction.

This mechanism is Hund's first rule. In 1925, Friedrich Hund catalogued an empirical pattern in atomic spectra: for a given electron configuration, the term with highest total spin $S$ has the lowest energy. The mechanism just derived is the explanation. Higher $S$ → more symmetric spin state → more antisymmetric spatial state → electrons keep farther apart → lower Coulomb repulsion. Hund's rule, like Pauli's rule, is not a separate postulate. It is a corollary of antisymmetry.

---

## The periodic table

Three facts combine to produce the structure of the periodic table. You now have all three.

**Fact one: hydrogenic energy ordering, modified by screening.** In a multi-electron atom, inner electrons partially shield the nuclear charge from outer electrons. The shielding is least effective for orbitals that penetrate close to the nucleus (low $\ell$, which have significant probability density near $r = 0$) and most effective for orbitals that stay far out (high $\ell$). At fixed principal quantum number $n$, low-$\ell$ states lie below high-$\ell$ states — the $n^2$-fold Coulomb degeneracy of Chapter 7 breaks as soon as the potential departs from pure $1/r$. The 2s lies below 2p in lithium and every heavier atom. The 3s lies below 3p lies below 3d in sodium and every heavier atom.

<!-- → [CHART: Radial probability density P(r) = r²|R_{nℓ}(r)|² for 3s, 3p, and 3d overlaid on one plot — student should see that 3s has the most probability density near the nucleus (highest penetration, least screened), 3d the least; caption: "Screening breaks the n²-fold hydrogen degeneracy: orbitals that penetrate closer to the nucleus are less shielded and fall lower in energy"] -->

**Fact two: Pauli exclusion.** Each spatial orbital can hold at most two electrons — one with $m_s = +1/2$, one with $m_s = -1/2$. This is the corollary of antisymmetry we derived two sections ago. Without it, every electron in every atom would collapse to the 1s orbital and there would be no chemistry. The diversity of chemical behavior — the difference between lithium and neon, between iron and argon, between carbon's four bonds and helium's zero — is entirely the consequence of this constraint derived from a determinant.

**Fact three: Hund's rule.** Within a partially filled subshell, fill different $m_\ell$ orbitals with parallel spins before pairing electrons into the same orbital. The mechanism is the exchange integral argument: high spin → antisymmetric spatial state → electrons avoid each other → lower Coulomb energy. Oxygen's ground state has two unpaired electrons in the $2p$ subshell rather than one pair and one single, because the parallel-spin configuration is lower in energy by $2K$.

<!-- → [INFOGRAPHIC: Aufbau filling diagram for the first 18 elements — orbital boxes arranged in energy order (1s, 2s, 2p, 3s, 3p); arrows showing electron fill direction for H through Ar, with Hund's rule visible in N (three half-filled 2p boxes) and O (one paired + two half-filled); row lengths 2, 8, 8 labeled; caption: "Each row ends when a subshell is completely filled — two electrons per orbital (Pauli), parallel spins first (Hund)"] -->

Combine the three facts through the **Aufbau principle**: fill orbitals in order of increasing energy, two electrons per orbital (Pauli), with Hund's rule resolving choices within a subshell. The empirical ordering follows the Madelung rule — lowest $n + \ell$ first, ties broken by lowest $n$ — giving the sequence $1s, 2s, 2p, 3s, 3p, 4s, 3d, 4p, 5s, 4d, \ldots$ The row lengths 2, 8, 8, 18, 18, 32 are $2(2\ell+1)$ summed over the subshells in each period — twice the orbital degeneracy, because of spin.

About twenty atoms violate Madelung. Chromium ($3d^5\,4s^1$ instead of the predicted $3d^4\,4s^2$) and copper ($3d^{10}\,4s^1$ instead of $3d^9\,4s^2$) are the canonical cases: the exchange-energy stabilization of a half-filled or completely filled $3d$ subshell beats the small energy gap between 3d and 4s in those atoms. These are not anomalies in the framework; they are cases where Hund competes with Madelung and Hund wins by a small margin. The framework handles them; the simple mnemonic does not.

The periodic table is not a catalogue of empirical facts that happens to have a pattern. It is a theorem about antisymmetric wave functions, screened Coulomb potentials, and first-order perturbation theory. This is what the calculation shows.

---

## Bosons, briefly

Bosons have symmetric wave functions. Nothing prevents two — or $10^{23}$ — bosons from occupying the same single-particle state. At low temperature and high density, a macroscopic fraction can pile into the lowest-energy state: Bose-Einstein condensation. The first experimental BEC in a dilute gas was achieved at JILA in 1995 by Cornell, Wieman, and colleagues, cooling $^{87}$Rb to about 170 nK. Nobel Prize 2001 to Cornell, Wieman, and Ketterle.

One misconception worth naming here: bosons are not attracted to each other and fermions are not repelled by each other in the sense of forces. There is no term in the Hamiltonian corresponding to exchange statistics. What exists is a correlation in the joint probability density $|\psi(\vec{r}_1, \vec{r}_2)|^2$ that emerges from symmetrization: fermions show a Pauli node at $\vec{r}_1 = \vec{r}_2$; bosons show enhanced probability there. No force — a correlation. The simulation below makes this concrete: cycle through boson, fermion, and distinguishable particles at the same single-particle states, and the joint density changes dramatically. The marginal one-particle density does not change at all. If there were a force, the single-particle observable would differ. It doesn't.

<!-- → [IMAGE: Three 2D heat maps of |ψ(x₁,x₂)|² side by side for n_a=1, n_b=2 — left: distinguishable (asymmetric pattern); center: boson/symmetric (enhanced along x₁=x₂ diagonal); right: fermion/antisymmetric (dark Pauli node stripe along x₁=x₂ diagonal); below each: identical marginal density plot ρ(x₁); caption: "The joint density encodes exchange statistics; the marginal does not. A single-particle detector cannot tell boson from fermion."] -->

The fermionic correlation — the Pauli node — is also what holds up dead stars. Electrons in a white dwarf cannot pile into the same single-particle state. As the star contracts, electrons are forced into higher-energy states, raising the total kinetic energy and producing an outward **degeneracy pressure** with no thermal origin. Chandrasekhar showed in 1931 that this pressure has a relativistic limit at about $1.4\,M_\odot$: the Chandrasekhar mass. Above that mass the electrons become relativistic, the relativistic degeneracy pressure cannot hold back gravity, and the white dwarf collapses. The exclusion principle sets a ceiling on how much mass a dead star can carry. Chandrasekhar did this calculation at age 19 on a boat from India to England; he received the Nobel Prize for it in 1983.

---

## Still puzzling

I can trace the chain clearly: the periodic table follows from Pauli exclusion, Pauli exclusion follows from the vanishing of the Slater determinant, the determinant vanishes from antisymmetry, antisymmetry follows from the symmetrization postulate together with the spin-statistics theorem. What I cannot do is make the spin-statistics theorem feel inevitable from non-relativistic principles. Pauli's 1940 proof invokes microcausality — field operators at spacelike separation must commute or anticommute to preserve causality — and from there derives that integer-spin fields must commute (bosons) and half-integer-spin fields must anticommute (fermions). I can follow the steps. Whether microcausality is itself a foundational axiom or is derivable from something more primitive, I do not know. The chain runs clearly from antisymmetry downward to the periodic table. What lies beneath antisymmetry is a harder question.

---

## LLM Exercise — Building the Two-Particle Symmetry Explorer

You are going to build a simulation that visualizes the joint probability density $|\psi(x_1, x_2)|^2$ for two particles in a 1D infinite well or harmonic oscillator, with a toggle for boson / fermion / distinguishable. The Pauli node along $x_1 = x_2$ for fermions, the boson clustering on the same diagonal, and the contrast with distinguishable particles — all appear in real time as the user drags sliders.

### The CLAUDE.md prompt

Append this to your project's `CLAUDE.md`:

```
## Chapter 8 — Two-Particle Symmetry Explorer Rules

- Single HTML file, single SVG canvas. D3 v7 only.
- Layout:
  - Primary 2D heat map of |ψ(x₁, x₂)|² (top, ~400 × 400 px square).
  - Marginal one-particle density |ρ(x₁)|² = ∫|ψ(x₁, x₂)|² dx₂ as a line plot
    directly below (~400 × 150 px).
  - Control panel as plain HTML to the right.
- Color scale: d3.interpolateViridis, sequential. Recompute domain per state
  change to [0, max(|ψ|²)] on the rendered grid.
- Grid: 200 × 200 over (x₁, x₂) ∈ [0, L]² for the infinite well or
  [−5, +5]² (in oscillator-length units) for the harmonic oscillator.
- The diagonal x₁ = x₂ is drawn as a thin red overlay line.
- Controls (plain HTML form elements positioned beside the SVG):
  - Particle type: radio buttons {boson, fermion, distinguishable}.
  - Basis: dropdown {infinite well, harmonic oscillator}.
  - State a: slider for n_a ∈ {1, 2, 3, 4, 5}.
  - State b: slider for n_b ∈ {1, 2, 3, 4, 5}.
- Status text overlaid on the heat map when ψ = 0 (fermion with n_a = n_b):
  "ψ_- = 0: Pauli forbidden — no such state exists."
- Numeric readouts (≤ 3 sig figs, monospaced):
  - ⟨(x₁ − x₂)²⟩ (numerical integral on the grid)
  - max(|ψ|²) and its location
  - P(both in left half) = ∫∫_{x₁, x₂ < L/2} |ψ|² dx₁ dx₂.
- No DOM mutation outside the redraw function.
```

### The simulation prompt — four-move structure

```
Build me a D3 v7 two-particle symmetry explorer following CLAUDE.md.

HOOK. Render |ψ(x₁, x₂)|² for two particles in a 1D infinite well as a
2D heat map. Let the user toggle between boson (symmetric), fermion
(antisymmetric), and distinguishable, and watch the Pauli node appear
and vanish along x₁ = x₂.

UNFOLD. Single-particle eigenstates in the infinite well of width L:
  φ_n(x) = √(2/L) sin(n π x / L), with E_n = n² π² ℏ² / (2 m L²).
Two-particle wave functions:
  ψ_boson(x₁, x₂)  = (1/√2)[φ_a(x₁)φ_b(x₂) + φ_b(x₁)φ_a(x₂)]   (symmetric)
  ψ_fermion(x₁, x₂) = (1/√2)[φ_a(x₁)φ_b(x₂) − φ_b(x₁)φ_a(x₂)]   (antisymmetric)
  ψ_dist(x₁, x₂)   = φ_a(x₁) φ_b(x₂)                              (no symmetry)
Special case: ψ_fermion(x₁, x₂) = 0 when n_a = n_b. Render the wave function
as identically zero and show the status note.

MECHANISM. Three coupled panels.
  (1) Primary 2D heat map: at each grid pixel (x₁, x₂), compute |ψ(x₁, x₂)|²
      and color via Viridis. Recompute domain on every state change. Overlay
      the diagonal x₁ = x₂ as a thin red line.
  (2) Marginal one-particle density |ρ(x₁)|² = ∫|ψ(x₁, x₂)|² dx₂, plotted
      as a line plot below the heat map. The marginal is identical for
      boson, fermion, and distinguishable cases (when the same n_a, n_b
      are used) — this is itself a pedagogical point.
  (3) Control panel (plain HTML to the right): particle type radio,
      basis dropdown, n_a and n_b sliders.

SYNTHESIZE. Add a "Spin extension" toggle. When on, the user selects spin
state from {singlet, triplet}. The simulation then enforces total
antisymmetry by pairing:
  singlet (antisymmetric spin) ⊗ symmetric spatial → allowed
  triplet (symmetric spin) ⊗ antisymmetric spatial → allowed
If the user selects singlet + n_a = n_b: spatial part is φ_a(x₁)φ_a(x₂),
which is symmetric — allowed, and the simulation displays the heat map.
If the user selects triplet + n_a = n_b: spatial part must be antisymmetric
and identical, hence zero. Display status note: "Pauli forbidden — triplet
with both particles in same orbital is impossible."

Output a single self-contained HTML file using the D3 v7 CDN.
```

### Exploration tasks

1. **The Pauli node.** Set particle = fermion, $n_a = 1$, $n_b = 2$. Look at the heat map. The diagonal $x_1 = x_2$ should be a stripe of zero — the **Pauli node**. Now set $n_a = n_b = 1$. The status note should display: "$\psi_-$ = 0: Pauli forbidden." This is the simulation telling you directly that two fermions cannot occupy the same single-particle state.

2. **Bosonic clustering.** Switch particle = boson, keep $n_a = n_b = 1$. The wave function is now $\phi_1(x_1)\phi_1(x_2)$, perfectly fine. The heat map shows a single peak in the middle of the box, and the diagonal $x_1 = x_2$ runs right through the peak. Bosons happily share orbitals.

3. **Marginals don't reveal exchange.** Keep $n_a = 1, n_b = 2$. Cycle through particle = boson, fermion, distinguishable, and watch the heat map *change dramatically* — the Pauli node appears for fermions, the clustering on the diagonal appears for bosons. But the marginal line plot at the bottom should be *identical across all three cases*. The marginal $|\rho(x_1)|^2$ is the same regardless of exchange symmetry. This is the "exchange correlation lives in the joint density, not the marginal" lesson, made visible. A single-particle detector cannot distinguish boson from fermion from distinguishable; only two-particle coincidence measurements can.

4. **Compute and verify $\langle(x_1 - x_2)^2\rangle$.** Read the simulation's numerical readout for $\langle(x_1 - x_2)^2\rangle$ in each of the three cases at $n_a = 1, n_b = 2$. Confirm

$$\langle(x_1 - x_2)^2\rangle_{\text{fermion}} > \langle(x_1 - x_2)^2\rangle_{\text{dist}} > \langle(x_1 - x_2)^2\rangle_{\text{boson}}.$$

Fermions spread; bosons cluster; distinguishable particles split the difference.

5. **Spin extension and helium-like behavior.** Toggle the spin extension on. Select spin singlet, $n_a = n_b = 1$. Confirm the simulation shows $\phi_1(x_1)\phi_1(x_2)$ (symmetric spatial), which is allowed — this is the analog of the helium ground state. Now select spin triplet, $n_a = n_b = 1$. The status note should display "Pauli forbidden — triplet with both particles in same orbital is impossible."

6. **The 1s2s helium analog.** Spin extension on, select singlet, set $n_a = 1, n_b = 2$ — the parahelium 1s2s analog. The heat map is symmetric across the diagonal. Now select triplet — the orthohelium 1s2s analog. The heat map is antisymmetric across the diagonal, with a Pauli node. The exchange correlation that lowers orthohelium below parahelium (by $2K$) is geometrically visible: the electrons in the triplet case are kept apart, which would lower the Coulomb repulsion energy if you turned on an interaction.

### Extension prompts

**Extension 1 — Slater determinant for N = 3.**

```
Extend to N = 3 by computing the 3×3 Slater determinant for three fermions
in single-particle states n = 1, 2, 3 of the infinite well. The full wave
function is a function of three coordinates (x₁, x₂, x₃), which cannot be
shown as a single heat map. Instead, render three pair-correlation cuts:
  |ψ(x₁, x₂, x₃ = L/2)|² as a heat map in (x₁, x₂),
  |ψ(x₁, x₂ = L/2, x₃)|² as a heat map in (x₁, x₃),
  |ψ(x₁ = L/2, x₂, x₃)|² as a heat map in (x₂, x₃).
Each should show the Pauli nodes along the two visible diagonals.
Verify that swapping any two columns of the 3×3 determinant flips the sign
of the full wave function (a sanity check on the code).
```

**Extension 2 — Turn on the Coulomb interaction.**

```
Add an interaction term V_int(x₁, x₂) = λ / |x₁ - x₂| (regularized at
short distance with a soft core, say V_int = λ / √((x₁-x₂)² + ε²) with
ε = 0.05 L). Diagonalize the two-particle Hamiltonian numerically on a
20 × 20 grid of single-particle modes. Let the user adjust λ with a slider
from 0 to 10 (in dimensionless units). Watch the wave function deform.
For the fermion 1s2s case: confirm that turning on λ > 0 lowers the
antisymmetric (orthohelium analog) energy relative to the symmetric
(parahelium analog) energy. The splitting at small λ is approximately
2K · λ. This is the helium calculation, made into a numerical experiment.
```

**Extension 3 — Variational helium.**

```
Add a "Helium mode" toggle that switches from the infinite well to a 3D
hydrogenic basis. Use single-particle 1s orbitals with an effective
nuclear charge Z_eff as a variational parameter. Compute the ground-state
energy E(Z_eff) for two electrons in the singlet spatial-symmetric state
and minimize over Z_eff. Plot E(Z_eff) vs. Z_eff and mark the minimum.
The minimum should sit near Z_eff = 27/16 ≈ 1.69 with E ≈ −77.5 eV,
compared to experiment −79.0 eV. This is the variational helium
calculation, made into a slider.
```

### Six failure modes to watch for

1. **$1/\sqrt{2}$ normalization dropped.** A common bug: students forget the $1/\sqrt{2}$ in $\psi_\pm = (1/\sqrt{2})[\phi_a\phi_b \pm \phi_b\phi_a]$. The wave function is then over-normalized by a factor of 2, and $\langle\psi|\psi\rangle = 2$. Easy to spot — compute the integral $\int |\psi|^2 d^2r$ on the grid; if it's about 2 instead of 1, you dropped the factor.

2. **Marginals computed wrong.** $|\rho(x_1)|^2 = \int|\psi(x_1, x_2)|^2 dx_2$, summed over the $x_2$ axis of your 2D grid, multiplied by $\Delta x_2$. Confirm by checking that $\int |\rho(x_1)|^2 dx_1 = 1$.

3. **Fermion $n_a = n_b$ case not handled.** If the code attempts to compute $(1/\sqrt{2})[\phi_a\phi_a - \phi_a\phi_a]$ it returns zero — but the visualization might display "all zero" as a uniform color and confuse the student. Display the status note clearly: "$\psi_-$ = 0: Pauli forbidden." This is a feature, not a bug.

4. **Color domain not reset between particle types.** If you set the Viridis domain at $n_a = 1, n_b = 2$ for the boson case and then switch to fermion, the fermion heat map will look dim. Recompute the domain per render.

5. **Diagonal overlay rendered before the heat map.** SVG renders later elements on top of earlier ones. If you draw the diagonal $x_1 = x_2$ red line before the heat map rectangles, the diagonal will be hidden underneath. Draw the heat map first, then the diagonal overlay.

6. **Spin extension fails to enforce total antisymmetry.** A bug: the spin toggle lets the user select singlet + antisymmetric-spatial, giving a symmetric total wave function — not allowed. Implement the spin-extension logic so that singlet automatically pairs with symmetric-spatial and triplet with antisymmetric-spatial.

When you can drag $n_a$ and $n_b$ around, watch the Pauli node form and vanish, toggle through particle types and see the dramatic change in the joint density while the marginal stays the same, and toggle the spin extension to see the helium-like singlet/triplet behavior — at that point you have the machinery of multi-electron quantum mechanics on your screen, generated by you, governed by physics you can derive on demand.

---

## Exercises

### Warm-up

1. *[Tests: exchange operator, eigenvalue argument]* Define $\hat{P}_{12}$ and show from $\hat{P}_{12}^2 = \mathbb{1}$ that its eigenvalues can only be $\pm 1$. Then show that $[\hat{H}, \hat{P}_{12}] = 0$ for two identical particles interacting via a potential $V(|\vec{r}_1 - \vec{r}_2|)$, so that energy eigenstates can be chosen to have definite exchange symmetry. *Difficulty: warm-up.*

2. *[Tests: Slater determinant, antisymmetry check]* Write the Slater determinant for two fermions in states $\phi_a$ and $\phi_b$. Verify by direct computation that swapping particles 1 and 2 (swapping the two rows) yields $-\psi_-(1,2)$. Then verify that $\langle\psi_-|\psi_-\rangle = 1$ given $\langle\phi_a|\phi_a\rangle = \langle\phi_b|\phi_b\rangle = 1$ and $\langle\phi_a|\phi_b\rangle = 0$. *Difficulty: warm-up.*

3. *[Tests: composite-particle statistics, counting rule]* State whether each of the following is a boson or fermion, and give the constituent fermion count: (a) a photon; (b) a $^4$He atom; (c) a $^3$He atom; (d) a proton; (e) a $\pi^+$ meson (quark-antiquark pair). For (b) and (c), explain in one sentence why the superfluid transition temperatures differ by three orders of magnitude. *Difficulty: warm-up.*

### Application

4. *[Tests: Pauli exclusion from Slater determinant]* The $N = 3$ Slater determinant for fermions in orbitals $\phi_1, \phi_2, \phi_3$ is

$$\psi(1,2,3) = \frac{1}{\sqrt{6}}\det\begin{pmatrix}\phi_1(1)&\phi_2(1)&\phi_3(1)\\\phi_1(2)&\phi_2(2)&\phi_3(2)\\\phi_1(3)&\phi_2(3)&\phi_3(3)\end{pmatrix}.$$

(a) Set $\phi_2 = \phi_3$ and show that $\psi = 0$ identically. (b) Expand the determinant for distinct $\phi_1, \phi_2, \phi_3$ along the first row and write out all six terms with their signs. (c) Verify that swapping particles 1 and 2 (rows 1 and 2) gives $-\psi$. *Difficulty: application.*

5. *[Tests: helium symmetry sectors, ground state argument]* (a) Write down the two allowed antisymmetric total wave functions for the helium 1s2s configuration — one for parahelium, one for orthohelium. Identify the spin part (singlet or triplet) and the spatial part (symmetric or antisymmetric) in each. (b) Explain why a $1s^2$ orthohelium ground state cannot exist, using the Pauli exclusion argument. (c) Suppose you add a very small spin-orbit coupling $\hat{H}' = \alpha\,\vec{L}\cdot\vec{S}$ as a perturbation. Would this allow transitions between the parahelium and orthohelium sectors? Why or why not? *Difficulty: application.*

6. *[Tests: direct and exchange integrals, physical interpretation]* For the helium 1s2s configuration, the first-order Coulomb correction is $\langle V_{12}\rangle = J \pm K$. (a) Write down the integrals defining $J$ and $K$. (b) Explain in words why $J$ has a classical analog and $K$ does not. (c) For real hydrogenic orbitals $\phi_{1s}$ and $\phi_{2s}$ and the positive kernel $1/r_{12}$, argue from the form of $K$ that $K > 0$. (d) Which state — parahelium or orthohelium — has the lower energy at the 1s2s configuration, and by how much? *Difficulty: application.*

### Synthesis

7. *[Tests: Hund's rule mechanism, connection to exchange integral]* The ground configuration of oxygen is $1s^2\,2s^2\,2p^4$. The $2p$ subshell has three spatial orbitals ($m_\ell = -1, 0, +1$) and four electrons to fill them. (a) Write down the Hund's-rule ground state: which orbitals are doubly occupied, which are singly occupied, and what is the total spin $S$? (b) Using the exchange-integral argument from the helium calculation, explain in three sentences why this configuration has lower Coulomb energy than the alternative with two doubly-occupied $2p$ orbitals and one empty. (c) Is Hund's rule a postulate or a consequence? Cite the mechanism. *Difficulty: synthesis.*

8. *[Tests: exchange correlation vs. exchange force, marginal density argument]* Two electrons are in the $n_a = 1, n_b = 2$ states of a 1D infinite well. (a) Write the joint probability densities $|\psi_+|^2$, $|\psi_-|^2$, and $|\psi_\text{dist}|^2$ in terms of the single-particle densities $|\phi_1(x)|^2$ and $|\phi_2(x)|^2$. (b) Compute the marginal density $\rho(x_1) = \int |\psi(x_1, x_2)|^2\,dx_2$ for each case and show they are all equal to $|\phi_1(x_1)|^2 + |\phi_2(x_1)|^2$ (up to normalization). (c) Explain why this means that a single-particle measurement cannot distinguish bosons, fermions, or distinguishable particles in the same pair of orbitals. What kind of measurement could? *Difficulty: synthesis.*

### Challenge

9. *[Tests: degeneracy pressure, Chandrasekhar mass, order-of-magnitude physics]* A white dwarf of mass $M$ and radius $R$ is supported against gravity by non-relativistic electron degeneracy pressure. (a) The number of electrons is $N \sim M/m_p$ where $m_p$ is the proton mass. The electrons occupy the $N$ lowest momentum states in a sphere of volume $V = \frac{4}{3}\pi R^3$ — estimate the Fermi momentum $p_F \sim \hbar N^{1/3}/R$ (up to numerical factors). (b) The total kinetic energy scales as $E_\text{kin} \sim N p_F^2/2m_e$. The gravitational potential energy is $E_\text{grav} \sim -GM^2/R$. Minimize the total energy over $R$ to find the equilibrium radius. Show that $R \propto M^{-1/3}$: a more massive white dwarf is *smaller*. (c) In the ultra-relativistic limit $p_F \gg m_e c$, the kinetic energy scales as $E_\text{kin} \sim Ncp_F$. Show that both $E_\text{kin}$ and $|E_\text{grav}|$ scale as $1/R$, so there is a critical mass above which no equilibrium exists. Estimate that critical mass in solar masses. *Difficulty: challenge.*

---

**Chapter 9** takes the variational principle that made the helium ground-state calculation tractable and turns it into a systematic method. You have the mechanics of identical particles; Chapter 9 gives you the tools to calculate with them when exact solutions are unavailable — which is to say, for almost every multi-electron system in chemistry and materials science.
