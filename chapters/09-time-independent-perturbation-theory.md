# Chapter 9 — Time-Independent Perturbation Theory

> Almost no realistic quantum system is exactly solvable. Perturbation theory is the workhorse that takes a problem you can solve and squeezes useful answers out of a problem you cannot.

---

## 1. What this chapter is doing

You can solve the harmonic oscillator. You can solve the hydrogen atom. After that, the list of exactly solvable bound-state problems in three dimensions is roughly empty. The square well, the Coulomb potential, the harmonic well, a handful of toy models with hidden symmetries — that is the inventory. Everything else in physics, from helium upward, requires approximation.

Perturbation theory is the most important of those approximations. The setup is simple. You have a Hamiltonian $\hat{H}_0$ whose eigenstates $|n^{(0)}\rangle$ and eigenvalues $E_n^{(0)}$ you know exactly. Reality gives you $\hat{H} = \hat{H}_0 + \lambda \hat{H}'$ where $\hat{H}'$ is something else and $\lambda$ is a small dimensionless number you can think of as a knob. The question: how much do the energies and states *move* as $\lambda$ turns up from zero?

The chapter delivers two answers. First, a machine for computing the corrections order by order. Second, an honest accounting of where the machine breaks: when two unperturbed states share an energy (degenerate perturbation theory), and when $\lambda$ is not small enough for the series to converge (which, as Dyson noticed in 1952, is almost always — the series is usually asymptotic, not convergent). You are going to build a simulation that lets you *see* both failures happen in real time.

This is the opening chapter of Act Three. Up to now you have solved problems where the Hamiltonian was given and the solution was exact. From here on, you are doing what working physicists do — taking an exactly solvable nearby problem and pushing on it.

## 2. Learning objectives

By the end of this chapter you should be able to:

- Write the perturbation expansion $E_n = E_n^{(0)} + \lambda E_n^{(1)} + \lambda^2 E_n^{(2)} + \cdots$ and derive the first- and second-order corrections by substitution into the Schrödinger equation.
- Compute first-order energy corrections as expectation values: $E_n^{(1)} = \langle n^{(0)}|\hat{H}'|n^{(0)}\rangle$.
- Compute first-order state corrections and recognize when the formula diverges (degeneracy).
- Apply degenerate perturbation theory: diagonalize $\hat{H}'$ in the degenerate subspace.
- Work the hydrogen Stark effect on $n=2$ as the canonical degenerate-PT calculation.
- Sketch the fine-structure correction to hydrogen — relativistic kinetic, spin-orbit, Darwin — and identify which good quantum numbers emerge after the perturbation lifts the degeneracy.
- Build a D3 simulation that watches energy levels split and shift as a perturbation slider turns up, and that flags when perturbation theory has failed.

## 3. Motivating problem

A hydrogen atom sits in a uniform electric field of strength $\mathcal{E}$. Classically, the proton-electron system is a dipole that polarizes — the electron cloud shifts slightly opposite to the field. Quantum mechanically, the levels should shift too. The question is by how much, and in what pattern.

Johannes Stark, working with a modified canal-ray tube in Aachen in the fall of 1913, applied fields up to about $10^5$ V/cm to hydrogen and watched the Balmer lines *split* into multiple components ([Stark 1914, *Annalen der Physik* 348, 965](https://doi.org/10.1002/andp.19143480702)). Within days of Stark's submission, Antonino Lo Surdo in Italy reported the same effect from a different experimental setup; the simultaneous discovery is documented by Leone, Paoletti & Robotti, "[A simultaneous discovery: the case of Johannes Stark and Antonino Lo Surdo](https://link.springer.com/article/10.1007/s00016-003-0203-x)" (*Physics in Perspective* 6, 271, 2004) [verify]. Stark won the Nobel in 1919. Lo Surdo did not.

Here is the puzzle. The ground state of hydrogen, $|1s\rangle$, is non-degenerate. The first excited level at $n=2$ is fourfold degenerate (ignoring spin) — $2s$, $2p_{-1}$, $2p_0$, $2p_{+1}$ all sit at the same energy in the unperturbed problem. When you turn on the electric field, the $n=2$ level splits into *three* lines, not four — two of the four states do not shift at all. The ground state shifts only at *second* order in $\mathcal{E}$ (quadratic, very small). And the splitting pattern is exactly symmetric: one component up by $3 e a_0 \mathcal{E}$, one down by the same amount, one (a doubly degenerate pair) flat.

Why three lines from four states? Why a quadratic shift for the ground state but a linear shift for the excited? The answers will come from the machinery this chapter builds. We need a way to take a problem we cannot solve in closed form ($\hat{H}_{\text{hydrogen}} + e\mathcal{E}\hat{z}$) and squeeze quantitative predictions out of it using only the spectrum and the wave functions of a problem we *can* solve.

## 4. Concept block — the perturbation expansion

### 4.1 The setup

Write the full Hamiltonian as

$$\hat{H} = \hat{H}_0 + \lambda \hat{H}'$$

where $\lambda$ is a dimensionless bookkeeping parameter — small in practice, formally treated as a Taylor expansion variable. At the end you can set $\lambda = 1$ and read off corrections in powers of whatever physical small quantity $\hat{H}'$ contains (the electric field, the perturbation strength, $v/c$, whatever).

Expand the eigenstate and eigenvalue of the perturbed problem in powers of $\lambda$:

$$|n\rangle = |n^{(0)}\rangle + \lambda|n^{(1)}\rangle + \lambda^2|n^{(2)}\rangle + \cdots$$
$$E_n = E_n^{(0)} + \lambda E_n^{(1)} + \lambda^2 E_n^{(2)} + \cdots$$

Substitute into $\hat{H}|n\rangle = E_n|n\rangle$:

$$(\hat{H}_0 + \lambda \hat{H}')(|n^{(0)}\rangle + \lambda|n^{(1)}\rangle + \lambda^2|n^{(2)}\rangle + \cdots) = (E_n^{(0)} + \lambda E_n^{(1)} + \lambda^2 E_n^{(2)} + \cdots)(|n^{(0)}\rangle + \lambda|n^{(1)}\rangle + \cdots)$$

Expand both sides and demand equality at each order of $\lambda$. The whole machine is in that one move. (Griffiths §7.1; Liboff §13.1.)

### 4.2 Order zero — the unperturbed problem

Collecting the $\lambda^0$ terms:

$$\hat{H}_0 |n^{(0)}\rangle = E_n^{(0)}|n^{(0)}\rangle$$

This is just the problem you already solved. No new content. The unperturbed Hamiltonian has its eigenstates, you know them, move on.

### 4.3 Order one — energy correction

Collecting $\lambda^1$ terms:

$$\hat{H}_0|n^{(1)}\rangle + \hat{H}'|n^{(0)}\rangle = E_n^{(0)}|n^{(1)}\rangle + E_n^{(1)}|n^{(0)}\rangle$$

Take the inner product with $\langle n^{(0)}|$:

$$\langle n^{(0)}|\hat{H}_0|n^{(1)}\rangle + \langle n^{(0)}|\hat{H}'|n^{(0)}\rangle = E_n^{(0)}\langle n^{(0)}|n^{(1)}\rangle + E_n^{(1)}\langle n^{(0)}|n^{(0)}\rangle$$

The first term on the left equals the first term on the right because $\hat{H}_0$ is Hermitian: $\langle n^{(0)}|\hat{H}_0|n^{(1)}\rangle = E_n^{(0)}\langle n^{(0)}|n^{(1)}\rangle$. They cancel. The last factor $\langle n^{(0)}|n^{(0)}\rangle = 1$. What is left:

$$\boxed{E_n^{(1)} = \langle n^{(0)}|\hat{H}'|n^{(0)}\rangle}$$

This is the single most useful equation in the chapter. *The first-order shift of an energy level is the expectation value of the perturbation in the unperturbed state.* If you can compute that integral, you have the leading correction. No new diagonalization required.

### 4.4 Order one — state correction

Now take the inner product with $\langle m^{(0)}|$ for $m \neq n$:

$$\langle m^{(0)}|\hat{H}_0|n^{(1)}\rangle + \langle m^{(0)}|\hat{H}'|n^{(0)}\rangle = E_n^{(0)}\langle m^{(0)}|n^{(1)}\rangle$$

Using $\hat{H}_0|m^{(0)}\rangle = E_m^{(0)}|m^{(0)}\rangle$ on the first term (Hermitian, acts to the left):

$$E_m^{(0)}\langle m^{(0)}|n^{(1)}\rangle + \langle m^{(0)}|\hat{H}'|n^{(0)}\rangle = E_n^{(0)}\langle m^{(0)}|n^{(1)}\rangle$$

Solve for $\langle m^{(0)}|n^{(1)}\rangle$:

$$\langle m^{(0)}|n^{(1)}\rangle = \frac{\langle m^{(0)}|\hat{H}'|n^{(0)}\rangle}{E_n^{(0)} - E_m^{(0)}}$$

Sum over $m \neq n$ (the $m = n$ component is fixed by normalization to be zero at first order):

$$\boxed{|n^{(1)}\rangle = \sum_{m \neq n} \frac{\langle m^{(0)}|\hat{H}'|n^{(0)}\rangle}{E_n^{(0)} - E_m^{(0)}}\,|m^{(0)}\rangle}$$

Read the formula. *The first-order correction to a state is a sum over every other unperturbed state, weighted by the matrix element of $\hat{H}'$ connecting them and divided by the energy gap between them.* States nearby in energy contribute more; states with large matrix elements contribute more.

Notice the energy denominator. When $E_m^{(0)} \to E_n^{(0)}$, the formula explodes. That is the signal: the basis you started with is the wrong one for this problem, and you must move to degenerate perturbation theory before the formula will work.

### 4.5 Order two — energy correction

Collect $\lambda^2$ terms from the Schrödinger equation:

$$\hat{H}_0|n^{(2)}\rangle + \hat{H}'|n^{(1)}\rangle = E_n^{(0)}|n^{(2)}\rangle + E_n^{(1)}|n^{(1)}\rangle + E_n^{(2)}|n^{(0)}\rangle$$

Inner product with $\langle n^{(0)}|$. The $|n^{(2)}\rangle$ terms cancel by the same Hermitian trick as before. The middle term on the right vanishes because $\langle n^{(0)}|n^{(1)}\rangle = 0$ at the chosen normalization. What remains:

$$E_n^{(2)} = \langle n^{(0)}|\hat{H}'|n^{(1)}\rangle$$

Substitute the formula for $|n^{(1)}\rangle$ from §4.4:

$$\boxed{E_n^{(2)} = \sum_{m \neq n}\frac{|\langle m^{(0)}|\hat{H}'|n^{(0)}\rangle|^2}{E_n^{(0)} - E_m^{(0)}}}$$

Two features of this formula are worth pausing on.

*The numerator is non-negative.* It is the modulus squared of a matrix element.

*The denominator changes sign depending on whether $E_n^{(0)}$ is above or below $E_m^{(0)}$.* For the ground state, every other state is above, so every denominator is negative. Every term in $E_0^{(2)}$ is therefore negative. **The second-order correction to the ground-state energy is always negative.** The ground state is always pushed *down* by a perturbation. This is a small theorem that follows from one sign analysis.

### 4.6 What the formulas say, in words

Three sentences carry the chapter.

1. Energies at first order: take the expectation value of the perturbation in the unperturbed state. Done.
2. States at first order: mix in every other state, weighted by matrix element over energy gap. Watch for vanishing gaps.
3. Energies at second order: sum the squared matrix elements over the same energy gap. Ground state always goes down.

Everything else is bookkeeping.

## 5. Concept block — degenerate perturbation theory

### 5.1 Where the basis is wrong

Suppose two unperturbed states $|a\rangle$ and $|b\rangle$ share an energy: $E_a^{(0)} = E_b^{(0)} = E^{(0)}$. The first-order state formula has a zero in the denominator. Something has gone wrong, but it is not the perturbation theory — it is the *basis*. Any linear combination $\alpha|a\rangle + \beta|b\rangle$ is still an eigenstate of $\hat{H}_0$ with the same energy. The choice of basis within the degenerate subspace is arbitrary at zeroth order. The perturbation breaks that arbitrariness.

### 5.2 The fix

Restrict $\hat{H}'$ to the degenerate subspace and write it as a matrix:

$$W = \begin{pmatrix} W_{aa} & W_{ab} \\ W_{ba} & W_{bb} \end{pmatrix}, \quad W_{ij} = \langle i|\hat{H}'|j\rangle$$

Diagonalize $W$. The eigenvalues are the first-order energy corrections; the eigenvectors are the "good" zeroth-order states — the unique linear combinations that connect smoothly to the perturbed eigenstates as $\lambda \to 0$.

This is not a "special case." It is the general case. *Non-degenerate perturbation theory is what you get when the degenerate subspace is one-dimensional and the diagonalization is trivial.* For any system with symmetry — hydrogen, the 2D harmonic oscillator, spin systems — the unperturbed Hamiltonian is degenerate by construction, and degenerate perturbation theory is the first move.

### 5.3 Worked example — Stark effect on the $n=2$ manifold

This is the cleanest application in the chapter. Apply a uniform electric field along $\hat{z}$ to a hydrogen atom; the perturbation is

$$\hat{H}' = e\mathcal{E}\hat{z}$$

(The electron has charge $-e$; the field is along $+\hat{z}$. Signs convention: see Griffiths §7.4 / Liboff §13.4.)

For the ground state, $\langle 1s|\hat{z}|1s\rangle = 0$ because $|1s\rangle$ is parity-even and $\hat{z}$ is parity-odd. So $E_1^{(1)} = 0$ — the ground state does not shift at first order. The leading correction is $E_1^{(2)} = -\tfrac{1}{2}\alpha_{\text{pol}}\mathcal{E}^2$, where $\alpha_{\text{pol}}$ is the polarizability. Quadratic in $\mathcal{E}$. Tiny.

For the $n=2$ level, you have four degenerate states: $|2s\rangle$, $|2p_0\rangle$, $|2p_{+1}\rangle$, $|2p_{-1}\rangle$. Build the $4 \times 4$ matrix of $\hat{H}' = e\mathcal{E}\hat{z}$ in this subspace.

Selection rules kill most entries:

- $\hat{z}$ is parity-odd, so $\langle 2s|\hat{z}|2s\rangle = 0$ and $\langle 2p_m|\hat{z}|2p_{m'}\rangle = 0$ (both parities are odd; the product is even, but actually all four $\hat{z}$-matrix-elements among the $2p$ states vanish; see Griffiths Example 7.4 [verify]).
- $\hat{z}$ commutes with $\hat{L}_z$, so $\langle\ell, m|\hat{z}|\ell', m'\rangle \propto \delta_{mm'}$ — only $\Delta m = 0$ contributes.

The only nonzero matrix element is $\langle 2s|\hat{z}|2p_0\rangle$. Computing it directly (Griffiths §7.4):

$$\langle 2s|\hat{z}|2p_0\rangle = -3 a_0$$

where $a_0 = \hbar^2/(m_e e^2/4\pi\epsilon_0)$ is the Bohr radius. So the matrix $W$, with the basis order $\{|2s\rangle, |2p_0\rangle, |2p_{+1}\rangle, |2p_{-1}\rangle\}$:

$$W = e\mathcal{E}\begin{pmatrix} 0 & -3a_0 & 0 & 0 \\ -3a_0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{pmatrix}$$

This block-diagonalizes. The bottom $2 \times 2$ block is already diagonal — $|2p_{+1}\rangle$ and $|2p_{-1}\rangle$ have zero first-order shift. The top $2 \times 2$ block

$$\begin{pmatrix} 0 & -3a_0 e\mathcal{E} \\ -3a_0 e\mathcal{E} & 0 \end{pmatrix}$$

has eigenvalues $\pm 3 a_0 e\mathcal{E}$ and eigenvectors $(|2s\rangle \mp |2p_0\rangle)/\sqrt{2}$.

The $n=2$ level splits into three lines: one shifted up by $3 a_0 e\mathcal{E}$, one shifted down by the same amount, and a doubly degenerate pair (the $m = \pm 1$ states) that does not shift at all. *Three lines from four states.* The "good" zeroth-order eigenstates are the $(|2s\rangle \pm |2p_0\rangle)/\sqrt{2}$ hybrids — polarized states with the electron cloud asymmetric along $\hat{z}$. That asymmetry is what couples to the electric field. The $|2p_{\pm 1}\rangle$ states have $m = \pm 1$, their probability density is azimuthally symmetric about $\hat{z}$, and they cannot polarize along $\hat{z}$ at first order. So they sit still.

This is the worked example that anchors the chapter. Stare at the matrix until the answer feels obvious; then build the simulation and watch the three lines emerge from one as you turn the field up.

## 6. Concept block — when perturbation theory breaks

### 6.1 The anharmonic oscillator

Take the harmonic oscillator and add a quartic perturbation:

$$\hat{H} = \frac{\hat{p}^2}{2m} + \tfrac{1}{2}m\omega^2\hat{x}^2 + \lambda \hat{x}^4$$

The unperturbed problem is exactly solvable (Chapter 3). Compute the first-order shift using ladder operators. Recall $\hat{x} = \sqrt{\hbar/2m\omega}(\hat{a}_+ + \hat{a}_-)$, so

$$\hat{x}^4 = \left(\frac{\hbar}{2m\omega}\right)^2 (\hat{a}_+ + \hat{a}_-)^4$$

Expanding $(\hat{a}_+ + \hat{a}_-)^4$, only diagonal terms — those that return to $|n\rangle$ after acting — survive in $\langle n|\hat{x}^4|n\rangle$. Counting carefully (six combinations of two raises and two lowers, each weighted by the ladder factors):

$$\langle n|\hat{x}^4|n\rangle = \left(\frac{\hbar}{2m\omega}\right)^2 (6n^2 + 6n + 3)$$

So

$$E_n^{(1)} = \lambda \cdot \frac{3\hbar^2}{4m^2\omega^2}(2n^2 + 2n + 1)$$

[verify exact prefactor against Griffiths Problem 7.2 / Liboff §13.1].

This formula has two features worth noting. First, it grows as $n^2$ — perturbation theory works *worst* for highly excited states, where the wave function spreads farthest and probes the $\hat{x}^4$ term most strongly. Second, it grows linearly in $\lambda$. So far so good.

The problem comes at second order. The matrix elements $\langle m|\hat{x}^4|n\rangle$ are nonzero for $m = n, n\pm 2, n\pm 4$ (four powers of ladder operators). The energy denominators are $\pm 2\hbar\omega$ and $\pm 4\hbar\omega$. Carry out the sum and you get $E_n^{(2)}$ as a specific negative number proportional to $\lambda^2$.

### 6.2 The asymptotic series

What about $E_n^{(3)}, E_n^{(4)}, \ldots$? Bender and Wu, in a beautiful 1969 calculation ([Bender & Wu, *Phys. Rev.* 184, 1231](https://journals.aps.org/pr/abstract/10.1103/PhysRev.184.1231)), showed that the perturbation series for the quartic oscillator has *zero radius of convergence*. The coefficients grow faster than $n!$. The series

$$E_n(\lambda) = E_n^{(0)} + E_n^{(1)}\lambda + E_n^{(2)}\lambda^2 + \cdots$$

diverges for any $\lambda \neq 0$. And yet it is *useful*. Truncate at the optimal order (which depends on $\lambda$) and you get an exponentially good approximation to the true energy. Add more terms and you make things worse.

This is the canonical example of an *asymptotic series* — one that does not converge but produces accurate answers when truncated at the right place. The argument is delicate but the picture is clean: in physical terms, the quartic oscillator with $\lambda < 0$ has an unbounded-below potential (it is the inverted quartic) and no normalizable ground state. The energy is not analytic at $\lambda = 0$. Any series expansion around $\lambda = 0$ must capture that singularity by diverging.

Dyson made this argument first, in 1952, for quantum electrodynamics ([Dyson, "Divergence of perturbation theory in quantum electrodynamics," *Phys. Rev.* 85, 631](https://journals.aps.org/pr/abstract/10.1103/PhysRev.85.631)). Flip the sign of the fine-structure constant and electron-positron pairs become attractive, the vacuum is unstable, and the energy is non-analytic at $\alpha = 0$. The same logic — analytic continuation breaks at $\lambda < 0$ — applies to most perturbation series in quantum mechanics and field theory. **Perturbation series almost always diverge.** That they are still useful is one of the deep surprises of the formalism.

The simulation you build will let you watch this directly. Dial $\lambda$ up; first-order PT diverges from the exact answer at some $\lambda$, second-order PT does better for a while and then also fails. Adding orders is not a free lunch. Past the optimal truncation, every additional term moves you further from the truth.

### 6.3 Two misconceptions to break

*"Perturbation theory always converges as long as the terms get smaller."* The terms can get smaller, then start to grow. The optimal truncation is the term where they bottom out. Past it, more terms hurt.

*"First-order is always sufficient for small $\lambda$."* Only when there is no near-degeneracy. If two unperturbed states are nearly degenerate, the second-order correction has a tiny denominator and can be enormous even when $\lambda$ is small. Always check the ratio $|\langle m|\hat{H}'|n\rangle|/|E_n^{(0)} - E_m^{(0)}|$ before you trust first-order. If it is not small, you need degenerate or near-degenerate PT.

## 7. Concept block — hydrogen fine structure

### 7.1 What "fine structure" means

The hydrogen spectrum, as computed in Chapter 8 using the bare Coulomb Hamiltonian, has energies $E_n^{(0)} = -13.6\,\text{eV}/n^2$ depending only on $n$. The full hydrogen spectrum, measured by high-resolution spectroscopy, has small corrections at the level of $\alpha^2 E_n^{(0)} \sim 10^{-4}\,\text{eV}$ for $n=2$, where $\alpha = e^2/(4\pi\epsilon_0 \hbar c) \approx 1/137$ is the fine-structure constant. These corrections are called *fine structure*, and three perturbations produce them.

### 7.2 The three perturbations

**Relativistic kinetic correction.** The non-relativistic kinetic energy $\hat{p}^2/2m$ is the leading term in the expansion of $\sqrt{p^2 c^2 + m^2 c^4} - mc^2$:

$$\sqrt{p^2 c^2 + m^2 c^4} - mc^2 = \frac{p^2}{2m} - \frac{p^4}{8m^3 c^2} + \cdots$$

So at the next order:

$$\hat{H}'_{\text{rel}} = -\frac{\hat{p}^4}{8m^3 c^2}$$

This shifts every level. (Griffiths §7.3.1.)

**Spin-orbit coupling.** In the electron's rest frame, the proton orbits it. A moving charge generates a magnetic field. The electron's spin magnetic moment couples to that field. After the Thomas precession factor of $1/2$:

$$\hat{H}'_{\text{SO}} = \frac{1}{2m^2 c^2}\frac{1}{r}\frac{dV}{dr}\,\vec{L}\cdot\vec{S}$$

(Griffiths §7.3.2; Liboff §13.3 [verify]). For the Coulomb potential, $(1/r)(dV/dr) = e^2/(4\pi\epsilon_0 r^3)$.

**Darwin term.** A relativistic correction affecting only $s$-states (zero orbital angular momentum) where the electron has nonzero probability at the origin:

$$\hat{H}'_{\text{Darwin}} = \frac{\pi\hbar^2}{2m^2 c^2}\,\frac{e^2}{4\pi\epsilon_0}\,\delta^3(\vec{r})$$

### 7.3 The good quantum numbers

All three perturbations are small relative to the unperturbed Coulomb Hamiltonian and they share a common structure: each is proportional to $\alpha^2$ times the Rydberg energy. The unperturbed $|n\ell m_\ell m_s\rangle$ basis is degenerate at fixed $n$ (the famous $n^2$-fold Coulomb degeneracy). Apply degenerate perturbation theory: diagonalize the sum of the three perturbations in the degenerate $n$-manifold.

The result, after a calculation that exploits the symmetry $[\hat{L}\cdot\hat{S}, \hat{J}^2] = 0$ where $\hat{J} = \hat{L} + \hat{S}$: the good quantum numbers become $(n, \ell, j, m_j)$ rather than $(n, \ell, m_\ell, m_s)$. The total angular momentum $j = \ell \pm 1/2$ replaces the separate $m_\ell, m_s$ pair. The fine-structure energy correction is

$$E_n^{\text{fs}} = \frac{(E_n^{(0)})^2}{2mc^2}\left(\frac{2n}{j + 1/2} - \frac{3}{2}\right)$$

depending only on $n$ and $j$, *not* on $\ell$ separately. So the $2p_{1/2}$ and $2s_{1/2}$ states ($j=1/2$, different $\ell$) remain degenerate after fine structure. The $2p_{3/2}$ state ($j=3/2$) sits about $4.5 \times 10^{-5}\,\text{eV}$ above [verify against Griffiths §7.3]. That gap is the *fine structure*.

A subtlety: experimentally, $2s_{1/2}$ and $2p_{1/2}$ are *not* exactly degenerate. There is a $\sim 4 \times 10^{-6}\,\text{eV}$ splitting called the Lamb shift, first measured by Lamb & Retherford in 1947 ([*Phys. Rev.* 72, 241](https://journals.aps.org/pr/abstract/10.1103/PhysRev.72.241)). It is a *QED* effect — quantization of the electromagnetic field, vacuum fluctuations — beyond the semiclassical perturbation theory of this chapter. The chapter cannot derive the Lamb shift; it can only point at it and note where the chapter's framework ends.

## 8. Worked examples and exercises

### Worked example 1 — first-order shift for $\hat{H}' = \lambda \hat{x}^2$

Take the harmonic oscillator and add $\hat{H}' = \lambda\hat{x}^2$. (Yes, this just renormalizes $\omega$; that is the point — we can check our answer against the exact solution.) The first-order shift:

$$E_n^{(1)} = \lambda\langle n|\hat{x}^2|n\rangle = \lambda\cdot\frac{\hbar}{2m\omega}(2n+1) = \frac{\lambda\hbar}{m\omega}(n + \tfrac{1}{2})$$

The exact answer: shift $\omega^2 \to \omega^2 + 2\lambda/m$, so $\omega_{\text{new}} = \omega\sqrt{1 + 2\lambda/(m\omega^2)} \approx \omega + \lambda/(m\omega)$ for small $\lambda$. The new energies are $(n+1/2)\hbar\omega_{\text{new}} \approx (n+1/2)\hbar\omega + (n+1/2)\hbar\lambda/(m\omega)$. Matches the first-order PT result. Good.

### Worked example 2 — second-order shift, ground state of perturbed oscillator

For $\hat{H}' = \lambda\hat{x}$, compute $E_0^{(2)}$. Matrix element: $\langle m|\hat{x}|0\rangle$ is nonzero only for $m=1$, with value $\sqrt{\hbar/2m\omega}$. So

$$E_0^{(2)} = \frac{|\langle 1|\hat{x}|0\rangle|^2 \lambda^2}{E_0^{(0)} - E_1^{(0)}} = \frac{\lambda^2 \hbar/(2m\omega)}{-\hbar\omega} = -\frac{\lambda^2}{2m\omega^2}$$

The ground state moves *down*, as it must. (This is the linear-perturbation case: $\hat{H} = \hat{p}^2/2m + (1/2)m\omega^2\hat{x}^2 + \lambda\hat{x}$ is just a shifted harmonic oscillator, $\hat{x} \to \hat{x} - \lambda/(m\omega^2)$, with the same spectrum displaced by $-\lambda^2/(2m\omega^2)$. PT gets the exact answer at second order. Good check.)

### Exercises

**Warm-up.**

1. Compute $E_0^{(1)}$ for the harmonic oscillator with $\hat{H}' = \lambda\hat{x}^3$. By parity, the answer should be zero. Confirm by ladder-operator algebra.

2. Compute $E_0^{(2)}$ for the perturbation in problem 1. (You will need matrix elements $\langle m|\hat{x}^3|0\rangle$ for $m = 1, 3$.) Show the result is negative.

3. For the infinite square well of width $L$, compute $E_1^{(1)}$ under the perturbation $\hat{H}' = V_0$ (a constant offset). Result should be just $V_0$. Confirm.

**Application.**

4. Hydrogen in a uniform electric field $\mathcal{E}\hat{z}$. Show by parity that $E_n^{(1)} = 0$ for every non-degenerate state. State the regime where the *quadratic* Stark shift ($E^{(2)} \propto \mathcal{E}^2$) is the leading correction.

5. Build the $4\times 4$ Stark matrix for the hydrogen $n=2$ manifold by hand. Diagonalize. Confirm three eigenvalues: $+3a_0 e\mathcal{E}, -3a_0 e\mathcal{E}, 0, 0$.

6. The hydrogen Zeeman effect at moderate field: write the perturbation $\hat{H}' = \mu_B B(L_z + 2S_z)/\hbar$. For the $n=2$ states *without* spin-orbit coupling, what are the first-order shifts? You should find six distinct values for $\{2s, 2p_m\}$ with $m_s = \pm 1/2$.

**Synthesis.**

7. The anharmonic oscillator $\hat{H} = \hat{H}_{\text{HO}} + \lambda\hat{x}^4$. Compute $E_0^{(1)}$ as a function of $\lambda$ using ladder operators. Then numerically diagonalize the Hamiltonian in the first 30 harmonic-oscillator eigenstates for several values of $\lambda$. Plot $E_0^{(0)} + \lambda E_0^{(1)}$ and the exact $E_0(\lambda)$ on the same axes. Identify the $\lambda$ at which first-order PT diverges from the exact answer by 10%.

8. Argue from a sign analysis that *second-order perturbation theory always lowers the ground-state energy*, regardless of the form of $\hat{H}'$, as long as $\hat{H}'$ has some nonzero matrix element to excited states.

**Challenge.**

9. The hydrogen fine-structure correction (relativistic + spin-orbit + Darwin) has the closed form

$$E_n^{\text{fs}} = \frac{(E_n^{(0)})^2}{2mc^2}\left(\frac{2n}{j+1/2} - \tfrac{3}{2}\right)$$

Verify that the $2p_{3/2}$–$2p_{1/2}$ splitting is approximately $\alpha^2$ times the $n=2$ unperturbed energy, divided by a small integer factor. Compute numerically and compare to the experimental value $\sim 4.5 \times 10^{-5}\,\text{eV}$ [verify against NIST atomic spectra database].

10. The asymptotic series for the anharmonic oscillator. Numerically diagonalize $\hat{H}_{\text{HO}} + \lambda\hat{x}^4$ for $\lambda = 0.1$. Compute the first $N$ terms of the perturbation series for $E_0$ and plot the partial sum vs. $N$. Find the optimal truncation order $N^*$ (where the partial sum is closest to the exact value) and identify the regime where adding more terms makes the approximation *worse*. This is the signature of an asymptotic series; you have reproduced Bender & Wu's discovery numerically.

## 9. What would change my mind

The framework rests on a structural claim: that physical Hamiltonians close to exactly solvable ones can be tackled order-by-order in a small parameter, and that the resulting series — even when divergent — gives accurate predictions when truncated near the optimal order. If a clean physical system (no degeneracies, no obvious near-degeneracies, a genuinely small $\lambda$) were found where first- and second-order PT both badly missed the experimental value, the chapter's premise would be in trouble. So far no such case is known in basic atomic physics; the high-precision agreement between QED perturbation theory and the electron $g$-factor (better than ten significant figures) is one of the most stringent tests in all of physics. The framework is in remarkably good shape.

## 10. Still puzzling

It is not obvious why a divergent series should give good answers at all. Borel summation, transseries, resurgent analysis — Écalle, Costin, Mariño — recover information from the divergent tail by analytic continuation in cleverly chosen ways. The arguments work in some cases and fail in others. I do not have a satisfying answer to *why* truncating at the optimal order is exponentially close to the truth in every well-studied case. The empirical fact is that it is. The theoretical understanding is still in progress.

## 11. LLM Exercise — the perturbation explorer

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

1. Anharmonic mode, $n=0$. Slide $\lambda$ from $0$ to $0.5$. At what value of $\lambda$ does first-order PT depart from the exact curve by more than 10%? At what value of $\lambda$ does *second-order* PT depart by more than 10%? Note the warning text trigger; record the $\lambda$ at which it fires.

2. Repeat for $n=4$. The departure happens earlier — PT works worst for high-$n$ states. Quantify: what is the ratio of the breakdown $\lambda$ for $n=4$ vs. $n=0$?

3. Stark mode. Set the field strength to $\mathcal{E} = 0.01$ atomic units. Verify by hand that the upper eigenvalue is $+3 a_0 e \mathcal{E} = 0.03$ Hartree, and that the two middle lines do not shift. Increase the field. The simulation should remain accurate up to $\mathcal{E} \sim 0.04$ a.u.; above that, real hydrogen ionizes via the tilted-Coulomb mechanism (Stark ionization), which this simulation does not capture.

4. Toggle off the "show eigenvectors" view in Stark mode. Look at the matrix. The three shifted lines come from diagonalizing a $2\times 2$ block; the two flat lines come from a $2\times 2$ zero block. Confirm this is what you see.

5. Back to anharmonic mode. Set $\lambda = 0.3$ and toggle $n$ through 0, 1, 2, 3, 4 quickly. Where do first-order and second-order PT *agree* with the exact result, and where do they not? The pattern — PT works better for the ground state than for excited states — should be visible.

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

*Sources consulted: Griffiths §7.1–7.4 (non-degenerate and degenerate perturbation theory, hydrogen fine structure, Stark effect; Problems 7.2, 7.4); Liboff §13.1–13.4 (Rayleigh-Schrödinger perturbation theory, fine structure, Zeeman effect); Bender & Wu, "[Anharmonic Oscillator](https://journals.aps.org/pr/abstract/10.1103/PhysRev.184.1231)," *Physical Review* 184, 1231 (1969); Dyson, "[Divergence of Perturbation Theory in Quantum Electrodynamics](https://journals.aps.org/pr/abstract/10.1103/PhysRev.85.631)," *Physical Review* 85, 631 (1952); Stark, *Annalen der Physik* 348, 965 (1914) [verify]; Leone, Paoletti & Robotti, *Physics in Perspective* 6, 271 (2004) [verify]; Lamb & Retherford, "[Fine Structure of the Hydrogen Atom by a Microwave Method](https://journals.aps.org/pr/abstract/10.1103/PhysRev.72.241)," *Physical Review* 72, 241 (1947).*

*Tags: perturbation-theory, stark-effect, fine-structure, asymptotic-series, anharmonic-oscillator, degenerate-perturbation, d3-simulation*

*Status: draft for Nik's review. Several `[verify]` flags throughout — see specifically Stark/Lo Surdo simultaneous-discovery citation, exact prefactors on $x^4$ matrix elements, fine-structure splitting numerical value against NIST.*
