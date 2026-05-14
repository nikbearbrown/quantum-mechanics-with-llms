# Chapter 10 — Time-Dependent Perturbation Theory and Transitions

> The theory behind spectroscopy, laser-atom interactions, NMR, and qubit control — and the chapter where one of the most famous formulas in physics turns out to belong to the wrong man.

---

## 1. What this chapter is doing

Chapter 9 handled perturbations that sit still. This chapter handles perturbations that turn on, turn off, or oscillate. The question changes shape. Instead of *"how do the energy levels shift?"*, we ask *"if the system starts in state $|i\rangle$ and a time-varying perturbation acts, what is the probability of finding it in state $|f\rangle$ at a later time?"*

This is the framework behind every absorption spectrum, every fluorescence measurement, every NMR pulse sequence, every laser cooling experiment, every qubit gate, and every photoionization calculation in nuclear and condensed-matter physics. It is, by raw count of applications, the most important calculation in the second half of an undergraduate QM course.

The chapter delivers four results. The first-order transition amplitude: a Fourier integral over the matrix element. The canonical resonance lineshape: $\sin^2(\Omega t/2)/\Omega^2$. Fermi's golden rule (which, as we will see, was Dirac's, twenty years earlier — Fermi just named it). And the exact two-level Rabi solution, which serves as both the simulation centerpiece and the diagnostic for when perturbation theory is and is not allowed.

The simulation is the workshop of the chapter. You will build a Rabi oscillator that displays exact and perturbative answers side by side. You will see — visually — where the perturbative answer agrees with the exact one, where it disagrees, and exactly when "long times + continuum of final states" turns the $\sin^2$ profile into Fermi's delta function.

## 2. Learning objectives

By the end of this chapter you should be able to:

- Derive the first-order transition amplitude $c_f(t)$ from the interaction-picture Schrödinger equation.
- Recognize the transition amplitude as a Fourier component of the matrix element $\langle f|\hat{H}'(t)|i\rangle$.
- Specialize to monochromatic driving and obtain the $\sin^2[(\omega - \omega_{fi})t/2]/(\omega - \omega_{fi})^2$ profile.
- Take the long-time-plus-continuum limit and derive Fermi's golden rule (and acknowledge it was Dirac's first).
- State and apply electric-dipole selection rules: $\Delta\ell = \pm 1$, $\Delta m = 0, \pm 1$, $\Delta s = 0$.
- Solve the two-level Rabi problem exactly: $P_{g\to e}(t) = (\Omega^2/(\Omega^2+\Delta^2))\sin^2(\sqrt{\Omega^2+\Delta^2}\,t/2)$.
- Compare exact and perturbative answers and identify the regime where PT fails (large $\Omega t$).
- Build a D3 simulation showing Rabi oscillations, resonance lineshape, and the continuum-to-golden-rule transition.

## 3. Motivating problem

January 1938. Columbia University. Isidor Rabi, with Sidney Millman, Polykarp Kusch, Jerrold Zacharias, and a graduate student named Norman Ramsey, has built a molecular-beam apparatus. A beam of LiCl molecules passes through three magnets. The first magnet selects molecules with a particular spin orientation. The second magnet is the *interaction region* — it carries an oscillating radio-frequency field. The third magnet analyzes the spin state at the output. By detecting the beam intensity as a function of the RF frequency, Rabi's group can ask, for the first time, *exactly which frequency drives the lithium-7 nucleus from one spin orientation to the other*.

The signal they saw was sharp ([Rabi, Zacharias, Millman & Kusch, "A new method of measuring nuclear magnetic moment," *Phys. Rev.* 53, 318, 1938](https://journals.aps.org/pr/abstract/10.1103/PhysRev.53.318)). At a particular frequency $\omega_0$, set by the Zeeman splitting in the constant field, the beam intensity *dropped* — molecules had been driven from one spin state to another. Off-resonance, almost nothing happened. The line was narrow, well-defined, and theoretically predicted. Rabi won the Nobel in 1944.

Here is the puzzle that animates this chapter. The two-state system Rabi was driving — a spin-up state and a spin-down state, separated by energy $\hbar\omega_0$, coupled by an oscillating perturbation — is the same physical object as: an atom in a laser field, an NMR sample in a coil, a superconducting qubit in a microwave drive, a trapped ion in a Raman beam, an electron spin in an ESR experiment. *Every quantum control experiment of the last 80 years is, in essence, Rabi's 1938 setup, written in different molecular handwriting.* So the math we develop for one will work for all of them.

The first question: what is the probability of finding the system in the "wrong" state at time $t$, given that an oscillating field drove it for that long? The second: how does that probability depend on the frequency mismatch? The third: when the system can decay into a *continuum* of final states — an electron ionized into free-particle states, an atom emitting a photon into the infinite continuum of EM modes — what is the *rate* of transition? Those three questions get three answers in this chapter, and they unfold from a single derivation in the interaction picture.

## 4. Concept block — the interaction picture and first-order amplitude

### 4.1 Two pictures, one physics

In the Schrödinger picture, the state vector $|\psi(t)\rangle$ evolves under the full Hamiltonian:

$$i\hbar\,\partial_t|\psi(t)\rangle = (\hat{H}_0 + \hat{H}'(t))|\psi(t)\rangle$$

This is unwieldy: the perturbation $\hat{H}'(t)$ and the trivial evolution under $\hat{H}_0$ are entangled.

Define a new state vector by stripping out the $\hat{H}_0$ evolution:

$$|\tilde\psi(t)\rangle = e^{i\hat{H}_0 t/\hbar}\,|\psi(t)\rangle$$

This is the *interaction picture* state. Substitute and use the chain rule:

$$i\hbar\,\partial_t|\tilde\psi(t)\rangle = i\hbar(i\hat{H}_0/\hbar)|\tilde\psi\rangle + e^{i\hat{H}_0 t/\hbar}\,i\hbar\,\partial_t|\psi\rangle$$
$$= -\hat{H}_0|\tilde\psi\rangle + e^{i\hat{H}_0 t/\hbar}(\hat{H}_0 + \hat{H}'(t))|\psi(t)\rangle$$
$$= -\hat{H}_0|\tilde\psi\rangle + \hat{H}_0|\tilde\psi\rangle + e^{i\hat{H}_0 t/\hbar}\hat{H}'(t)e^{-i\hat{H}_0 t/\hbar}|\tilde\psi\rangle$$
$$= \tilde{H}'(t)\,|\tilde\psi(t)\rangle$$

where $\tilde{H}'(t) = e^{i\hat{H}_0 t/\hbar}\hat{H}'(t)e^{-i\hat{H}_0 t/\hbar}$. The interaction picture state evolves only under the perturbation. When $\hat{H}'(t) = 0$, $|\tilde\psi\rangle$ stops. All the dynamics is in the perturbation.

### 4.2 Expand in the unperturbed basis

The unperturbed eigenstates $\{|n\rangle\}$ form a basis. Expand:

$$|\tilde\psi(t)\rangle = \sum_n c_n(t)\,|n\rangle$$

Suppose the system starts in $|i\rangle$ at $t = 0$, so $c_n(0) = \delta_{ni}$. Project the interaction-picture Schrödinger equation onto $|f\rangle$:

$$i\hbar\,\dot{c}_f(t) = \sum_n c_n(t)\,\langle f|\tilde{H}'(t)|n\rangle = \sum_n c_n(t)\,\langle f|\hat{H}'(t)|n\rangle\,e^{i\omega_{fn} t}$$

where $\omega_{fn} = (E_f - E_n)/\hbar$ is the Bohr frequency between $|f\rangle$ and $|n\rangle$. So

$$\boxed{\dot{c}_f(t) = \frac{1}{i\hbar}\sum_n c_n(t)\,\langle f|\hat{H}'(t)|n\rangle\,e^{i\omega_{fn} t}}$$

This is exact. It is also coupled — every $c_f$ depends on every other $c_n$. Perturbation theory cuts the knot.

### 4.3 First-order solution

If $\hat{H}'$ is small, the coefficients change slowly. To leading order in $\hat{H}'$, replace $c_n(t)$ on the right-hand side by its initial value $\delta_{ni}$:

$$\dot{c}_f^{(1)}(t) = \frac{1}{i\hbar}\,\langle f|\hat{H}'(t)|i\rangle\,e^{i\omega_{fi} t}$$

Integrate from $0$ to $t$:

$$\boxed{c_f^{(1)}(t) = \frac{1}{i\hbar}\int_0^t \langle f|\hat{H}'(t')|i\rangle\,e^{i\omega_{fi} t'}\,dt'}$$

**Read this carefully.** The transition amplitude is the *Fourier component of the matrix element* $\langle f|\hat{H}'(t)|i\rangle$ at the Bohr frequency $\omega_{fi}$. Resonance is Fourier resonance. The system absorbs energy when the perturbation has spectral weight at the gap.

(Griffiths §11.1; Liboff §13.5.)

## 5. Concept block — the resonance lineshape

### 5.1 Monochromatic perturbation

Take $\hat{H}'(t) = \hat{V}\cos(\omega t) = (\hat{V}/2)(e^{i\omega t} + e^{-i\omega t})$. The first-order amplitude:

$$c_f^{(1)}(t) = \frac{V_{fi}}{2i\hbar}\int_0^t (e^{i\omega t'} + e^{-i\omega t'})e^{i\omega_{fi} t'}\,dt'$$

where $V_{fi} = \langle f|\hat{V}|i\rangle$. The two exponentials combine:

$$c_f^{(1)}(t) = \frac{V_{fi}}{2i\hbar}\left[\frac{e^{i(\omega_{fi}+\omega)t} - 1}{i(\omega_{fi}+\omega)} + \frac{e^{i(\omega_{fi}-\omega)t} - 1}{i(\omega_{fi}-\omega)}\right]$$

When $\omega \approx \omega_{fi}$ (the resonance condition, near the absorption peak), the second term has a near-vanishing denominator and dominates over the first. The first term oscillates rapidly and averages to a small effect. Dropping it is the *rotating-wave approximation* (RWA) — standard in this chapter, but with a name and a regime of validity. (Outside the RWA, the Bloch-Siegert shift and counter-rotating effects appear; relevant when $V/\hbar\omega_0$ is not small, e.g., in strong-field atomic physics or superconducting circuits driven hard.)

### 5.2 The $\sin^2/\Delta\omega^2$ profile

Keeping only the resonant term, the transition probability is

$$P_{i\to f}(t) = |c_f^{(1)}(t)|^2 = \frac{|V_{fi}|^2}{4\hbar^2}\cdot\frac{|e^{i(\omega_{fi}-\omega)t} - 1|^2}{(\omega_{fi}-\omega)^2}$$

Use $|e^{ix} - 1|^2 = 2(1 - \cos x) = 4\sin^2(x/2)$:

$$\boxed{P_{i\to f}(t) = \frac{|V_{fi}|^2}{\hbar^2}\cdot\frac{\sin^2[(\omega_{fi} - \omega)t/2]}{(\omega_{fi} - \omega)^2}}$$

This is the canonical resonance lineshape. As a function of $\Delta = \omega - \omega_{fi}$ at fixed $t$:

- Peak height at $\Delta = 0$: $|V_{fi}|^2 t^2/(4\hbar^2)$ — grows as $t^2$.
- Width (first zero): $\Delta = 2\pi/t$ — narrows as $1/t$.
- Area under the peak: $\sim |V_{fi}|^2 t/\hbar^2$ — grows linearly with $t$.

This is the signature of a delta function emerging in the long-time limit. Hold that thought; it is the input to Fermi's golden rule in §6.

A second feature is critical for what comes later. The peak-height growth as $t^2$ is *unphysical* at long times — the probability $P_{i\to f}$ cannot exceed 1, but the formula says it can. *This is the failure mode of first-order PT.* The exact Rabi solution we will see in §7 caps the probability at 1 (or less, off-resonance) by including the back-action of the populated $|f\rangle$ state on $|i\rangle$. PT misses that back-action. The simulation will let you watch the failure happen.

## 6. Concept block — Fermi's golden rule (which is Dirac's golden rule)

### 6.1 The continuum and the long-time limit

Most realistic problems are *not* two-level. An atom ionizing into the continuum, an electron scattering into a band of free-particle states, an excited atom decaying into the infinite continuum of electromagnetic modes — in every case the final state is part of a *continuum* with density of states $\rho(E_f)$ (number of states per unit energy near $E_f$). The right question is not "what is the probability of transitioning to one specific state?" but "what is the total rate of transitioning into any state in the continuum near $E_i + \hbar\omega$?"

Sum the $\sin^2/\Delta\omega^2$ formula over the continuum. The continuum density of final states near $E_f = E_i + \hbar\omega$ is $\rho(E_f)$, and we integrate:

$$P_{i\to\text{cont}}(t) = \int dE_f\,\rho(E_f)\,\frac{|V_{fi}|^2}{\hbar^2}\,\frac{\sin^2[(\omega_{fi} - \omega)t/2]}{(\omega_{fi} - \omega)^2}$$

For long $t$, the $\sin^2/\Delta\omega^2$ is a sharply peaked function of $\omega_{fi}$ centered at $\omega_{fi} = \omega$. The mathematical identity

$$\lim_{t\to\infty}\frac{\sin^2(\alpha t/2)}{\alpha^2} = \frac{\pi t}{2}\,\delta(\alpha)$$

(check: the area under the LHS as a function of $\alpha$ is $\pi t/2$, the height grows as $t^2/4$, the width shrinks as $4\pi/t$; in the limit a delta function emerges) gives, after substituting $\alpha = \omega_{fi} - \omega$ and converting $\delta(\omega_{fi} - \omega) = \hbar\,\delta(E_f - E_i - \hbar\omega)$:

$$P_{i\to\text{cont}}(t) = \frac{|V_{fi}|^2}{\hbar^2}\cdot\frac{\pi t}{2}\cdot 2\,\rho(E_f)\bigg|_{E_f = E_i + \hbar\omega}\cdot\hbar = \frac{\pi t}{\hbar}|V_{fi}|^2\rho(E_f)$$

Wait — the original $\cos\omega t = (e^{i\omega t} + e^{-i\omega t})/2$ contained a factor of $1/2$, and we kept only one term. Putting the factor of $|V_{fi}/2|^2 = |V_{fi}|^2/4$ in (so for a perturbation $\hat{H}' = \hat{V}\cos\omega t$):

$$P_{i\to\text{cont}}(t) = \frac{2\pi}{\hbar}|V_{fi}/2|^2\rho(E_f)\cdot t = \frac{\pi}{2\hbar}|V_{fi}|^2\rho(E_f)\cdot t$$

The probability per unit time is the **transition rate**:

$$\boxed{W_{i\to f} = \frac{2\pi}{\hbar}\,|\langle f|\hat{H}'|i\rangle|^2\,\rho(E_f)}$$

(where $\hat{H}'$ here refers to the *amplitude* of the perturbation, with the rotating-wave-approximation factor absorbed; conventions vary across textbooks — see Griffiths §11.3 for the canonical statement.)

This is **Fermi's golden rule**. It is one of the most used formulas in all of atomic, molecular, condensed-matter, and nuclear physics.

### 6.2 The historical correction

The formula is named after Enrico Fermi. Fermi did *not* derive it. Fermi wrote, in his Chicago lecture notes compiled by Orear, Rosenfeld, and Schluter (*Nuclear Physics: A Course Given by Enrico Fermi at the University of Chicago*, 1950), that this expression was so useful in nuclear physics that he called it "Golden Rule No. 2." The name stuck.

The actual derivation appeared in 1927, when Fermi was a 25-year-old reader at Florence. P.A.M. Dirac, then 25 himself, published "[The Quantum Theory of the Emission and Absorption of Radiation](https://royalsocietypublishing.org/doi/10.1098/rspa.1927.0039)" in *Proc. R. Soc. London A* 114, 243 (1927). The paper carried out exactly the calculation above: time-dependent perturbation theory applied to a charged particle in an electromagnetic field, the long-time limit, the delta-function emergence, the $2\pi/\hbar$ prefactor. Dirac's paper is the foundational document of quantum electrodynamics. The "golden rule" — the rate formula for transitions into a continuum — appears explicitly in it.

Fermi knew Dirac's paper. Naming the result after himself was not theft; it was a teaching shorthand that propagated through generations of nuclear physics textbooks. By the time the name had stuck, the misattribution was hard to reverse.

This chapter calls it "Fermi's golden rule" because no one will know what you mean if you call it anything else. But you should know what happened, and you should know that the historical record matters. Naming a thing after the wrong person is a small example of how scientific communities flatten the record. Feynman would have called it out. So this chapter does.

### 6.3 Where Fermi's golden rule applies and where it does not

Three conditions need to hold:

1. *Continuum of final states.* If the final states are discrete (two-level atom, isolated bound states), the delta-function step fails. The exact $\sin^2/\Delta\omega^2$ profile applies, not Fermi's rate. The chapter's simulation will show you this directly: drive a two-level system and the population *Rabi-oscillates*, it does not grow linearly in time as Fermi's rate would predict.

2. *Long times compared to $1/\Delta\omega$.* You need enough time for the sinc² to look like a delta function. Short pulses ($t \lesssim 1/\omega_{fi}$) produce broadened lineshapes, not sharp resonances.

3. *Short times compared to $1/(V_{fi}/\hbar)$.* Otherwise the probability $W_{i\to f}\cdot t$ becomes comparable to 1 and PT fails (in either direction — see the saturation in §7).

When all three conditions hold — atomic absorption into the infinite electromagnetic continuum, nuclear beta decay into the continuum of electron-neutrino phase-space momenta (Fermi's original 1934 application; [Fermi, "Versuch einer Theorie der β-Strahlen," *Z. Phys.* 88, 161, 1934](https://link.springer.com/article/10.1007/BF01351864)), photoionization into the electron continuum — Fermi's golden rule is the workhorse.

## 7. Concept block — exact Rabi oscillations

### 7.1 The two-level driven problem

Two states $|g\rangle$ (ground) and $|e\rangle$ (excited) with energies $E_g = 0$ and $E_e = \hbar\omega_0$. Drive with $\hat{H}'(t) = \hbar\Omega\cos(\omega t)(|e\rangle\langle g| + |g\rangle\langle e|)$. (The coupling $\Omega$ is the *Rabi frequency*; physically it is $|V_{fi}|/\hbar$.)

Expand the state as $|\psi(t)\rangle = c_g(t)|g\rangle + c_e(t)e^{-i\omega_0 t}|e\rangle$. Substitute into the Schrödinger equation, apply RWA, and you get a pair of coupled first-order ODEs in $c_g$ and $c_e$. The exact solution (with initial conditions $c_g(0)=1$, $c_e(0)=0$):

$$\boxed{P_{g\to e}(t) = |c_e(t)|^2 = \frac{\Omega^2}{\Omega^2 + \Delta^2}\,\sin^2\!\left(\frac{\sqrt{\Omega^2 + \Delta^2}}{2}\,t\right)}$$

with $\Delta = \omega - \omega_0$ the detuning. (Griffiths §11.1.2; Liboff §13.7 [verify].)

### 7.2 What this formula says

At resonance ($\Delta = 0$):

$$P_{g\to e}(t) = \sin^2\!\left(\frac{\Omega t}{2}\right)$$

The population oscillates fully between $0$ and $1$. At $t = \pi/\Omega$ (a "$\pi$-pulse"), the population is *entirely* in the excited state. At $t = 2\pi/\Omega$, it is back in the ground state. The energy sloshes between drive and atom indefinitely.

Off-resonance ($\Delta \neq 0$):

- The maximum probability is $\Omega^2/(\Omega^2 + \Delta^2) < 1$. *Full transfer is impossible off-resonance.*
- The oscillation frequency is $\sqrt{\Omega^2 + \Delta^2}$ — the *generalized Rabi frequency*. Faster than $\Omega$ but capped in amplitude.

This is the exact answer. No truncation, no PT, no approximation beyond the RWA.

### 7.3 PT vs. exact, in two regimes

Compare the exact Rabi formula to the first-order PT prediction for the same problem. At resonance:

- Exact: $P_{g\to e}^{\text{exact}}(t) = \sin^2(\Omega t/2)$, bounded by 1.
- PT: $P_{g\to e}^{\text{PT}}(t) = (\Omega t/2)^2$, unbounded.

The two agree for $\Omega t \ll 1$ (Taylor-expand $\sin^2 x \approx x^2$). They disagree dramatically for $\Omega t \sim 1$. **The simulation will let you slide $t$ out from zero and watch the PT prediction cross 1 — at which point you know with certainty that PT has failed.**

This is the signature pedagogical move of the chapter. Perturbation theory is a tool; the tool has a domain of validity; outside that domain you need the exact solution (or the right resummation, or a different framework — open-system master equations, full numerical integration, etc.).

## 8. Concept block — selection rules and dipole transitions

### 8.1 The dipole approximation

For an atom in a weak optical field $\vec{\mathcal{E}}(t) = \vec{\mathcal{E}}_0\cos(\omega t)$, the perturbation is

$$\hat{H}'(t) = -\hat{\vec{p}}\cdot\vec{\mathcal{E}}(t) = -(-e\hat{\vec{r}})\cdot\vec{\mathcal{E}}(t) = e\hat{\vec{r}}\cdot\vec{\mathcal{E}}_0\cos(\omega t)$$

The matrix element $\langle f|\hat{\vec{r}}|i\rangle$ controls the transition. *When it vanishes by symmetry, the transition is forbidden* (in the dipole approximation).

### 8.2 The selection rules for hydrogen

For hydrogenic states $|n\ell m\rangle$, the angular integrals (computed using spherical harmonics; Liboff §10) give:

- $\langle n'\ell' m'|\hat{z}|n\ell m\rangle \neq 0$ requires $\Delta\ell = \pm 1$ and $\Delta m = 0$.
- $\langle n'\ell' m'|\hat{x} \pm i\hat{y}|n\ell m\rangle \neq 0$ requires $\Delta\ell = \pm 1$ and $\Delta m = \pm 1$.

So *electric dipole transitions* in hydrogen require $\Delta\ell = \pm 1$. The transition $1s \to 2s$ is forbidden ($\Delta\ell = 0$); $1s \to 2p$ is allowed. The selection rule on $m$ depends on photon polarization: linear $\hat{z}$-polarized light drives $\Delta m = 0$; circularly polarized light drives $\Delta m = \pm 1$.

Spin does not enter the electric dipole operator, so $\Delta s = 0$ at this order — the electron's spin does not flip in an electric dipole transition. (Magnetic dipole and electric quadrupole transitions can flip spin, but they are weaker by factors of $\alpha^2$ and rarely matter in atomic spectra unless the dipole is forbidden.)

### 8.3 Worked example — why $1s \to 2s$ is forbidden

Compute $\langle 2s|\hat{z}|1s\rangle$. Both $|1s\rangle$ and $|2s\rangle$ are spherically symmetric (parity-even). The operator $\hat{z}$ is parity-odd. The integral of a parity-odd function over all space is zero. So $\langle 2s|\hat{z}|1s\rangle = 0$.

By the same parity argument, $\langle 2s|\hat{x}|1s\rangle = \langle 2s|\hat{y}|1s\rangle = 0$. The matrix element of *any* component of $\hat{\vec{r}}$ between two parity-even states is zero. *Forbidden* is not a recipe; it is a calculation that returns zero.

Now compute $\langle 2p_0|\hat{z}|1s\rangle$. The radial wave function of $2p_0$ contains $r$, the angular part is $\cos\theta$. The radial integral $\int r^3 R_{2p}^* R_{1s}\,dr$ is nonzero. The angular integral $\int \cos^2\theta\,d\Omega$ is also nonzero (it equals $4\pi/3$). The transition is *allowed*. Direct calculation in Griffiths Example 11.1 gives a specific number; the point here is that *the selection rule emerges as the absence of vanishing factors*, not as an axiomatic rule.

## 9. Worked examples and exercises

### Worked example — hydrogen 2p $\to$ 1s lifetime

Einstein's argument (1916/1917) related the spontaneous emission rate $A_{21}$ and the stimulated emission rate $B_{21}$ via thermodynamic equilibrium with blackbody radiation:

$$\frac{A_{21}}{B_{21}} = \frac{8\pi h\nu^3}{c^3}$$

(Einstein, "Zur Quantentheorie der Strahlung," *Physikalische Zeitschrift* 18, 121, 1917 [verify]). Without quantizing the field, Einstein got the ratio. Quantization comes later (Dirac 1927); the upshot for hydrogen is

$$A_{2p\to 1s} = \frac{e^2\omega_{21}^3}{3\pi\epsilon_0\hbar c^3}\,|\langle 1s|\hat{\vec{r}}|2p\rangle|^2$$

Computing $|\langle 1s|\hat{\vec{r}}|2p\rangle|^2 \approx 0.555\,a_0^2$ [verify against Griffiths Example 11.5] and plugging in $\omega_{21} = (3/4)\,\text{Ry}/\hbar$, you get

$$A_{2p\to 1s} \approx 6.27 \times 10^8\,\text{s}^{-1}$$

The lifetime is $\tau = 1/A \approx 1.6$ ns [verify against NIST atomic spectra database]. This is the number every introductory spectroscopist learns. The atom sits in $|2p\rangle$ for about a nanosecond before emitting a Lyman-$\alpha$ photon at 121.6 nm.

### Exercises

**Warm-up.**

1. Derive the rotating-wave approximation explicitly. Starting from $\hat{H}'(t) = \hat{V}\cos\omega t$, split into $e^{+i\omega t}$ and $e^{-i\omega t}$ terms. Near $\omega = \omega_{fi}$, argue which term is resonant and which is counter-rotating. State precisely the condition (involving $\omega, \omega_{fi}, V/\hbar$) under which the RWA is valid.

2. The $\sin^2/\Delta\omega^2$ profile: compute the height, width (first zero), and area under the central peak at fixed time $t$. Verify the limiting behavior as $t \to \infty$ gives a delta function.

3. State the dipole selection rules for hydrogen and explain in one sentence each why they hold (parity, angular-momentum addition, spin orthogonality).

**Application.**

4. A two-level system with $\omega_0 = 2\pi\times 5\,\text{GHz}$ is driven at resonance with Rabi frequency $\Omega = 2\pi\times 10\,\text{MHz}$ (typical superconducting-qubit parameters). What is the duration of a $\pi$-pulse? What about a $\pi/2$-pulse? Calculate.

5. Compute $\langle 2p_0|\hat{z}|1s\rangle$ in atomic units, using the explicit radial and angular forms of $R_{1s}$, $R_{2p}$, and the spherical harmonics. Check that your answer matches Griffiths Example 11.5.

6. The 21-cm hydrogen line — the transition between the two hyperfine levels of the $1s$ ground state — is a magnetic dipole transition. By the electric dipole selection rules, the transition has $\Delta\ell = 0$, which is *forbidden* in the dipole approximation. The lifetime is about $10^7$ years. Without computing the magnetic dipole matrix element, explain why dipole-forbidden transitions have such long lifetimes and why the 21-cm line nonetheless illuminates radio astronomy.

**Synthesis.**

7. Apply Fermi's golden rule to compute the photoionization rate of hydrogen from the $1s$ state by light of frequency $\omega > \omega_{\text{ion}} = 13.6\,\text{eV}/\hbar$. Take the final state as a plane wave with momentum $\hbar\vec{k}$. The density of states is $\rho(E_f) = (V m/\hbar^2)k\cdot\text{angular factor}/(2\pi)^3$. Identify the matrix element $\langle\vec{k}|\hat{z}|1s\rangle$, plug in, and find the photoionization cross-section's dependence on $\omega$.

8. Show that off-resonance, the maximum exact Rabi probability is $\Omega^2/(\Omega^2 + \Delta^2)$. Compare to the first-order PT prediction at the same $t$ and $\Delta$. For what range of $\Omega t$ do PT and exact agree to 10%?

**Challenge.**

9. *Dirac vs. Fermi.* Read the first two pages of Dirac's 1927 paper "The Quantum Theory of the Emission and Absorption of Radiation," *Proc. R. Soc. A* 114, 243. Identify the equation that is now called Fermi's golden rule. Note the year and the page number. Write a one-paragraph reflection on what it means for a foundational formula to be named after the wrong person, and what the cost is to scientific literacy when this happens.

10. The Bloch-Siegert shift. The full (no-RWA) two-level problem with $\hat{H}'(t) = \hbar\Omega\cos(\omega t)$ has, at resonance, a shifted effective Rabi frequency $\Omega_{\text{eff}} = \Omega + \Omega^2/(4\omega_0) + \cdots$ The first correction is the Bloch-Siegert shift. Estimate its size for a typical NMR experiment ($\omega_0 \sim 2\pi\times 500\,\text{MHz}$, $\Omega \sim 2\pi\times 10\,\text{kHz}$). Argue why the RWA is essentially exact for NMR but not for hard-driven superconducting qubits where $\Omega/\omega_0 \sim 0.1$.

## 10. What would change my mind

The framework rests on the validity of perturbation theory in the weak-coupling regime and on the rotating-wave approximation in the near-resonance regime. The most stringent tests are in QED — the electron $g$-factor agrees with QED prediction to better than ten significant figures, and the Lamb shift is reproduced to four significant figures. If a precision NMR or qubit experiment were performed in the regime where RWA is *expected* to hold ($V_{fi}/\hbar\omega_0 \ll 1$, long times in the continuum sense) and the measured transition rate disagreed with Fermi's golden rule by more than the experimental uncertainty, that would be a problem. Existing data shows the formalism is in remarkably good shape.

What would *modify* the framework is operating outside its conditions — strong driving (Bloch-Siegert), short pulses (sinc² lineshape), discrete final states (Rabi oscillations rather than golden-rule rates). The framework already accommodates these; the chapter named the conditions and pointed at where to go when they fail.

## 11. Still puzzling

Spontaneous emission. With the perturbation theory of this chapter, the excited atomic eigenstate $|e\rangle$ has *no* time-dependent perturbation acting on it — it is an eigenstate of $\hat{H}_0$, and it should sit there forever. Yet excited atoms decay. The reason is that the *electromagnetic field* is itself a quantum object with its own ground-state fluctuations; coupling the atom to the *quantized* vacuum field gives a non-trivial perturbation even when no classical field is applied. Einstein's $A$-coefficient comes out of this calculation; this chapter handed it to you via Einstein's thermodynamic argument, but the underlying mechanism is field quantization.

The framework of this chapter is *semi*-classical. It treats atomic states quantum mechanically and the electromagnetic field classically. Spontaneous emission marks the edge of where that approximation can take you. The full story — quantum electrodynamics — is a graduate course. I cannot derive the $A$-coefficient from first principles within this chapter. The chapter shows you where the wall is, and points at the gate.

## 12. LLM Exercise — the Rabi resonance simulator

You are going to build a single-file D3 simulation that shows time-dependent perturbation theory at work and at its breaking point. Three nested panels: population vs. time at fixed detuning, transition probability vs. detuning at fixed time, and a continuum-to-golden-rule toggle. The deliverable is `10-rabi-resonance.html` in your working directory.

### Part 1 — Update `PROJECT.md`

```
Append a new entry to PROJECT.md describing this chapter's simulation:

Chapter 10 — Time-Dependent Perturbation Theory and Transitions
Deliverable: 10-rabi-resonance.html
Status: in progress

The simulation displays a driven two-level system with three nested panels:

Panel A — Population vs. time at fixed detuning.
On a single plot, two lines for P_{g->e}(t):
  - Exact Rabi formula (solid black): P = (Omega^2 / (Omega^2 + Delta^2))
    * sin^2(sqrt(Omega^2 + Delta^2) t / 2)
  - First-order PT (dashed teal): P = (Omega t / 2)^2 at resonance,
    sinc^2 lineshape integrated to fixed t off resonance.
Watch them agree at short times and diverge at long times.

Panel B — Transition probability vs. detuning at fixed time.
On a single plot, P_{g->e}(Delta) at chosen t.
  - Exact (solid black): the saturating Lorentzian-like shape.
  - PT (dashed teal): the sinc^2 profile with central peak and sidelobes.
At short t the two agree everywhere; at long t the PT sidelobes are
artifacts.

Panel C — Fermi's golden rule regime (toggle).
Replace the single |e> with a band of N equally spaced excited states
covering an energy range +/- Delta_band around E_e. Plot the total
P_total(t) = sum over band states of |c_n(t)|^2 vs. time. After a
transient of duration ~ 2 pi / Delta_band, the total population grows
LINEARLY in t with slope equal to the Fermi golden rule rate
W = (2 pi / hbar) |V|^2 rho. Mark the slope on the plot.

Controls:
- Bare Rabi frequency Omega (0 to 0.5 omega_0)
- Detuning Delta = omega - omega_0 (range +/- 5 Omega)
- Time t (range 0 to a few generalized-Rabi periods)
- Toggle: show PT, show exact, show both
- Toggle: two-level mode (Panels A, B) vs. continuum mode (Panel C)
- For continuum mode: number of band states N (5 to 50), band width
  Delta_band

Time axis scales as 1 / Omega for the two-level mode (so a Rabi period
is always visible) and 1 / Delta_band for the continuum mode (so the
transient is visible).
```

### Part 2 — The CLAUDE.md amendment

```
Append to CLAUDE.md the following physics rules for Chapter 10 simulations:

TIME-DEPENDENT PERTURBATION-THEORY PHYSICS RULES

1. TWO-LEVEL EXACT RABI. For initial state |g> and drive
   H' = hbar Omega cos(omega t) (|e><g| + |g><e|), in the RWA:
     P_{g->e}(t) = (Omega^2 / Omega_gen^2) * sin^2(Omega_gen t / 2)
   where Omega_gen = sqrt(Omega^2 + Delta^2) and Delta = omega - omega_0.
   This formula is exact; no PT approximation.

2. FIRST-ORDER PT for the same problem (RWA, keeping only the resonant
   exponential):
     P_PT(t) = |Omega/2|^2 * |1 - exp(i Delta t)|^2 / Delta^2
           = (Omega^2 / Delta^2) * sin^2(Delta t / 2)
   At resonance (Delta = 0), use the limit: P_PT(t) = (Omega t / 2)^2.
   Note: this can exceed 1 and is unphysical at long times.

3. NORMALIZATION CHECK. The exact formula obeys 0 <= P_{g->e}(t) <= 1
   always. The PT formula does not. When PT predicts P > 1, display
   a warning "PT NO LONGER VALID — population overflow" in red.

4. CONTINUUM MODE. Replace the single |e> with N equally spaced excited
   states |e_k> at energies E_e + k * dE_band, k = -N/2..N/2. Assume
   each has the same |V_k|^2 = |V|^2 / N (so the matrix element times
   density of states is preserved as the band fills out). For each
   band state, compute c_k(t) by first-order PT individually:
     c_k(t) = (V/(2 i hbar)) * (1 - exp(i (omega_k - omega) t)) / (omega_k - omega)
   Sum |c_k(t)|^2 over the band. This is P_total(t).

5. FERMI GOLDEN RULE PREDICTION. The slope of P_total(t) at long times
   (t >> 2 pi / Delta_band) should match
     W = (2 pi / hbar) * |V|^2 * rho(E)
   where rho(E) = N / (Delta_band * hbar) = number of states per unit
   energy in the band. Display this predicted slope as a dashed reference
   line on Panel C.

6. UNITS. hbar = 1, omega_0 = 1. Rabi frequency Omega is dimensionless
   (in units of omega_0). Detuning Delta is in the same units. Time
   axis is in units of 2 pi / Omega for the two-level panels and
   2 pi / Delta_band for the continuum panel.

KNOWN FAILURE MODES:
(a) PT formula divergence at Delta = 0. Use a small-Delta Taylor
    expansion or evaluate sin(Delta t / 2)/Delta as t/2 in the limit.
(b) Sign of detuning. Be consistent: Delta = omega - omega_0 (drive
    above resonance is positive).
(c) For the continuum, summing too few band states (N < 10) leaves
    visible spikes; N >= 20 is recommended.
(d) Time axis pinned to a fixed range when Omega changes — the Rabi
    period scales as 1/Omega, so the axis should rescale.
(e) Forgetting the 1/2 in cos(omega t) = (e^{i omega t} + e^{-i omega t})/2
    when comparing the exact RWA formula to PT.
```

### Part 3 — The simulation prompt

```
You are working in my directory which contains CLAUDE.md, DESIGN.md, and
PROJECT.md. Read all three first.

Build 10-rabi-resonance.html: a single self-contained HTML file using
D3 v7 from a CDN and d3-simple-slider. No other dependencies. The
simulation has two modes selectable by tabs at the top: "Two-level"
and "Continuum (Fermi)".

TWO-LEVEL MODE
Single SVG canvas 1100 x 600 split into two panels:

Panel A (left, 550 wide): P_{g->e} vs. time. X-axis: time t in units
of 2 pi / Omega, range 0 to 4 (so up to four Rabi periods at resonance).
Y-axis: probability 0 to 1.2 (so the PT formula's overflow is visible).
Two curves:
  - Exact (solid black): the Rabi formula
  - PT (dashed teal): the first-order amplitude squared
Vertical reference line at t = 1 / Omega (one bare Rabi period) and at
t = 2 / Omega (two periods). Annotation: "PT valid for Omega t << 1"
above the t-axis near zero.

Panel B (right, 550 wide): P_{g->e}(Delta) at fixed time T_fixed.
X-axis: Delta from -5 Omega to +5 Omega. Y-axis: 0 to 1.2.
Two curves:
  - Exact (solid black): the saturating shape
  - PT (dashed teal): sinc^2(Delta T_fixed / 2) * (Omega T_fixed / 2)^2
Slider for T_fixed (range 0.5 / Omega to 5 / Omega). As T_fixed
increases, watch the exact curve saturate while the PT central peak
sharpens and the sidelobes become visible.

Controls (two-level mode):
- Omega slider, range 0.01 to 0.5 omega_0, default 0.1
- Delta slider for Panel A, range -5 Omega to +5 Omega, default 0
- T_fixed slider for Panel B, range 0.5 / Omega to 5 / Omega, default 1 / Omega

CONTINUUM MODE
Single SVG canvas 1100 x 600 with one main panel (Panel C):
P_total(t) vs. time. X-axis: time in units of 2 pi / Delta_band.
Y-axis: probability 0 to 1. Two curves:
  - Sum of |c_k(t)|^2 from explicit summation over N band states (solid black)
  - Linear reference: W * t with W = 2 pi |V|^2 rho (dashed orange)
Watch the explicit sum agree with the linear reference after the
transient (~ 1 unit of 2 pi / Delta_band).

Controls (continuum mode):
- N slider (number of band states), range 5 to 50, default 20
- Delta_band slider (band width), range 0.1 to 2 omega_0, default 0.5
- |V| slider, range 0 to 0.2 hbar omega_0, default 0.05

GLOBAL
Real-time response to slider changes (< 50 ms render time). For the
continuum mode, vectorize the c_k(t) computation over the band — this
is a single matrix multiply.

Runtime sanity checks to console:
- At Omega t = 0, both exact and PT should give P = 0.
- At Omega t = 0.1 (resonance), exact and PT should agree to within 1%.
- At Omega t = pi (resonance), exact = 1 and PT = (pi/2)^2 ~= 2.47;
  the warning should be triggered.
- Continuum mode: at t = 5 * 2 pi / Delta_band, P_total / t should
  equal W within 5%.

Comments at every non-trivial physics step. Pure functions for the
Rabi formula and the band sum.
```

### Part 4 — Exploration tasks and extension prompt

Run the simulation and answer the following:

1. Two-level mode, Panel A, at resonance ($\Delta = 0$). Set $\Omega = 0.1\,\omega_0$. Watch the exact and PT curves agree initially. At what value of $\Omega t$ do they first differ by 10%? At what value does the PT prediction cross 1? Record both.

2. Two-level mode, Panel B. Set $T_{\text{fixed}} = 1/\Omega$. Note that the exact curve has a narrow central peak and no sidelobes; the PT curve has sidelobes. Increase $T_{\text{fixed}}$ to $5/\Omega$. The exact curve saturates; the PT curve sharpens. Explain in your own words what physical effect the saturation represents.

3. Two-level mode, off-resonance. Set $\Delta = 2\Omega$, $\Omega = 0.1\,\omega_0$. Slide time out. The exact curve oscillates with smaller amplitude and faster frequency. Read off the maximum probability and compare to $\Omega^2/(\Omega^2 + \Delta^2) = 1/5$. The simulation should confirm.

4. Continuum mode. Set $N = 5$, $\Delta_{\text{band}} = 0.5\,\omega_0$. Watch $P_{\text{total}}(t)$. You should see oscillatory behavior — the band is too discrete to look like a continuum. Increase $N$ to $20$, then $50$. The oscillations smooth into a linear ramp matching the Fermi prediction (dashed orange line).

5. Continuum mode. With $N = 50$ band states, decrease $|V|$ from $0.05$ to $0.01$. The slope of $P_{\text{total}}(t)$ should drop by a factor of 25 ($W \propto |V|^2$). Verify.

**Extension prompt:**

```
Modify 10-rabi-resonance.html to add a Bloch-sphere visualization panel
for the two-level mode. The two-level state |psi(t)> = c_g |g> +
c_e exp(-i omega_0 t) |e> maps to a point on the unit sphere via
  x = 2 Re(c_g^* c_e exp(-i omega_0 t))
  y = 2 Im(c_g^* c_e exp(-i omega_0 t))
  z = |c_g|^2 - |c_e|^2
Plot this point in a 3D-projected view (use orthographic projection
or simple perspective; do NOT use a 3D library — just compute and
project to 2D).

At resonance, the Bloch vector rotates around the x-axis (or y-axis,
depending on phase convention) at frequency Omega. Off-resonance, the
rotation axis tilts. The trajectory is a circle for the exact solution.

For the PT solution, the Bloch vector traces a small arc near the
south pole that grows without bound — visualize this overshoot
explicitly as the PT trajectory leaving the sphere.

Update PROJECT.md to mark Chapter 10 as complete and note the Bloch-
sphere extension as the bridge to Chapter 11 (where another approximation
method — WKB — handles a different regime).
```

---

*Sources consulted: Griffiths §11.1–11.3 (time-dependent perturbation theory, Fermi's golden rule, electromagnetic transitions); Liboff §13.5–13.7 (time-dependent perturbation theory, harmonic perturbation, transition rates); Dirac, "[The Quantum Theory of the Emission and Absorption of Radiation](https://royalsocietypublishing.org/doi/10.1098/rspa.1927.0039)," *Proc. R. Soc. London A* 114, 243 (1927) — the actual origin of the formula now called Fermi's golden rule; Fermi, *Nuclear Physics: A Course Given by Enrico Fermi at the University of Chicago*, compiled by Orear, Rosenfeld & Schluter (Chicago, 1950) — the lecture notes where "Golden Rule No. 2" was coined; Einstein, "Zur Quantentheorie der Strahlung," *Physikalische Zeitschrift* 18, 121 (1917) [verify]; Rabi, Zacharias, Millman & Kusch, "[A new method of measuring nuclear magnetic moment](https://journals.aps.org/pr/abstract/10.1103/PhysRev.53.318)," *Phys. Rev.* 53, 318 (1938); Fermi, "Versuch einer Theorie der β-Strahlen," *Z. Phys.* 88, 161 (1934).*

*Tags: time-dependent-perturbation-theory, fermi-golden-rule, dirac-1927, rabi-oscillations, selection-rules, einstein-coefficients, d3-simulation*

*Status: draft for Nik's review. Historical correction on the "Fermi's golden rule" misattribution made explicit in §6.2 per pantry guidance. Several `[verify]` flags throughout — see specifically Einstein 1917 citation, hydrogen $2p$ lifetime against NIST, dipole matrix element prefactor.*
