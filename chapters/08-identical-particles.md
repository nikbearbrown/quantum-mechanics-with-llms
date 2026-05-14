# Chapter 8 — Identical Particles

> Where quantum mechanics diverges most sharply from classical mechanics: no labels survive, antisymmetry generates Pauli exclusion, and the structure of the periodic table is a corollary of a symmetry.

---

## 1. A 1925 puzzle that wasn't supposed to be solved

The visible spectrum of helium, by the early 1920s, had been catalogued in fine detail. There were two distinct families of lines. One family was called *parahelium*; the other, *orthohelium*. They looked, for all practical purposes, like spectra of two different elements — different selection rules, different transition rates, different fine-structure patterns. But helium, chemists insisted, was helium. One element, one electron configuration, one set of lines.

Werner Heisenberg, in 1926, looked at this from the new wave-mechanics perspective and asked a sharp question: if hydrogen is one electron in a Coulomb potential and we solved it exactly, what is helium? Two electrons in the field of a $+2$ nucleus, plus their mutual Coulomb repulsion. The Schrödinger equation has a definite answer; he set up to compute it.

The first thing he found was that the answer depends on something he had not expected to think about: whether the wave function is symmetric or antisymmetric under exchange of the two electrons. The two cases — symmetric spatial wave function paired with antisymmetric spin (parahelium), and antisymmetric spatial wave function paired with symmetric spin (orthohelium) — gave different energies. The two "different elements" of the helium spectrum were *the same element in two different exchange symmetry sectors*. Heisenberg (*Zeitschrift für Physik* 39, 499 [verify]) had the explanation in print by mid-1926.

Wolfgang Pauli had laid the empirical groundwork the year before, with his exclusion principle (1925, *Zeitschrift für Physik* 31, 765 [verify]): no two electrons in an atom share the same set of quantum numbers $(n, \ell, m_\ell, m_s)$. Pauli stated this as a phenomenological rule to explain the periodic table. But the rule looked arbitrary. *Why* this restriction, of all possible restrictions? John Slater (1929, *Physical Review* 34, 1293 [verify]) supplied the missing machinery: write multi-electron wave functions as determinants of single-particle orbitals, and the exclusion principle becomes a corollary of the determinant vanishing when two rows are identical. Pauli's rule is not a separate postulate. It is a property of antisymmetric wave functions.

This chapter develops that machinery from scratch. We will set up the exchange operator, prove that its eigenvalues are $\pm 1$, postulate the symmetrization principle in 3+1 dimensions, derive Slater determinants and the Pauli exclusion principle, and run the helium singlet–triplet calculation that exposes how antisymmetry — a structural property of the wave function — drives chemical energy differences through the Coulomb integral. By the end you will know why the periodic table looks the way it does.

**Learning objectives.** By the end of this chapter, you should be able to:

- State precisely what it means for two particles to be "identical" in quantum mechanics and distinguish it from "very similar."
- Define the exchange operator $\hat{P}_{12}$, prove $\hat{P}_{12}^2 = \mathbb{1}$, and conclude that its eigenvalues are $\pm 1$.
- State the symmetrization postulate in 3+1 dimensions and identify which fundamental particles are bosons and which are fermions.
- Write a Slater determinant for $N$ identical fermions for $N = 2$ and $N = 3$ and verify antisymmetry under exchange.
- Derive the Pauli exclusion principle from antisymmetry: a Slater determinant with two identical rows vanishes.
- Set up the helium singlet–triplet calculation, identify the direct integral $J$ and the exchange integral $K$, and explain why orthohelium 1s2s lies below parahelium 1s2s.
- Distinguish exchange correlation (a structural property of $|\psi(\vec{r}_1, \vec{r}_2)|^2$) from a "force" (a term in the Hamiltonian).
- Build a two-particle simulation that displays $|\psi(x_1, x_2)|^2$ as a 2D heat map, switches between boson / fermion / distinguishable cases, and visualizes the Pauli node along $x_1 = x_2$.

**Prerequisites.** Wave functions, the Born rule (Ch. 1–2). Schrödinger equation (Ch. 2). Hilbert spaces, operators (Ch. 4). Single-particle eigenstates of the infinite well or harmonic oscillator (Ch. 2–3). Spin-1/2 algebra, singlet and triplet construction (Ch. 6). Hydrogenic single-particle orbitals (Ch. 7).

---

## 2. Indistinguishability — what it really means

### 2.1 The classical move that is no longer available

In classical mechanics, two identical objects can always be tracked individually. Paint a dot on one billiard ball at $t = 0$; follow its trajectory through any sequence of collisions; the dot survives because the position is a continuous function of time and the ball never disappears between snapshots. Even without the dot, if you have arbitrarily precise sensors, you can in principle keep the two balls sorted by their worldlines. Classical identity is *labeling by trajectory*, and the labeling is robust because worldlines do not cross or fork.

In quantum mechanics this move fails. The wave function $\psi(\vec{r}_1, \vec{r}_2)$ for two particles spreads each over a region of space; the regions overlap; the "trajectory" you would track is not a sharp curve but a probability distribution. And there is no measurement — even in principle — that can tell you, when a detector at location $\vec{r}$ registers a click, which of the two particles produced it. The labels "1" and "2" we write in the wave function are mathematical bookkeeping. They are not physical identities. The Hamiltonian, the observables, and the measurable predictions of the theory are all invariant under permutation of the labels.

### 2.2 The exchange operator

Define the **exchange operator** $\hat{P}_{12}$ on the two-particle Hilbert space by

$$ \hat{P}_{12} \psi(\vec{r}_1, \vec{r}_2) = \psi(\vec{r}_2, \vec{r}_1). $$

Two immediate consequences:

**(a) $\hat{P}_{12}^2 = \mathbb{1}$.** Swap twice: $\hat{P}_{12}^2 \psi(\vec{r}_1, \vec{r}_2) = \hat{P}_{12} \psi(\vec{r}_2, \vec{r}_1) = \psi(\vec{r}_1, \vec{r}_2)$. So $\hat{P}_{12}^2 = \mathbb{1}$, and its eigenvalues must square to 1: $\hat{P}_{12}$ has eigenvalues $\pm 1$.

**(b) If the two particles are identical, $[\hat{H}, \hat{P}_{12}] = 0$.** A Hamiltonian for two identical particles is symmetric under their exchange — it contains terms like $\hat{p}_1^2/2m + \hat{p}_2^2/2m + V(\vec{r}_1) + V(\vec{r}_2) + V_{12}(|\vec{r}_1 - \vec{r}_2|)$, all of which commute with the swap. So $\hat{H}$ and $\hat{P}_{12}$ share a common eigenbasis: every energy eigenstate can be chosen to be either symmetric ($\hat{P}_{12} \psi = +\psi$) or antisymmetric ($\hat{P}_{12} \psi = -\psi$) under exchange.

### 2.3 The symmetrization postulate

So far we have shown that energy eigenstates can be chosen with definite exchange symmetry $\pm 1$. We have not shown which one nature chooses for any given particle species. The empirical fact, elevated to a postulate:

**Symmetrization postulate (3+1 dimensions).** All identical particles in 3+1 dimensions fall into one of two classes:
- **Bosons** — multi-particle wave function symmetric under exchange ($\hat{P}_{12} \psi = +\psi$).
- **Fermions** — multi-particle wave function antisymmetric under exchange ($\hat{P}_{12} \psi = -\psi$).

This is a *postulate* in non-relativistic quantum mechanics. We do not derive it from the rest of the formalism. The deeper result that connects spin to statistics — integer spin → bosons, half-integer spin → fermions — is the **spin-statistics theorem**, proven by Pauli (1940, *Physical Review* 58, 716 [verify]) in relativistic quantum field theory from the requirement that field operators at spacelike separation either commute (bosons) or anticommute (fermions). The proof requires QFT machinery beyond this book. You should know the theorem exists, that it requires QFT, and that within your current toolkit it is a postulate.

A subtlety the chapter must flag: the $\pm 1$ dichotomy is specific to 3+1 dimensions. In effectively 2D systems — fractional quantum Hall fluids, certain topological superconductors — exchange phases other than $\pm 1$ are possible, giving rise to **anyons** with statistics that depend continuously on a parameter or, in the non-abelian case, transform under a representation of the braid group. Leinaas and Myrheim (1977, *Il Nuovo Cimento B* 37, 1 [verify]) first analyzed this; Wilczek (1982, *Physical Review Letters* 49, 957 [verify]) named anyons; direct experimental evidence appeared in two-dimensional electron gas systems (Bartolomei et al. 2020 *Science* 368, 173 [verify]; Nakamura et al. 2020 *Nature Physics* 16, 931 [verify]). The chapter's postulate is 3+1-dimensional; the anyon story belongs to Chapter 13.

### 2.4 Which particles are which

The empirical (and provable, in QFT) statistics-spin correspondence:

| Spin | Statistics | Examples |
|---|---|---|
| Integer ($s = 0, 1, 2, \ldots$) | Bosons | Photon ($s=1$), gluons, W/Z bosons, Higgs ($s=0$), composite particles built from even number of fermions: ${}^4$He, ${}^{87}$Rb, $\pi$ mesons |
| Half-integer ($s = 1/2, 3/2, \ldots$) | Fermions | Electrons ($s=1/2$), protons, neutrons, quarks, neutrinos, composite particles built from odd number of fermions: ${}^3$He |

**The composite-particle counting rule.** For a composite particle made of constituent fermions, count them. Even → behaves as a boson. Odd → behaves as a fermion. So ${}^4$He (2 protons + 2 neutrons + 2 electrons = 6 fermions, even) is a boson; ${}^3$He (2 protons + 1 neutron + 2 electrons = 5 fermions, odd) is a fermion. This is why ${}^4$He becomes a superfluid below 2.17 K (Bose-Einstein-like condensation of the bosonic atoms) but ${}^3$He requires temperatures below 2.5 mK to enter its superfluid phase (which involves Cooper pairing of fermionic atoms, BCS-like). Three orders of magnitude separating the two transition temperatures from a single sign in the wave function.

### 2.5 A common misconception worth confronting now

"Two electrons in distant atoms can be told apart because they are in different atoms." This is wrong but tempting. The correct statement: the exchange symmetry *still applies*; the multi-electron wave function for the whole universe is antisymmetric across all electron labels, full stop. The reason exchange effects between distant electrons are usually negligible is that the spatial overlap integral $\langle\phi_A | \phi_B\rangle$ is exponentially small when $\phi_A$ and $\phi_B$ are localized in distant atoms. Indistinguishability is universal; what varies is whether it produces measurable consequences.

---

## 3. Slater determinants — antisymmetry as a property of matrices

### 3.1 The two-fermion case

For two identical fermions in single-particle states $\phi_a$ and $\phi_b$, the antisymmetric wave function is

$$ \psi_-(1, 2) = \frac{1}{\sqrt{2}}\big[\phi_a(1)\phi_b(2) - \phi_b(1)\phi_a(2)\big]. $$

(I am writing $\phi_a(1) \equiv \phi_a(\vec{r}_1, m_{s,1})$ — the orbital evaluated at particle 1's coordinates, including spin if relevant.) Check antisymmetry directly:

$$ \hat{P}_{12}\psi_-(1, 2) = \psi_-(2, 1) = \frac{1}{\sqrt{2}}\big[\phi_a(2)\phi_b(1) - \phi_b(2)\phi_a(1)\big] = -\psi_-(1, 2). \checkmark $$

Rewrite the bracket as a 2×2 determinant:

$$ \psi_-(1, 2) = \frac{1}{\sqrt{2}} \det\begin{pmatrix} \phi_a(1) & \phi_b(1) \\ \phi_a(2) & \phi_b(2) \end{pmatrix}. $$

This is the **Slater determinant** for $N = 2$. Antisymmetry is now a property of the determinant: swapping rows (swapping particles) flips the sign. The wave function form *automatically* satisfies $\hat{P}_{12}\psi = -\psi$.

### 3.2 The general case: $N$ fermions

For $N$ identical fermions in single-particle orbitals $\phi_1, \phi_2, \ldots, \phi_N$, the antisymmetric wave function is the determinant

$$ \boxed{ \psi(1, 2, \ldots, N) = \frac{1}{\sqrt{N!}} \det\begin{pmatrix} \phi_1(1) & \phi_2(1) & \cdots & \phi_N(1) \\ \phi_1(2) & \phi_2(2) & \cdots & \phi_N(2) \\ \vdots & \vdots & \ddots & \vdots \\ \phi_1(N) & \phi_2(N) & \cdots & \phi_N(N) \end{pmatrix}. } $$

The $(i, j)$ entry is the $i$-th single-particle orbital evaluated at the $j$-th particle's coordinates. The $1/\sqrt{N!}$ normalizes the wave function to unity (assuming the $\phi_i$ are orthonormal). Slater introduced this construction in 1929.

Let me write the $N = 3$ case explicitly so you can see the structure:

$$ \psi(1, 2, 3) = \frac{1}{\sqrt{6}} \det\begin{pmatrix} \phi_1(1) & \phi_2(1) & \phi_3(1) \\ \phi_1(2) & \phi_2(2) & \phi_3(2) \\ \phi_1(3) & \phi_2(3) & \phi_3(3) \end{pmatrix}. $$

Expanding along the first row:

$$ \psi(1, 2, 3) = \frac{1}{\sqrt{6}}\Big[ \phi_1(1)\big(\phi_2(2)\phi_3(3) - \phi_3(2)\phi_2(3)\big) $$
$$ - \phi_2(1)\big(\phi_1(2)\phi_3(3) - \phi_3(2)\phi_1(3)\big) $$
$$ + \phi_3(1)\big(\phi_1(2)\phi_2(3) - \phi_2(2)\phi_1(3)\big) \Big]. $$

Six terms with alternating signs — the six permutations of three labels, each weighted by the sign of the permutation. Swap any two rows (any two particles) and the determinant flips sign. Swap any two columns (any two orbitals) and the determinant also flips sign, which means relabeling the orbitals does not change physical content.

### 3.3 Pauli exclusion from antisymmetry

Here is the move that justifies the chapter's existence. Suppose two of the orbitals are identical: $\phi_i = \phi_j$ for some $i \neq j$. Then two columns of the Slater determinant are identical. A determinant with two identical columns is zero. So $\psi(1, 2, \ldots, N) = 0$ identically — everywhere in space, for all configurations.

A wave function that is zero everywhere is not a state at all (it cannot be normalized; $\int 0 \, d^N r = 0 \neq 1$). So *two fermions cannot occupy the same single-particle state*, because the wave function we would construct to represent that situation is identically zero.

**The Pauli exclusion principle is a corollary of antisymmetry, not a separate postulate.**

This is the single most important conceptual move in the chapter. Many of you have learned Pauli exclusion as "no two electrons can have the same four quantum numbers $(n, \ell, m_\ell, m_s)$" — a rule about labels, with no machinery behind it. That phrasing is correct but incomplete. The deeper version is: the multi-electron wave function is antisymmetric; the Slater determinant enforces antisymmetry; putting two fermions in identical states makes the determinant zero. Quantum numbers $(n, \ell, m_\ell, m_s)$ are just labels for single-particle hydrogenic orbitals — when we move to solid-state physics, the labels become band indices and crystal momenta, but the rule (still derived from antisymmetry) survives. Better to learn the symmetry-based version once, here, than to have to re-derive it later.

### 3.4 Where Slater determinants live in practice

The **Hartree–Fock approximation** — the workhorse of computational quantum chemistry — is exactly the following: assume the $N$-electron ground state of a molecule is a single Slater determinant; minimize $\langle\psi|\hat{H}|\psi\rangle$ variationally over the choice of single-particle orbitals $\phi_i$. The result is a set of self-consistent integro-differential equations (the Hartree–Fock equations) whose solutions are the optimal orbitals.

Every subsequent quantum-chemistry method — configuration interaction, coupled-cluster theory, density functional theory in some readings — is either a correction to or a generalization of the single-Slater-determinant ansatz. When you read about a quantum-chemistry computation of, say, a transition state in catalysis or the binding energy of a drug to a receptor, the calculation is built on the construction in §3.2. You are now standing on the foundation of computational chemistry.

---

## 4. Helium — the deep dive

This is the chapter's earned explanation. We will compute the helium spectrum at first order in perturbation theory, see how antisymmetry produces a measurable energy splitting between parahelium and orthohelium, and identify the exchange integral $K$ as the mechanism. The calculation is half a page; the payoff is that you understand the helium puzzle that opened the chapter — and Hund's first rule along the way.

### 4.1 Setting up the spin structure

Helium has two electrons. The total electron wave function is a product of a spatial part and a spin part:

$$ \Psi_{\text{total}}(1, 2) = \psi_{\text{spatial}}(\vec{r}_1, \vec{r}_2) \cdot \chi_{\text{spin}}(m_{s,1}, m_{s,2}). $$

The total wave function must be antisymmetric under exchange. So one of the two factors is symmetric and the other is antisymmetric.

From Chapter 6, the two-spin Hilbert space (4 states) decomposes by total spin $S$:

- **Spin singlet** (antisymmetric, $S = 0$, one state):
  $$ \chi_{\text{singlet}} = \frac{1}{\sqrt{2}}\big(|\!\uparrow\downarrow\rangle - |\!\downarrow\uparrow\rangle\big). $$
- **Spin triplet** (symmetric, $S = 1$, three states):
  $$ \chi_{\text{triplet}} = \begin{cases} |\!\uparrow\uparrow\rangle, \\ \tfrac{1}{\sqrt{2}}(|\!\uparrow\downarrow\rangle + |\!\downarrow\uparrow\rangle), \\ |\!\downarrow\downarrow\rangle. \end{cases} $$

Two cases for the total wave function:

- **Parahelium:** spin singlet (antisymmetric) ⊗ spatial symmetric. $S = 0$.
- **Orthohelium:** spin triplet (symmetric) ⊗ spatial antisymmetric. $S = 1$.

Both are honest antisymmetric total wave functions. Both are observed spectroscopically.

### 4.2 The ground state — why parahelium

Try to put both electrons in the 1s orbital: $\phi_a = \phi_b = \phi_{1s}$. The spatial product $\phi_{1s}(\vec{r}_1)\phi_{1s}(\vec{r}_2)$ is symmetric. The antisymmetric counterpart $\phi_{1s}(\vec{r}_1)\phi_{1s}(\vec{r}_2) - \phi_{1s}(\vec{r}_1)\phi_{1s}(\vec{r}_2) = 0$ vanishes (the Slater determinant with two identical columns).

So both electrons in 1s only via the symmetric-spatial branch, which requires the spin singlet. The helium ground state is

$$ \Psi_{\text{GS}}(1, 2) = \phi_{1s}(\vec{r}_1)\phi_{1s}(\vec{r}_2) \cdot \frac{1}{\sqrt{2}}\big(|\!\uparrow\downarrow\rangle - |\!\downarrow\uparrow\rangle\big). $$

This is parahelium with $S = 0$. **No orthohelium ground state with both electrons in 1s exists** — Pauli forbids it (the spatial antisymmetric construction vanishes). The lowest orthohelium state must have one electron in 1s and one elsewhere, the lowest "elsewhere" being 2s, giving the 1s2s ${}^3$S state.

### 4.3 Zeroth-order energy

Treat the electrons as non-interacting (drop the $V_{12} = e^2/(4\pi\epsilon_0 r_{12})$ term). Each electron sees a hydrogen-like Coulomb potential from a $+Z$ nucleus with $Z = 2$. The single-particle energies for $Z = 2$ are

$$ E_n = -\frac{Z^2 \cdot 13.6 \text{ eV}}{n^2} = -\frac{54.4 \text{ eV}}{n^2}. $$

Two electrons in 1s each at $-54.4$ eV give a zeroth-order total energy

$$ E^{(0)} = 2 \times (-54.4 \text{ eV}) = -108.8 \text{ eV}. $$

The experimental helium ground-state binding energy is $-79.0$ eV [verify NIST]. The non-interacting prediction overshoots by 29.8 eV — the missing piece is the electron-electron Coulomb repulsion energy, which we ignored.

### 4.4 First-order correction

Treat $V_{12} = e^2/(4\pi\epsilon_0 r_{12})$ as a perturbation. The first-order energy shift for the ground state (where the spin part is irrelevant because $V_{12}$ doesn't act on spin) is

$$ \Delta E_{\text{GS}}^{(1)} = \langle\psi_{\text{GS,spatial}}|V_{12}|\psi_{\text{GS,spatial}}\rangle = \iint |\phi_{1s}(\vec{r}_1)|^2 \frac{e^2/(4\pi\epsilon_0)}{|\vec{r}_1 - \vec{r}_2|} |\phi_{1s}(\vec{r}_2)|^2 \, d^3r_1 \, d^3r_2. $$

This integral has been computed many times in the literature; the result (Griffiths §5.2.1 [verify]) is

$$ \Delta E_{\text{GS}}^{(1)} = \frac{5}{8} Z \cdot \frac{e^2}{4\pi\epsilon_0 a_0} = \frac{5}{8} \cdot 2 \cdot 27.2 \text{ eV} = 34.0 \text{ eV}. $$

Adding: $E^{(0)} + \Delta E_{\text{GS}}^{(1)} = -108.8 + 34.0 = -74.8$ eV. Compare to experiment, $-79.0$ eV. We are now about 5 eV off, much closer than the non-interacting estimate. The remaining gap closes with the variational principle (Ch. 9 or 10), where you let an effective $Z$ be a variational parameter and find $Z_{\text{eff}} \approx 27/16 \approx 1.69$ and $E \approx -77.5$ eV [verify].

This is the canonical demonstration that hydrogen-like single-particle orbitals + first-order Coulomb gets you to within 5% of the truth even in the simplest multi-electron atom.

### 4.5 The singlet–triplet splitting — where exchange shows up

Now consider an excited state: one electron in 1s, one in 2s. The spatial wave function can be either symmetric (parahelium 1s2s ${}^1$S) or antisymmetric (orthohelium 1s2s ${}^3$S):

$$ \psi_\pm(\vec{r}_1, \vec{r}_2) = \frac{1}{\sqrt{2}}\big[\phi_{1s}(\vec{r}_1)\phi_{2s}(\vec{r}_2) \pm \phi_{2s}(\vec{r}_1)\phi_{1s}(\vec{r}_2)\big]. $$

The first-order Coulomb correction is

$$ \langle\psi_\pm|V_{12}|\psi_\pm\rangle = J \pm K, $$

where, expanding the inner product:

$$ \boxed{ J = \iint |\phi_{1s}(\vec{r}_1)|^2 \frac{e^2/(4\pi\epsilon_0)}{r_{12}} |\phi_{2s}(\vec{r}_2)|^2 \, d^3r_1 \, d^3r_2 \quad \text{(direct integral)}, } $$

$$ \boxed{ K = \iint \phi_{1s}^*(\vec{r}_1) \phi_{2s}^*(\vec{r}_2) \frac{e^2/(4\pi\epsilon_0)}{r_{12}} \phi_{2s}(\vec{r}_1) \phi_{1s}(\vec{r}_2) \, d^3r_1 \, d^3r_2 \quad \text{(exchange integral)}. } $$

The direct integral $J$ has a classical interpretation: the Coulomb interaction energy between two charge clouds, one shaped like $|\phi_{1s}|^2$ and one like $|\phi_{2s}|^2$. A classical-physics undergraduate could write this integral, even without knowing quantum mechanics.

The exchange integral $K$ has *no classical analog*. It arises purely from the cross-term in the antisymmetrized (or symmetrized) wave function. For real $\phi_{1s}$ and $\phi_{2s}$ and the positive Coulomb kernel $1/r_{12}$, $K > 0$. So:

- **Parahelium (spatial symmetric, ${}^1$S):** $E = E^{(0)} + J + K$ — higher.
- **Orthohelium (spatial antisymmetric, ${}^3$S):** $E = E^{(0)} + J - K$ — lower.

**The orthohelium 1s2s ${}^3$S state lies below the parahelium 1s2s ${}^1$S state by $2K$.** This splitting is real, measurable, and historically anomalous: at the time of its observation it suggested that parallel-spin states were energetically preferred, which seemed to require a spin-dependent force. The post-1925 explanation is that there is no spin-dependent force at this order. The chain runs:

> Spins control the symmetry of the spin part of the wave function.
> Antisymmetry of the total wave function forces the spatial part to have opposite symmetry.
> The spatial symmetry controls how strongly the electrons "see" each other through the Coulomb repulsion — antisymmetric spatial states keep electrons apart (the exchange correlation pulls $|\psi_-|^2$ to zero at $r_1 = r_2$), which lowers the Coulomb energy.

Spin acts on the spatial geometry, which acts on the Coulomb energy. That is the mechanism. Make sure you can recite this chain in your sleep — it is the conceptual headline of the chapter, and it generalizes to every multi-electron atom and molecule.

The experimental 1s2s ${}^1$S − ${}^3$S splitting in helium is about 0.80 eV [verify NIST atomic spectra database], both states sitting ~ 20 eV above the parahelium ground state. The non-zero value of $K$ for these orbitals is what produces all the magnetic phenomena of multi-electron atoms — ferromagnetism, antiferromagnetism, Hund's rules — through the same mechanism.

### 4.6 Hund's first rule — a corollary, not a postulate

In 1925 Friedrich Hund (*Zeitschrift für Physik* 33, 345 [verify]) catalogued an empirical pattern in atomic spectra: for a given electron configuration, the term with the highest total spin $S$ has the lowest energy. Sodium's $3s^1$ ground state is ${}^2$S$_{1/2}$ ($S = 1/2$, no choice). Oxygen's $2p^4$ ground state is ${}^3$P (two unpaired electrons, $S = 1$). Iron's $3d^6 4s^2$ valence configuration produces a ${}^5$D$_4$ ground state ($S = 2$).

Hund's first rule is, in the helium framework, a corollary of antisymmetry:

> Higher $S$ → symmetric spin state → antisymmetric spatial state → electrons avoid coincidence (Pauli node along $\vec{r}_1 = \vec{r}_2$) → lower Coulomb repulsion energy.

The rule that gets quoted in chemistry as a separate empirical fact is the *consequence* of the symmetry. You did not need to memorize Hund's rule; you can derive it on demand from antisymmetry + Coulomb.

---

## 5. The periodic table

The architecture of the periodic table — why noble gases are inert, why alkali metals are reactive, why the d-block sits where it does, why the row lengths are 2, 8, 8, 18, 18, 32, 32 — is the synthesis of three ingredients:

**1. Hydrogenic energy ordering, modified by screening.** Inner electrons screen the nuclear charge from outer electrons, so the effective potential the outer electrons see is no longer pure $1/r$. The screening is weakest for low-$\ell$ orbitals (which penetrate close to the nucleus, where shielding is partial) and strongest for high-$\ell$ orbitals (which stay away from the nucleus, where shielding is more complete). So at fixed $n$, low-$\ell$ states lie below high-$\ell$ — the $n^2$-degeneracy of pure hydrogen splits. The 2s lies below 2p in lithium and beyond; the 3s lies below 3p lies below 3d in sodium and beyond. The visualizer you built in Chapter 7 lets you see this — overlay the radial probability $P(r) = r^2|R_{n\ell}|^2$ for 3s, 3p, 3d, and notice that the 3s wave function has the highest density near the nucleus.

**2. Pauli exclusion.** From §3.3 — antisymmetry of the total wave function implies that two fermions cannot occupy the same single-particle state. Each spatial orbital can hold at most two electrons (one $m_s = +1/2$, one $m_s = -1/2$). Without Pauli, every electron in every atom would collapse to 1s and chemistry would not exist. There would be no periodic table — just N copies of "helium-but-bigger" stacked with increasing nuclear charge.

**3. Hund's rule.** From §4.6 — within a partially filled subshell, fill different $m_\ell$ orbitals with parallel spins before pairing. This minimizes Coulomb repulsion through the exchange-integral mechanism.

The **Aufbau** ("building-up") principle compiles these: fill orbitals in order of increasing energy, respecting Pauli, with Hund's rule resolving the within-subshell choices. The **Madelung rule** (Madelung 1936, *Die mathematischen Hilfsmittel des Physikers* [verify]) gives the empirical filling order — lowest $n + \ell$ first, ties broken by lowest $n$ — producing the sequence

$$ 1s, 2s, 2p, 3s, 3p, 4s, 3d, 4p, 5s, 4d, 5p, 6s, 4f, 5d, 6p, 7s, 5f, 6d, 7p. $$

Notice the 4s/3d flip — 4s fills before 3d for low-Z atoms (potassium, calcium) — because screening makes 3d less stable than 4s in that regime. Madelung is empirical, not derived. About twenty atoms across the periodic table violate it. The classic exceptions:

- **Chromium** (Z = 24): actual configuration $3d^5 4s^1$, not the Madelung-predicted $3d^4 4s^2$. The stability of a half-filled $3d$ subshell beats the small $4s$/$3d$ gap.
- **Copper** (Z = 29): actual $3d^{10} 4s^1$, not $3d^9 4s^2$. The stability of a filled $3d$ subshell again wins.

These are not mysterious — when orbital energies are close to degenerate, small effects (Hund's rule preferences, exchange-correlation energy differences) tip the balance. Madelung is a 95%-accurate rule of thumb, not a law.

**Worth saying out loud.** Chemistry — the periodic table, valence, bonding, the rules students memorize in high school — is the low-energy effective theory of atoms whose ground states are dictated by fermionic antisymmetry plus Coulomb plus (for heavy atoms) relativistic corrections. Without antisymmetry, no periodic table. The formal structure of the table really is determined by exchange symmetry. This is not a poetic claim; it is what the calculation shows.

---

## 6. Bosons — what happens when the sign flips

For completeness, the boson side of the story. Bosons have *symmetric* multi-particle wave functions, so two bosons happily occupy the same single-particle state. At low temperature and high density, a macroscopic fraction of bosons can pile into the single lowest-energy state — **Bose–Einstein condensation (BEC)**.

The first BEC in dilute alkali gases was observed in 1995 by Eric Cornell, Carl Wieman, and collaborators at JILA, cooling ${}^{87}$Rb atoms in a magnetic trap to about 170 nK (Anderson et al. 1995, *Science* 269, 198 [verify pages]). Wolfgang Ketterle at MIT produced the second BEC weeks later with ${}^{23}$Na (Davis et al. 1995, *Physical Review Letters* 75, 3969 [verify]). Nobel 2001 to Cornell, Wieman, and Ketterle.

The composite-particle counting matters here. ${}^{87}$Rb: 37 protons + 50 neutrons + 37 electrons = 124 fermions, even, so the atom is a boson. ${}^4$He: 6 fermions, even, boson — and ${}^4$He becomes a superfluid below 2.17 K through a related (but more strongly interacting) condensation. ${}^3$He: 5 fermions, odd, fermion — and ${}^3$He superfluidity at 2.5 mK proceeds via Cooper pairing of atoms into composite bosons, a BCS-like mechanism. Same nuclear element, vastly different low-temperature physics, traced to a single parity.

### 6.1 A misconception: bosons attract, fermions repel

This is wrong as a statement about forces. There is no *statistical force* — no term in the Hamiltonian that couples to particle identity. What there is is a correlation in $|\psi(\vec{r}_1, \vec{r}_2)|^2$ that emerges from (anti)symmetrization. For two identical fermions in a symmetric spin state, the spatial wave function must be antisymmetric, so $|\psi_-(\vec{r}, \vec{r})|^2 \to 0$. For two identical bosons in any orbital combination, the symmetric spatial wave function enhances $|\psi_+(\vec{r}, \vec{r})|^2$ relative to the distinguishable case.

The right name for this is **exchange correlation**, not exchange force. The distinction matters because a student who pictures Pauli as a force will be unable to do the helium calculation cleanly. The Hamiltonian for two non-interacting electrons in a box has no exchange term. The Pauli node along $\vec{r}_1 = \vec{r}_2$ is purely a structural property of the antisymmetric wave function.

A correct way to phrase "Pauli's effect" without summoning a phantom force: in a many-fermion system, antisymmetry forces the wave function to occupy distinct single-particle states. Compressing the system requires populating more (higher-energy) single-particle modes, raising the total kinetic energy. The resulting **degeneracy pressure** is what holds up a white dwarf against gravitational collapse (Chandrasekhar 1931, *Astrophysical Journal* 74, 81 [verify pages]) or a neutron star against further collapse beyond a neutron star's mass. Chandrasekhar showed that this pressure has a relativistic limit at about $M_{\text{Ch}} \approx 1.4 M_\odot$ for the electron-degeneracy case — above which a white dwarf collapses to a neutron star or black hole. Nobel 1983 to Chandrasekhar, citing the work he did at age 19 on the boat from India to England.

Degeneracy pressure is kinetic in origin, not from any direct exchange potential. "Pauli prevents collapse" is correct in this sense; "Pauli is a force" is not.

---

## 7. Three misconceptions worth confronting

**Misconception 1: "Identical particles are just very similar particles."** They are not. Indistinguishability is a statement about which observables exist in the theory, not about how well our measuring devices can distinguish. The exchange operator $\hat{P}_{12}$ is a symmetry of the Hamiltonian, and its eigenvalues $\pm 1$ classify physical states. Two electrons in the universe are not "electron A" and "electron B" with similar properties; they are one quantum state of a two-electron system that has no factor of identity to separate them.

**Misconception 2: "The Pauli exclusion principle is a separate postulate."** It follows from antisymmetry of the multi-fermion wave function, which follows from the symmetrization postulate together with the spin-statistics theorem. Slater's construction makes the implication algorithmic: a determinant with two identical columns is zero. Pauli is a corollary, not a postulate. The 1925 "rule" is a pedagogical shorthand; the structural fact is antisymmetry.

**Misconception 3: "Bosons attract; fermions repel."** Wrong as forces. The Hamiltonian contains no exchange term. What there is is *exchange correlation* — a structure in the joint probability density $|\psi(\vec{r}_1, \vec{r}_2)|^2$ that emerges from (anti)symmetrization. For fermions, the joint density vanishes on the diagonal $\vec{r}_1 = \vec{r}_2$. For bosons, it is enhanced. There is no force pushing fermions apart; there is a correlation that makes them avoid each other in the symmetrization sense. The simulation in §9 makes this distinction visible — bosons cluster on the diagonal, fermions vanish there, and the *marginal* one-particle density is identical across both cases. There can be no force, because if there were, single-particle observables would differ.

---

## 8. Synthesis — what you can now do

This chapter is the conceptual hinge of multi-particle quantum mechanics. You have:

- A precise definition of "identical": the exchange operator $\hat{P}_{12}$ commutes with the Hamiltonian, and eigenstates can be chosen to have definite exchange eigenvalue $\pm 1$.
- A postulate (in 3+1 dimensions): each particle species sits in one of two slots — bosons (+1) or fermions (−1), correlating with integer or half-integer spin via the spin-statistics theorem.
- A construction (the Slater determinant) that builds the antisymmetric $N$-fermion wave function automatically.
- A derivation of the Pauli exclusion principle as a corollary of antisymmetry.
- A worked example (helium) that shows how exchange symmetry, through the exchange integral $K$, controls real measurable energy differences.
- A derivation of Hund's first rule as a corollary of antisymmetry + Coulomb.
- A first-principles account of the structure of the periodic table.

What this chapter does *not* do, and what comes next:

- **Second quantization.** Creation and annihilation operators $\hat{a}^\dagger_i, \hat{a}_i$ with anticommutators $\{\hat{a}_i, \hat{a}_j^\dagger\} = \delta_{ij}$ for fermions and commutators for bosons. The natural next step, but it requires more machinery than we have built. Ch. 13 may flag it.
- **The Hartree–Fock equations.** Computational chemistry territory. We named them; we did not solve them.
- **The full spin-statistics theorem.** Requires relativistic QFT. We postulated the bosons/fermions correspondence and named Pauli's 1940 paper.
- **BEC and BCS theory.** Mentioned briefly; the rich physics belongs to a condensed-matter course.
- **Anyons.** Mentioned in §2.3 as a flag. Their existence in 2D systems and their (currently active) role in topological quantum computing belongs to Ch. 13.

The visualizer you build below will travel forward. In Chapter 9 you will extend it to include a Coulomb interaction term and watch the wave function deform. In Chapter 13, the same two-particle framework supports the entangled states of quantum information.

---

## 9. LLM Exercise — Building the Two-Particle Symmetry Explorer

You are going to build a simulation that visualizes the joint probability density $|\psi(x_1, x_2)|^2$ for two particles in a 1D infinite well or harmonic oscillator, with a toggle for boson / fermion / distinguishable. The Pauli node along $x_1 = x_2$ for fermions, the boson clustering on the same diagonal, and the contrast with distinguishable particles — all appear in real time as the user drags sliders.

### 9.1 The CLAUDE.md prompt

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

### 9.2 The simulation prompt — four-move structure

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

### 9.3 Exploration tasks

1. **The Pauli node.** Set particle = fermion, $n_a = 1$, $n_b = 2$. Look at the heat map. The diagonal $x_1 = x_2$ should be a stripe of zero — the **Pauli node**. Now set $n_a = n_b = 1$. The status note should display: "ψ$_-$ = 0: Pauli forbidden." This is the simulation telling you directly that two fermions cannot occupy the same single-particle state.

2. **Bosonic clustering.** Switch particle = boson, keep $n_a = n_b = 1$. The wave function is now $\phi_1(x_1)\phi_1(x_2)$, perfectly fine. The heat map shows a single peak in the middle of the box, and the diagonal $x_1 = x_2$ runs right through the peak. Bosons happily share orbitals.

3. **Marginals don't reveal exchange.** Keep $n_a = 1, n_b = 2$. Cycle through particle = boson, fermion, distinguishable, and watch the heat map *change dramatically* — the Pauli node appears for fermions, the clustering on the diagonal appears for bosons. But the marginal line plot at the bottom should be *identical across all three cases*. The marginal $|\rho(x_1)|^2 = |\phi_1(x_1)|^2 + |\phi_2(x_1)|^2$ (after some integration) is the same regardless of exchange symmetry. This is the chapter's "exchange correlation lives in joint, not marginal" lesson, made visible. A single-particle detector cannot distinguish boson from fermion from distinguishable; only correlation measurements (two-particle coincidence) can.

4. **Compute and verify $\langle(x_1 - x_2)^2\rangle$.** Read the simulation's numerical readout for $\langle(x_1 - x_2)^2\rangle$ in each of the three cases at $n_a = 1, n_b = 2$. Confirm

$$ \langle(x_1 - x_2)^2\rangle_{\text{fermion}} > \langle(x_1 - x_2)^2\rangle_{\text{dist}} > \langle(x_1 - x_2)^2\rangle_{\text{boson}}. $$

Fermions spread; bosons cluster; distinguishable particles split the difference. Quantitatively, the difference between the symmetric and antisymmetric cases is $\pm 2|\langle x\rangle_{12}|^2$, where $\langle x\rangle_{12} = \langle\phi_1|x|\phi_2\rangle$ is the position matrix element between the two single-particle states.

5. **Spin extension and helium-like behavior.** Toggle the spin extension on. Select spin singlet, $n_a = n_b = 1$. Confirm the simulation shows $\phi_1(x_1)\phi_1(x_2)$ (symmetric spatial), which is allowed — this is the analog of the helium ground state. Now select spin triplet, $n_a = n_b = 1$. The status note should display "Pauli forbidden — triplet with both particles in same orbital is impossible." This is the Slater-determinant zero from §3.3, made visible.

6. **The 1s2s helium analog.** Spin extension on, select singlet, set $n_a = 1, n_b = 2$ — the parahelium 1s2s analog. The heat map is symmetric across the diagonal. Now select triplet — the orthohelium 1s2s analog. The heat map is antisymmetric across the diagonal, with a Pauli node. The exchange correlation that lowers orthohelium below parahelium (by $2K$) is geometrically visible: the electrons in the triplet case are kept apart, which would lower the Coulomb repulsion energy if you turned on an interaction.

### 9.4 Extension prompts

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

### 9.5 Six failure modes to watch for

1. **$1/\sqrt{2}$ normalization dropped.** A common bug: students forget the $1/\sqrt{2}$ in $\psi_\pm = (1/\sqrt{2})[\phi_a\phi_b \pm \phi_b\phi_a]$. The wave function is then over-normalized by a factor of 2, and $\langle\psi|\psi\rangle = 2$. Easy to spot — compute the integral $\int |\psi|^2 d^2r$ on the grid; if it's about 2 instead of 1, you dropped the factor.

2. **Marginals computed wrong.** $|\rho(x_1)|^2 = \int|\psi(x_1, x_2)|^2 dx_2$, summed over the $x_2$ axis (or columns) of your 2D grid, multiplied by $\Delta x_2$. Some students integrate over the wrong axis and get nonsense. Confirm by checking that $\int |\rho(x_1)|^2 dx_1 = 1$.

3. **Fermion $n_a = n_b$ case not handled.** If the code attempts to compute $(1/\sqrt{2})[\phi_a\phi_a - \phi_a\phi_a]$, it returns zero — but the visualization might display "all zero" as a uniform color and confuse the student. Display the status note clearly: "$\psi_-$ = 0: Pauli forbidden." This is a feature, not a bug.

4. **Color domain not reset between particle types.** If you set Viridis domain at $n_a = 1, n_b = 2$ for the boson case, then switch to fermion, the fermion heat map will look dim (because its peak is at the antisymmetric construction's maximum, in a different location). Recompute the domain per render.

5. **Diagonal overlay rendered before the heat map.** SVG renders later elements on top of earlier ones. If you draw the diagonal $x_1 = x_2$ red line and then draw the heat map rectangles, the diagonal will be hidden underneath. Draw the heat map first, then the diagonal overlay.

6. **Spin extension fails to enforce total antisymmetry.** A bug: the spin toggle lets the user select singlet + antisymmetric-spatial (which gives a symmetric total wave function — not allowed). Implement the spin-extension logic so that singlet *automatically* pairs with symmetric-spatial and triplet with antisymmetric-spatial. The user picks one of two physically meaningful combinations; the simulation does the pairing.

When you can drag $n_a$ and $n_b$ around, watch the Pauli node form and vanish, toggle through particle types and see the dramatic change in the joint density while the marginal stays the same, and toggle the spin extension to see the helium-like singlet/triplet behavior — at that point you have the machinery of multi-electron quantum mechanics on your screen, generated by you, governed by physics you can derive on demand.

---

**What would change my mind:** an experimental demonstration that some 3+1-dimensional particle species evades the bosons-or-fermions dichotomy — e.g., a particle whose multi-particle wave function neither symmetrizes nor antisymmetrizes under exchange — at a precision incompatible with the spin-statistics theorem within experimental and theoretical uncertainties.

**Still puzzling:** I can derive Pauli exclusion from antisymmetry and antisymmetry from the symmetrization postulate, but the postulate itself — *why* nature places each particle into exactly one of two boxes — is something I quote from QFT rather than understand from non-relativistic principles. The spin-statistics theorem is the deepest answer we have, and even it pushes the question one layer deeper: why do quantum fields at spacelike separation have to either commute or anticommute? "Microcausality" is the textbook answer; whether that answer is foundational or itself derivable, I don't know.

**Tags:** identical particles, exchange operator, symmetrization postulate, Pauli exclusion, Slater determinant, helium, exchange integral, Hund's rule, periodic table, D3.js
