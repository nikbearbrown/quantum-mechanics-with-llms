# Chapter 2 — The Time-Independent Schrödinger Equation

> Quantization is not assumed. It falls out of asking a wave function to be continuous in a box with hard walls — and once you have seen that derivation, you have seen one of the cleanest "oh" moments in physics.

---

## 1. What this chapter is doing

Chapter 1 told you what $\psi$ means once you have one. This chapter tells you where $\psi$ comes from. Given a potential $V(x)$, the time-dependent Schrödinger equation $i\hbar\,\partial_t \psi = \hat{H}\psi$ is a PDE — first-order in time, second-order in space, complex-valued. By a trick — separation of variables — it splits into a trivial time equation $\dot\phi = -(iE/\hbar)\phi$ and an *eigenvalue problem* in space, the **time-independent Schrödinger equation** (TISE) $\hat{H}\psi_E = E\psi_E$. Solving the TISE for a given $V(x)$ gives you a set of allowed energies and the spatial wave functions that go with them. For the infinite square well — the canonical problem — the allowed energies are *discrete*, the wave functions are *standing waves*, and the discreteness comes out of nothing more sinister than asking $\psi$ to be continuous at the walls.

The chapter's deep-dive is that derivation, eight steps from ansatz to spectrum. Then we use the eigenstates as building blocks: superpose two of them, watch the resulting probability density "slosh" between the left and right halves of the well at the beat frequency $(E_2 - E_1)/\hbar$. The simulation makes all of this watchable: energy levels drawn at the right $n^2$ spacing, $\psi_n(x)$ overlaid at each level, $|\Psi(x, t)|^2$ animating live as you mix and match coefficients.

## 2. Learning objectives

- **(Apply)** Apply separation of variables to the time-dependent Schrödinger equation and derive the TISE plus the trivial time phase.
- **(Apply)** Solve the TISE for the infinite square well — boundary conditions, general solution, normalization — and read off the discrete energy spectrum.
- **(Analyze)** Identify which step of the derivation forces quantization (it is the boundary condition $\psi(L) = 0$, not the differential equation).
- **(Apply)** Compute expansion coefficients $c_n = \langle \psi_n | \psi(\cdot, 0) \rangle$ for a given initial state, then evolve in time as $\Psi(x, t) = \sum_n c_n \psi_n(x)\,e^{-i E_n t/\hbar}$.
- **(Evaluate)** Distinguish a stationary state ($|\psi|^2$ time-independent) from a "particle at rest" ($\psi$ time-dependent through the phase).
- **(Create)** Produce `02-infinite-well.html`: an energy diagram with overlaid eigenstates, a dynamical $|\Psi(x, t)|^2$ panel, coefficient and phase sliders, an expansion bar chart, and the "draw your own $\psi(x, 0)$" extension.

## 3. The motivating problem

An electron is confined to a region of length $L$ — say, by an infinite potential everywhere else. Classically, this electron can have any energy from zero to infinity. It can be at rest with $E = 0$ (sitting at the bottom of the well). It can have any kinetic energy you like by moving faster.

The quantum answer is famously different. The electron *cannot* have zero energy. The lowest allowed energy is $E_1 = \pi^2 \hbar^2 / (2 m L^2)$, strictly positive. The next allowed energy is $E_2 = 4 E_1$. The next is $E_3 = 9 E_1$. There is *nothing* between them — no $E_{1.5}$. The spectrum is discrete and starts above zero.

Why? Bohr's old 1913 picture assumed quantization by fiat — he wrote down "$m v r = n \hbar$" and called it a postulate ([Bohr, N. (1913), *Phil. Mag.* 26, 1–25](https://doi.org/10.1080/14786441308634955)). The result fit the hydrogen spectrum, but the rule itself was unexplained. Schrödinger, in 1926, showed the discreteness was not a separate assumption. It was a *consequence* of two ordinary requirements: that $\psi$ satisfy the wave equation, and that $\psi$ be continuous at the walls of the well. The "ad hoc quantization" of Bohr became a *derived* quantization. ([Schrödinger, E. (1926), *Annalen der Physik* 384, 361–376](https://onlinelibrary.wiley.com/doi/10.1002/andp.19263840404).)

This chapter walks the derivation. The "oh" moment is at step seven, when $\sin(kL) = 0$ forces $kL = n\pi$. Watch for it.

## 4. Separation of variables

### 4.1 The technique

Start with the TDSE:

$$i\hbar\,\frac{\partial \psi}{\partial t} = \hat{H}\,\psi, \qquad \hat{H} = -\frac{\hbar^2}{2m}\,\frac{\partial^2}{\partial x^2} + V(x).$$

Note $\hat{H}$ has no explicit time dependence — $V$ depends on $x$ alone. Try the ansatz

$$\psi(x, t) = \psi(x)\,\phi(t).$$

Substitute:

$$i\hbar\,\psi(x)\,\phi'(t) = \phi(t)\,\hat{H}\psi(x).$$

Divide both sides by $\psi(x)\phi(t)$ (legal where neither vanishes):

$$i\hbar\,\frac{\phi'(t)}{\phi(t)} = \frac{\hat{H}\psi(x)}{\psi(x)}.$$

The left side depends only on $t$. The right side depends only on $x$. They are equal everywhere. The only way a function of $t$ alone can equal a function of $x$ alone is if both are constant. Call the constant $E$. Two equations result:

$$i\hbar\,\phi'(t) = E\,\phi(t) \implies \phi(t) = \phi(0)\,e^{-i E t/\hbar},$$

and

$$\hat{H}\,\psi(x) = E\,\psi(x).$$

The first is solved by inspection. The second is the **time-independent Schrödinger equation**. It is an eigenvalue problem: find functions $\psi$ such that $\hat{H}\psi$ is a constant multiple of $\psi$. The constant is $E$, the energy.

**Here's the trick.** The full PDE has collapsed into an *algebraic* problem — find eigenfunctions of $\hat{H}$ — plus a universal time phase that you tack on at the end. The technique works whenever $\hat{H}$ has no explicit time dependence. (Griffiths *Introduction to Quantum Mechanics* 3rd ed., §2.1.)

### 4.2 What you have not yet earned

Separation of variables produces *some* solutions of the TDSE, namely the *stationary states*. It does not immediately tell you that *every* solution is a superposition of separable ones. That stronger statement requires the eigenstates of $\hat{H}$ to form a *complete* basis, which is a theorem about self-adjoint operators in $L^2$ — we will hand-wave it for now and return to it in Section 7. The takeaway: solve the TISE, get a list of stationary states, and *then* worry about whether you can build arbitrary solutions from them.

## 5. The TISE in 1D

$$-\frac{\hbar^2}{2m}\,\frac{d^2\psi}{dx^2} + V(x)\,\psi(x) = E\,\psi(x).$$

A second-order linear ODE. For each choice of $V(x)$, it is a *constrained* problem: not every $E$ admits a normalizable solution. The allowed $E$'s — the spectrum — depend on $V$. For unbound problems (continuous spectrum) every $E$ above some threshold is allowed; for bound problems (discrete spectrum) only certain $E$'s are.

This chapter focuses on the simplest bound problem: $V = \infty$ outside a finite interval.

## 6. The infinite square well — the deep-dive

This is the eight-step derivation. Every step on the page.

**Step 1. State the potential.**

$$V(x) = \begin{cases} 0 & \text{for } 0 < x < L,\\ \infty & \text{elsewhere.}\end{cases}$$

The walls are infinitely high. The particle cannot exist outside. Therefore $\psi(x) = 0$ for $x \leq 0$ and $x \geq L$.

**Step 2. Write the TISE inside the well.**

Inside $(0, L)$, $V = 0$. The TISE becomes

$$-\frac{\hbar^2}{2m}\,\frac{d^2\psi}{dx^2} = E\,\psi.$$

Rearrange:

$$\frac{d^2\psi}{dx^2} = -\frac{2 m E}{\hbar^2}\,\psi.$$

**Step 3. Define $k^2 = 2 m E / \hbar^2$.**

If $E > 0$, then $k^2 > 0$ and $k$ is real. The equation is

$$\psi'' = -k^2\,\psi,$$

the classical equation for a simple harmonic oscillator in space — solutions are sines and cosines of $kx$. (If $E < 0$, the analysis is different and produces no normalizable solutions; we omit it. Griffiths §2.2.)

**Step 4. Write the general solution.**

$$\psi(x) = A\,\sin(kx) + B\,\cos(kx).$$

Two undetermined constants $A$ and $B$. So far, no quantization — any $k$ (any $E > 0$) satisfies the differential equation.

**Step 5. Apply the boundary condition at $x = 0$.**

$\psi$ must be continuous (so that $|\psi|^2$ is well-defined and probability is meaningful). Since $\psi(x) = 0$ for $x \leq 0$, continuity at $x = 0$ requires $\psi(0) = 0$. Therefore

$$A\,\sin(0) + B\,\cos(0) = 0 \implies B = 0.$$

The cosine component is killed. The solution is now

$$\psi(x) = A\,\sin(kx).$$

**Step 6. Apply the boundary condition at $x = L$.**

Continuity at $x = L$ requires $\psi(L) = 0$:

$$A\,\sin(kL) = 0.$$

Either $A = 0$ (the trivial solution $\psi \equiv 0$, which is the "no particle" state — not physical) or

$$\sin(kL) = 0.$$

**Step 7. Quantization.**

$\sin(kL) = 0$ has solutions $kL = n\pi$ for $n = 1, 2, 3, \ldots$. So

$$k_n = \frac{n\pi}{L}.$$

*This is where quantization enters.* Not from a postulate. From asking that $\psi$ vanish at the walls. The continuous range of allowed wavenumbers in step 4 has collapsed to a discrete set, indexed by an integer $n$.

Why does $n = 0$ not appear? Because $k_0 = 0$ gives $\sin(0 \cdot x) = 0$ for all $x$ — the trivial wave function, identically zero. No particle. Discarded.

Why no $n < 0$? Because $\sin(-n\pi x/L) = -\sin(n\pi x/L)$, which is the same wave function up to a global sign. Global signs are irrelevant (they cancel in $|\psi|^2$ and can be absorbed into $A$). So $n$ and $-n$ give the same physical state; we keep $n \geq 1$.

**Step 8. Energy spectrum and normalization.**

$E = \hbar^2 k^2 / (2 m)$ (from step 3), so

$$\boxed{\,E_n = \frac{n^2\,\pi^2\,\hbar^2}{2\,m\,L^2}, \quad n = 1, 2, 3, \ldots\,}$$

The energies scale as $n^2$. The ratios are $E_n / E_1 = 1, 4, 9, 16, 25, \ldots$.

Normalize $\psi_n(x) = A\sin(n\pi x / L)$:

$$\int_0^L A^2\,\sin^2(n\pi x / L)\,dx = A^2\,\frac{L}{2} = 1 \implies A = \sqrt{\frac{2}{L}}.$$

(Use $\sin^2\theta = (1 - \cos 2\theta)/2$; the $\cos$ term integrates to zero over an integer number of half-periods.)

$$\boxed{\,\psi_n(x) = \sqrt{\frac{2}{L}}\,\sin\!\left(\frac{n\pi x}{L}\right) \text{ for } 0 \leq x \leq L, \text{ zero elsewhere.}\,}$$

**The lesson.** Quantization came from continuity at the walls. No mystical postulate, no Bohr-style fiat. A confining boundary turns a continuous spectrum into a discrete one. **The limit.** This argument relies on $V = \infty$ outside the well — an idealization. For a finite well (Section 8.1), the spectrum is still discrete for bound states but only *finitely* many discrete energies exist; the rest of the spectrum is continuous. The discreteness is robust; the infinity is the cartoon.

### 6.1 Ground state and zero-point energy

The lowest energy is $E_1 = \pi^2 \hbar^2 / (2 m L^2)$, strictly positive. The particle *cannot* sit at rest at the bottom of the well. This is the **zero-point energy**.

**Misconception, addressed inline.** *"Why can't $n = 0$ be the ground state?"* Because $\psi_0(x) \equiv 0$ is not a physical state — it is the absence of a particle. The lowest *physical* state is $n = 1$.

There is a deeper reason the energy can't be zero. If the particle had $E = 0$ in the well, it would have $p = 0$ (since $V = 0$ inside), so $\langle p \rangle = 0$ *and* $\sigma_p = 0$. But the particle is confined to $[0, L]$, so $\sigma_x \leq L/2$. Then $\sigma_x \sigma_p = 0 < \hbar/2$, violating the uncertainty principle. The uncertainty principle *forbids* zero energy in a confined particle.

You can check this explicitly for the ground state. $\langle x \rangle = L/2$, $\langle x^2 \rangle = L^2 (1/3 - 1/(2\pi^2))$, so $\sigma_x = L\sqrt{1/12 - 1/(2\pi^2)} \approx 0.181\,L$. From the simulation in Section 9, $\sigma_p \approx \pi\hbar/L$. Then $\sigma_x \sigma_p \approx 0.181 \cdot \pi\,\hbar \approx 0.568\,\hbar \geq \hbar/2$. ✓

### 6.2 Numerical scale

For an electron ($m = 9.109 \times 10^{-31}$ kg) in a well of width $L = 1$ nm = $10^{-9}$ m:

$$E_1 = \frac{\pi^2\,(1.055 \times 10^{-34})^2}{2\,(9.109 \times 10^{-31})\,(10^{-9})^2}\ \text{J}.$$

Compute the numerator: $\pi^2 \approx 9.870$, $\hbar^2 \approx 1.113 \times 10^{-68}$ J²·s², product $\approx 1.099 \times 10^{-67}$. Denominator: $2 \cdot 9.109 \times 10^{-31} \cdot 10^{-18} = 1.822 \times 10^{-48}$. Quotient: $E_1 \approx 6.03 \times 10^{-20}$ J. Convert to eV ($1$ eV $= 1.602 \times 10^{-19}$ J): $E_1 \approx 0.377$ eV.

So $E_1 \approx 0.38$ eV, $E_2 \approx 1.51$ eV, $E_3 \approx 3.39$ eV. These are *real* energies on the scale of chemistry — comparable to thermal energy at room temperature ($k_B T \approx 0.025$ eV) and to optical photons (visible light $\sim 2$ eV). Quantum confinement in nanoscale wells produces optical transitions you can see in a spectrometer. (Semiconductor quantum wells in laser diodes work on exactly this principle; [Esaki & Tsu 1970, *IBM J. Res. Dev.* 14, 61–65](https://doi.org/10.1147/rd.141.0061), is the foundational paper.)

For a marble in a $1$ cm box, $E_1 \sim 10^{-58}$ eV — completely negligible compared to any other energy scale. The "quantum-ness" of the spectrum is set by $\hbar^2 / (m L^2)$, which is tiny for macroscopic objects and significant for nanoscale ones.

## 7. Orthonormality, completeness, and time evolution

### 7.1 The eigenstates are orthonormal

$$\langle \psi_m | \psi_n \rangle = \int_0^L \psi_m^*(x)\,\psi_n(x)\,dx = \delta_{mn}.$$

Direct computation. Use $\sin(\alpha)\sin(\beta) = (1/2)[\cos(\alpha - \beta) - \cos(\alpha + \beta)]$:

$$\langle \psi_m | \psi_n \rangle = \frac{2}{L}\int_0^L \sin(m\pi x/L)\sin(n\pi x/L)\,dx = \frac{1}{L}\int_0^L [\cos((m - n)\pi x/L) - \cos((m + n)\pi x/L)]\,dx.$$

For $m \neq n$: both cosines integrate over an integer number of half-periods on $[0, L]$ and give zero. For $m = n$: the first cosine becomes $\cos 0 = 1$, integrating to $L$; the second has integer period and gives zero. Total: $\delta_{mn}$. ✓

Orthonormality is the *engine* of the expansion technique. Without it, the $c_n$'s in the next section would be hard to extract.

### 7.2 Completeness

**Claim.** Any function $f(x)$ on $[0, L]$ with $f(0) = f(L) = 0$ and $\int_0^L |f|^2\,dx < \infty$ can be expanded as

$$f(x) = \sum_{n=1}^{\infty} c_n\,\psi_n(x), \quad c_n = \int_0^L \psi_n^*(x)\,f(x)\,dx.$$

This is the **Fourier sine series**, established by Joseph Fourier in 1822 in *Théorie analytique de la chaleur* — older than quantum mechanics by a century. ([Fourier, J. (1822), *Théorie analytique de la chaleur*, Paris: Firmin Didot.](https://archive.org/details/thorieanalytiqu00fourgoog)) The convergence theorem is technical; in the $L^2$ sense it holds for any square-integrable $f$ with the boundary conditions. The chapter takes the result as given and points the curious to a real-analysis text (Stein & Shakarchi, *Fourier Analysis: An Introduction*, 2003, Ch. 4).

**Misconception, addressed inline.** *"Completeness is a quantum thing."* No. Completeness of the sine basis is a theorem from 1822 about heat conduction. Quantum mechanics inherits it. The chapter should not let students treat "any $\psi$ is a superposition of eigenstates" as quantum mysticism — it is classical Fourier analysis.

### 7.3 Time evolution via expansion

Given an initial state $\Psi(x, 0) = f(x)$ with $f(0) = f(L) = 0$, expand:

$$\Psi(x, 0) = \sum_n c_n\,\psi_n(x), \qquad c_n = \int_0^L \psi_n^*(x)\,f(x)\,dx.$$

Each $\psi_n$ is a stationary state with time evolution $\psi_n(x)\,e^{-i E_n t/\hbar}$. Linearity of the Schrödinger equation lets you superpose:

$$\boxed{\,\Psi(x, t) = \sum_n c_n\,\psi_n(x)\,e^{-i E_n t/\hbar}.\,}$$

Solve the TISE *once*. Get the $\{\psi_n, E_n\}$. Project the initial condition onto them. Phase-rotate each component at its own $E_n / \hbar$. Sum. *That is the entire dynamics of any state in the infinite well.* No time integration. The expansion method is the dominant tool for the rest of the book.

## 8. Worked examples

### 8.1 Probability in the central third, $n = 1$ versus $n = 2$

Question: for an infinite well of width $L$, what is the probability of finding the particle in the middle third — i.e., in $[L/3, 2L/3]$ — for the ground state ($n = 1$) and for the first excited state ($n = 2$)?

**$n = 1$.**

$$P_1 = \int_{L/3}^{2L/3} \frac{2}{L}\sin^2(\pi x/L)\,dx.$$

Substitute $u = \pi x / L$, $du = \pi\,dx/L$, $dx = L\,du/\pi$:

$$P_1 = \frac{2}{L}\cdot\frac{L}{\pi}\int_{\pi/3}^{2\pi/3} \sin^2 u\,du = \frac{2}{\pi}\cdot\frac{1}{2}\left[u - \sin u \cos u\right]_{\pi/3}^{2\pi/3}.$$

(Use $\sin^2 u = (1 - \cos 2u)/2$, antiderivative $u/2 - \sin(2u)/4 = (u - \sin u \cos u)/2$.)

Evaluate at the endpoints. $\sin(2\pi/3) = \sqrt{3}/2$, $\cos(2\pi/3) = -1/2$, product $= -\sqrt{3}/4$. So at $u = 2\pi/3$: $2\pi/3 - (-\sqrt{3}/4) = 2\pi/3 + \sqrt{3}/4$. At $u = \pi/3$: $\sin = \sqrt{3}/2$, $\cos = 1/2$, product $= \sqrt{3}/4$. So $\pi/3 - \sqrt{3}/4$. Difference:

$$\left[(2\pi/3 + \sqrt{3}/4) - (\pi/3 - \sqrt{3}/4)\right] = \pi/3 + \sqrt{3}/2.$$

So

$$P_1 = \frac{1}{\pi}(\pi/3 + \sqrt{3}/2) = \frac{1}{3} + \frac{\sqrt{3}}{2\pi} \approx 0.333 + 0.276 = 0.609.$$

About 61%. The ground state is concentrated in the middle of the well, so the central third holds well over a third of the probability.

**$n = 2$.**

$$P_2 = \int_{L/3}^{2L/3} \frac{2}{L}\sin^2(2\pi x/L)\,dx.$$

Substitute $u = 2\pi x/L$, $dx = L\,du/(2\pi)$. Limits: $u = 2\pi/3$ to $u = 4\pi/3$.

$$P_2 = \frac{2}{L}\cdot\frac{L}{2\pi}\int_{2\pi/3}^{4\pi/3} \sin^2 u\,du = \frac{1}{2\pi}\left[u - \sin u\cos u\right]_{2\pi/3}^{4\pi/3}.$$

At $u = 4\pi/3$: $\sin = -\sqrt{3}/2$, $\cos = -1/2$, product $= \sqrt{3}/4$. So $4\pi/3 - \sqrt{3}/4$. At $u = 2\pi/3$ (from above): $2\pi/3 + \sqrt{3}/4$. Difference:

$$(4\pi/3 - \sqrt{3}/4) - (2\pi/3 + \sqrt{3}/4) = 2\pi/3 - \sqrt{3}/2.$$

$$P_2 = \frac{1}{2\pi}(2\pi/3 - \sqrt{3}/2) = \frac{1}{3} - \frac{\sqrt{3}}{4\pi} \approx 0.333 - 0.138 = 0.196.$$

About 20%. The $n=2$ state has a node at $x = L/2$ — the very center. The probability density is suppressed where the wave function crosses zero, so the central third holds *less* than a third.

**The lesson.** Higher-$n$ states are not "in a larger region" — the particle is still confined to $[0, L]$. Higher-$n$ states have *more nodes*, which redistributes the probability density. The classical intuition "more energy means more space" is wrong; the right intuition is "more energy means more curvature," because $E \propto k^2$ and $k$ is set by the number of half-wavelengths fitting between the walls.

### 8.2 The "sloshing" superposition

Take $\Psi(x, 0) = (1/\sqrt{2})[\psi_1(x) + \psi_2(x)]$. (Normalize: $|c_1|^2 + |c_2|^2 = 1/2 + 1/2 = 1$ ✓.) Time evolution:

$$\Psi(x, t) = \frac{1}{\sqrt{2}}\left[\psi_1(x)\,e^{-i E_1 t/\hbar} + \psi_2(x)\,e^{-i E_2 t/\hbar}\right].$$

The probability density:

$$|\Psi(x, t)|^2 = \frac{1}{2}\left[\psi_1^2 + \psi_2^2 + 2\psi_1\psi_2\cos((E_2 - E_1)\,t/\hbar)\right]$$

(using $\psi_n$ real and the cross term $2\,\mathrm{Re}\bigl(c_1^*c_2\,\psi_1^*\psi_2\,e^{-i(E_2-E_1)t/\hbar}\bigr)$ collapsing to $\psi_1\psi_2\cos((E_2-E_1)t/\hbar)$ for real coefficients).

The cross term oscillates at angular frequency $\omega = (E_2 - E_1)/\hbar = 3 E_1/\hbar$. The probability density "sloshes" left-right with period $T = 2\pi / \omega = 2\pi\hbar/(3 E_1) = h/(3 E_1)$.

For the $L = 1$ nm electron: $E_1 \approx 0.377$ eV $\approx 6.03 \times 10^{-20}$ J. $T = h / (3 E_1) = 6.626 \times 10^{-34} / (3 \cdot 6.03 \times 10^{-20})$ s $\approx 3.66 \times 10^{-15}$ s $\approx 3.7$ fs. **The particle's probability density swings from one side of the well to the other in about $3.7$ femtoseconds.** You will see this in the simulation.

### 8.3 The stationary state is not stationary

**Misconception, addressed inline.** *"Stationary states are time-independent."* The probability density $|\psi_n(x)\,e^{-iE_n t/\hbar}|^2 = |\psi_n(x)|^2$ is time-independent. The wave function itself is not: $\psi_n(x)\,e^{-iE_n t/\hbar}$ rotates in the complex plane at angular frequency $E_n/\hbar$. In a single stationary state, you can't see this rotation because it cancels in $|\psi|^2$. The moment you take a superposition of two stationary states with different $E$'s, the *relative* phase shows up in the cross term — and that is where all time dependence comes from. Stationary states are *building blocks*. Real dynamics lives in their superpositions.

## 9. LLM Exercise — the infinite-well explorer

The chapter's signature deliverable: `02-infinite-well.html`. Four panels. Energy diagram with eigenstates overlaid. Dynamical $|\Psi(x, t)|^2$. Coefficient and phase sliders. Expansion bar chart. The extension is a "draw your own $\psi(x, 0)$" canvas.

### Part A — `CLAUDE.md` snippet for this chapter

````markdown
## Chapter 2 — Infinite Square Well

- Eigenstates: ψ_n(x) = √(2/L) sin(nπx/L) for 0 ≤ x ≤ L, zero elsewhere.
  Use this closed form directly. Do NOT Gram-Schmidt; orthonormality
  follows from the trigonometric identity.
- Energy levels: E_n = n² π² ℏ²/(2 m L²). When L = 1 nm, electron:
  E_1 ≈ 0.377 eV, E_2 ≈ 1.508 eV, E_3 ≈ 3.39 eV. Verify the n²
  scaling: E_n / E_1 must equal n² in the displayed values.
- Boundary conditions are DIRICHLET (ψ = 0 at x = 0 and x = L), not
  Neumann (ψ' = 0). The n = 1 state must visibly vanish at both walls.
- Time evolution: ANALYTIC, per-eigenstate. Ψ(x, t) = Σ_n c_n ψ_n(x)
  exp(−i E_n t/ℏ). Do NOT integrate the TDSE numerically. ⟨H⟩ must
  be exactly constant in time (drift > 10⁻³ relative is a bug).
- Phase sign: exp(−i E_n t/ℏ). Not +. Wrong sign flips the slosh direction.
- n_max slider exposed (range 1..20) so the user can watch convergence
  in the "draw your own" extension.
````

### Part B — The simulation prompt

````markdown
SHOW.
Infinite square well: V(x) = 0 for 0 < x < L, V = ∞ elsewhere.
Eigenstates: ψ_n(x) = √(2/L) sin(nπx/L) for n = 1, 2, 3, ...
Energies: E_n = n² π² ℏ² / (2 m L²).
Time evolution of a general state:
  Ψ(x, t) = Σ_{n=1}^{n_max} c_n ψ_n(x) exp(−i E_n t/ℏ)
where c_n are complex coefficients normalized so Σ |c_n|² = 1.

Energy conservation: ⟨H⟩ = Σ |c_n|² E_n, time-independent.

Use the existing CLAUDE.md (with the Chapter 2 stanza above) and DESIGN.md.

SAY.
Produce a single file `02-infinite-well.html`.

Layout (four panels, top to bottom):
  1. Energy diagram (top, 200 px tall):
     - Vertical red lines at x = 0 and x = L (the walls).
     - Horizontal green lines at y = E_n for n = 1..n_max, labeled with
       the energy in eV.
     - Each ψ_n drawn on top of its energy level, with the zero of ψ_n
       offset to y = E_n and amplitude scaled to fit between adjacent levels.
       (Standard textbook convention, Griffiths Fig. 2.2.)
  2. |Ψ(x, t)|² animation (middle, 200 px tall):
     - Blue filled curve, animated via requestAnimationFrame.
     - x-axis shared with panel 1.
     - Overlay: a thin vertical line marking ⟨x⟩(t), updated each frame.
  3. Expansion bar chart |c_n|² (300 px wide, side panel):
     - One bar per n, height = |c_n|². Updates when coefficient sliders change.
  4. Coefficient sliders + numerical readouts (bottom):
     - c_1, c_2, c_3, c_4, c_5 (real magnitudes, range 0 to 1).
     - θ_1, θ_2, θ_3, θ_4, θ_5 (phases, range 0 to 2π).
     - Normalize Σ |c_n|² to 1 automatically and display the renormalized
       values.
     - L slider (1 to 20 nm).
     - Mass dropdown {electron, proton}.
     - n_max slider (1 to 20) — number of basis states used.
     - Time slider (0 to T_slosh where T_slosh = 2π ℏ / (E_2 − E_1)).
     - Pause/play, reset.

Numerical readouts (side panel):
  - ⟨x⟩(t)  in nm  (live)
  - ⟨H⟩     in eV  (must be CONSTANT — flag red if drift > 0.1%)
  - ∫|Ψ|² dx  (must read 1.000)
  - E_1, E_2, E_3 in eV
  - T_slosh in fs

CONSTRAIN.
- D3 v7 from CDN. SVG only. Vanilla JS.
- N = 200 grid points on x ∈ [0, L].
- Eigenstates computed from the closed form √(2/L) sin(nπx/L); no
  Gram-Schmidt, no numerical eigensolver.
- Time evolution: analytic Σ c_n ψ_n exp(−i E_n t/ℏ). Complex storage
  required.
- Phase sign: exp(−i E_n t/ℏ). Verify by setting c_1 = c_2 = 1/√2,
  θ_1 = θ_2 = 0, and watching ⟨x⟩(t): at t = 0, ⟨x⟩ = L/2 (symmetry);
  it should first decrease (slosh left) for the −i convention, increase
  for the +i convention. The chapter requires −i.
- ⟨H⟩ must be constant. If it drifts, the simulation is wrong.

VERIFY.
Give me five checks for the browser:
(a) For L = 1 nm electron: E_1 = 0.377 eV, E_2 = 1.508 eV, E_3 = 3.39 eV.
    E_2 / E_1 = 4.00 exactly; E_3 / E_1 = 9.00 exactly.
(b) ψ_n has exactly n−1 internal nodes (counting zeros strictly inside (0, L)).
(c) c_1 = c_2 = 1/√2, others = 0: sloshing period T = 2πℏ/(E_2 − E_1) =
    h/(3 E_1) ≈ 3.66 fs for L = 1 nm electron. Verify by reading T_slosh.
(d) ⟨H⟩ = (|c_1|² E_1 + |c_2|² E_2 + ...) — for c_1 = c_2 = 1/√2,
    ⟨H⟩ = (E_1 + E_2)/2 ≈ 0.942 eV. Must be constant to 4 decimal places.
(e) For an n = 1 eigenstate only (c_1 = 1, others = 0), |Ψ(x, t)|² is
    visibly time-independent (no sloshing), and the centroid ⟨x⟩ = L/2
    is stationary.

List known LLM failure modes and confirm guards:
  - Wrong boundary conditions (Neumann instead of Dirichlet).
  - E_n not scaling as n² (verify (b) check).
  - Phase sign error (exp(+iE_n t/ℏ) flips slosh direction).
  - ⟨H⟩ drift in time (signals explicit Euler or recomputing c_n's).
  - Forced Gram-Schmidt orthogonality hiding the trigonometric identity.
  - Finite-well: ψ' discontinuity at the wall (irrelevant here — infinite well — but watch in extension).
  - Broken n_max slider in the extension.
````

### Part C — Exploration tasks

1. **Verify the $n^2$ spectrum.** Set $L = 1$ nm, electron. Read $E_1, E_2, E_3$ from the energy-level diagram. Compute the ratios. State whether $E_n = n^2 E_1$ holds to displayed precision.

2. **Watch a single eigenstate.** Set $c_1 = 1$, all others $0$. Play the time slider. $|\Psi|^2$ does not change. $\langle x \rangle$ stays at $L/2$. $\langle H \rangle$ stays at $E_1$. Now look at Re $\psi$ if your simulation exposes it: it should oscillate in time at frequency $E_1/\hbar$. The probability density is stationary; the wave function is not.

3. **Slosh.** Set $c_1 = c_2 = 1/\sqrt{2}$, $\theta_1 = \theta_2 = 0$. Run time. The probability density swings between the left and right halves of the well at period $T \approx 3.66$ fs. Watch $\langle x \rangle(t)$ oscillate. *Note that $\langle H \rangle$ does not change.* The sloshing carries no energy flux.

4. **Phase matters.** With $c_1 = c_2 = 1/\sqrt{2}$, set $\theta_2 = \pi$ (other phases unchanged). The probability density now sloshes in the *opposite* phase — starts on the right rather than the left. Explain in two sentences why the relative phase of the coefficients changes the initial $|\Psi|^2$ shape.

5. **More eigenstates, more localization.** Set $c_1 = c_2 = c_3 = c_4 = c_5 = 1/\sqrt{5}$. The probability density is more concentrated than for any single eigenstate. Now use the extension's "draw your own" feature, draw a narrow Gaussian, increase $n_\max$ from $5$ to $20$, and watch the bar chart and the spatial reconstruction sharpen.

### Part D — Extension prompt

````markdown
Add a "Draw your own ψ(x, 0)" feature in a fifth panel.

Behavior:
  - The user clicks-and-drags on a 600 × 150 SVG canvas to sketch a
    real-valued ψ(x, 0). The curve is sampled at the same N = 200 grid.
  - The sampled curve is normalized to ∫|ψ|² dx = 1.
  - The coefficients c_n = ∫_0^L ψ_n(x) ψ(x, 0) dx are computed by
    Simpson's rule for n = 1..n_max.
  - The expansion bar chart updates.
  - |Ψ(x, t)|² is animated forward from the drawn initial state.
  - A faint gray curve overlays the *reconstruction* Σ c_n ψ_n at t = 0,
    so the user can see how well the truncated basis captures the drawing.
  - The n_max slider (range 1..30) controls how many basis states are used.

Verify by drawing a Gaussian centered at L/4. Reconstruction at n_max = 5
should be visibly poor (smoothed, broader than drawn). At n_max = 20,
it should be visually indistinguishable from the drawing. The bar chart
shows which c_n's dominate — for a Gaussian centered at L/4, the largest
|c_n|² values cluster around n where nπx/L has its first peak near L/4.

Then time-evolve. Watch the drawn shape disperse — because it is a
superposition of many energies, the relative phases scramble over time.
State why: more eigenstates mean more pairwise beat frequencies, mean
faster dephasing.

Do not regress the four existing panels.
````

When you watch your hand-drawn pulse disperse, you have seen the inverse of localization: a particle "found" at one location is a superposition of many energies, and the energies dephase. Chapter 3 (harmonic oscillator) shows the only system where a special superposition — the coherent state — escapes this fate.

## 10. What would change my mind

The chapter's structural claim is that quantization of energy in a confined system follows from continuity of the wave function at the boundary — a regularity condition, not a postulate. If a careful experimental test of, say, semiconductor quantum-well spectroscopy ([Esaki & Tsu 1970](https://doi.org/10.1147/rd.141.0061), [Capasso et al. 1994, *Science* 264, 553–556](https://www.science.org/doi/10.1126/science.264.5158.553)) revealed a deviation from the $n^2$ scaling that could *not* be attributed to a non-rectangular potential, band-structure effects, or excitonic corrections — a clean violation of the TISE for a confined free particle — I would have to revise. The spectroscopic evidence is consistent with the TISE to the precision of the experiments. Higher-precision tests in cold-atom optical lattices ([Bloch 2005, *Nature Physics* 1, 23–30](https://www.nature.com/articles/nphys138)) likewise agree with the TISE within experimental error.

## 11. Still puzzling

- The infinite square well is a cartoon — no real potential is infinite. The finite well (briefly Section 8.1 in some treatments, deferred to Chapter 8 here) has bound states with $\psi$ extending into the classically forbidden region (the tail). The chapter has not yet developed a clean treatment of *why* a wave function in a forbidden region is acceptable, only that it is. Chapter 8's tunneling treatment is owed.
- Completeness of the eigenstates of $\hat{H}$ — that any normalizable $\psi$ in $[0, L]$ with the right boundary conditions is a sum of $\psi_n$'s — is a theorem from Fourier analysis. The chapter cites this rather than proves it. The proof requires functional-analysis machinery (the spectral theorem for self-adjoint operators on $L^2$) that an undergraduate text cannot fairly include. The student should know it is *not* magic, but the chapter does not yet point them to a sufficient mathematical reference. (Stein & Shakarchi 2003 is the cleanest I know.)
- The "draw your own $\psi$" feature reveals beautifully that a localized state requires many energies. The chapter does not yet have a tidy statement of *how many* — i.e., how fast the truncation error decays with $n_\max$. The answer depends on the smoothness of the drawing; smooth ones converge fast, ones with corners converge slowly. This deserves a sidebar.
- The chapter's framing — "quantization is derived, not postulated" — is true for the infinite well. For continuous spectra (free particle), quantization does not happen at all; for the hydrogen atom, the discrete part of the spectrum comes from analogous boundary conditions at infinity. The general theory is the spectral theory of self-adjoint operators. The chapter has not yet decided how much of that lineage to preview.

**Tags:** TISE, infinite-square-well, separation-of-variables, energy-quantization, stationary-state, Fourier-completeness, sloshing, McKagan-Perkins-Wieman

---

*Bridge to Chapter 3: The infinite well is exactly solvable because the potential is piecewise constant. The next exactly solvable system has a continuous potential — the harmonic oscillator $V = (1/2) m \omega^2 x^2$. The differential-equation approach works but is ugly; the elegant approach uses ladder operators. Chapter 3 builds them.*
