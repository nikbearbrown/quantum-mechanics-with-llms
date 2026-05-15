# Chapter 9 — Time-Independent Perturbation Theory
*The art of squeezing answers from problems you cannot solve.*

Johannes Stark, working in Aachen in the fall of 1913, took a canal-ray tube, applied an electric field up to about $10^5$ V/cm to a hydrogen discharge, and watched the Balmer lines split. What he found was specific and strange: the $n = 2$ level, which is fourfold degenerate in the unperturbed atom — $2s$, $2p_0$, $2p_{+1}$, $2p_{-1}$, all at the same energy — split into exactly three lines. Not four. Three. One shifted up, one shifted down by the same amount, and one that did not shift at all. And the ground state barely moved.

Why three lines from four states? Why does the ground state shift so little while the $n = 2$ level splits dramatically? And why is the splitting symmetric — exactly equal distances up and down — rather than some lopsided mess?

These questions have clean answers, and the machinery that gives them is perturbation theory. That machinery is what this chapter builds.

---

## The setup

You can solve the harmonic oscillator. You can solve the hydrogen atom. After that, the list of exactly solvable three-dimensional bound-state problems is essentially empty. The square well, the Coulomb potential, the harmonic well, a handful of toy models with hidden symmetries — that is the inventory. Everything else in physics, from helium upward, requires approximation.

Perturbation theory is the most important of those approximations. The idea is simple. You have a Hamiltonian $\hat{H}_0$ whose eigenstates $|n^{(0)}\rangle$ and eigenvalues $E_n^{(0)}$ you know exactly. Reality gives you something else:

$$\hat{H} = \hat{H}_0 + \lambda \hat{H}'$$

where $\hat{H}'$ is some additional term and $\lambda$ is a small dimensionless parameter — a knob you can think of as being slowly turned up from zero. The question: how do the energies and states change as $\lambda$ increases?

The strategy is to expand the answer as a power series in $\lambda$:

$$|n\rangle = |n^{(0)}\rangle + \lambda|n^{(1)}\rangle + \lambda^2|n^{(2)}\rangle + \cdots$$
$$E_n = E_n^{(0)} + \lambda E_n^{(1)} + \lambda^2 E_n^{(2)} + \cdots$$

Substitute into $\hat{H}|n\rangle = E_n|n\rangle$, expand both sides, and collect terms at each power of $\lambda$. The whole machine lives in that one move.

---

## What the machine gives you

At zeroth order in $\lambda$ you recover the unperturbed problem. No news.

At first order, take the inner product of the first-order equation with $\langle n^{(0)}|$. The $\hat{H}_0$ terms cancel because $\hat{H}_0$ is Hermitian — the same trick that appeared in Chapter 4 whenever we wanted to extract information from an eigenvalue equation. What is left is remarkably clean:

$$\boxed{E_n^{(1)} = \langle n^{(0)}|\hat{H}'|n^{(0)}\rangle}$$

The first-order shift in the energy is the expectation value of the perturbation in the unperturbed state. That is all. If you can compute that integral, you have the leading correction without any new diagonalization.

The correction to the state comes from taking the inner product with a *different* unperturbed state $\langle m^{(0)}|$, $m \neq n$. Working through the same algebra:

$$|n^{(1)}\rangle = \sum_{m \neq n} \frac{\langle m^{(0)}|\hat{H}'|n^{(0)}\rangle}{E_n^{(0)} - E_m^{(0)}}\,|m^{(0)}\rangle$$

Read this carefully. The perturbation mixes neighboring states into each other. The amount of mixing depends on two things: how large the matrix element $\langle m|\hat{H}'|n\rangle$ is — how strongly the perturbation connects the two states — and how large the energy gap $E_n^{(0)} - E_m^{(0)}$ is. Small gap means large mixing. That is not surprising: a tiny perturbation can have a large effect on states that are nearly degenerate in energy.

And there it is — the denominator that will cause trouble. When $E_m^{(0)} \to E_n^{(0)}$, the formula blows up. The machine has broken. But it is not perturbation theory that failed; it is the *basis*. You started with the wrong zeroth-order states for this problem.

At second order, the energy correction is:

$$E_n^{(2)} = \sum_{m \neq n}\frac{|\langle m^{(0)}|\hat{H}'|n^{(0)}\rangle|^2}{E_n^{(0)} - E_m^{(0)}}$$

The numerator is a squared absolute value — always non-negative. The denominator changes sign: states above $n$ make it negative; states below make it positive. For the ground state, every other state sits above it. Every denominator is negative. Every term in the sum is negative. This gives us a small theorem: **the second-order correction to the ground-state energy is always negative**. Whatever the perturbation, the ground state always gets pushed down at second order. It is a consequence of one sign, and it is exact.

<!-- → [INFOGRAPHIC: schematic diagram of the three perturbation corrections — three horizontal panels stacked vertically, each showing an energy level E_n with arrows indicating the correction at that order; panel 1: "zeroth order — the level you started with, no shift"; panel 2: "first order — shifts by ⟨n|H'|n⟩, the expectation value, shown as a single upward or downward arrow"; panel 3: "second order — a sum over all other states m, each contributing a term proportional to |⟨m|H'|n⟩|²/(E_n−E_m), ground state always goes down"; caption: "The machine in three steps. Each order squeezes one more digit of accuracy from the perturbation"] -->

---

## When the denominator vanishes: degenerate perturbation theory

Suppose two unperturbed states share an energy: $E_a^{(0)} = E_b^{(0)}$. The first-order state correction has a zero in the denominator — the formula is undefined. Something has gone wrong, but it is not that perturbation theory itself fails. It is that the *basis choice within the degenerate subspace* was wrong.

Here is what I mean. If $\hat{H}_0|a\rangle = E^{(0)}|a\rangle$ and $\hat{H}_0|b\rangle = E^{(0)}|b\rangle$, then any linear combination $\alpha|a\rangle + \beta|b\rangle$ is also an eigenstate of $\hat{H}_0$ at the same energy. The unperturbed Hamiltonian cannot distinguish between bases in the degenerate subspace — all are equally good at zeroth order. The perturbation $\hat{H}'$ breaks this symmetry and picks out a preferred basis: the one in which states connect smoothly to the perturbed eigenstates as $\lambda \to 0$.

The fix is direct. Restrict $\hat{H}'$ to the degenerate subspace and write it as a matrix:

$$W_{ij} = \langle i|\hat{H}'|j\rangle$$

Diagonalize $W$. The eigenvalues are the first-order energy corrections. The eigenvectors are the "good" zeroth-order states — the unique linear combinations that perturbation theory needs as its starting point.

Non-degenerate perturbation theory is not the general case. It is what you get when the degenerate subspace is one-dimensional, so the diagonalization is trivial. Whenever there is symmetry — and hydrogen has it in spades — you should reach for the degenerate version first.

---

## The Stark effect: three lines from four states

Now we have the tools to answer Stark's puzzle.

Apply a uniform electric field along $\hat{z}$ to a hydrogen atom. The perturbation is $\hat{H}' = e\mathcal{E}\hat{z}$. For the ground state $|1s\rangle$, the first-order shift is:

$$E_1^{(1)} = \langle 1s|e\mathcal{E}\hat{z}|1s\rangle = 0$$

It vanishes by parity. The $|1s\rangle$ wave function is parity-even, $\hat{z}$ is parity-odd, so the integrand is parity-odd and integrates to zero over all space. There is no first-order shift. The ground state shifts only at second order — quadratically in $\mathcal{E}$, very small for ordinary lab fields.

For the $n = 2$ level we have four degenerate states: $|2s\rangle$, $|2p_0\rangle$, $|2p_{+1}\rangle$, $|2p_{-1}\rangle$. We need the $4\times 4$ matrix of $\hat{H}' = e\mathcal{E}\hat{z}$ in this subspace, then we diagonalize it.

Selection rules eliminate most entries before we compute anything. The operator $\hat{z}$ commutes with $\hat{L}_z$ — it cannot change the $z$-component of angular momentum — so matrix elements with $\Delta m \neq 0$ vanish. That zeroes out everything involving $|2p_{\pm 1}\rangle$ coupling to $|2s\rangle$ or $|2p_0\rangle$. Parity kills the remaining diagonal entries: $\langle 2s|\hat{z}|2s\rangle = 0$ (parity-even times parity-odd), and $\langle 2p_0|\hat{z}|2p_0\rangle = 0$ similarly.

The only surviving entry is $\langle 2s|\hat{z}|2p_0\rangle$. Compute it directly from the radial and angular integrals:

$$\langle 2s|\hat{z}|2p_0\rangle = -3a_0$$

So the full $4\times 4$ matrix, with rows and columns ordered $\{|2s\rangle, |2p_0\rangle, |2p_{+1}\rangle, |2p_{-1}\rangle\}$:

$$W = e\mathcal{E}\begin{pmatrix} 0 & -3a_0 & 0 & 0 \\ -3a_0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{pmatrix}$$

This block-diagonalizes immediately. The bottom $2\times 2$ block is the zero matrix — $|2p_{+1}\rangle$ and $|2p_{-1}\rangle$ are already good states and they do not shift. The top $2\times 2$ block:

$$\begin{pmatrix} 0 & -3a_0 e\mathcal{E} \\ -3a_0 e\mathcal{E} & 0 \end{pmatrix}$$

has eigenvalues $\pm 3a_0 e\mathcal{E}$ and eigenvectors $(|2s\rangle \mp |2p_0\rangle)/\sqrt{2}$.

The $n=2$ level splits into three lines: one up by $3a_0 e\mathcal{E}$, one down by $3a_0 e\mathcal{E}$, and a doubly degenerate pair that does not shift. Three lines from four states. The "good" zeroth-order eigenstates are the $(|2s\rangle \pm |2p_0\rangle)/\sqrt{2}$ hybrids — probability clouds asymmetric along $\hat{z}$, which is exactly what couples to a field in the $\hat{z}$ direction. The $|2p_{\pm 1}\rangle$ states are azimuthally symmetric about $\hat{z}$ and cannot polarize along it at first order; they sit still.

The splitting is linear in $\mathcal{E}$ — a linear Stark effect — while the ground state has a quadratic Stark effect. The difference comes from the degeneracy. Degenerate states mix with each other at first order; non-degenerate states can only mix with states at different energies, which costs more and enters at second order.

Stare at the matrix until the answer feels obvious. Then build the simulation and watch the three lines emerge from one as you turn the field up.

<!-- → [INFOGRAPHIC: Stark splitting diagram for the n=2 manifold — left side: four degenerate horizontal lines all at E_2 = −3.4 eV, labeled |2s⟩, |2p₀⟩, |2p₊₁⟩, |2p₋₁⟩; right side: the split levels after applying field ε, showing (|2s⟩−|2p₀⟩)/√2 shifted up by +3a₀eε, (|2s⟩+|2p₀⟩)/√2 shifted down by −3a₀eε, and |2p±1⟩ pair flat; the 4×4 W matrix shown between them with the two off-diagonal −3a₀eε entries highlighted and all other entries zero; caption: "Three lines from four states. Selection rules zero out the matrix everywhere except one entry; that one entry splits the fourfold degeneracy into three distinct levels"] -->

<!-- → [IMAGE: electron probability density cross-sections of the two Stark eigenstates (|2s⟩±|2p₀⟩)/√2 in the xz-plane — left panel: (|2s⟩−|2p₀⟩)/√2 showing density shifted toward +z (polarized up); right panel: (|2s⟩+|2p₀⟩)/√2 showing density shifted toward −z (polarized down); Viridis color scale; caption: "The 'good' zeroth-order states are polarized clouds. One has its electron shifted upward along the field axis, the other downward — exactly what you need to couple to an electric field"] -->

---

## When perturbation theory breaks

So far the story sounds clean: expand in $\lambda$, compute corrections order by order, get increasingly accurate answers. But there is something hiding in the formalism that Dyson noticed in 1952, and it changes everything.

Take the harmonic oscillator and add a quartic perturbation:

$$\hat{H} = \frac{\hat{p}^2}{2m} + \tfrac{1}{2}m\omega^2\hat{x}^2 + \lambda\hat{x}^4$$

The first-order correction uses $\hat{x} = \sqrt{\hbar/2m\omega}(\hat{a}_+ + \hat{a}_-)$, so $\hat{x}^4$ expressed in ladder operators has diagonal matrix elements:

$$\langle n|\hat{x}^4|n\rangle = \left(\frac{\hbar}{2m\omega}\right)^2(6n^2 + 6n + 3)$$

The first-order energy shift is:

$$E_n^{(1)} = \lambda\cdot\frac{3\hbar^2}{4m^2\omega^2}(2n^2 + 2n + 1)$$

Notice that this grows as $n^2$. Perturbation theory works worst for highly excited states, where the wave function extends furthest and probes the $\hat{x}^4$ term most strongly. The second-order correction is computable too — matrix elements $\langle m|\hat{x}^4|n\rangle$ are nonzero for $m = n, n\pm 2, n\pm 4$, with energy denominators $\pm 2\hbar\omega$ and $\pm 4\hbar\omega$. Everything looks controlled for small $\lambda$.

Then Bender and Wu asked, in a 1969 calculation, what happens when you compute all the higher-order corrections. What they found is that the perturbation series for the quartic oscillator has zero radius of convergence. The coefficients $E_n^{(k)}$ grow faster than $k!$ as $k \to \infty$. The series

$$E_n(\lambda) = E_n^{(0)} + E_n^{(1)}\lambda + E_n^{(2)}\lambda^2 + \cdots$$

diverges for every nonzero value of $\lambda$.

And yet the series is *useful*. Truncate at the optimal order — the term where the coefficients bottom out before starting to grow — and you get an answer exponentially close to the true energy. Add more terms past that point and the approximation gets worse. The series is not a convergent sum. It is an asymptotic expansion, and there is a deep reason for it.

Dyson gave the argument for quantum electrodynamics, but it applies here too. Suppose $\lambda < 0$. The quartic term $\lambda\hat{x}^4$ is now *negative*, which means the potential goes to $-\infty$ as $|x| \to \infty$. The Hamiltonian is unbounded below; there is no normalizable ground state. The energy, as a function of $\lambda$, is not analytic at $\lambda = 0$ — it has a singularity somewhere on the negative real axis, even if the physical value of $\lambda$ is small and positive. Any Taylor series centered at $\lambda = 0$ must capture that singularity somehow, and it does so by diverging. **Perturbation series almost always diverge.** The coupling constant in QED is the fine-structure constant $\alpha \approx 1/137$, and the same argument applies: flip the sign of $\alpha$, the vacuum is unstable, the energy is non-analytic at $\alpha = 0$, the QED perturbation series diverges.

This should alarm you. All of the spectacular agreements between QED and experiment — the electron anomalous magnetic moment, computed and measured to thirteen significant figures — rest on a divergent series. That they are still right is one of the genuinely strange things about quantum field theory. The series diverges; the partial sum at optimal truncation is exponentially close to the truth. Why? The answer involves Borel summation and resurgent analysis — techniques that reconstruct the exact answer from the divergent series by analytic continuation in carefully chosen ways. They work. The theoretical understanding is still evolving. The empirical fact is not in doubt.

The simulation you will build lets you watch this directly. Turn $\lambda$ up. First-order PT diverges from the exact answer at some value of $\lambda$; second-order PT does better for a while and then also fails. Past the optimal truncation, every additional term moves you further from the truth.

Two misconceptions are worth naming.

*"Perturbation theory always converges as long as the terms get smaller."* The terms can get smaller, then start to grow again. The optimal truncation is the term where they reach their minimum. Past it, more terms hurt.

*"First-order is always sufficient for small $\lambda$."* Only when there is no near-degeneracy. If two unperturbed states are nearly degenerate, the second-order correction has a tiny denominator and can be large even when $\lambda$ is small. Always check the ratio $|\langle m|\hat{H}'|n\rangle|/|E_n^{(0)} - E_m^{(0)}|$ before trusting first-order. If it is not small, you need degenerate or near-degenerate perturbation theory.

<!-- → [CHART: three overlaid curves of E_0(λ) vs. λ for the anharmonic oscillator (natural units ℏ=m=ω=1) — solid black: exact numerical diagonalization; dashed teal: E_0^(0) + λE_0^(1) (first-order PT); dashed orange: E_0^(0) + λE_0^(1) + λ²E_0^(2) (second-order PT); x-axis: λ from 0 to 0.5; curves track closely at small λ then diverge; a shaded region beyond the departure point labeled "PT unreliable"; caption: "First-order and second-order PT both eventually fail. The departure happens earlier for higher n. Adding more orders past the optimal truncation makes things worse, not better"] -->

<!-- → [CHART: log-scale plot of |E_0^(N) − E_0^exact| vs. truncation order N for the anharmonic oscillator at λ=0.1 — the curve descends steeply from N=0 to N≈4 (optimal truncation), marked with a vertical dashed line labeled "optimal truncation N*"; then rises as higher orders are added; caption: "The Bender–Wu asymptotic series: truncate at the minimum (N*) for the best answer. Every term added beyond N* moves you further from the truth. This is what a divergent-but-useful series looks like"] -->

---

## Hydrogen fine structure

Hydrogen, as computed in Chapter 7 using the bare Coulomb Hamiltonian, has energies $E_n^{(0)} = -13.6\,\text{eV}/n^2$ depending only on $n$. High-resolution spectroscopy reveals small corrections at the level of $\alpha^2 E_n^{(0)} \sim 10^{-4}\,\text{eV}$ for $n = 2$, where $\alpha = e^2/(4\pi\epsilon_0\hbar c) \approx 1/137$ is the fine-structure constant. These are the fine structure corrections, and three perturbations produce them.

The relativistic kinetic term: the non-relativistic kinetic energy $\hat{p}^2/2m$ is the leading term in the expansion of $\sqrt{p^2c^2 + m^2c^4} - mc^2$. At the next order:

$$\hat{H}'_\text{rel} = -\frac{\hat{p}^4}{8m^3c^2}$$

This shifts every level. Spin-orbit coupling: in the electron's rest frame, the orbiting proton generates a magnetic field that couples to the electron's spin magnetic moment. After the Thomas precession correction of $1/2$:

$$\hat{H}'_\text{SO} = \frac{1}{2m^2c^2}\frac{1}{r}\frac{dV}{dr}\,\vec{L}\cdot\vec{S}$$

For the Coulomb potential this reduces to something proportional to $\vec{L}\cdot\vec{S}/r^3$. The Darwin term: a purely relativistic correction, nonzero only for $\ell = 0$ states where the electron has finite probability at the nucleus:

$$\hat{H}'_\text{Darwin} = \frac{\pi\hbar^2}{2m^2c^2}\frac{e^2}{4\pi\epsilon_0}\,\delta^3(\vec{r})$$

All three corrections are of order $\alpha^2$ times the Rydberg energy. The unperturbed hydrogen levels at fixed $n$ are $n^2$-fold degenerate — the Coulomb degeneracy discussed in Chapter 7. Apply degenerate perturbation theory: diagonalize the sum of the three perturbations in the degenerate $n$-manifold.

The key insight is that $\vec{L}\cdot\vec{S}$ commutes with $\hat{J}^2$ and $\hat{J}_z$ where $\hat{J} = \hat{L} + \hat{S}$ is the total angular momentum. The good quantum numbers that diagonalize the perturbation are $(n, \ell, j, m_j)$ — where $j = \ell \pm 1/2$ — rather than the separate $(n, \ell, m_\ell, m_s)$ pair. After the calculation, the fine-structure energy correction is:

$$E_n^\text{fs} = \frac{(E_n^{(0)})^2}{2mc^2}\left(\frac{2n}{j + 1/2} - \frac{3}{2}\right)$$

This depends on $n$ and $j$ only — not on $\ell$ separately. So the $2p_{1/2}$ and $2s_{1/2}$ states ($j = 1/2$, different $\ell$) remain degenerate after fine structure. The $2p_{3/2}$ state ($j = 3/2$) sits about $4.5 \times 10^{-5}\,\text{eV}$ above the $j = 1/2$ pair.

Experimentally, $2s_{1/2}$ and $2p_{1/2}$ are not exactly degenerate. There is a $\sim 4 \times 10^{-6}\,\text{eV}$ splitting called the Lamb shift, first measured by Lamb and Retherford in 1947. It is a QED effect — quantization of the electromagnetic field, vacuum fluctuations — and it lies beyond the semiclassical perturbation theory of this chapter. The chapter cannot derive the Lamb shift. It can only point at it and mark where the chapter's framework ends.

<!-- → [IMAGE: hydrogen n=2 fine-structure energy level diagram — starting from the degenerate n=2 level at −3.4 eV on the left; a first split shows 2p_{3/2} (j=3/2) rising by ~4.5×10⁻⁵ eV and 2s_{1/2}, 2p_{1/2} (j=1/2) remaining degenerate; a second split (magnified inset) shows 2s_{1/2} lifted above 2p_{1/2} by the Lamb shift ~4×10⁻⁶ eV; each level labeled with (n, ℓ, j); a bracket labels the fine-structure splitting as "~α² × E_2"; a second bracket labels the Lamb shift as "QED — beyond this chapter"; caption: "Three perturbations, two splittings. Fine structure lifts the j-degeneracy; the Lamb shift requires quantizing the electromagnetic field itself"] -->

---

## Still puzzling

It is not obvious why a divergent series should give good answers at all. Borel summation, transseries, resurgent analysis — Écalle, Costin, Mariño — recover information from the divergent tail by analytic continuation in cleverly chosen ways. The arguments work in some cases and fail in others. I do not have a satisfying answer to *why* truncating at the optimal order is exponentially close to the truth in every well-studied case. The empirical fact is that it is. The theoretical understanding is still in progress.

---

## LLM Exercise — the perturbation explorer

You are going to build a single-file D3 simulation that does two things at once: shows the anharmonic-oscillator energy levels as functions of $\lambda$, with first-order and second-order PT compared against exact numerical diagonalization (so you can watch PT diverge); and shows the hydrogen $n=2$ Stark manifold splitting into three lines as the electric field turns up (so you can watch degenerate PT do its job). The deliverable is `09-perturbation-explorer.html` in your working directory.

### Part 1 — Update `PROJECT.md`

```
Append a new entry to PROJECT.md describing this chapter's simulation:

Chapter 09 — Time-Independent Perturbation Theory
Deliverable: 09-perturbation-explorer.html
Status: in progress

The simulation has two modes, selectable by tab:

Mode A — Anharmonic oscillator. Hamiltonian H = HO + lambda * x^4. Three
curves of E_n(lambda) plotted vs. lambda for n = 0..4:
  - First-order PT (dashed teal)
  - Second-order PT (dashed orange)
  - Exact numerical diagonalization on a truncated 30x30 basis (solid black)
Slider for lambda from 0 to 0.5 (in natural units where hbar = m = omega = 1).
Slider for which n to highlight. When |E_n^(2)| > |E_n^(0) - E_{n+1}^(0)| / 4
display the warning text "PT NO LONGER RELIABLE" in red below the active level.

Mode B — Hydrogen Stark effect on n=2 manifold. Four horizontal energy
levels, all starting at E_2^(0) (unperturbed n=2 hydrogen energy) on the
left. Slider for electric-field strength E in atomic units (0 to 0.05;
above this hydrogen ionizes). As E increases:
  - The (|2s> + |2p_0>)/sqrt(2) state shifts up by +3 a_0 e E
  - The (|2s> - |2p_0>)/sqrt(2) state shifts down by -3 a_0 e E
  - The |2p_{+1}> and |2p_{-1}> states stay flat
Annotate the eigenstates next to their lines. Show the 4x4 W matrix on
the right; live-update as the field changes.

Natural units throughout: hbar = m = 1 for the oscillator; atomic units
(a_0 = 1, e = 1, energy in Hartree) for the Stark effect.
Render at 60 fps; smooth slider response.
```

### Part 2 — The CLAUDE.md amendment

```
Append to CLAUDE.md the following physics rules for Chapter 9 simulations:

PERTURBATION-THEORY PHYSICS RULES

1. ANHARMONIC OSCILLATOR — first-order energy correction:
   E_n^(1) = (3 hbar^2 / (4 m^2 omega^2)) * (2 n^2 + 2 n + 1)
   In natural units (hbar = m = omega = 1): E_n^(1) = (3/4)(2n^2 + 2n + 1).
   E_n^(0) = n + 1/2.

2. ANHARMONIC OSCILLATOR — second-order correction. Matrix elements
   <m | x^4 | n> are nonzero for m = n-4, n-2, n, n+2, n+4. Compute
   using ladder-operator expansion of x = (a_+ + a_-)/sqrt(2):
     x^4 = (1/4)(a_+ + a_-)^4
   Expand by binomial theorem; collect terms that map |n> to a given |m>.
   The diagonal (m=n) term gives E_n^(1) above. The off-diagonal terms
   feed E_n^(2) = sum |<m|x^4|n>|^2 / (E_n^(0) - E_m^(0)) for m != n.

3. ANHARMONIC OSCILLATOR — exact diagonalization. Build H = H_0 + lambda * X4
   in the harmonic-oscillator basis, truncated at N = 30. The matrix is
   pentadiagonal (nonzero on diagonal, plus or minus 2, plus or minus 4).
   Diagonalize using Jacobi rotation or a tridiagonal reduction. Sort
   eigenvalues; the first 5 are E_n^exact for n = 0..4.

4. WARNING TRIGGER. After computing E_n^(1), E_n^(2), display the warning
   text "PT NO LONGER RELIABLE" when |E_n^(2)| > |E_{n+1}^(0) - E_n^(0)| / 4.
   This is the empirical onset of breakdown; the second-order correction
   exceeds one quarter of the unperturbed level spacing.

5. STARK EFFECT — n=2 manifold. The only nonzero matrix element of e * E * z
   in the 4-dim n=2 subspace is
     <2s | z | 2p_0> = -3 a_0
   (with our sign convention; absolute value is what enters the eigenvalues).
   The 4x4 matrix:
        2s    2p_0   2p_{+1}  2p_{-1}
     2s   0    -3 a_0 e E   0       0
     2p_0  -3 a_0 e E   0   0       0
     2p_+1  0     0      0       0
     2p_-1  0     0      0       0
   Eigenvalues: +3 a_0 e E, -3 a_0 e E, 0, 0. Eigenvectors of the upper
   2x2 block: (|2s> mp |2p_0>) / sqrt(2).

6. UNITS. For the oscillator: hbar = m = omega = 1, so x and lambda are
   dimensionless. For Stark: atomic units, a_0 = e = 1, energy in Hartree
   (E_2^(0) = -1/8 Hartree). Field strength E_field measured in
   Hartree/(e * a_0) = 5.14e9 V/cm.

KNOWN FAILURE MODES:
(a) Numerical diagonalization of x^4 in too-small a basis. For lambda = 0.5,
    use N >= 50. For lambda <= 0.2, N = 30 suffices.
(b) Sign error in <2s | z | 2p_0>. The integral is straightforward; do it
    once and pin the value to the code.
(c) Forgetting that the 2p_{plus/minus 1} states do NOT shift at first order.
    They appear in the matrix but contribute zero rows/columns.
(d) Plotting E_n^(2) without its sign. The ground-state second-order
    correction is negative; show the negative sign explicitly.
```

### Part 3 — The simulation prompt

```
You are working in my directory which contains CLAUDE.md, DESIGN.md, and
PROJECT.md. Read all three first.

Build 09-perturbation-explorer.html: a single self-contained HTML file using
D3 v7 from a CDN and d3-simple-slider (https://cdn.jsdelivr.net/npm/d3-simple-slider).
No other dependencies. The simulation has two modes selectable by tabs at
the top: "Anharmonic oscillator" and "Stark effect n=2".

ANHARMONIC OSCILLATOR MODE
Single SVG canvas 1100 x 600. Left half (550 wide): energy-level diagram.
Horizontal lines at the current E_n(lambda) for n = 0..4, computed via
exact diagonalization. Pin the y-axis from 0 to 8 in natural units so
levels stay in view as they shift. Right half (550 wide): plot of
E_n(lambda) vs. lambda for the currently highlighted n. Three overlaid
curves: first-order PT (dashed teal), second-order PT (dashed orange),
exact (solid black). X-axis: lambda from 0 to 0.5. Y-axis: pinned to a
range that shows the divergence at large lambda for the active n.

Controls:
- Lambda slider, range 0 to 0.5, default 0.1
- n selector, integer 0..4 via buttons or a small slider
- Warning text "PT NO LONGER RELIABLE" appears in red below the active
  level when the trigger condition fires (see CLAUDE.md item 4)

STARK EFFECT MODE
Single SVG canvas 1100 x 600. Left half (700 wide): four horizontal
energy lines starting at E_2 = -1/8 Hartree on the left edge. As the
field slider increases from 0 to 0.05 atomic units, the lines move
according to the eigenvalues of the 4x4 matrix from CLAUDE.md item 5.
Annotate each line with its eigenstate at the right edge: top line
"(|2s> - |2p_0>)/sqrt(2)", middle line "|2p_+1>, |2p_-1>", bottom line
"(|2s> + |2p_0>)/sqrt(2)". Right half (400 wide): the 4x4 W matrix
displayed live with current numerical entries. Highlight the only
nonzero entry (the -3 a_0 e E off-diagonal pair).

Controls:
- Electric field strength slider, range 0 to 0.05 a.u., default 0.01
- Toggle: "show eigenvectors" (default on) vs. "show matrix only"

GLOBAL
Implement the Jacobi diagonalization or symmetric-tridiagonal reduction
in pure JavaScript. Do NOT use math.js, numeric.js, or any other library
beyond D3 v7 and d3-simple-slider. The diagonalization for a 30x30
matrix should take under 100ms.

Runtime sanity checks to console:
- For lambda = 0, the diagonalized energies should equal n + 1/2 within 1e-6.
- For E_field = 0, the Stark eigenvalues should all equal 0 (relative to
  the unperturbed n=2 level).
- The sum of the four Stark eigenvalues should equal 0 (trace of a traceless
  matrix) at every field strength.

Comments at every non-trivial physics step. No dead code. Pure functions
for the matrix-element computation and the diagonalization.
```

### Part 4 — Exploration tasks and extension prompt

Run the simulation and answer the following:

1. Anharmonic mode, $n=0$. Slide $\lambda$ from $0$ to $0.5$. At what value of $\lambda$ does first-order PT depart from the exact curve by more than 10%? At what value does *second-order* PT depart by more than 10%? Note the warning text trigger; record the $\lambda$ at which it fires.

2. Repeat for $n=4$. The departure happens earlier — PT works worst for high-$n$ states. Quantify: what is the ratio of the breakdown $\lambda$ for $n=4$ vs. $n=0$?

3. Stark mode. Set the field strength to $\mathcal{E} = 0.01$ atomic units. Verify by hand that the upper eigenvalue is $+3a_0 e\mathcal{E} = 0.03$ Hartree, and that the two middle lines do not shift. Increase the field. The simulation should remain accurate up to $\mathcal{E} \sim 0.04$ a.u.; above that, real hydrogen ionizes via the tilted-Coulomb mechanism (Stark ionization), which this simulation does not capture.

4. Toggle off the "show eigenvectors" view in Stark mode. Look at the matrix. The two shifted lines come from diagonalizing a $2\times 2$ block; the two flat lines come from a $2\times 2$ zero block. Confirm this is what you see.

5. Back to anharmonic mode. Set $\lambda = 0.3$ and toggle $n$ through 0, 1, 2, 3, 4 quickly. Where do first-order and second-order PT agree with the exact result, and where do they not? The pattern — PT works better for the ground state than for excited states — should be visible.

**Extension prompt:**

```
Modify 09-perturbation-explorer.html to add a third mode: "Asymptotic
truncation". For the anharmonic oscillator at fixed lambda = 0.1 and
n = 0, compute the first N terms of the perturbation series E_0^(0) +
sum_k lambda^k E_0^(k) for k = 0..20. Plot the partial sum vs. N as a
log-scale plot of |E_0^N - E_0^exact|. Mark the minimum of this curve
(the optimal truncation order) with a vertical line. Below it, in
caption text, name this regime as "Bender-Wu 1969 asymptotic behavior".

To compute E_0^(k) for k > 2, use the recursive Rayleigh-Schrodinger
formula on the 30x30 truncated basis. (You can also do this by computing
E_0^exact, fitting the partial sum, and showing the divergence
empirically without deriving E_0^(k) symbolically.)

Update PROJECT.md to mark Chapter 09 as complete and note the asymptotic-
series extension as the bridge to Chapter 10, where time-dependent PT
extends the formalism into the time domain.
```

---

## Exercises

### Warm-up

**9.1** Take the harmonic oscillator with perturbation $\hat{H}' = \lambda\hat{x}^3$. (a) By a parity argument, explain why $E_n^{(1)} = 0$ for every $n$. (b) Now compute $E_0^{(2)}$ for the cubic perturbation. You need the matrix elements $\langle m|\hat{x}^3|0\rangle$; use $\hat{x} = \sqrt{\hbar/2m\omega}(\hat{a}_+ + \hat{a}_-)$ and ladder algebra to find which $m$ contribute and with what value. Show the result is negative. *(Tests: parity argument for vanishing first-order corrections; second-order calculation from ladder-operator matrix elements; verification that the ground state goes down.)*

**9.2** For the infinite square well of width $L$ with $\psi_n(x) = \sqrt{2/L}\sin(n\pi x/L)$, add a constant perturbation $\hat{H}' = V_0$ over the entire well. (a) Compute $E_n^{(1)}$ for all $n$. The answer should be $V_0$ — explain in one sentence why this is exact and why second-order PT adds nothing. (b) Now perturb with $\hat{H}' = V_0$ over only the left half of the well ($0 < x < L/2$). Compute $E_1^{(1)}$ and $E_2^{(1)}$. Are they equal? *(Tests: first-order expectation-value calculation in a simple basis; recognizing when the perturbation series terminates.)*

**9.3** State the selection rules that kill the off-diagonal entries of the $4\times 4$ Stark matrix for the hydrogen $n = 2$ manifold, *before* computing a single integral. For each of the five independent pairs $\{2s, 2p_0\}$, $\{2s, 2p_{+1}\}$, $\{2s, 2p_{-1}\}$, $\{2p_0, 2p_{+1}\}$, $\{2p_0, 2p_{-1}\}$: state which selection rule — parity or $\Delta m = 0$ — kills the matrix element, or confirm it survives. *(Tests: application of selection rules before calculation; understanding which symmetry kills which entry.)*

### Application

**9.4** The second-order correction to the ground-state energy of hydrogen in a uniform electric field $\mathcal{E}$ is $E_1^{(2)} = -\frac{1}{2}\alpha_\text{pol}\mathcal{E}^2$, where $\alpha_\text{pol}$ is the polarizability. (a) From the formula $E_n^{(2)} = \sum_{m\neq n}|\langle m|\hat{H}'|n\rangle|^2/(E_n^{(0)} - E_m^{(0)})$, explain the sign: why is $E_1^{(2)}$ guaranteed to be negative for the ground state? (b) The dominant contribution to $\alpha_\text{pol}$ comes from the $|2p\rangle$ intermediate state. Estimate $E_1^{(2)}$ by keeping only that term, using $|\langle 2p|\hat{z}|1s\rangle|^2 = 2^{15}a_0^2/3^{10}$ (look this up or quote it). Compare your estimate to the exact value $\alpha_\text{pol} = \frac{9}{2}a_0^3$. *(Tests: second-order formula applied to a physical system; the dominant-intermediate-state approximation; understanding why the ground-state quadratic Stark shift is small.)*

**9.5** The anharmonic oscillator $\hat{H} = \hat{H}_\text{HO} + \lambda\hat{x}^4$ in natural units ($\hbar = m = \omega = 1$). (a) Compute $E_0^{(1)}$ using the formula $\langle n|\hat{x}^4|n\rangle = \frac{3}{4}(2n^2 + 2n + 1)$. (b) The first-order correction to $E_0$ grows as $n^2$ for large $n$. At what $n$ does the first-order correction $\lambda E_n^{(1)}$ become comparable to the unperturbed spacing $\hbar\omega = 1$ for $\lambda = 0.1$? This is the $n$ at which PT first becomes unreliable. (c) Without computing, explain why the second-order correction $E_n^{(2)}$ is negative for the ground state and positive for some excited states. *(Tests: first-order ladder-operator calculation; identifying the breakdown regime; sign analysis of second-order corrections.)*

**9.6** Hydrogen fine structure. The energy formula is $E_n^\text{fs} = \frac{(E_n^{(0)})^2}{2mc^2}\!\left(\frac{2n}{j+1/2} - \frac{3}{2}\right)$. (a) Compute the fine-structure correction for the $n=2$, $j=3/2$ state and the $n=2$, $j=1/2$ state numerically in eV. (b) The splitting between $2p_{3/2}$ and $2p_{1/2}$ is $\Delta E_{FS}$. Express it as a multiple of $\alpha^2|E_2^{(0)}|$ and verify it is approximately $4.5\times 10^{-5}$ eV. (c) The Lamb shift lifts the $2s_{1/2}$–$2p_{1/2}$ degeneracy by $\sim 4\times 10^{-6}$ eV. How does this compare in magnitude to the fine-structure splitting? *(Tests: numerical evaluation of the fine-structure formula; understanding the hierarchy of corrections; locating where QED effects become visible.)*

### Synthesis

**9.7** Degenerate perturbation theory for a two-level system. Two states $|a\rangle$ and $|b\rangle$ share energy $E^{(0)}$. The perturbation matrix in this subspace is $W = \begin{pmatrix} \alpha & \beta \\ \beta^* & \alpha \end{pmatrix}$ where $\alpha$ is real and $\beta$ may be complex. (a) Find the two eigenvalues of $W$. (b) Find the eigenvectors ("good" zeroth-order states). (c) If $\alpha = 0$ and $\beta$ is real, the two eigenvalues are $\pm\beta$ and the good states are $(|a\rangle \pm |b\rangle)/\sqrt{2}$. Identify which case in the Stark matrix this corresponds to. (d) Now suppose $|\beta| \ll |\alpha|$: one diagonal entry dominates. What are the eigenvalues to leading order in $\beta/\alpha$? When does off-diagonal mixing become negligible? *(Tests: diagonalizing the general 2×2 perturbation matrix; recognizing the Stark effect as a special case; the limit where a perturbation barely mixes states.)*

**9.8** The Dyson argument for divergence. Consider a potential $V(x) = \frac{1}{2}m\omega^2x^2 + \lambda x^4$ with $\lambda < 0$. (a) Sketch the potential for $\lambda = -0.1$ and $\lambda = 0$. What happens to the bound states when $\lambda < 0$? (b) Explain in two sentences why the energy $E_0(\lambda)$ cannot be analytic at $\lambda = 0$ — that is, why a convergent Taylor series in $\lambda$ around $\lambda = 0$ cannot exist. (c) Why does this imply that the perturbation series *for positive $\lambda$* must also diverge? (d) The same argument applies to QED with the fine-structure constant $\alpha$. State in one sentence the physical instability that would occur if $\alpha < 0$. *(Tests: understanding the Dyson analyticity argument; connecting the sign of the coupling to the stability of the vacuum; why physical series that look well-behaved must still diverge.)*

### Challenge

**9.9** Prove from a sign analysis that $E_n^{(2)} \leq 0$ for the ground state for *any* perturbation $\hat{H}'$, not just specific examples. Your proof should use only the formula $E_n^{(2)} = \sum_{m\neq n}|\langle m|\hat{H}'|n\rangle|^2/(E_n^{(0)} - E_m^{(0)})$ and the fact that the ground state has lower energy than all other states. Then find a counterexample: construct a state $|k\rangle$ that is *not* the ground state for which $E_k^{(2)}$ can be positive. *(Tests: general proof of a result stated in the chapter; constructing a counterexample to show the result does not extend to excited states.)*

**9.10** The Zeeman effect at moderate field: add $\hat{H}' = \mu_B B(\hat{L}_z + 2\hat{S}_z)/\hbar$ to hydrogen. (a) For the $n=2$ states *ignoring* spin-orbit coupling, enumerate all distinct first-order energy shifts for the set $\{|2s, m_\ell, m_s\rangle, |2p, m_\ell, m_s\rangle\}$. How many distinct values are there? (b) For the $n=2$ states *including* fine structure (using the good quantum numbers $j, m_j$ from this chapter), write the perturbation $\hat{L}_z + 2\hat{S}_z$ in terms of $\hat{J}_z$ and $\hat{L}_z - \hat{S}_z$. The first-order shift of state $|n, \ell, j, m_j\rangle$ in a weak field is $E^{(1)} = g_J \mu_B B m_j$, where $g_J = 1 + \frac{j(j+1) + s(s+1) - \ell(\ell+1)}{2j(j+1)}$ is the Landé g-factor. Compute $g_J$ for the $2p_{1/2}$ and $2p_{3/2}$ states. (c) Sketch the splitting pattern for the $n=2$, $j=3/2$ states as a function of $B$. How many distinct levels are there? *(Tests: Zeeman effect with and without spin-orbit coupling; Landé g-factor computation; recognizing that the "good" quantum numbers change depending on which perturbation dominates.)*

---

*Sources: Griffiths §7.1–7.4; Liboff §13.1–13.4; Bender & Wu, "Anharmonic Oscillator," Physical Review 184, 1231 (1969); Dyson, "Divergence of Perturbation Theory in Quantum Electrodynamics," Physical Review 85, 631 (1952); Stark, Annalen der Physik 348, 965 (1914); Lamb & Retherford, "Fine Structure of the Hydrogen Atom by a Microwave Method," Physical Review 72, 241 (1947).*
