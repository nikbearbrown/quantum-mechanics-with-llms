# Chapter 10 — Time-Dependent Perturbation Theory and Transitions
*The system absorbs when the perturbation has spectral weight at the gap.*

Here is the question this chapter answers. The atom is in its ground state. An oscillating field turns on. At some later time $t$, you measure the atom. What is the probability of finding it in the excited state?

That question sounds narrow. It is not. It is the question behind every absorption spectrum, every fluorescence measurement, every NMR pulse, every laser cooling experiment, every qubit gate, every photoionization cross-section in atomic and nuclear physics. It is the most applied calculation in the second half of an undergraduate quantum mechanics course. The answer, as we will see, is a Fourier integral — and resonance is Fourier resonance. The system responds when the perturbation has spectral weight at the gap frequency. Everything else in the chapter — the lineshape, Fermi's golden rule, the exact Rabi solution — is that one idea developed in different directions.

---

## The interaction picture

Chapter 9 handled perturbations that sit still. The strategy there was to correct the energy levels. Here the perturbation $\hat{H}'(t)$ oscillates or switches on, and the question is not about levels but about *transitions*: given that we start in $|i\rangle$, how does probability leak into $|f\rangle$?

The Schrödinger equation for the full Hamiltonian $\hat{H}_0 + \hat{H}'(t)$ mixes something we understand (the $\hat{H}_0$ eigenstates) with something we are treating as small ($\hat{H}'$). The trick is to remove the trivial part. Define the **interaction picture** state vector by stripping out the $\hat{H}_0$ evolution:

$$|\tilde\psi(t)\rangle = e^{i\hat{H}_0 t/\hbar}\,|\psi(t)\rangle.$$

Substitute into the Schrödinger equation and the $\hat{H}_0$ terms cancel exactly. What remains:

$$i\hbar\,\partial_t|\tilde\psi(t)\rangle = \tilde{H}'(t)\,|\tilde\psi(t)\rangle,$$

where $\tilde{H}'(t) = e^{i\hat{H}_0 t/\hbar}\hat{H}'(t)e^{-i\hat{H}_0 t/\hbar}$. The interaction picture state evolves *only* under the perturbation. When $\hat{H}'(t) = 0$, $|\tilde\psi\rangle$ freezes. All the dynamics is in the perturbation — which is exactly where we want to look.

Expand in the unperturbed eigenstates: $|\tilde\psi(t)\rangle = \sum_n c_n(t)\,|n\rangle$, with initial conditions $c_n(0) = \delta_{ni}$ (start in $|i\rangle$). Project onto $|f\rangle$:

$$i\hbar\,\dot{c}_f(t) = \sum_n c_n(t)\,\langle f|\hat{H}'(t)|n\rangle\,e^{i\omega_{fn} t},$$

where $\omega_{fn} = (E_f - E_n)/\hbar$. This is exact and coupled — every $c_f$ depends on every $c_n$.

Perturbation theory cuts the coupling. If $\hat{H}'$ is small, the coefficients move slowly. Replace $c_n(t)$ on the right-hand side by its initial value $\delta_{ni}$ and integrate:

$$\boxed{c_f^{(1)}(t) = \frac{1}{i\hbar}\int_0^t \langle f|\hat{H}'(t')|i\rangle\,e^{i\omega_{fi} t'}\,dt'.}$$

Read this carefully. The transition amplitude is the **Fourier component of the matrix element** $\langle f|\hat{H}'(t)|i\rangle$ evaluated at the Bohr frequency $\omega_{fi} = (E_f - E_i)/\hbar$. That is the whole content of first-order perturbation theory. Resonance is Fourier resonance: the system responds when the perturbation oscillates at the frequency of the gap.

---

## The resonance lineshape

Now specialize to a monochromatic perturbation: $\hat{H}'(t) = \hat{V}\cos(\omega t) = (\hat{V}/2)(e^{i\omega t} + e^{-i\omega t})$. Substituting into the first-order amplitude produces two terms — one with $e^{i(\omega_{fi}+\omega)t}$ and one with $e^{i(\omega_{fi}-\omega)t}$. Near resonance, where $\omega \approx \omega_{fi}$, the second term has a nearly vanishing denominator and dominates. The first oscillates rapidly and averages away. Dropping it is the **rotating-wave approximation** (RWA), valid when $V_{fi}/\hbar\omega_0 \ll 1$ — the coupling is much smaller than the transition frequency.

Keeping only the resonant term and squaring:

$$\boxed{P_{i\to f}(t) = \frac{|V_{fi}|^2}{\hbar^2}\cdot\frac{\sin^2[(\omega_{fi} - \omega)t/2]}{(\omega_{fi} - \omega)^2}.}$$

This is the canonical resonance lineshape. Look at what it says as a function of $\Delta = \omega - \omega_{fi}$ at fixed $t$: the peak sits at $\Delta = 0$ with height $|V_{fi}|^2 t^2/(4\hbar^2)$, the width to the first zero is $\Delta = 2\pi/t$, and the area under the central peak grows as $|V_{fi}|^2 t/\hbar^2$. Peak height grows as $t^2$; width shrinks as $1/t$; area grows as $t$. The $\sin^2/\Delta^2$ profile is narrowing and sharpening, preserving area — it is a proto-delta-function.

One feature of this lineshape must be flagged immediately. The peak height grows as $t^2$ without bound. But a probability cannot exceed 1. The $\sin^2/\Delta^2$ formula will eventually predict $P > 1$ at resonance — which is nonsense. This is not a minor technical failure; it is the signal that first-order perturbation theory has exited its regime of validity. What is missing is the back-action: as probability flows into $|f\rangle$, it must stop coming from $|i\rangle$, and the first-order calculation ignores that coupling. The exact Rabi solution corrects it.

---

## Fermi's golden rule, which is Dirac's

When the final state is part of a continuum — an electron ionizing into free-particle states, an atom emitting into the infinite bath of electromagnetic modes, a nucleus decaying into a phase-space continuum of daughter products — the right question changes. Instead of "what is the probability of landing in a specific state $|f\rangle$?", we ask "what is the total rate of transition into any state in the continuum near energy $E_f$?"

Sum the $\sin^2/\Delta^2$ profile over the continuum. The density of final states is $\rho(E_f)$ — states per unit energy near $E_f$. Integrate over energy, using the mathematical identity that for large $t$:

$$\frac{\sin^2(\alpha t/2)}{\alpha^2} \longrightarrow \frac{\pi t}{2}\,\delta(\alpha).$$

The integral collapses. The probability grows linearly in $t$, which means the *transition rate* — probability per unit time — is constant:

$$\boxed{W_{i\to f} = \frac{2\pi}{\hbar}\,|\langle f|\hat{H}'|i\rangle|^2\,\rho(E_f).}$$

This is **Fermi's golden rule**. One of the most used formulas in atomic, molecular, condensed-matter, and nuclear physics.

It is also Dirac's formula. P.A.M. Dirac derived it in 1927, in "The Quantum Theory of the Emission and Absorption of Radiation," *Proc. R. Soc. London A* 114, 243. Dirac was 25. The paper is the foundational document of quantum electrodynamics. The rate formula — the $2\pi/\hbar$ prefactor, the matrix element squared, the density of states — is in it explicitly.

Fermi did not derive it. Fermi applied it to nuclear beta decay in 1934 and called it "Golden Rule No. 2" in Chicago lecture notes compiled in 1950. The name stuck. Naming the result after himself was not theft; it was a teaching shorthand that propagated through generations of nuclear physics textbooks until the misattribution had calcified.

This chapter calls it Fermi's golden rule because no one will know what you mean if you call it anything else. But you should know what happened. When a community names a formula after the popularizer rather than the discoverer, it flattens the historical record in a way that is almost impossible to reverse. Dirac's 1927 paper deserves the credit. Read it — it is short, clear, and available.

Three conditions must hold for the golden rule to apply. First, a true continuum of final states — or enough closely spaced discrete states that the sum looks like an integral. Second, long enough time that the $\sin^2/\Delta^2$ has sharpened into something indistinguishable from a delta function: $t \gg 1/\Delta\omega$. Third, short enough time that the total probability $W_{i\to f}\cdot t$ is still small compared to 1, so that perturbation theory is valid. All three conditions fail in different experiments. When the final states are discrete, the exact Rabi formula applies. When times are long enough that the rate prediction saturates, neither formula applies without modification. The golden rule is for the wedge in between — and in that wedge it is extraordinarily accurate.

---

## Exact Rabi oscillations, and where perturbation theory breaks

The two-level problem has an exact solution. Take two states $|g\rangle$ and $|e\rangle$ with energies $0$ and $\hbar\omega_0$, coupled by a drive $\hat{H}'(t) = \hbar\Omega\cos(\omega t)(|e\rangle\langle g| + |g\rangle\langle e|)$. The Rabi frequency $\Omega = |V_{fi}|/\hbar$ measures the coupling strength. In the RWA, the Schrödinger equation reduces to two coupled first-order ODEs that can be solved exactly. With initial conditions $c_g(0) = 1$, $c_e(0) = 0$:

$$\boxed{P_{g\to e}(t) = \frac{\Omega^2}{\Omega^2 + \Delta^2}\,\sin^2\!\left(\frac{\sqrt{\Omega^2 + \Delta^2}}{2}\,t\right),}$$

where $\Delta = \omega - \omega_0$ is the detuning. This formula is exact within the RWA — no perturbation approximation.

At resonance ($\Delta = 0$): $P_{g\to e}(t) = \sin^2(\Omega t/2)$. The population oscillates between 0 and 1. At $t = \pi/\Omega$, called a $\pi$-pulse, every atom is in the excited state. At $t = 2\pi/\Omega$, every atom is back in the ground state. The energy sloshes between drive and atom indefinitely, without loss or decay. This is a coherent oscillation, not a rate process.

Off-resonance ($\Delta \neq 0$): two things change. The maximum population is $\Omega^2/(\Omega^2 + \Delta^2) < 1$ — full inversion is impossible. And the oscillation frequency is $\sqrt{\Omega^2 + \Delta^2}$, the generalized Rabi frequency — faster than $\Omega$ but capped in amplitude. The atom flickers between ground and excited but never fully transfers.

Now compare to the first-order PT prediction for the same problem at resonance. The PT formula gives $P_{g\to e}^{\text{PT}}(t) = (\Omega t/2)^2$ — a parabola growing without bound. The exact formula gives $\sin^2(\Omega t/2)$ — bounded by 1 and periodically returning to zero. For small $\Omega t$, Taylor-expand $\sin^2 x \approx x^2$: the two agree. For $\Omega t \sim 1$, they diverge. At $\Omega t = \pi$, the exact formula says $P = 1$ and the PT formula says $P = (\pi/2)^2 \approx 2.47$. PT has predicted a probability greater than 1 — the unambiguous signal that the approximation has failed.

The failure is not a numerical inconvenience. It tells you something physical. First-order PT treats the population of $|f\rangle$ as negligible in computing the rate of change of $c_f$ — it never feeds the depleted $|i\rangle$ population back into the equation. The exact solution includes that feedback. When enough probability has moved into $|e\rangle$ that the reverse drive — emission stimulated by the perturbation — pushes it back, the exact solution captures the Rabi oscillation. PT misses the whole second half of the cycle.

The simulation you build below will let you slide time out from zero and watch the PT prediction cross 1. That crossing is a diagnostic: at that moment you know you need either the exact solution or a higher-order resummation.

---

## Selection rules and dipole transitions

Not every transition can be driven by an oscillating electric field. The rate is proportional to $|\langle f|\hat{H}'|i\rangle|^2$. For an atom in a monochromatic optical field $\vec{\mathcal{E}}_0\cos(\omega t)$, the perturbation is the electric dipole term $\hat{H}'(t) = e\hat{\vec{r}}\cdot\vec{\mathcal{E}}_0\cos(\omega t)$. The matrix element is $\langle f|e\hat{\vec{r}}|i\rangle$. When this matrix element is zero by symmetry, the transition is electric-dipole forbidden.

For hydrogen states $|n\ell m\rangle$, the angular integrals impose three constraints. The operator $\hat{\vec{r}}$ has odd parity. A matrix element of an odd-parity operator between two states of the same parity is zero — the integrand is odd, and the integral over all space vanishes. Since parity under $\vec{r} \to -\vec{r}$ takes $Y_\ell^m \to (-1)^\ell Y_\ell^m$, states with the same $\ell$ have the same parity. So $\Delta\ell = 0$ is forbidden. The algebra of spherical harmonics then shows that the angular integral is also zero unless $|\Delta\ell| = 1$, and that the $m$ quantum number satisfies $\Delta m = 0$ for light polarized along $\hat{z}$ and $\Delta m = \pm 1$ for circularly polarized light.

The selection rules for electric dipole transitions are therefore: $\Delta\ell = \pm 1$ and $\Delta m = 0, \pm 1$. Spin does not enter the electric dipole operator, so $\Delta s = 0$ — the electron's spin does not flip in an electric dipole transition.

These are not memorized rules; they are calculations that return zero. The $1s \to 2s$ transition is forbidden because both states are spherically symmetric — parity-even. The operator $\hat{z}$ is parity-odd. The integral of a parity-odd function over all of $\mathbb{R}^3$ is zero. That is the whole argument. The $1s \to 2p$ transition is allowed because $|2p\rangle$ has odd parity ($\ell = 1$); the product $\langle 2p|\hat{z}|1s\rangle$ integrates a parity-even function and gives a nonzero result.

What about forbidden transitions? They still occur — just slowly. The $2s \to 1s$ transition in hydrogen is electric-dipole forbidden with $\Delta\ell = 0$. It proceeds via two-photon emission, with a lifetime of about 0.12 s compared to nanosecond lifetimes for allowed transitions. The 21-cm hyperfine transition in hydrogen is magnetic dipole, with a lifetime of about $10^7$ years — which is why it illuminates the interstellar medium: the gas has enough time to emit even at cosmic densities. Forbidden does not mean impossible. It means suppressed by factors of $\alpha^2$ or more, where $\alpha \approx 1/137$ is the fine-structure constant.

---

## The spontaneous emission wall

This chapter hands you the spontaneous emission rate via Einstein's thermodynamic argument, not via quantum electrodynamics. The $A$-coefficient for hydrogen $2p \to 1s$, computed from the dipole matrix element and the transition frequency, gives a lifetime of about 1.6 ns. That number is correct.

But the reasoning has a gap. The framework of this chapter — time-dependent perturbation theory applied to an atom in a classical oscillating field — treats the electromagnetic field as an external driver. An atom in its excited state, with no classical field present, has no perturbation. By this framework it should sit in $|e\rangle$ forever.

It doesn't. Excited atoms decay. The reason is that the electromagnetic field is itself a quantum system with its own vacuum fluctuations. Even in the ground state of the field — no photons anywhere — there are fluctuations. Coupling the atom to the *quantized* field gives a non-trivial perturbation even with zero photons, and it is this coupling that drives spontaneous emission. The correct derivation of the $A$-coefficient requires quantizing the field. That is Dirac's 1927 paper again — the same paper that contains Fermi's golden rule. Einstein got the ratio $A/B$ from thermodynamics in 1917 without quantizing the field, which is a remarkable feat. But the mechanism — why $A$ is nonzero in the first place — requires quantum field theory.

The current framework is semiclassical: atomic states are quantum, the field is classical. Spontaneous emission marks the boundary. The chapter shows you where the wall is and points at the gate.

---

## Still puzzling

There is a self-consistency condition buried in the derivation of Fermi's golden rule that I find I cannot make feel inevitable. The long-time limit that turns the $\sin^2/\Delta\omega^2$ profile into a delta function requires $t \to \infty$. But the derivation also requires $W_{i\to f}\cdot t \ll 1$ — small total probability transferred — for first-order perturbation theory to be valid. Both conditions cannot hold simultaneously at arbitrarily long times. The golden rule is derived from a limit that violates its own condition of applicability.

The resolution is that the golden rule applies in an intermediate regime: long enough for the delta function to be a good approximation ($t \gg 1/\Delta\omega$), short enough for $P_{\text{total}} \ll 1$ ($t \ll \hbar/|V_{fi}|^2\rho$). For a typical atomic transition into the electromagnetic continuum, this window is enormous — many orders of magnitude wide in time. So the formula works, and works well, in virtually every application we care about. But the derivation technically requires a limit that the formula's validity condition forbids. I can state the resolution; I am not sure I can make the foundations feel completely clean.

---

## LLM Exercise — the Rabi resonance simulator

You are going to build a single-file D3 simulation showing time-dependent perturbation theory at work and at its breaking point. Three nested panels: population vs. time at fixed detuning, transition probability vs. detuning at fixed time, and a continuum-to-golden-rule toggle. The deliverable is `10-rabi-resonance.html` in your working directory.

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

**Chapter 11** takes up the other classical regime: large quantum numbers, short wavelengths, and the approximation that turns the wave equation back into something that looks like ray optics. Where this chapter handled small perturbations in time, Chapter 11 handles small wavelengths in space — the WKB approximation, tunneling, and the connection between quantum and classical mechanics at large quantum numbers.
