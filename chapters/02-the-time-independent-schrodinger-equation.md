# Chapter 2 — The Time-Independent Schrödinger Equation
*What the Wall Demands.*

> Quantization is not assumed. It falls out of asking a wave function to be continuous in a box with hard walls — and once you have seen that derivation, you have seen one of the cleanest "oh" moments in physics.

---

In 1913, Bohr wrote down a rule. He said the angular momentum of an electron orbiting a hydrogen nucleus had to be a whole-number multiple of $\hbar$: $mvr = n\hbar$, for $n = 1, 2, 3, \ldots$. The rule worked — it predicted the hydrogen spectrum with stunning precision. But Bohr could not explain why. He had no mechanism. He had a rule that fit, attached to no deeper principle. When pressed, he said it was a new law of nature and left it there.

Schrödinger, in 1926, showed that Bohr's rule was not a new law. It was a *consequence* — of the wave equation, and of one completely ordinary requirement: that the wave function be continuous. The discreteness of atomic spectra is not imposed from outside. It falls out of the mathematics of waves in confined spaces. The fact that an electron in a hydrogen atom can have only certain energies is, at bottom, the same kind of fact as the observation that a guitar string can vibrate at only certain frequencies. Boundary conditions create discrete spectra. They always have.

This chapter is that derivation, done carefully, for the simplest case: a particle confined to a box.

---

## Separating the problem

The Schrödinger equation, in its full time-dependent form, is

$$i\hbar\,\frac{\partial \psi}{\partial t} = \hat{H}\,\psi, \qquad \hat{H} = -\frac{\hbar^2}{2m}\,\frac{\partial^2}{\partial x^2} + V(x).$$

This is a partial differential equation — it has both time and space derivatives, and they are coupled. In general, solving it is hard. But there is a case where it simplifies dramatically: when $V$ depends only on $x$, not on $t$. Most of the potentials we care about — the infinite well, the harmonic oscillator, the hydrogen atom — have this property.

When $V = V(x)$, try the ansatz $\psi(x, t) = \psi(x)\,\phi(t)$: a product of a purely spatial function and a purely temporal one. Substitute into the TDSE and divide through by $\psi \phi$:

$$i\hbar\,\frac{\phi'(t)}{\phi(t)} = \frac{\hat{H}\psi(x)}{\psi(x)}.$$

Now look at what this says. The left side is a function of $t$ only. The right side is a function of $x$ only. They are equal for all $x$ and all $t$. The only way that can happen is if both sides equal the same constant. Call it $E$.

Two equations emerge. The time equation,

$$i\hbar\,\phi'(t) = E\,\phi(t),$$

is solved immediately: $\phi(t) = e^{-iEt/\hbar}$. The spatial equation is

$$\hat{H}\,\psi(x) = E\,\psi(x).$$

This second equation is the **time-independent Schrödinger equation**. It is an eigenvalue problem: find functions $\psi$ such that applying $\hat{H}$ to $\psi$ gives back $\psi$ multiplied by a constant. The constant is the energy $E$.

<!-- → [INFOGRAPHIC: separation-of-variables split diagram — one box labeled "TDSE: ∂ψ/∂t coupled to ∂²ψ/∂x²" with an arrow pointing to two boxes: left "Time equation: iℏφ'= Eφ → φ(t) = e^{−iEt/ℏ} (trivial)" and right "TISE: Ĥψ = Eψ (all the physics)"; caption: "The separation trick converts a PDE into two ODEs. The time part is solved by inspection; the spatial part is the eigenvalue problem that determines the allowed energies"] -->

The trick has converted a PDE into an ODE. The time evolution is trivial — just a rotating phase. All the physics is in the spatial problem: what values of $E$ are allowed? What do the corresponding $\psi$'s look like?

One clarification is worth making now. The separation ansatz produces *some* solutions of the full TDSE — the separable ones, which we will call stationary states. It does not immediately tell you that *every* solution is a superposition of separable ones. That stronger claim requires the eigenstates of $\hat{H}$ to form a complete basis for the space of allowable wave functions, which is a theorem — an important one, and not a trivial one, but a theorem established by the mathematics of self-adjoint operators long before quantum mechanics existed. We will use it and note that it is not magic; it is Fourier analysis.

---

## The TISE, written out

In one dimension:

$$-\frac{\hbar^2}{2m}\,\frac{d^2\psi}{dx^2} + V(x)\,\psi(x) = E\,\psi(x).$$

This is a second-order linear ODE. For a given $V(x)$, it is a *constrained* problem: not every value of $E$ admits a normalizable, physically acceptable solution. The allowed $E$'s — the spectrum — depend entirely on the shape of $V$.

For potentials that go to infinity at large $|x|$ (confining potentials), the spectrum is discrete: only certain $E$'s are allowed. For potentials that eventually level off, the spectrum has both a discrete piece (bound states) and a continuous piece (scattering states) above the potential's asymptotic value. The chapter focuses on the purest case of the discrete spectrum: a particle confined between infinitely hard walls.

---

## The infinite square well — eight steps

A particle of mass $m$ lives in the region $0 < x < L$. Outside this region, $V = \infty$: the particle cannot exist there. The potential is

$$V(x) = \begin{cases} 0 & 0 < x < L, \\ \infty & \text{elsewhere.} \end{cases}$$

Because $V = \infty$ outside, the wave function must vanish outside: $\psi(x) = 0$ for $x \leq 0$ and $x \geq L$. That is not a separate assumption; it is what $V = \infty$ means.

**Inside the well**, $V = 0$, and the TISE becomes

$$-\frac{\hbar^2}{2m}\,\psi'' = E\,\psi, \qquad \text{i.e.,} \qquad \psi'' = -\frac{2mE}{\hbar^2}\,\psi.$$

Define $k^2 = 2mE/\hbar^2$. For $E > 0$, $k$ is real and the equation reads $\psi'' = -k^2\psi$ — the equation of a harmonic oscillator in space. The general solution is

$$\psi(x) = A\sin(kx) + B\cos(kx).$$

Any value of $k$ — any value of $E > 0$ — satisfies this equation. There is no quantization yet. The differential equation has a continuous family of solutions.

Now apply the boundary conditions.

**At $x = 0$:** continuity of $\psi$ requires $\psi(0) = 0$ (since $\psi = 0$ for $x < 0$). Therefore $A \cdot 0 + B \cdot 1 = 0$, so $B = 0$. The cosine term is eliminated:

$$\psi(x) = A\sin(kx).$$

Still no quantization. Any $k$ still works.

**At $x = L$:** continuity requires $\psi(L) = 0$:

$$A\sin(kL) = 0.$$

Either $A = 0$ — the trivial solution, no particle — or

$$\sin(kL) = 0.$$

This is the step where everything changes.

$\sin(kL) = 0$ has solutions only when $kL$ is an integer multiple of $\pi$:

$$kL = n\pi, \qquad n = 1, 2, 3, \ldots$$

The continuous range of allowed $k$'s — which was any positive real number — has collapsed to a discrete set, indexed by an integer. This is where quantization enters the physics. Not from a postulate about angular momentum. Not from a rule written down by hand. From asking that the wave function be continuous at the wall.

<!-- → [INFOGRAPHIC: two-panel diagram illustrating the collapse from continuous to discrete — left panel: a continuous horizontal band of allowed k values labeled "General solution: any k works"; right panel: the same axis with only discrete tick marks at k = π/L, 2π/L, 3π/L, ... labeled "After boundary condition ψ(L) = 0: only k_n = nπ/L survive"; an arrow between panels labeled "sin(kL) = 0 forces kL = nπ"; caption: "Quantization is not assumed. It is what happens when you ask a sine wave to vanish at both walls simultaneously"] -->

Why does $n = 0$ not count? Because $k_0 = 0$ gives $\psi(x) = A\sin(0) = 0$ everywhere — no particle. Why no negative $n$? Because $\sin(-n\pi x/L) = -\sin(n\pi x/L)$: the same physical state, up to a global sign that cancels in $|\psi|^2$.

From $k_n = n\pi/L$ and $E = \hbar^2 k^2 / (2m)$, the allowed energies are

$$\boxed{E_n = \frac{n^2\,\pi^2\,\hbar^2}{2\,m\,L^2}, \qquad n = 1, 2, 3, \ldots}$$

The energies scale as $n^2$. The ratio $E_n / E_1 = n^2$: the sequence is $1, 4, 9, 16, 25, \ldots$ There is nothing between them.

Normalize $\psi_n(x) = A\sin(n\pi x/L)$ by requiring $\int_0^L |\psi_n|^2\,dx = 1$:

$$A^2 \int_0^L \sin^2\!\left(\frac{n\pi x}{L}\right)dx = A^2 \cdot \frac{L}{2} = 1 \implies A = \sqrt{\frac{2}{L}}.$$

The normalized eigenstates are

$$\psi_n(x) = \sqrt{\frac{2}{L}}\,\sin\!\left(\frac{n\pi x}{L}\right), \quad 0 \leq x \leq L; \quad \psi_n(x) = 0 \text{ elsewhere.}$$

Each $\psi_n$ has exactly $n - 1$ nodes inside the well. The ground state has no internal zeros; it is a half-period sine, pushed up to the wall on both sides. The first excited state has one node at $x = L/2$. In general, the $n$-th state is $n$ half-wavelengths fitted between the walls.

<!-- → [IMAGE: energy-level diagram in the style of Griffiths Fig. 2.2 — vertical axis is energy, horizontal axis is x from 0 to L; five horizontal green lines at heights E_1, E_2, E_3, E_4, E_5 labeled in units of E_1 (1, 4, 9, 16, 25); each eigenstate ψ_n drawn as a sine wave with its zero offset to the corresponding energy level and amplitude scaled to fit between adjacent levels; node count labeled for each: n=1 has 0 nodes, n=2 has 1 node, etc.; red vertical walls at x=0 and x=L; caption: "The n-th eigenstate fits exactly n half-wavelengths between the walls. Nodes count the number of half-wavelengths minus one"] -->

---

## What the ground state tells us about zero

The lowest energy, $E_1 = \pi^2\hbar^2/(2mL^2)$, is strictly positive. The particle cannot have $E = 0$.

This is sometimes described as the zero-point energy, as if it were a peculiar quantum anomaly. But it is not peculiar at all. If the particle had $E = 0$, it would have $p = 0$ — zero momentum. If $p = 0$ exactly, then $\sigma_p = 0$. But the particle is confined to $[0, L]$, so its position uncertainty is at most $L$. Then $\sigma_x \sigma_p \leq L \cdot 0 = 0 < \hbar/2$, which violates the uncertainty principle derived in Chapter 1. The uncertainty principle *requires* a positive minimum energy for any confined particle. The zero-point energy is not a surprise; it is the uncertainty principle made quantitative.

You can check the numbers. For the ground state, $\sigma_x = L\sqrt{1/12 - 1/(2\pi^2)} \approx 0.181\,L$ and $\sigma_p = \pi\hbar/L$ (derivable directly from the eigenstate). So $\sigma_x\sigma_p \approx 0.568\,\hbar$, which is indeed $\geq \hbar/2$. The inequality is satisfied, and not by much — the ground state is close to the uncertainty-principle bound. That closeness is telling you something: the ground state of the infinite well is, in a specific sense, as localized as it is allowed to be.

<!-- → [CHART: scatter plot or bar chart comparing σ_x · σ_p for n = 1 through 6 — horizontal axis: quantum number n; vertical axis: σ_x σ_p / ℏ; a horizontal dashed line at 0.5 marking the ℏ/2 lower bound; data points plotted showing the n=1 value ≈ 0.568 just above the bound, with values increasing for higher n; caption: "The ground state (n=1) comes closest to saturating the uncertainty bound. Higher eigenstates have more nodes, wider momentum distributions, and larger σ_x σ_p"] -->

---

## What the energy scale tells us

For an electron ($m = 9.109 \times 10^{-31}$ kg) in a well of width $L = 1$ nm:

$$E_1 = \frac{\pi^2\,(1.055 \times 10^{-34})^2}{2\,(9.109 \times 10^{-31})\,(10^{-9})^2} \approx 6.03 \times 10^{-20}\ \text{J} \approx 0.377\ \text{eV.}$$

So $E_1 \approx 0.38$ eV, $E_2 \approx 1.51$ eV, $E_3 \approx 3.39$ eV. These are energies on the scale of chemistry. Thermal energy at room temperature is $k_BT \approx 0.025$ eV; visible photons carry roughly $2$ eV. A nanometer-scale quantum well has level spacings in the optical range. This is not a theoretical curiosity — it is the operating principle of semiconductor quantum-well lasers, in which the emission wavelength is tuned by adjusting $L$.

For a marble in a 1 cm box, $E_1 \sim 10^{-58}$ eV — immeasurably small compared to any other energy in the problem. Quantum discreteness is set by $\hbar^2/(mL^2)$. Make $m$ or $L$ large and it vanishes. The classical limit is not a philosophical claim; it is a calculation.

<!-- → [TABLE: energy scales across particle and box sizes — rows: electron in 1 nm well, electron in 1 cm box, proton in 1 nm well, C60 molecule in 10 nm trap, marble in 1 cm box; columns: mass (kg), L (m), E_1 (eV), E_2−E_1 (eV), verdict (quantum / borderline / classical); student should see that E_1 ∝ 1/(mL²) and identify which rows fall above and below thermal energy k_BT ≈ 0.025 eV at room temperature] -->

---

## Building states from eigenstates

The eigenstates $\{\psi_n\}$ are orthonormal:

$$\langle \psi_m \,|\, \psi_n \rangle = \int_0^L \psi_m(x)\,\psi_n(x)\,dx = \delta_{mn}.$$

This follows from the trigonometric identity $\sin\alpha\sin\beta = \frac{1}{2}[\cos(\alpha - \beta) - \cos(\alpha + \beta)]$: for $m \neq n$, both resulting cosines integrate over an integer number of half-periods on $[0, L]$ and give zero; for $m = n$, the first cosine becomes $1$, integrating to $L$, and the second integrates to zero. The $\delta_{mn}$ falls out of a one-line calculation.

They are also complete: any function $f(x)$ on $[0, L]$ with $f(0) = f(L) = 0$ and $\int_0^L|f|^2\,dx < \infty$ can be expanded as

$$f(x) = \sum_{n=1}^{\infty} c_n\,\psi_n(x), \qquad c_n = \langle \psi_n \,|\, f \rangle = \int_0^L \psi_n(x)\,f(x)\,dx.$$

This is the Fourier sine series. Fourier established it in 1822, in his analysis of heat conduction — a century before quantum mechanics. The convergence theorem is not easy to prove, but the result is classical mathematics, not quantum postulation. A student who treats "any state is a superposition of energy eigenstates" as quantum mysticism has missed the point: it is a statement about square-integrable functions, and it was understood long before anyone had heard of a wave function.

Given an initial state $\Psi(x, 0) = f(x)$, expand it in eigenstates, attach to each eigenstate its time-evolution phase, and sum:

$$\Psi(x, t) = \sum_n c_n\,\psi_n(x)\,e^{-i E_n t/\hbar}.$$

Solve the TISE once. Get the $\{\psi_n, E_n\}$. Project the initial condition. Phase-rotate each piece at its own frequency. That is the complete dynamics of any state in the infinite well.

---

## What "stationary" actually means

A stationary state $\psi_n(x)\,e^{-iE_n t/\hbar}$ has a time-independent probability density: $|\psi_n|^2$ does not depend on $t$. This is the sense in which it is stationary. But it would be a mistake to conclude that the wave function is time-independent. The phase $e^{-iE_n t/\hbar}$ rotates in the complex plane at angular frequency $E_n/\hbar$. If you could measure the phase, you would see it spinning.

In a single eigenstate, you cannot see the spinning, because the phase cancels when you compute $|\psi|^2$. The moment you take a superposition of two eigenstates with different energies, the relative phase between them becomes observable — it shows up as a time-varying interference term.

Take the simplest example: $c_1 = c_2 = 1/\sqrt{2}$, all other $c_n = 0$. Then

$$|\Psi(x, t)|^2 = \frac{1}{2}\!\left[\psi_1^2 + \psi_2^2 + 2\,\psi_1\,\psi_2\,\cos\!\left(\frac{(E_2 - E_1)t}{\hbar}\right)\right].$$

The first two terms are time-independent — they are the average of the two probability densities. The third term oscillates at angular frequency $\omega = (E_2 - E_1)/\hbar$. Because $\psi_1$ is concentrated in the center of the well and $\psi_2$ is concentrated near the walls (with a node at $x = L/2$), the cross term shifts probability from one half of the well to the other. The probability density *sloshes*.

The period of the sloshing is

$$T = \frac{2\pi\hbar}{E_2 - E_1} = \frac{2\pi\hbar}{3E_1} = \frac{h}{3E_1}.$$

For the $L = 1$ nm electron, $E_1 \approx 6.03 \times 10^{-20}$ J, so

$$T = \frac{6.626 \times 10^{-34}}{3 \times 6.03 \times 10^{-20}} \approx 3.66 \times 10^{-15}\ \text{s} = 3.66\ \text{fs.}$$

The probability density swings from one side of the well to the other in about $3.7$ femtoseconds. The energy of the state — $\langle H \rangle = (E_1 + E_2)/2 \approx 0.94$ eV — does not change during the sloshing. The particle's probability distribution is moving; its energy is not.

This is the thing the simulation makes visible. The energy levels and eigenstates are static — drawn once from the closed form. The sloshing is what happens when you set the phases running. Watch $\langle x \rangle(t)$ oscillate on screen while $\langle H \rangle$ stays pinned. That dissociation between where the particle probably is and how much energy it has is one of the genuinely non-classical features of quantum mechanics — not strange in its mathematics, but strange in what it implies about the relationship between position and energy.

<!-- → [CHART: two-panel time-series — top panel: ⟨x⟩(t) in nm oscillating sinusoidally between ~0.3L and ~0.7L with period T ≈ 3.66 fs for the c_1=c_2=1/√2 superposition, dashed line at L/2 marking the mean; bottom panel: ⟨H⟩(t) in eV as a flat horizontal line at (E_1+E_2)/2 ≈ 0.942 eV across the same time axis; caption: "Position expectation oscillates at the beat frequency; energy expectation is exactly constant. The sloshing carries no energy — it is a phase phenomenon"] -->

---

## A note on completeness

The claim that any state in the well is a sum of eigenstates is not something to accept on authority. Here is why it is true, in outline. The operator $\hat{H} = -(\hbar^2/2m)\,d^2/dx^2$ on the space of square-integrable functions on $[0, L]$ that vanish at the boundary is a self-adjoint operator. Self-adjoint operators on Hilbert spaces have a spectral theorem: their eigenvectors form a complete orthonormal basis. This is a theorem of functional analysis, established in its modern form by von Neumann in the late 1920s, building on spectral theory that mathematicians had developed for ordinary differential operators throughout the nineteenth century. The sine functions $\{\psi_n\}$ are not just convenient — they are provably the complete basis for this space. The proof is in Stein and Shakarchi's *Fourier Analysis* (2003), Chapter 4, for the reader who wants the details.

The relevant practical point: any state you can write down that vanishes at $x = 0$ and $x = L$ and is square-integrable can be represented as a sum of the $\psi_n$'s. Truncating the sum — using only the first $N$ terms — gives an approximation that improves as $N$ increases. How fast it improves depends on how smooth the initial state is: smooth initial conditions converge rapidly, states with sharp features (kinks, jumps) converge slowly. The simulation's "draw your own $\psi$" extension makes this rate of convergence visible.

---

## What would change my mind

The claim that quantization follows from continuity of the wave function at the boundary is not just the theoretical story — it is experimentally tested, and the tests are precise. Semiconductor quantum-well spectroscopy measures the transition energies between levels in artificially fabricated wells. The $n^2$ scaling of the infinite-well approximation is confirmed, with corrections that arise predictably from the finite depth of real wells, band-structure effects in the semiconductor, and excitonic interactions. The foundational experimental work is Esaki and Tsu (1970), with extensive later confirmation in quantum-well laser work through the 1980s and 1990s. Cold-atom experiments in optical lattices provide a cleaner realization of the ideal well, and their spectroscopic results agree with the TISE within experimental precision.

If a well-controlled experiment found an energy spacing that could not be explained by the TISE plus known corrections — if the $n^2$ scaling failed in a way attributable to neither potential shape, band structure, nor many-body effects — I would have to revise the picture. As of now, no such failure has been found.

---

## Exercises

**Warm-up**

**2.1** Apply separation of variables to the TDSE with $V = V(x)$. Write down the two equations that result, name the separation constant, and state what each equation's solution looks like. *(Tests: can execute the separation argument from memory and identify the role of the constant E)*

**2.2** For the infinite square well, state the boundary conditions on $\psi$ at $x = 0$ and $x = L$. Apply them in sequence to the general solution $\psi(x) = A\sin(kx) + B\cos(kx)$ and show that $B = 0$ and $\sin(kL) = 0$. At which step does quantization first appear, and why? *(Tests: can reproduce the eight-step argument and identify the specific moment quantization enters)*

**2.3** For a well of width $L = 2$ nm containing an electron, compute $E_1$, $E_2$, and $E_3$ in eV. Verify that $E_n/E_1 = n^2$ to three significant figures. How do these values compare to the $L = 1$ nm case in the chapter? *(Tests: can apply the energy formula numerically; can identify the $L^{-2}$ scaling)*

---

**Application**

**2.4** For the ground state $\psi_1(x) = \sqrt{2/L}\sin(\pi x/L)$, compute $\langle x \rangle$ and $\langle x^2 \rangle$ and hence $\sigma_x$. Show that $\sigma_x = L\sqrt{1/12 - 1/(2\pi^2)}$. Use $\sigma_p = \pi\hbar/L$ (which you may take as given) to verify $\sigma_x\sigma_p \approx 0.568\,\hbar \geq \hbar/2$. *(Tests: can compute expectation values from an eigenstate and verify the uncertainty principle numerically)*

**2.5** A particle is prepared in the state $\Psi(x, 0) = (1/\sqrt{2})[\psi_1(x) + \psi_3(x)]$. (a) Write down $\Psi(x, t)$. (b) Compute $|\Psi(x,t)|^2$. (c) Find the angular frequency of the oscillating cross term. (d) Compute $\langle H \rangle$ and show it is time-independent. *(Tests: can time-evolve a two-term superposition; can identify the beat frequency; can verify energy conservation)*

**2.6** Compute the probability of finding the particle in the left quarter of the well — $x \in [0, L/4]$ — for the ground state ($n = 1$) and for the first excited state ($n = 2$). Which state is more concentrated there, and why does this match the shape of $\psi_1$ versus $\psi_2$? *(Tests: can evaluate definite integrals of $\sin^2$; can connect probability calculation to the spatial shape of the eigenstate)*

**2.7** An electron is in the $n = 3$ state of a $1$ nm well. (a) How many nodes does $\psi_3$ have inside the well? (b) What is its energy in eV? (c) A photon is emitted and the electron drops to $n = 1$. What is the wavelength of the photon? Is it in the visible range? *(Tests: can apply the energy formula and the photon-energy relation; can connect the calculation to a physically observable quantity)*

---

**Synthesis**

**2.8** The chapter argues that the zero-point energy $E_1 > 0$ is required by the uncertainty principle. Make this argument quantitative: show that if $E = 0$ in the well, then $\sigma_p = 0$, and derive the contradiction with $\sigma_x \sigma_p \geq \hbar/2$. Then show that $E_1 = \pi^2\hbar^2/(2mL^2)$ gives a product $\sigma_x\sigma_p$ that satisfies but does not saturate the bound. What kind of state saturates the uncertainty bound exactly? *(Tests: can use the uncertainty principle as a constraint on allowed energies; can identify the Gaussian as the minimum-uncertainty state)*

**2.9** Fourier established completeness of the sine basis in 1822 for the heat equation. Write the heat equation $\partial_t u = D\,\partial_{xx} u$ with $u(0,t) = u(L,t) = 0$. (a) Apply separation of variables and find the spatial eigenfunctions. (b) Compare them to the TISE eigenstates $\psi_n$ for the infinite well. (c) Identify the structural difference: in the heat equation the time evolution is $e^{-Dk_n^2 t}$ (decay), while in quantum mechanics it is $e^{-iE_n t/\hbar}$ (rotation). What does this difference imply about whether probability is conserved? *(Tests: can apply separation of variables to a different PDE; can identify the structural analogy between QM and classical wave/diffusion equations; can connect the imaginary exponent to unitarity)*

---

**Challenge**

**2.10** The chapter states that a drawn initial state with sharp features (kinks, corners) converges slowly in the eigenstate basis. Make this precise: if $\Psi(x, 0)$ has a discontinuity in its first derivative at some interior point $x_0 \in (0, L)$, how does $|c_n|$ decay with $n$ for large $n$? (Hint: integrate $c_n = \int_0^L \psi_n\,\Psi\,dx$ by parts twice and examine what survives.) Compare the convergence rate to a smooth initial state with no kinks. In the simulation's "draw your own" extension, what do you expect to see in the bar chart when you draw (a) a smooth Gaussian versus (b) a tent function (triangular shape with a corner)? *(Tests: requires integration by parts and asymptotic reasoning; connects the mathematical convergence rate to a visible simulation behavior)*

---

## LLM Exercise — the infinite-well explorer

The chapter's deliverable is `02-infinite-well.html`: an energy diagram with eigenstates overlaid, a dynamical $|\Psi(x,t)|^2$ panel, coefficient and phase sliders, and an expansion bar chart. The extension adds a "draw your own $\psi(x,0)$" canvas.

### Part A — `CLAUDE.md` snippet for this chapter

```
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
```

### Part B — The simulation prompt

```
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
Produce a single file 02-infinite-well.html.

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
     - Normalize Σ |c_n|² to 1 automatically and display the renormalized values.
     - L slider (1 to 20 nm).
     - Mass dropdown {electron, proton}.
     - n_max slider (1 to 20).
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
- Time evolution: analytic Σ c_n ψ_n exp(−i E_n t/ℏ). Complex storage required.
- Phase sign: exp(−i E_n t/ℏ). Verify by setting c_1 = c_2 = 1/√2,
  θ_1 = θ_2 = 0, and watching ⟨x⟩(t): at t = 0, ⟨x⟩ = L/2 (symmetry);
  it should first decrease (slosh left) for the −i convention.
- ⟨H⟩ must be constant. If it drifts, the simulation is wrong.

VERIFY.
Give me five checks for the browser:
(a) For L = 1 nm electron: E_1 = 0.377 eV, E_2 = 1.508 eV, E_3 = 3.39 eV.
    E_2 / E_1 = 4.00 exactly; E_3 / E_1 = 9.00 exactly.
(b) ψ_n has exactly n−1 internal nodes (counting zeros strictly inside (0, L)).
(c) c_1 = c_2 = 1/√2, others = 0: sloshing period T ≈ 3.66 fs for
    L = 1 nm electron. Verify by reading T_slosh.
(d) ⟨H⟩ = (E_1 + E_2)/2 ≈ 0.942 eV for c_1 = c_2 = 1/√2.
    Must be constant to 4 decimal places.
(e) For c_1 = 1 only, |Ψ(x,t)|² is visibly time-independent and ⟨x⟩ = L/2
    is stationary.

List known LLM failure modes and confirm guards:
  - Wrong boundary conditions (Neumann instead of Dirichlet).
  - E_n not scaling as n².
  - Phase sign error (exp(+iE_n t/ℏ) flips slosh direction).
  - ⟨H⟩ drift in time.
  - Forced Gram-Schmidt hiding the trigonometric identity.
  - Broken n_max slider in the extension.
```

### Part C — Exploration tasks

1. **Verify the $n^2$ spectrum.** Set $L = 1$ nm, electron. Read $E_1, E_2, E_3$. Compute the ratios. Confirm $E_n/E_1 = n^2$ to displayed precision.

2. **Watch a single eigenstate.** Set $c_1 = 1$, all others zero. Play the time slider. $|\Psi|^2$ does not change. $\langle x \rangle$ stays at $L/2$. $\langle H \rangle$ stays at $E_1$. The probability density is stationary; the wave function is not.

3. **Slosh.** Set $c_1 = c_2 = 1/\sqrt{2}$, $\theta_1 = \theta_2 = 0$. Run time. Watch $\langle x \rangle(t)$ oscillate. Measure the period against the predicted $T \approx 3.66$ fs. Note that $\langle H \rangle$ does not change throughout.

4. **Phase matters.** With $c_1 = c_2 = 1/\sqrt{2}$, set $\theta_2 = \pi$. The sloshing starts on the opposite side. Explain in two sentences why the *relative* phase of two coefficients determines the initial shape of $|\Psi|^2$.

5. **More eigenstates, more localization.** Set $c_1 = \cdots = c_5 = 1/\sqrt{5}$. Use the extension's "draw your own" feature: draw a narrow Gaussian, increase $n_\max$ from $5$ to $20$, and watch the bar chart and spatial reconstruction sharpen.

### Part D — Extension prompt

```
Add a "Draw your own ψ(x, 0)" feature in a fifth panel.

Behavior:
  - The user clicks-and-drags on a 600 × 150 SVG canvas to sketch a
    real-valued ψ(x, 0). The curve is sampled at the same N = 200 grid.
  - The sampled curve is normalized to ∫|ψ|² dx = 1.
  - The coefficients c_n = ∫_0^L ψ_n(x) ψ(x, 0) dx are computed by
    Simpson's rule for n = 1..n_max.
  - The expansion bar chart updates.
  - |Ψ(x, t)|² is animated forward from the drawn initial state.
  - A faint gray curve overlays the reconstruction Σ c_n ψ_n at t = 0,
    so the user can see how well the truncated basis captures the drawing.
  - The n_max slider (range 1..30) controls how many basis states are used.

Verify by drawing a Gaussian centered at L/4. Reconstruction at n_max = 5
should be visibly poor (smoothed, broader than drawn). At n_max = 20,
it should be visually indistinguishable from the drawing.

Then time-evolve. Watch the drawn shape disperse. State why: more eigenstates
mean more pairwise beat frequencies, mean faster dephasing.

Do not regress the four existing panels.
```

When you watch your hand-drawn pulse disperse, you have seen the inverse of localization: a particle "found" at a single position is a superposition of many energies, and the energies dephase. Chapter 3 shows the only system where a special superposition — the coherent state — escapes this fate.

---

*Bridge to Chapter 3: The infinite well is exactly solvable because the potential is piecewise constant — the differential equation inside is trivially simple, and all the work is done by the boundary conditions. The next exactly solvable system has a continuous potential, $V = \frac{1}{2}m\omega^2 x^2$, and the differential equation itself is no longer trivial. The brute-force approach via power series works but is ungainly. Chapter 3 introduces ladder operators — a cleaner method that reveals the harmonic oscillator's structure without fighting the differential equation.*
