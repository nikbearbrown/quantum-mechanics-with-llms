# Chapter 10 — Time-Dependent Perturbation Theory and Transitions
*Every quantum control experiment ever built is Rabi's 1938 apparatus in different molecular handwriting.*

January 1938. Columbia University. Isidor Rabi's group passes a beam of LiCl molecules through three magnets. The first selects a particular spin orientation. The second — the interaction region — carries an oscillating radio-frequency field. The third analyzes what comes out. As they sweep the RF frequency, at one specific value the beam intensity drops sharply. The molecules have been flipped: driven from one spin state to the other by the oscillating field. The line is narrow, well-defined, and theoretically predicted. Rabi won the Nobel in 1944.

Here is what makes Rabi's experiment worth understanding before doing the math. The two-state system he was driving — a spin-up nuclear state and a spin-down nuclear state, separated by energy $\hbar\omega_0$, coupled by an oscillating perturbation — is the same physical object as an atom in a laser field, an NMR sample in a coil, a superconducting qubit in a microwave drive, a trapped ion in a Raman beam, an electron spin in an ESR apparatus. Every quantum control experiment of the last eighty years is Rabi's 1938 setup, written in different molecular handwriting. So the calculation we develop for Rabi's problem will work for all of them.

The question: what is the probability of finding the system in the "wrong" state at time $t$? And — critically — when does perturbation theory give the right answer, and when does it break?

---

## The interaction picture

The Schrödinger equation for a system with $\hat{H} = \hat{H}_0 + \hat{H}'(t)$ mixes something we understand — the eigenstates of $\hat{H}_0$ — with something we are treating as small. The interaction picture separates them cleanly.

Define a new state vector by stripping out the trivial $\hat{H}_0$ evolution:

$$|\tilde\psi(t)\rangle = e^{i\hat{H}_0 t/\hbar}\,|\psi(t)\rangle.$$

Substituting into the Schrödinger equation, the $\hat{H}_0$ terms cancel exactly, leaving:

$$i\hbar\,\partial_t|\tilde\psi(t)\rangle = \tilde{H}'(t)\,|\tilde\psi(t)\rangle,$$

where $\tilde{H}'(t) = e^{i\hat{H}_0 t/\hbar}\hat{H}'(t)e^{-i\hat{H}_0 t/\hbar}$. The interaction picture state evolves only under the perturbation. When $\hat{H}'(t) = 0$, it freezes. All the interesting dynamics is in the perturbation — which is where we want to look.

Now expand in the unperturbed eigenstates $|\tilde\psi(t)\rangle = \sum_n c_n(t)|n\rangle$, with initial condition $c_n(0) = \delta_{ni}$ (start in $|i\rangle$). Project onto the final state $|f\rangle$:

$$i\hbar\,\dot{c}_f = \sum_n c_n(t)\,\langle f|\hat{H}'(t)|n\rangle\,e^{i\omega_{fn}t},$$

where $\omega_{fn} = (E_f - E_n)/\hbar$. This is exact and coupled — every $c_f$ depends on every other $c_n$. To first order in $\hat{H}'$, replace $c_n(t)$ by its initial value $\delta_{ni}$ and integrate:

$$\boxed{c_f^{(1)}(t) = \frac{1}{i\hbar}\int_0^t \langle f|\hat{H}'(t')|i\rangle\,e^{i\omega_{fi}t'}\,dt'.}$$

The transition amplitude is the Fourier transform of the matrix element $\langle f|\hat{H}'(t)|i\rangle$, evaluated at the Bohr frequency $\omega_{fi}$. Resonance is Fourier resonance. Everything else follows from this.

---

## The resonance lineshape

Take $\hat{H}'(t) = \hat{V}\cos(\omega t)$. Near resonance $\omega \approx \omega_{fi}$, one term in the cosine — the counter-rotating term — oscillates rapidly and averages away. Keeping only the resonant term (the rotating-wave approximation, valid when $|V_{fi}|/\hbar\omega_0 \ll 1$) and squaring the amplitude:

$$\boxed{P_{i\to f}(t) = \frac{|V_{fi}|^2}{\hbar^2}\cdot\frac{\sin^2[(\omega_{fi}-\omega)t/2]}{(\omega_{fi}-\omega)^2}.}$$

At resonance ($\omega = \omega_{fi}$), the peak height grows as $t^2$. The width to the first zero shrinks as $2\pi/t$. The area under the central peak grows as $t$. Everything is consistent with a delta function emerging as $t\to\infty$ — which is the input to Fermi's golden rule.

But notice what the formula also says on-resonance: $P_{i\to f}(t) = |V_{fi}|^2t^2/(4\hbar^2)$. At long enough times this exceeds 1. A probability greater than 1 is nonsense. This is not a numerical inconvenience — it is the diagnostic that first-order perturbation theory has broken. The cause: PT ignores the back-action. Once probability flows into $|f\rangle$, it must stop coming from $|i\rangle$, but the first-order equations keep drawing from $|i\rangle$ as if nothing has changed. The exact Rabi solution accounts for the feedback. PT does not.

---

## The exact Rabi solution — and where PT fails

The two-level problem has an exact solution. Two states $|g\rangle$ and $|e\rangle$, energies $0$ and $\hbar\omega_0$, drive $\hat{H}'(t) = \hbar\Omega\cos(\omega t)(|e\rangle\langle g| + |g\rangle\langle e|)$. Here $\Omega = |V_{fi}|/\hbar$ is the Rabi frequency — it sets the coupling strength and, at resonance, the rate at which population cycles between the two states.

In the rotating-wave approximation, the Schrödinger equation reduces to two coupled first-order ODEs in $c_g$ and $c_e$. They can be solved exactly. With $c_g(0) = 1$, $c_e(0) = 0$:

$$\boxed{P_{g\to e}(t) = \frac{\Omega^2}{\Omega^2+\Delta^2}\,\sin^2\!\left(\frac{\sqrt{\Omega^2+\Delta^2}}{2}\,t\right),}$$

where $\Delta = \omega - \omega_0$ is the detuning. No perturbative approximation. This is the Rabi formula.

At resonance ($\Delta = 0$): $P_{g\to e}(t) = \sin^2(\Omega t/2)$. The population oscillates between 0 and 1. At $t = \pi/\Omega$ — a $\pi$-pulse — the entire population is in $|e\rangle$. At $t = 2\pi/\Omega$ it is back in $|g\rangle$. This is the coherent Rabi oscillation that Rabi's molecular beam showed in 1938, and that every qubit readout protocol relies on today.

Off-resonance ($\Delta \neq 0$): the maximum probability achievable is $\Omega^2/(\Omega^2+\Delta^2) < 1$. Full population transfer is impossible away from resonance. The oscillation frequency is the *generalized Rabi frequency* $\sqrt{\Omega^2+\Delta^2}$ — faster than $\Omega$ but smaller in amplitude. The further you detune the drive, the shallower and faster the oscillation.

Now compare to first-order PT at resonance. PT gives $P_{g\to e}^{\text{PT}}(t) = (\Omega t/2)^2$ — a parabola. The exact formula gives $\sin^2(\Omega t/2)$ — a bounded oscillation. For $\Omega t \ll 1$, Taylor-expand: $\sin^2 x \approx x^2$. The two agree. For $\Omega t \sim 1$, they diverge. At $\Omega t = \pi$, the exact answer is $P = 1$ and the PT answer is $(\pi/2)^2 \approx 2.47$. PT has predicted a probability of 247%. The simulation below will let you slide time out from zero and watch the moment of failure happen.

The failure is not a numerical accident. PT treats the amplitude in $|i\rangle$ as constant — $c_i(t) \approx 1$ — even as probability drains out of it. The exact solution feeds the depleted $|i\rangle$ population back in, which is what produces the return half of the Rabi cycle. PT misses the return entirely. The regime of validity is $\Omega t \ll 1$ — small coupling times short time. Outside that regime you need the exact solution or a resummation.

This is the lesson Rabi's experiment teaches. The precision of the resonance signal comes from running the drive long enough for the population to complete a $\pi$-pulse. At that point PT has failed by a factor of 2.47. The physics is right; the approximation is wrong.

---

## Fermi's golden rule (which is Dirac's)

When the final state is not a single discrete level but a continuum — an electron ionizing, an atom emitting a photon into the infinite continuum of electromagnetic modes, a nucleus decaying — the Rabi oscillation disappears. There is no single $|f\rangle$ to bounce back from. The population leaks irreversibly into the continuum and the question becomes a *rate*: how many transitions per second?

Sum the $\sin^2/\Delta\omega^2$ lineshape over the continuum, with density of states $\rho(E_f)$. For large $t$, the $\sin^2(\alpha t/2)/\alpha^2$ factor becomes $(\pi t/2)\delta(\alpha)$ — the proto-delta-function of the lineshape completes its sharpening. The probability grows linearly in $t$, giving a constant rate:

$$\boxed{W_{i\to f} = \frac{2\pi}{\hbar}\,|\langle f|\hat{H}'|i\rangle|^2\,\rho(E_f).}$$

This is Fermi's golden rule — the most used formula in atomic, molecular, condensed-matter, and nuclear physics.

It is also Dirac's formula. P.A.M. Dirac derived it in 1927, in "The Quantum Theory of the Emission and Absorption of Radiation," *Proc. R. Soc. London A* 114, 243. The paper is the foundational document of quantum electrodynamics and the $2\pi/\hbar$ prefactor, the matrix element squared, and the density of states appear in it explicitly. Fermi called it "Golden Rule No. 2" in 1950 Chicago lecture notes because it was useful in nuclear physics — not because he derived it. The name stuck. This chapter calls it Fermi's golden rule because no one will understand you if you call it anything else. But you should know that Dirac got there first, by twenty-three years.

The golden rule applies in a specific window. The continuum must be dense enough that the $\sin^2/\Delta\omega^2$ sum looks like an integral. The time must be long enough that the lineshape has sharpened ($t \gg 1/\Delta\omega$). And the time must be short enough that $W\cdot t \ll 1$ — the total probability transferred is still small, so PT is still valid. For an atom emitting into the electromagnetic vacuum, this window is enormous — nanoseconds to microseconds, while the Bohr oscillation period is femtoseconds. For a two-level atom driven on resonance, the window is $1/\omega_0 \ll t \ll 1/\Omega$ — it exists, but it is narrower, and it vanishes entirely at strong coupling. That is when you need the Rabi formula instead.

---

## Selection rules and dipole transitions

For an atom in an optical field, the perturbation is $\hat{H}'(t) = e\hat{\vec{r}}\cdot\vec{\mathcal{E}}_0\cos(\omega t)$. The transition matrix element is $\langle f|e\hat{\vec{r}}|i\rangle$. When it vanishes by symmetry, the transition is electric-dipole forbidden.

For hydrogen states $|n\ell m\rangle$, the symmetry constraints are: the operator $\hat{\vec{r}}$ has odd parity. A matrix element of an odd-parity operator between two states of the same parity is zero — the integrand is odd over all space. Since parity under $\vec{r}\to-\vec{r}$ takes $Y_\ell^m \to (-1)^\ell Y_\ell^m$, same $\ell$ means same parity, so $\Delta\ell = 0$ is forbidden. The algebra of spherical harmonics forces $|\Delta\ell| = 1$, and the azimuthal integral forces $\Delta m = 0$ for $\hat{z}$-polarized light and $\Delta m = \pm 1$ for circularly polarized light. Spin is invisible to the electric dipole operator, so $\Delta s = 0$.

The selection rules $\Delta\ell = \pm 1$, $\Delta m = 0, \pm 1$, $\Delta s = 0$ are calculations that return zero, not memorized recipes. The $1s\to 2s$ transition is forbidden because both states are spherically symmetric — parity even — and $\hat{z}$ is parity odd. The integral of an odd function over all space is zero. That is the argument, not a rule about quantum numbers.

Forbidden means slow, not impossible. The $2s\to 1s$ hydrogen transition has $\Delta\ell = 0$ and proceeds via two-photon emission with a lifetime of 0.12 seconds — eight orders of magnitude slower than an allowed transition. The 21-cm hyperfine transition is a magnetic dipole transition with a lifetime of roughly $10^7$ years. Because the interstellar medium gives it that much time, it illuminates the structure of galaxies. Long lifetimes are useful.

---

## The spontaneous emission wall

Chapter 9's perturbation theory, and the framework of this chapter, treats the electromagnetic field as an external classical driver. An atom in its excited eigenstate, with no classical field present, has no time-dependent perturbation and should sit there forever. Yet excited atoms decay.

They decay because the electromagnetic field is itself quantum. Even in its vacuum state — no photons anywhere — the field fluctuates. Coupling the atom to the *quantized* field gives a non-trivial perturbation even with zero applied drive, and it is this vacuum coupling that drives spontaneous emission. The correct derivation of the $A$-coefficient requires quantizing the field — which is exactly what Dirac did in 1927 in the same paper that contains the golden rule. Einstein extracted the ratio $A_{21}/B_{21}$ from thermodynamics in 1917 without quantizing the field, a remarkable tour de force. But the mechanism — why $A$ is nonzero at all — requires quantum electrodynamics.

For hydrogen $2p \to 1s$, computing the dipole matrix element $|\langle 1s|\hat{\vec{r}}|2p\rangle|^2 \approx 0.555\,a_0^2$ and plugging into the Einstein $A$-coefficient formula gives a lifetime of about 1.6 ns, matching the measured value. The number is right. The semiclassical derivation of that number is technically incomplete. This chapter shows you where the wall is and points at the gate: Dirac 1927, quantum field theory, a later course.

---

## Still puzzling

The derivation of Fermi's golden rule requires taking $t\to\infty$ to sharpen the $\sin^2/\Delta\omega^2$ into a delta function. But the derivation also requires $W\cdot t \ll 1$ for first-order perturbation theory to be valid. Both conditions cannot hold simultaneously at arbitrarily long times.

The resolution is that there is a wide intermediate window — $t$ large enough for the delta function to be a good approximation, small enough for PT to hold — and in that window the golden rule is accurate. For atomic emission into the vacuum, the window spans many orders of magnitude in time, so the formula is extraordinarily well-tested. But the derivation technically invokes a limit that the validity condition forbids. The physics is right; the logical structure of the derivation has a seam. I can state this cleanly. I cannot make it feel fully resolved.

---

## LLM Exercise — the Rabi resonance simulator

You are going to build a single-file D3 simulation showing the exact Rabi formula and first-order perturbation theory side by side, with a continuum mode where the Rabi oscillation collapses into Fermi's linear growth. The deliverable is `10-rabi-resonance.html` in your working directory.

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

**Chapter 11** moves from perturbations in time to approximations in space. Where this chapter handled small coupling between levels, Chapter 11 handles large quantum numbers and short wavelengths — the WKB approximation, tunneling, and the connection formula that bridges classical and quantum mechanics at a turning point.
