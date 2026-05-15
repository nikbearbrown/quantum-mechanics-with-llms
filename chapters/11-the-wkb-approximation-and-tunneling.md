# Chapter 11 — The WKB Approximation and Tunneling
*The chapter where a particle passes through a wall it has no business passing through.*

Polonium-212 has a halflife of about $3 \times 10^{-7}$ seconds. Thorium-232 has a halflife of about $1.4 \times 10^{10}$ years. Both decay by emitting an alpha particle through the same mechanism — a cluster of two protons and two neutrons, formed inside the nucleus, escaping to the outside. The ratio of their halflives is roughly $10^{24}$. Twenty-four orders of magnitude.

In 1911, Hans Geiger and John Mitchell Nuttall found that for alpha emitters of the same daughter charge, the log of the halflife is approximately linear in $1/\sqrt{E_\alpha}$ — a straight line on a log-vs-inverse-square-root plot. The observation was clean and the explanation was completely absent.

Here is the classical problem. An alpha particle approaching a nucleus sees a Coulomb barrier. At the nuclear surface, the barrier is about 30 MeV. The emitted alpha has about 5 MeV. Classically, the alpha is stuck. It does not have enough energy to get over the wall. And yet out it comes.

In the summer of 1928, George Gamow in Göttingen computed the probability of the alpha particle *tunneling* through the Coulomb barrier using brand-new quantum mechanics. Within days, Ronald Gurney and Edward Condon at Princeton published the same idea independently. Both found the same thing: the tunneling probability is exponentially sensitive to barrier height, width, and particle energy. That exponential sensitivity is the source of the 24-decade dynamic range. A small change in alpha energy corresponds to a huge change in the exponent, which corresponds to an astronomical change in the halflife. The Geiger-Nuttall line is a plot of that exponent as a function of alpha energy.

This chapter builds the machinery that gives you that result.

---

## The WKB ansatz

The time-independent Schrödinger equation in one dimension is

$$-\frac{\hbar^2}{2m}\psi''(x) + V(x)\psi(x) = E\psi(x).$$

Define the local classical momentum

$$p(x) = \sqrt{2m(E - V(x))},$$

which is real where the particle is classically allowed ($E > V$) and imaginary in the forbidden region ($E < V$). Now write the wave function as

$$\psi(x) = e^{iS(x)/\hbar}$$

for some function $S(x)$. This is not an approximation — it is an exact rewriting. Any $\psi$ can be written this way; $S$ is in general complex. Substitute into the Schrödinger equation and you get an exact equation for $S$:

$$\frac{(S')^2}{2m} - \frac{i\hbar}{2m}S'' = E - V(x).$$

Now expand $S$ in powers of $\hbar$: $S = S_0 + (\hbar/i)S_1 + \cdots$. At zeroth order in $\hbar$ the equation gives $(S_0')^2/2m = E - V$, so

$$S_0'(x) = \pm p(x) \quad\Longrightarrow\quad S_0 = \pm\int p(x')\,dx'.$$

At first order, the correction satisfies $S_1' = -p'/(2p)$, giving $S_1 = -\frac{1}{2}\ln p$. Assembling the pieces and tracking the normalization:

$$\boxed{\psi_{\text{WKB}}(x) \approx \frac{C}{\sqrt{p(x)}}\,\exp\!\left[\pm\frac{i}{\hbar}\int p(x')\,dx'\right]}$$

in the classically allowed region, and

$$\psi_{\text{WKB}}(x) \approx \frac{C}{\sqrt{|p(x)|}}\,\exp\!\left[\pm\frac{1}{\hbar}\int |p(x')|\,dx'\right]$$

in the classically forbidden region. The two signs correspond to right- and left-moving solutions, or in the forbidden region, to growing and decaying exponentials.

The $1/\sqrt{p(x)}$ prefactor has a clean interpretation. The classical probability of finding the particle near $x$ is proportional to how long it spends there — proportional to $1/v(x) \propto 1/p(x)$. So $|\psi|^2 \propto 1/p(x)$: the wave function is large where the classical particle is slow and small where it moves quickly. The envelope tracks classical mechanics; the phase oscillates quantum-mechanically. This is why the approximation is called semiclassical.

<!-- → [CHART: three panels showing ψ_WKB(x) in an arbitrary smooth potential well — top panel: V(x) as a smooth curve with horizontal line at E marking the classical turning points a and b; middle panel: |ψ_WKB(x)|² showing large amplitude where p(x) is small (near turning points), small amplitude where p(x) is large (deep in the well), with the 1/p(x) envelope drawn as a dashed line; bottom panel: Im[ψ] showing rapid phase oscillations where p is large, slow oscillations near turning points; caption: "The WKB wave function: large amplitude where the classical particle is slow, rapid phase where it moves fast"] -->

---

## When the approximation is valid — and when it is not

The expansion above is controlled if higher-order terms are small. The condition works out to

$$\left|\frac{d\lambda_{\text{dB}}}{dx}\right| \ll 1$$

where $\lambda_{\text{dB}} = h/p(x)$ is the local de Broglie wavelength. The potential must vary slowly across one de Broglie wavelength. Equivalently, the classical action $\int p\,dx$ must be large compared to $\hbar$.

This condition fails *exactly* at a classical turning point $x_0$ where $E = V(x_0)$ and $p \to 0$. As the particle slows down at the turning point, its de Broglie wavelength grows without bound, and the WKB forms on each side cannot be matched naively. The fix is the *connection formula*: near $x_0$, linearize the potential and solve the resulting Airy equation exactly, then match its asymptotic forms to the WKB expressions on each side. Each turning point contributes a phase of $\pi/4$ — the Maslov index — which shifts the phase of the oscillating WKB solution by that amount.

The derivation of the connection formulas is involved, and doing it once carefully is worth the effort; but for the applications in this chapter, the output is what matters. Each classical turning point contributes $\pi/4$ to the accumulated phase.

<!-- → [IMAGE: diagram of the WKB connection at a single turning point x₀ — left side (x < x₀, classically allowed): oscillating WKB wave labeled "C/√p cos(∫p dx/ℏ − π/4)"; right side (x > x₀, classically forbidden): decaying exponential labeled "C/2√|p| exp(−∫|p|dx/ℏ)"; at x₀: the Airy function Ai(z) bridges the two regions, shown as a smooth curve that transitions from oscillation to decay; a small inset shows the linearized potential V(x) ≈ E + V'(x₀)(x−x₀) used to derive the Airy equation; caption: "The Airy function is the exact solution near the turning point. Its asymptotic forms on each side pin down the WKB connection, including the π/4 Maslov phase"] -->

---

## Bound states: the Bohr-Sommerfeld condition

A particle bound between two turning points $a$ and $b$ — classically allowed between them, forbidden outside — must have a wave function that oscillates in the interior and decays on both sides. Threading the WKB solution through both turning points, demanding a self-consistent single-valued solution, and using the Maslov contributions from each turning point gives:

$$\boxed{\oint p(x)\,dx = 2\int_a^b p(x)\,dx = \left(n + \frac{1}{2}\right)h, \quad n = 0, 1, 2, \ldots}$$

This is the Bohr-Sommerfeld quantization condition. The $1/2$ inside the bracket is the Maslov correction — the two $\pi/4$ contributions from the two turning points, added together. The original Bohr-Sommerfeld of 1913–1916 had $nh$ and no Maslov correction; the upgrade came with WKB.

For the harmonic oscillator, $V = \frac{1}{2}m\omega^2 x^2$, the phase-space orbit at energy $E$ is an ellipse with area $2\pi E/\omega$. The Bohr-Sommerfeld condition gives $2\pi E/\omega = (n+\frac{1}{2})h$, so $E_n = (n+\frac{1}{2})\hbar\omega$ — the *exact* quantum-mechanical energies, not just an approximation. The same miracle happens for hydrogen in the Coulomb potential. These are not coincidences; they reflect hidden symmetries in those particular potentials. For most other potentials, Bohr-Sommerfeld is a leading-order estimate.

<!-- → [IMAGE: phase-space diagram illustrating Bohr-Sommerfeld for the harmonic oscillator — an ellipse in (x, p) space at energy E, with axes labeled x and p; the area of the ellipse shaded and labeled "∮p dx = 2πE/ω"; horizontal lines at energies E_0 = ℏω/2, E_1 = 3ℏω/2, E_2 = 5ℏω/2 showing that each allowed orbit has area (n+1/2)h; caption: "The Bohr-Sommerfeld condition as a phase-space area quantization. Each allowed orbit encloses area (n+½)h. For the harmonic oscillator, this gives the exact energies"] -->

---

## Tunneling: the Gamow factor

Now the main event. A particle with energy $E$ encounters a potential barrier $V(x) > E$ between two classical turning points $a$ and $b$. The particle cannot get over the barrier classically; quantum-mechanically, the wave function does not vanish inside the barrier — it decays exponentially, and a small piece emerges on the other side.

Thread the WKB solution through the barrier. On the incident side, the wave function oscillates. Inside the forbidden region, the dominant WKB solution decays as $\exp[-(1/\hbar)\int|p|\,dx]$. On the transmitted side, it oscillates again. Following the mathematics through the connection formulas at both turning points, the *transmission coefficient* — the ratio of transmitted to incident probability current — comes out to:

$$\boxed{T \approx e^{-2\gamma}, \qquad \gamma = \frac{1}{\hbar}\int_a^b\sqrt{2m(V(x)-E)}\,dx}$$

The exponent $\gamma$ is the Gamow factor.

Three things to notice immediately. First, the transmission depends *exponentially* on the Gamow factor. A small change in barrier height, width, or particle energy gets amplified into a large change in $T$. This is the origin of the 24-decade dynamic range — it is the dynamic range of an exponential. Second, the barrier shape integrates into the formula automatically; any shape gets the same treatment, just a different integral. Third, the exponential carries essentially all the physics. The exact WKB formula has prefactors of order unity that depend on barrier-matching details, but those are smooth functions of $E/V_0$ and rarely matter for order-of-magnitude estimates.

For a rectangular barrier of height $V_0$ and width $L$, the Gamow integral is trivial: $\gamma = \kappa L$ where $\kappa = \sqrt{2m(V_0-E)}/\hbar$. The exact transmission coefficient (derived by matching plane waves at the barrier edges) is

$$T_{\text{exact}} = \left[1 + \frac{V_0^2\sinh^2(\kappa L)}{4E(V_0-E)}\right]^{-1}$$

In the thick-barrier limit $\kappa L \gg 1$, this approaches $T_{\text{exact}} \approx [16E(V_0-E)/V_0^2]\,e^{-2\kappa L}$. The WKB gives $T_{\text{WKB}} = e^{-2\kappa L}$. On a log plot, the two curves run parallel: same exponential slope, offset by the smooth prefactor $16E(V_0-E)/V_0^2$. WKB nails the exponent and misses the prefactor by an $O(1)$ factor. For physics that spans decades, that is exactly the right trade.

<!-- → [CHART: T vs. E/V₀ on a log y-axis from 10⁻¹² to 1, for V₀=5 and L=5 in natural units — two curves: T_exact (solid black) and T_WKB (dashed teal); below the barrier (E/V₀ < 1) the curves are parallel on the log axis with a constant vertical offset labeled "missing prefactor ≈ 16E(V₀−E)/V₀²"; above the barrier (E/V₀ > 1) T_exact shows interference fringes while T_WKB = 1; vertical reference line at E/V₀ = 1 labeled "barrier top"; caption: "WKB nails the exponent, misses the prefactor by an O(1) factor. The two curves are parallel below the barrier; the offset is the smooth function the leading WKB drops"] -->

---

## Alpha decay and the Geiger-Nuttall law

Model an alpha particle as a pre-formed cluster bouncing inside a heavy nucleus. Inside the nucleus at radius $r < R$, it is held by the strong force. Outside, at $r > R$, it sees the Coulomb repulsion from the daughter nucleus (charge $Z' = Z - 2$):

$$V(r) = \frac{2Z'e^2}{4\pi\epsilon_0 r}, \quad r > R.$$

The barrier extends from $r = R$ out to the classical turning point $r_c$ where $V(r_c) = E_\alpha$:

$$r_c = \frac{2Z'e^2}{4\pi\epsilon_0 E_\alpha}.$$

For uranium-238 ($Z' = 90$, $E_\alpha \approx 4.2\,\text{MeV}$, $R \approx 7.4\,\text{fm}$), the turning point sits at $r_c \approx 60\,\text{fm}$ — the alpha must tunnel through a barrier eight times wider than the nucleus.

The Gamow integral over the Coulomb barrier can be done analytically with the substitution $r = r_c\sin^2\theta$. In the limit $R \ll r_c$, which holds for heavy nuclei, the result simplifies to

$$\gamma \approx \frac{\pi Z' e^2}{4\epsilon_0\hbar}\sqrt{\frac{m_\alpha}{2E_\alpha}} - 2\sqrt{\frac{2m_\alpha}{\hbar^2}Rr_c \cdot E_\alpha / E_\alpha}$$

The first term grows as $1/\sqrt{E_\alpha}$; the second is a smaller correction. The decay rate is

$$\Gamma \sim \nu_0\,e^{-2\gamma}$$

where $\nu_0 \sim v/(2R) \sim 10^{21}\,\text{Hz}$ is the attempt frequency — how many times per second the alpha bounces against the inside of the barrier. Taking the logarithm:

$$\log_{10}\tau_{1/2} \approx A(Z') + \frac{B(Z')}{\sqrt{E_\alpha}}$$

This is the Geiger-Nuttall law. A straight line on a log-vs-$1/\sqrt{E}$ plot, for fixed daughter charge. The empirical observation from 1911 is *derived* from the WKB tunneling formula.

Let me put numbers on it for $^{238}$U. The Gamow factor $\gamma \approx 43$, so $e^{-2\gamma} \approx e^{-86} \approx 4\times 10^{-38}$. The decay rate is $\Gamma \sim 10^{21} \times 4\times 10^{-38} \approx 4\times 10^{-17}\,\text{s}^{-1}$, giving a halflife of roughly $5\times 10^8\,\text{years}$. The experimental value is $4.5\times 10^9\,\text{years}$. We are off by a factor of 10. On a quantity that spans $10^{24}$, that is excellent. The remaining factor comes from the pre-formation probability of the alpha cluster inside the nucleus and from finer-grained prefactors in the WKB formula that we dropped.

This is one of the high-water marks of quantum mechanics applied to nuclear physics. A back-of-envelope calculation, using the WKB formula and a model that a first-year graduate student can write down, reproduces a halflife of billions of years.

<!-- → [IMAGE: Coulomb barrier diagram for alpha decay — radial potential V(r) plotted vs. r for a heavy nucleus; inside r < R: a flat nuclear well (strong force); outside r > R: Coulomb barrier 2Z'e²/(4πε₀r) falling as 1/r; horizontal line at E_α ≈ 5 MeV intersecting the Coulomb curve at r_c ≈ 60 fm; the classically forbidden tunneling region [R, r_c] shaded gray; the nuclear radius R ≈ 7.4 fm and turning point r_c labeled; arrows showing the alpha bouncing at frequency ν₀ inside the well and the exponentially attenuated wave emerging outside; caption: "The alpha tunnels from r = R to r = r_c through the Coulomb barrier. For ²³⁸U, the barrier is 8× wider than the nucleus. The Gamow factor γ ≈ 43 gives e^{−2γ} ≈ 10^{−38}"] -->

<!-- → [CHART: Geiger-Nuttall plot — log₁₀(τ₁/₂) vs. 1/√(E_α) for uranium isotopes (or a fixed daughter charge Z'=90) — experimental data points as filled circles for at least five isotopes (e.g., ²³²U through ²³⁸U); straight line fit showing the linear WKB prediction; axes labeled with log₁₀(τ₁/₂) in seconds on y-axis and 1/√(E_α) in MeV^{-1/2} on x-axis; caption: "The Geiger-Nuttall law: log halflife is linear in 1/√E_α. Twenty-four decades of dynamic range on a single straight line, derived from the WKB Gamow factor"] -->

---

## What else the formula explains

The same Gamow factor runs through a surprising range of physics.

In a scanning tunneling microscope, a metal tip is held a few angstroms above a conducting surface. A small bias voltage drives electrons through the vacuum gap. The work function of a typical metal is $\phi \approx 4\,\text{eV}$, so $\kappa = \sqrt{2m_e\phi}/\hbar \approx 1\,\text{Å}^{-1}$. The tunneling current goes as $I \propto e^{-2\kappa d}$. When the tip moves one angstrom closer to the surface, the current increases by a factor of $e^2 \approx 7$. When it moves one angstrom farther, the current drops by the same factor. A surface feature of sub-angstrom amplitude produces a measurable swing in current. This is why an STM can image individual atoms: the exponential transduction turns atomic-scale topography into macroscopic current variations. The exponential is the measurement.

In stars, the fusion of hydrogen nuclei is classically forbidden at solar-core temperatures ($kT \sim 1\,\text{keV}$) because the Coulomb barrier between protons is of order 1 MeV. The fusion rate is the product of the Maxwell-Boltzmann tail — the probability that a proton pair has unusually high relative energy — and the Gamow tunneling factor at that energy. The product peaks at an intermediate energy, the Gamow peak, where most of the fusion occurs. Every star burns by tunneling.

Flash memory stores bits by trapping electrons on a polysilicon gate isolated by a thin oxide layer. Writing a bit drives electrons through the oxide by Fowler-Nordheim tunneling — the electrons see a triangular barrier in the oxide, and the Gamow factor for that barrier shape determines the write speed and the retention time. The entire device geometry of a USB stick is an exercise in engineering that exponential.

<!-- → [CHART: Gamow peak diagram for stellar pp fusion — two curves plotted vs. relative kinetic energy E on the same axes: Maxwell-Boltzmann tail exp(−E/kT) falling steeply from left, Gamow tunneling factor exp(−b/√E) rising steeply from left; their product (the integrand of the fusion rate) shown as a narrow peaked curve labeled "Gamow peak" at energy E_G ≈ (bkT/2)^{2/3}; for T = 1.5×10⁷ K (solar core), E_G ≈ 6 keV while kT ≈ 1 keV; caption: "The Gamow peak: fusion happens where the thermal tail and the tunneling probability overlap. The peak sits well above kT because tunneling is exponentially suppressed at low energy"] -->

---

## The back-of-envelope as a falsification tool

In 1989, Martin Fleischmann and Stanley Pons announced "cold fusion" — deuterium-deuterium fusion at room temperature in a palladium electrochemical cell. Evaluating this claim requires exactly one calculation.

At room temperature, the thermal energy is $kT \approx 0.025\,\text{eV}$. The Coulomb barrier for D-D fusion at nuclear-contact distance is of order 1 MeV. Compute the Gamow factor: $\gamma \approx (\pi e^2/4\epsilon_0\hbar)\sqrt{m_D/2kT}$. Plugging in numbers gives $\gamma \sim 1000$, so $e^{-2\gamma} \sim 10^{-900}$. Even if chemistry could boost the tunneling rate by a factor of $10^{50}$ — which it cannot — you would still be $10^{850}$ short of the claimed power output. The Gamow factor does not care about the details of the palladium lattice. The number is $10^{-900}$.

This is the honest use of the back-of-envelope estimate: not to refine but to falsify. Knowing how to compute a Gamow factor is enough to evaluate any "novel nuclear effect at ambient conditions" claim quantitatively. The cold fusion case required no deep physics beyond what this chapter contains.

---

## The one application that remains genuinely open

Per-Olov Löwdin proposed in 1963 that protons in the hydrogen bonds of Watson-Crick DNA base pairs can tunnel between their two tautomeric positions, occasionally flipping a base into a mismatched form and causing a point mutation during replication. The mechanism is over sixty years old and remains contested.

The Gamow factor for a proton tunneling across a hydrogen bond is not $10^{-900}$. The relevant barrier is about 0.3 eV wide and a few tenths of an eV tall; the relevant mass is that of a proton. The rate is not obviously impossible. Recent open-system quantum simulations suggest the mechanism may be viable for guanine-cytosine pairs. Whether proton tunneling *actually contributes* to mutation rates in living cells — as opposed to thermal tautomeric isomerization, which also exists — is not settled.

The methodology for telling settled tunneling stories from speculative ones is the back-of-envelope Gamow factor you have now learned. Apply it to every quantum-biology claim you read. When the exponent comes out to $10^{-900}$, the claim is dead. When it comes out to something plausible, the physics is open and the biology deserves investigation. The calculation will tell you which.

---

## Still puzzling

How long does a particle spend inside the barrier? This question is surprisingly difficult to answer, and not for computational reasons.

There are at least four well-defined definitions of "tunneling time" in the literature — the dwell time, the phase time, the Büttiker-Landauer time, the Larmor clock — and they give different numerical answers, sometimes differing by orders of magnitude. Recent attosecond-streaking experiments measure something. What they measure, and which theoretical time it corresponds to, is actively debated.

The pop-science answer to the tunneling question — "the particle borrows energy from the vacuum for a brief time and pays it back, allowed by the uncertainty principle" — is wrong in detail. Energy is conserved at every measurement. The wave function inside the barrier is not a particle with kinetic energy $E - V < 0$; it is an exponentially decaying solution to the Schrödinger equation for a particle *with energy* $E$. There is no energy borrowing. There is just the wave, decaying through the forbidden region and emerging on the other side.

The WKB formalism of this chapter gives you the transmission coefficient $T$ but does not give you a tunneling time. I do not have a satisfying answer to which of the proposed times is the right one. The framework is incomplete here. Saying so honestly is the right move.

---

## LLM Exercise — the tunneling simulator

You are going to build the chapter's signature simulation: three nested panels including an *animated Gaussian wave packet* that hits a barrier and splits into reflected and transmitted parts. This is the visualization that cannot be replicated in print. The deliverable is `11-tunneling-simulator.html` in your working directory.

### Part 1 — Update `PROJECT.md`

```
Append a new entry to PROJECT.md describing this chapter's simulation:

Chapter 11 — The WKB Approximation and Tunneling
Deliverable: 11-tunneling-simulator.html
Status: in progress

The simulation has three nested modes selectable by tabs:

Mode A — Stationary T(E) for rectangular barrier.
Plot T vs. E/V_0 on a LOG y-axis from 10^-12 to 1.
Two curves:
  - Exact transmission T_exact = [1 + V_0^2 sinh^2(kappa L)/(4 E (V_0 - E))]^-1
  - WKB: T_WKB = exp(-2 kappa L) for E < V_0; for E > V_0 fall back to
    classical T = 1 with interference fringes from exact.
On the log axis, the two curves run parallel below the barrier (same
exponential slope) with constant offset of order unity. Pedagogical
purpose: WKB nails the exponent, misses the prefactor.

Mode B — General WKB for arbitrary barrier shape.
Selector for barrier shape: rectangular, triangular, parabolic, double-
barrier. For each, plot V(x) on the left and T(E) on the right (log
y-axis). Compute T_WKB numerically by integrating
sqrt(2m(V(x) - E)) over the classically forbidden region for each E.
For the double barrier, watch resonant tunneling peaks emerge: T -> 1
at certain E values even though each individual barrier is opaque.

Mode C — Animated wave packet (Crank-Nicolson).
The pedagogical centerpiece. A Gaussian wave packet
psi_0(x) = (1/(2 pi sigma_x^2)^(1/4)) * exp(-(x - x_0)^2/(4 sigma_x^2))
       * exp(i p_0 (x - x_0) / hbar)
with center x_0 to the left of the barrier and momentum p_0 to the right.
Evolve the time-dependent Schrodinger equation using Crank-Nicolson:
  (1 + i H dt / 2 hbar) psi(t+dt) = (1 - i H dt / 2 hbar) psi(t)
On a spatial grid of 500 points with absorbing boundaries.
Display |psi(x, t)|^2 as a filled area chart; the barrier V(x) as a
shaded region; the energy E = E_0 = p_0^2 / 2m as a horizontal line.
Play/pause/reset controls. Time slider for scrubbing.

Controls (Mode C):
- V_0 slider (barrier height)
- L slider (barrier width)
- p_0 slider (incident momentum)
- sigma_x slider (wave-packet width)
- Time t (play/pause/scrub)

Natural units: hbar = m = 1. Spatial grid from -50 to +50 in natural
units. Barrier centered at x = 0.
```

### Part 2 — The CLAUDE.md amendment

```
Append to CLAUDE.md the following physics rules for Chapter 11 simulations:

WKB AND TUNNELING PHYSICS RULES

1. EXACT RECTANGULAR BARRIER. For E < V_0 (sub-barrier):
     T_exact = 1 / (1 + (V_0^2 / (4 E (V_0 - E))) * sinh^2(kappa L))
   with kappa = sqrt(2 m (V_0 - E)) / hbar. For E > V_0:
     T_exact = 1 / (1 + (V_0^2 / (4 E (E - V_0))) * sin^2(k_2 L))
   with k_2 = sqrt(2 m (E - V_0)) / hbar.

2. WKB FOR RECTANGULAR BARRIER. T_WKB = exp(-2 kappa L) for E < V_0;
   T_WKB = 1 for E > V_0 (no tunneling, classical transmission). The
   subleading prefactor 16 E (V_0 - E) / V_0^2 is NOT included in
   leading-order WKB; flag this on the plot as "WKB misses prefactor."

3. WKB FOR GENERAL BARRIER. T_WKB = exp(-2 gamma) where
     gamma = (1 / hbar) * integral_a^b sqrt(2 m (V(x) - E)) dx
   with a, b the classical turning points where V(x) = E. Compute the
   integral by Simpson's rule on a 1000-point sub-grid of the forbidden
   region.

4. CRANK-NICOLSON. On a uniform spatial grid x_i with spacing dx,
   discretize the Hamiltonian:
     H psi |_i = -hbar^2/(2 m dx^2) * (psi_{i+1} - 2 psi_i + psi_{i-1})
              + V(x_i) psi_i
   Build the tridiagonal matrices A = I + i H dt / (2 hbar) and
   B = I - i H dt / (2 hbar). Each time step solves A psi_new = B psi_old.
   Use Thomas algorithm for tridiagonal solve (30 lines; do NOT pull in
   numeric.js).

5. ABSORBING BOUNDARIES. Add an imaginary potential
     V_abs(x) = -i V_max * f((|x| - x_abs)/(L_box - x_abs))
   with f(s) = s^2 for s > 0 and 0 for s < 0, where x_abs is the start
   of the absorber (about 80% of the box edge) and V_max is chosen so
   that the absorber damps the wave packet over its width. Without this,
   the wave packet reflects off the box walls.

6. NORMALIZATION CHECK. After each Crank-Nicolson step, compute
   sum |psi(x_i, t)|^2 dx. In the absence of absorbing boundaries this
   should equal 1 within 1e-6. With absorbing boundaries, the norm
   decreases over time as the absorber "eats" the wave packet — this
   is expected.

7. INITIAL WAVE PACKET. Gaussian with width sigma_x (typical: 2 in
   natural units), center x_0 (typical: -20), momentum p_0 (typical:
   sqrt(2 m E) with E around V_0/2).

8. TIME STEP. Choose dt such that hbar * dt / (m dx^2) <= 1 for
   numerical stability. With dx = 0.2, dt = 0.05 is safe.

KNOWN FAILURE MODES:
(a) Crank-Nicolson tridiagonal Thomas-algorithm bugs. Write 30 lines,
    test against analytic Gaussian dispersion in free space first.
(b) Forgetting absorbing boundaries. The wave packet reflects off the
    edges and confuses the picture.
(c) Time step too large -> divergence in the imaginary part of the wave
    function.
(d) Plotting T on a linear y-axis. The whole point is the exponential
    suppression; LOG y-axis only.
(e) For Mode A, plotting only T_WKB without T_exact. The pedagogy
    requires both curves on the same plot.
(f) Barrier height not visible behind the wave packet (z-order). Render
    barrier as a translucent fill BEHIND the wave function.
```

### Part 3 — The simulation prompt

```
You are working in my directory which contains CLAUDE.md, DESIGN.md, and
PROJECT.md. Read all three first.

Build 11-tunneling-simulator.html: a single self-contained HTML file
using D3 v7 from a CDN and d3-simple-slider. No other dependencies.
Three modes selectable by tabs: "Stationary T(E)", "WKB barrier shape",
and "Wave packet (CN)".

STATIONARY T(E) MODE
Single SVG 1100 x 600. Plot T vs. E/V_0 on a LOG y-axis from 10^-12 to 1.
X-axis: E/V_0 from 0 to 2.5 (so we see both below and above barrier).
Two curves:
  - T_exact (solid black)
  - T_WKB (dashed teal)
Vertical reference line at E/V_0 = 1 (barrier height) labeled "barrier top."
For E < V_0, the two curves run parallel; the offset is the missing
prefactor. For E > V_0, only T_exact has interference fringes.

Controls: V_0 (1 to 10), L (1 to 10) in natural units.

WKB BARRIER SHAPE MODE
Single SVG 1100 x 600 split into two panels:

Left panel (550 wide): potential V(x). Selector for barrier shape:
- Rectangular: V = V_0 for |x| < L/2, 0 else
- Triangular: V = V_0 (1 - 2|x|/L) for |x| < L/2, 0 else
- Parabolic: V = V_0 (1 - (2x/L)^2) for |x| < L/2, 0 else
- Double barrier: two rectangular barriers of width L_b separated by W

Right panel (550 wide): T_WKB(E) on LOG y-axis from 10^-12 to 1.
For double barrier, watch resonant tunneling peaks emerge.

Controls: V_0, L, W (only for double barrier), shape selector.

WAVE PACKET MODE
Single SVG 1100 x 600. Single main plot:
- X-axis: position x from -50 to +50 in natural units.
- Y-axis: amplitude / probability density.
- Barrier V(x) drawn as a translucent gray fill behind the wave function.
- Horizontal dashed line at energy E = p_0^2 / 2m, with E/V_0 label.
- Wave function |psi(x, t)|^2 drawn as a filled area in blue.

Below the plot: t = current time, sum |psi|^2 dx (should be ~ 1 minus
absorber loss), and computed instantaneous "transmission" R(t) = integral
of |psi|^2 for x > L/2 + buffer.

Buttons: Play, Pause, Reset.
Controls: V_0, L, p_0, sigma_x.

GLOBAL
For Mode C, pre-compute the entire (x, t) grid of psi(x, t) when the
user clicks Play (or releases a slider). Crank-Nicolson on 500 spatial
points x 2000 time steps takes 2-5 seconds in JS. Cache the result;
playback is just iterating through stored frames at 60fps.

Implement the Thomas tridiagonal solve in pure JavaScript (about 25
lines). Implement complex arithmetic on a (re, im) pair (no library).

Runtime sanity checks to console:
- Mode A: at E/V_0 = 0.5, V_0 = 5, L = 5, T_exact should equal a
  specific value (compute it once and pin); T_WKB should be off by
  a factor of order unity.
- Mode C: before the wave packet reaches the barrier, sum |psi|^2 dx
  should equal 1 within 1e-5.
- Mode C: after the wave packet has fully passed through (or been
  absorbed), the fraction R = integral right of barrier, T = integral
  left of barrier, should satisfy R + T + absorbed = 1.

Comments at every non-trivial physics step. Pure functions for the
WKB integral and the Crank-Nicolson step.
```

### Part 4 — Exploration tasks and extension prompt

Run the simulation and answer the following:

1. Stationary mode. Set $V_0 = 5$, $L = 5$. Note that the exact and WKB curves are parallel on the log axis below the barrier. Read off the offset: $T_{\text{exact}}/T_{\text{WKB}}$ at $E/V_0 = 0.5$. Compare to the analytical prediction $16E(V_0 - E)/V_0^2 = 16 \cdot 0.5 \cdot 0.5/1 = 4$. The simulation should give a factor of about 4.

2. Stationary mode. Vary $L$ from 1 to 10. The slope of $T(E)$ on the log axis steepens. This is the exponential sensitivity to barrier width. Quantify: by what factor does $T$ at $E/V_0 = 0.5$ change when $L$ doubles?

3. Barrier-shape mode. Switch to the double-barrier configuration. Watch for resonant tunneling peaks where $T \to 1$. Find one of these peaks and identify the energy. (The condition: the inter-barrier well supports a bound state at that energy.)

4. Wave packet mode. Set $V_0 = 5$, $L = 5$, $p_0 = 2$ (so $E = 2$, well below $V_0$). Play. The wave packet hits the barrier, most of it reflects, a small piece emerges on the right. The transmitted bump should be visibly attenuated relative to the reflected one. *Watch this run; this is the moment to record what you see in your own words.*

5. Wave packet mode. Increase $p_0$ to $\sqrt{2\cdot 5} \approx 3.16$ (so $E = V_0$). The wave packet hits the barrier; you should see substantial transmission and reflection — both fragments comparable in amplitude. Increase $p_0$ further (so $E > V_0$); the wave packet mostly transmits with small reflection fringes.

6. Wave packet mode. Try a very wide wave packet ($\sigma_x = 10$) and a very narrow one ($\sigma_x = 1$). The wide packet has narrow momentum spread and gives the cleanest tunneling picture; the narrow packet has broad momentum spread and shows mixed tunneling/over-barrier behavior. Explain why in your own words.

**Extension prompt:**

```
Modify 11-tunneling-simulator.html to add a Geiger-Nuttall mode:

GEIGER-NUTTALL MODE
Compute the alpha-decay halflife as a function of alpha energy for a
fixed daughter charge Z_daughter (slider, integer 80 to 92). Use the
Coulomb-barrier Gamow factor:
  gamma(E) = (1/hbar) integral_R^{r_c} sqrt(2 m_alpha (V(r) - E)) dr
with V(r) = 2 Z_daughter e^2 / (4 pi eps_0 r), R = 1.2 * A^(1/3) fm
(use A = 2 Z_daughter + a slider for neutron excess), r_c = V/E inverse.
Plot log10(tau_1/2) vs. 1/sqrt(E_alpha) for E_alpha from 4 to 9 MeV.
Should yield a straight line — the Geiger-Nuttall correlation.

Overlay experimental data for at least 5 actual isotopes (look up from
NNDC or Wikipedia tables); plot as marker points. Compare slope and
intercept to the WKB prediction.

Update PROJECT.md to mark Chapter 11 as complete and note that this
simulation closes Act Three — the methods chapters that took the
student from "I can solve textbook problems" to "I can attack real
physics."
```

---

## Exercises

### Warm-up

**11.1** State the WKB validity condition $|d\lambda_\text{dB}/dx| \ll 1$ in words. Then explain in one sentence why it fails at a classical turning point. For each of the following potentials, sketch $\lambda_\text{dB}(x) = h/p(x)$ qualitatively and identify any regions where WKB will break down: (a) a harmonic oscillator at energy $E$; (b) a flat-topped rectangular barrier at energy $E < V_0$; (c) a linear potential $V = Fx$ with $F > 0$. *(Tests: ability to apply the validity condition and identify its failure modes in specific potentials.)*

**11.2** For the harmonic oscillator $V = \frac{1}{2}m\omega^2 x^2$, the classical turning points at energy $E$ are $x = \pm\sqrt{2E/m\omega^2}$. (a) Compute the phase-space area $\oint p\,dx$ enclosed by the orbit at energy $E$ — this is the area of an ellipse with semi-axes $\sqrt{2mE}/m\omega$ in $x$ and $\sqrt{2mE}$ in $p$. (b) Apply the Bohr-Sommerfeld condition $\oint p\,dx = (n+1/2)h$ and verify you recover $E_n = (n+1/2)\hbar\omega$ exactly. (c) State in one sentence why the WKB result here is exact rather than approximate. *(Tests: phase-space area calculation; Bohr-Sommerfeld applied to the harmonic oscillator; understanding which symmetries make WKB exact.)*

**11.3** Derive the exact transmission coefficient $T_\text{exact}$ for a rectangular barrier of height $V_0$ and width $L$ at energy $E < V_0$. Match the wave function and its derivative at $x = 0$ and $x = L$, using $\psi = Ae^{ikx} + Be^{-ikx}$ for $x < 0$, $\psi = Ce^{\kappa x} + De^{-\kappa x}$ for $0 < x < L$, and $\psi = Fe^{ikx}$ for $x > L$. Show that $T = |F/A|^2$ gives the formula quoted in the chapter. *(Tests: boundary-matching calculation; extraction of the transmission coefficient from wave function continuity conditions.)*

### Application

**11.4** An electron with kinetic energy $E = 1\,\text{eV}$ hits a rectangular barrier of height $V_0 = 5\,\text{eV}$ and width $L = 5\,\text{Å}$. (a) Compute $\kappa = \sqrt{2m_e(V_0 - E)}/\hbar$ and verify $\kappa \approx 1.0\,\text{Å}^{-1}$. (b) Compute $T_\text{WKB} = e^{-2\kappa L}$. (c) Compute $T_\text{exact}$ using the formula from 11.3. (d) Find the prefactor ratio $T_\text{exact}/T_\text{WKB}$ and compare to the predicted value $16E(V_0-E)/V_0^2$. *(Tests: numerical WKB and exact transmission; identification of the missing prefactor.)*

**11.5** An STM tip is held $d = 5\,\text{Å}$ above a nickel surface with work function $\phi = 5\,\text{eV}$. (a) Compute $\kappa = \sqrt{2m_e\phi}/\hbar$ in Å$^{-1}$. (b) Compute the factor by which the tunneling current changes when $d$ decreases by 1 Å. (c) A surface atom protrudes 0.5 Å above the surrounding surface. By what factor does the tunneling current differ when the tip is directly over the atom vs. over the flat region? (d) Explain in one sentence why this exponential sensitivity makes sub-angstrom topographic imaging possible. *(Tests: STM current calculation; connecting the Gamow factor to spatial resolution.)*

**11.6** Estimate the Gamow factor for an alpha particle ($m_\alpha = 4\,\text{u}$, $u = 1.66\times 10^{-27}\,\text{kg}$) of energy $E_\alpha = 5.5\,\text{MeV}$ tunneling through the Coulomb barrier of a daughter nucleus with $Z' = 82$ (lead). Use the approximation $\gamma \approx (\pi Z'e^2/4\epsilon_0\hbar)\sqrt{m_\alpha/2E_\alpha}$. Then estimate the halflife using attempt frequency $\nu_0 = 10^{21}\,\text{Hz}$. Compare to the uranium-238 case computed in the chapter. *(Tests: Gamow factor calculation for the Coulomb barrier; halflife estimate; understanding how the exponent controls 24 orders of magnitude.)*

### Synthesis

**11.7** The Geiger-Nuttall law. (a) Starting from $\log_{10}\tau_{1/2} \approx A(Z') + B(Z')/\sqrt{E_\alpha}$, show that if $\gamma \propto Z'/\sqrt{E_\alpha}$, the log of the halflife is indeed linear in $1/\sqrt{E_\alpha}$ for fixed $Z'$. (b) For polonium-212 ($Z' = 82$, $E_\alpha = 8.78\,\text{MeV}$, $\tau_{1/2} = 3\times 10^{-7}\,\text{s}$) and thorium-232 ($Z' = 90$, $E_\alpha = 4.08\,\text{MeV}$, $\tau_{1/2} = 1.4\times 10^{10}\,\text{yr}$), plot these two points on a $\log_{10}\tau$ vs. $1/\sqrt{E_\alpha}$ graph. The ratio of halflives is $10^{24}$; the ratio of $1/\sqrt{E_\alpha}$ values is only about 1.5. From this, estimate the coefficient $B$ in the Geiger-Nuttall formula and compare to the WKB prediction. *(Tests: derivation of the linear Geiger-Nuttall form from the Gamow factor; numerical check against two known isotopes; connecting the 24-decade range to the exponent.)*

**11.8** The cold fusion back-of-envelope. (a) At room temperature $T = 300\,\text{K}$, compute $kT$ in eV. (b) The Coulomb barrier for D-D fusion is $V_\text{max} \approx e^2/(4\pi\epsilon_0 r_0)$ where $r_0 \approx 2\,\text{fm}$ is the nuclear-contact distance. Compute $V_\text{max}$ in MeV. (c) Using the approximate Gamow factor $\gamma \approx (\pi e^2/4\epsilon_0\hbar)\sqrt{m_D/2kT}$, compute $\gamma$ and the tunneling probability $e^{-2\gamma}$ at room temperature. Express the result as a power of 10. (d) The claimed power output of 1 W in 1 cm³ of palladium requires roughly $10^{12}$ fusion events per second. Show that the required tunneling rate is inconsistent with your Gamow factor by many orders of magnitude. *(Tests: using the Gamow factor as a falsification tool; order-of-magnitude estimation; recognizing when the exponent decisively refutes a claim.)*

### Challenge

**11.9** The Gamow peak in stellar fusion. The rate per particle pair of pp fusion is proportional to $\int_0^\infty e^{-E/kT} \cdot e^{-b/\sqrt{E}}\,dE$ where $b = \pi e^2\sqrt{2m_p}/(4\epsilon_0\hbar)$ for proton-proton fusion. (a) Show that the integrand has a maximum at $E_G = (bkT/2)^{2/3}$, which is called the Gamow peak energy. (b) For the Sun's core at $T = 1.5\times 10^7\,\text{K}$, compute $kT$ in keV, then compute $b$ in keV$^{1/2}$, then compute $E_G$ in keV. (c) Compare $E_G$ to $kT$: the ratio tells you how far into the thermal tail the dominant fusion occurs. (d) Explain in one paragraph why this intermediate energy — neither the thermal energy nor the barrier height — is where fusion is concentrated. *(Tests: locating the maximum of the thermal-times-tunneling integrand; numerical evaluation of the Gamow peak; understanding why the peak sits between kT and V_max.)*

**11.10** WKB quantization beyond the harmonic oscillator. Consider the potential $V(x) = \alpha|x|^n$ for integer $n \geq 1$. (a) Show that the Bohr-Sommerfeld condition gives $E_m \propto m^{2n/(n+2)}$ for large quantum number $m$. (Hint: change variables in $\int_a^b \sqrt{2m_\text{particle}(E-V)}\,dx$ to reduce to a dimensionless integral, then use the scaling of $a$ and $b$ with $E$.) (b) Verify the $n=2$ (harmonic) case gives $E_m \propto m$. (c) For the linear potential $n=1$, what is the energy scaling? (d) For $n \to \infty$, the potential approaches a square well. What does the formula predict for $E_m$ in that limit, and does it agree with the exact square-well result $E_m \propto m^2$? *(Tests: WKB applied to a general power-law potential; dimensional analysis in the phase-space integral; checking limiting cases against exactly solvable problems.)*

---

*Sources: Griffiths §9.1–9.3; Liboff §7.7, §7.10; Gamow, "Zur Quantentheorie des Atomkernes," Zeitschrift für Physik 51, 204 (1928); Gurney & Condon, Nature 122, 439 (1928); Physical Review 33, 127 (1929); Geiger & Nuttall, Phil. Mag. 22, 613 (1911); 23, 439 (1912); Binnig & Rohrer, Physical Review Letters 49, 57 (1982); Atkinson & Houtermans, Z. Phys. 54, 656 (1929); Löwdin, Rev. Mod. Phys. 35, 724 (1963); Slocombe et al., Communications Physics 5, 109 (2022); Fowler & Nordheim, Proc. R. Soc. A 119, 173 (1928); Bender & Orszag, Advanced Mathematical Methods for Scientists and Engineers (1978), Chapter 10.*
