# Chapter 3 — The Harmonic Oscillator
*The one problem that hides inside every other problem.*

---

Here is something that should bother you. You can write down the potential for a pendulum, a diatomic molecule, a tuning fork, a bridge cable vibrating in the wind, an electromagnetic field mode in a laser cavity, a crystal lattice vibrating at low temperature — and in every single case, if you expand that potential around its minimum and keep only the first non-trivial term, you get the same equation. One equation. The same one every time. Either physics is conspiring against variety, or something deep is going on.

Something deep is going on. Near a stable equilibrium, *any* smooth potential looks like a parabola. That is just calculus: the first derivative vanishes at a minimum, so the quadratic term is what survives. Set $m\omega^2 = V''(x_0)$ and you have the harmonic oscillator every time, for any system, for any potential, as long as the oscillation is small. This is why the harmonic oscillator is not just an example in quantum mechanics. It is the universal model for small vibrations everywhere in physics.

<!-- → [INFOGRAPHIC: Grid of six physical systems — pendulum, diatomic molecule, tuning fork, bridge cable, laser cavity mode, crystal lattice — each with a sketch of its potential V(x); arrows pointing from each to a single shared quadratic V(x) ≈ (1/2)kx² at the bottom, with caption "Near any minimum, every smooth potential reduces to the same equation"] -->

The Hamiltonian is

$$\hat{H} = \frac{\hat{p}^2}{2m} + \frac{1}{2}m\omega^2\hat{x}^2.$$

Two terms. One kinetic, one quadratic in position. We are going to find every energy level, every eigenstate, and the classical-looking oscillation — without solving a single differential equation. Well, almost: one first-order ODE at the end, which takes twenty seconds. Everything else falls out of algebra.

---

## The trick

Let me factor the Hamiltonian. Not approximately. Exactly.

Define two operators:

$$\hat{a}_\pm = \frac{1}{\sqrt{2\hbar m\omega}}\bigl(\mp i\hat{p} + m\omega\hat{x}\bigr).$$

These look like someone concatenated two formulas that don't belong together. Bear with it. Compute $\hat{a}_-\hat{a}_+$:

$$\hat{a}_-\hat{a}_+ = \frac{1}{2\hbar m\omega}\bigl(i\hat{p} + m\omega\hat{x}\bigr)\bigl(-i\hat{p} + m\omega\hat{x}\bigr).$$

Expand the product. You get $\hat{p}^2 + m^2\omega^2\hat{x}^2$ plus the cross terms $im\omega(\hat{p}\hat{x} - \hat{x}\hat{p})$. Those cross terms are $im\omega$ times a commutator. And we know that commutator: $[\hat{x},\hat{p}] = i\hbar$, so $\hat{p}\hat{x} - \hat{x}\hat{p} = -i\hbar$. The cross terms become $m\omega\hbar$. Clean up:

$$\hat{a}_-\hat{a}_+ = \frac{\hat{H}}{\hbar\omega} + \frac{1}{2}.$$

Or equivalently,

$$\hat{H} = \hbar\omega\!\left(\hat{a}_-\hat{a}_+ - \frac{1}{2}\right) = \hbar\omega\!\left(\hat{a}_+\hat{a}_- + \frac{1}{2}\right).$$

The two forms differ because $\hat{a}_-$ and $\hat{a}_+$ do not commute. Subtract:

$$[\hat{a}_-, \hat{a}_+] = 1.$$

That is the whole thing. Every energy level, every eigenstate, every expectation value in this chapter is a consequence of that one commutator. From $[\hat{a}_-, \hat{a}_+] = 1$, the entire spectrum of the harmonic oscillator drops out without any further differential equations.

---

## Climbing the ladder

Suppose $|n\rangle$ is an energy eigenstate with energy $E_n$. Ask what energy $\hat{a}_+|n\rangle$ has. Compute $\hat{H}(\hat{a}_+|n\rangle)$ using the commutator $[\hat{H}, \hat{a}_+] = \hbar\omega\,\hat{a}_+$, which follows directly from $[\hat{a}_-, \hat{a}_+] = 1$:

$$\hat{H}(\hat{a}_+|n\rangle) = (\hat{a}_+\hat{H} + [\hat{H}, \hat{a}_+])|n\rangle = (E_n + \hbar\omega)\,\hat{a}_+|n\rangle.$$

So $\hat{a}_+|n\rangle$ is an eigenstate with energy $E_n + \hbar\omega$. The operator $\hat{a}_+$ climbs up by exactly one quantum of energy. The same argument with $\hat{a}_-$ gives energy $E_n - \hbar\omega$. They are a raising operator and a lowering operator. A ladder.

<!-- → [DIAGRAM: Vertical energy ladder with evenly spaced rungs labeled E_0 = ℏω/2, E_1 = 3ℏω/2, E_2 = 5ℏω/2, ..., E_n = (n+½)ℏω — upward arrow labeled â₊ "raises by ℏω", downward arrow labeled â₋ "lowers by ℏω"; ground rung marked with a barrier below it labeled "â₋|0⟩ = 0 — cannot descend further"] -->

---

## Why the ladder terminates downward

Here is the constraint that gives us the ground state. The Hamiltonian $\hat{H} = \hat{p}^2/2m + (1/2)m\omega^2\hat{x}^2$ is a sum of squares of Hermitian operators. Its expectation value in any state is non-negative. Energies cannot go below zero.

But the lowering operator $\hat{a}_-$ subtracts $\hbar\omega$ each time you apply it. Something has to stop. The only way the descent terminates is if there exists a state $|0\rangle$ that $\hat{a}_-$ kills:

$$\hat{a}_-|0\rangle = 0.$$

This is the ground state. Its energy: apply $\hat{a}_+$ to both sides, use $\hat{H} = \hbar\omega(\hat{a}_+\hat{a}_- + 1/2)$:

$$\hat{H}|0\rangle = \hbar\omega\!\left(\hat{a}_+\hat{a}_- + \frac{1}{2}\right)|0\rangle = \frac{1}{2}\hbar\omega\,|0\rangle.$$

The ground-state energy is $E_0 = \hbar\omega/2$.

This is not zero. The classical minimum-energy state is the particle sitting at rest at the bottom of the well — kinetic energy zero, potential energy zero, total energy zero. The quantum ground state has energy $\hbar\omega/2$, and it cannot be reduced. Try to make it zero: that would require $\sigma_x = 0$ and $\sigma_p = 0$ simultaneously, which the uncertainty principle forbids. The zero-point energy is the cost of confinement. Squeeze the particle into the well and it fights back with kinetic energy it cannot shed.

This is not a theoretical artifact. The Casimir force between two conducting plates — an attractive force measured in the lab, explained by the difference between zero-point energies of electromagnetic modes with and without the plates — is a macroscopic consequence of exactly this machinery. Lamoreaux measured it in 1997 to within roughly 5% of the theoretical prediction. Liquid helium does not solidify at atmospheric pressure even at temperatures near absolute zero because zero-point vibrational energy of the helium atoms is enough to prevent crystallization. Zero-point energy is real and it has a bill you can read.

---

## The whole spectrum

From $|0\rangle$, apply $\hat{a}_+$ once to get $|1\rangle$ with energy $\hbar\omega/2 + \hbar\omega = 3\hbar\omega/2$. Apply it again: $|2\rangle$ with $5\hbar\omega/2$. The pattern:

$$E_n = \left(n + \frac{1}{2}\right)\hbar\omega, \quad n = 0, 1, 2, \ldots$$

Equally spaced. The spacing is exactly $\hbar\omega$ — one quantum at a time. This is why an infrared spectrum of HCl shows a single sharp line: the molecule is a near-harmonic oscillator, all adjacent vibrational levels are equally spaced, and a photon can only drive a single transition. The spectrum is a ruler.

<!-- → [IMAGE: Schematic infrared absorption spectrum of HCl — a single dominant peak near 2886 cm⁻¹ against a flat baseline, with annotation showing the spacing ΔE = ℏω and a note that the equal spacing is a direct consequence of the ladder algebra] -->

Normalize the ladder relations — the prefactors that keep $|n\rangle$ unit-normalized as you climb:

$$\hat{a}_+|n\rangle = \sqrt{n+1}\,|n+1\rangle, \quad \hat{a}_-|n\rangle = \sqrt{n}\,|n-1\rangle.$$

Notice what we did not do: solve a differential equation, impose boundary conditions, guess a series form, match coefficients. We wrote down one commutator, used the non-negativity of $\hat{H}$, and the entire spectrum fell out. The algebra carried everything.

---

## What the eigenstates look like

The spectrum is clean. The wave functions are worth seeing explicitly. In the position representation, the condition $\hat{a}_-|0\rangle = 0$ becomes a first-order ODE. Substituting $\hat{p} = -i\hbar\,\partial_x$:

$$\bigl(\hbar\,\partial_x + m\omega x\bigr)\psi_0(x) = 0.$$

Separate:

$$\frac{d\psi_0}{\psi_0} = -\frac{m\omega}{\hbar}x\,dx.$$

Integrate, normalize:

$$\psi_0(x) = \left(\frac{m\omega}{\pi\hbar}\right)^{1/4}\exp\!\left(-\frac{m\omega x^2}{2\hbar}\right).$$

A Gaussian. The ground state of the harmonic oscillator is just the minimum-uncertainty Gaussian from Chapter 1 — same shape, same saturation of $\sigma_x\sigma_p = \hbar/2$. That is not a coincidence. The coherent state discussion at the end of this chapter will make the connection explicit.

Higher states follow by applying $\hat{a}_+$ repeatedly. Each application multiplies the Gaussian by a polynomial one degree higher. Those polynomials are the Hermite polynomials $H_n(\xi)$, where $\xi = \sqrt{m\omega/\hbar}\,x$:

$$\psi_n(x) = \left(\frac{m\omega}{\pi\hbar}\right)^{1/4}\frac{1}{\sqrt{2^n n!}}\,H_n(\xi)\,e^{-\xi^2/2}$$

with $H_0 = 1$, $H_1 = 2\xi$, $H_2 = 4\xi^2 - 2$, $H_3 = 8\xi^3 - 12\xi$, and the recursion $H_{n+1}(\xi) = 2\xi H_n(\xi) - 2n H_{n-1}(\xi)$.

<!-- → [IMAGE: Six stacked panels showing ψ_n(x) for n = 0..5 plotted inside the parabolic well V(x) — each eigenfunction drawn at its energy level E_n, classical turning points marked with vertical ticks, node count labeled for each; student should see that ψ_n has exactly n nodes and that the wave function tunnels visibly beyond the turning points] -->

Two things to notice:

The $n$-th eigenstate has exactly $n$ nodes — zero crossings, not counting the tails at $\pm\infty$. The ground state has none. The first excited state has one. This is the same counting rule as the infinite square well.

The probability density $|\psi_n|^2$ is a stranger thing than its classical cousin. A classical harmonic oscillator spends most of its time near the turning points, where it slows down, and least time at the bottom, where it moves fastest. The quantum ground state is the opposite: $|\psi_0|^2$ peaks at $x = 0$ and falls off. It takes a large quantum number — large $n$ — for the oscillating density to begin averaging out to the classical distribution. That convergence, the quantum probability washing out to the classical one as $n \to \infty$, is the correspondence principle in this system.

<!-- → [CHART: Side-by-side comparison of |ψ_n(x)|² for n = 1 and n = 20 — left panel shows quantum density peaking at center; right panel shows the oscillating density for n=20 with the classical turning-point distribution overlaid as a smooth curve, demonstrating convergence; caption: "The correspondence principle: at large n, quantum averages to classical"] -->

One more fact: roughly 16% of the ground-state probability density sits outside the classical turning points. The classical particle with energy $\hbar\omega/2$ cannot go beyond $x = \pm\sqrt{\hbar/m\omega}$ — it would need kinetic energy it does not have. The quantum ground state ignores this and tunnels anyway. Quantum tunneling is not exotic; it begins with the very first eigenstate.

---

## Expectation values without integrals

Here is a demonstration of what the ladder algebra buys you. Express position and momentum in terms of the ladder operators:

$$\hat{x} = \sqrt{\frac{\hbar}{2m\omega}}\,(\hat{a}_+ + \hat{a}_-), \quad \hat{p} = i\sqrt{\frac{m\hbar\omega}{2}}\,(\hat{a}_+ - \hat{a}_-).$$

Now $\langle n|\hat{x}|n\rangle$: $\hat{a}_+|n\rangle = \sqrt{n+1}\,|n+1\rangle$ and $\hat{a}_-|n\rangle = \sqrt{n}\,|n-1\rangle$, both orthogonal to $|n\rangle$, so the inner product is zero. No integral needed. Same for $\langle n|\hat{p}|n\rangle = 0$.

For the variance, compute $\langle n|\hat{x}^2|n\rangle$. Write $\hat{x}^2 = (\hbar/2m\omega)(\hat{a}_+ + \hat{a}_-)^2$ and expand. The terms $\hat{a}_+^2$ and $\hat{a}_-^2$ shift by two levels and drop from the diagonal; the remaining terms $\hat{a}_+\hat{a}_-$ and $\hat{a}_-\hat{a}_+$ give $n$ and $n+1$ respectively:

$$\langle n|\hat{x}^2|n\rangle = \frac{\hbar}{2m\omega}(2n+1).$$

Similarly for $\hat{p}^2$. The uncertainty product:

$$\sigma_x\sigma_p = \left(n + \frac{1}{2}\right)\hbar.$$

For $n = 0$: exactly $\hbar/2$, the minimum. For higher $n$: the product grows. The ground state is the only eigenstate that saturates the uncertainty bound. For every excited state, the position and momentum distributions are less tightly correlated than they could be.

<!-- → [CHART: σ_x · σ_p / (ℏ/2) plotted vs. n for n = 0..10 — a straight line starting at 1.0 for n=0 and rising linearly; horizontal dashed line at 1.0 labeled "Heisenberg minimum"; annotation showing the ground state is the only eigenstate that saturates the bound] -->

No integrals. No Hermite polynomials needed. The algebra carried everything.

---

## Eigenstates do not oscillate — and this is crucial to understand

Here is the misconception this chapter must kill before the simulation is built, because if you do not kill it now it will come back to haunt you.

A harmonic oscillator is, classically, an oscillator. The position of the particle oscillates back and forth at frequency $\omega$. You expect the quantum version to do the same. Build the time-dependent eigenstate:

$$\Psi_n(x,t) = \psi_n(x)\,e^{-iE_n t/\hbar}.$$

The time dependence is a phase factor. Compute the probability density:

$$|\Psi_n(x,t)|^2 = |\psi_n(x)|^2\,|e^{-iE_n t/\hbar}|^2 = |\psi_n(x)|^2.$$

Static. The phase rotates in the complex plane, but $|\psi_n(x)|^2$ does not change at all. An energy eigenstate of the harmonic oscillator is, in every observable respect, sitting still. Nothing sloshes. If quantum mechanics only had eigenstates, classical oscillation would never emerge from it.

This is not a problem with the formalism. It is a feature. The eigenstates are stationary states; that is their definition. The oscillation is a property of *superpositions* of eigenstates, where the different phase factors beat against each other. Take $\Psi = (\psi_0 + \psi_1)/\sqrt{2}$:

$$|\Psi(x,t)|^2 = \frac{1}{2}\bigl(|\psi_0|^2 + |\psi_1|^2\bigr) + \mathrm{Re}\!\left[\psi_0\psi_1^*\,e^{-i(E_0-E_1)t/\hbar}\right].$$

The cross-term beats at $(E_1 - E_0)/\hbar = \omega$. The probability density sloshes at exactly the classical frequency. But it also distorts — a two-state superposition does not maintain its shape. This is where coherent states come in.

<!-- → [IMAGE: Three-frame time sequence showing |Ψ(x,t)|² for the equal superposition (ψ₀ + ψ₁)/√2 at t = 0, T/4, T/2 — student should see the density shifting left and right while also visibly distorting in shape, motivating why a two-state superposition is not a clean classical oscillator] -->

---

## The quantum state that sloshes cleanly

A **coherent state** $|\alpha\rangle$ is an eigenstate of the lowering operator:

$$\hat{a}_-|\alpha\rangle = \alpha\,|\alpha\rangle$$

for any complex number $\alpha$. It is not an energy eigenstate. Its energy is uncertain — the probability of finding $n$ quanta is Poisson-distributed with mean $\langle n \rangle = |\alpha|^2$. But its time evolution is controlled:

$$\langle\hat{x}(t)\rangle = \sqrt{\frac{2\hbar}{m\omega}}\,|\alpha|\cos(\omega t - \arg\alpha), \quad \langle\hat{p}(t)\rangle = -\sqrt{2m\hbar\omega}\,|\alpha|\sin(\omega t - \arg\alpha).$$

Position and momentum oscillate sinusoidally at frequency $\omega$, exactly as a classical oscillator would. And the wave-packet shape: $\sigma_x\sigma_p = \hbar/2$ at all times. The packet stays a Gaussian with the same width as the ground state, riding its classical orbit without spreading or distorting. It just oscillates.

The coherent state in the energy basis is

$$|\alpha\rangle = e^{-|\alpha|^2/2}\sum_{n=0}^\infty \frac{\alpha^n}{\sqrt{n!}}\,|n\rangle.$$

Two limiting cases: $|\alpha| = 0$ gives $|0\rangle$, the ground state. $|\alpha| \to \infty$ gives a state with a large, well-defined energy that oscillates with large amplitude. The classical oscillator is the $|\alpha| \to \infty$ limit of the coherent state.

<!-- → [IMAGE: Phase-space diagram showing the coherent state orbit — a circle of radius |α| centered at the origin in the (⟨x⟩, ⟨p⟩) plane, with a filled Gaussian blob riding the circle; a second smaller circle at |α| = 0 collapsed to a point (the ground state); arrows indicating clockwise rotation at frequency ω] -->

Roy Glauber introduced coherent states in their modern form in a 1963 paper on the theory of laser light. The physical point: a laser, ideally, produces electromagnetic field modes in coherent states. The intensity fluctuations of ideal laser light follow a Poisson distribution — not because the light is classical, but because that is what coherent states predict. Glauber won the Nobel Prize in 2005 for this work. The connection between this simple harmonic oscillator algebra and the quantum theory of light is not a metaphor; it is the same mathematics, with $\hat{a}_\pm$ reinterpreted as photon creation and annihilation operators.

One thing coherent states are not: classical states. They are minimum-uncertainty quantum states with classical-like expectation values. The difference matters when you squeeze them — reduce the uncertainty in one quadrature at the cost of the other — which is what LIGO does to push below the standard quantum limit in gravitational-wave detection. Squeezed light is a different minimum-uncertainty state, not a coherent state. The hierarchy is: coherent states are the most classical-like quantum states of the harmonic oscillator; squeezed states push further at a price.

---

## The ladder again, differently

Before the simulation, a moment to see what just happened across this chapter.

The harmonic oscillator has an evenly spaced energy spectrum $E_n = (n+1/2)\hbar\omega$. That spacing is not a coincidence of the Gaussian; it is a consequence of the single commutator $[\hat{a}_-,\hat{a}_+]=1$, which follows from $[\hat{x},\hat{p}]=i\hbar$. The ground-state energy is $\hbar\omega/2$ because the uncertainty principle will not allow zero energy in a confined space.

The algebraic method here — factor the Hamiltonian into ladder operators, derive everything from a commutator — is not a trick specific to this problem. In Chapter 4 it becomes the standard language for quantum mechanics. In quantum field theory $\hat{a}_\pm$ become creation and annihilation operators for particles; the vacuum is the state annihilated by all lowering operators; a state of $n$ particles is $(\hat{a}_+)^n$ applied to the vacuum. The harmonic oscillator algebra is the skeleton on which quantum field theory is built. This chapter is not a special case. It is the template.

---

## LLM Exercise — the harmonic oscillator simulation

You are going to build a single-file D3 simulation that displays the harmonic-oscillator eigenstates, lets you watch a coherent state slosh, and lets you compare a static eigenstate to a dynamic superposition side by side. The deliverable is `03-harmonic-oscillator.html` in your working directory.

### Part 1 — Update `PROJECT.md`

```
Append a new entry to PROJECT.md describing this chapter's simulation:

Chapter 03 — The Harmonic Oscillator
Deliverable: 03-harmonic-oscillator.html
Status: in progress

The simulation displays the quantum harmonic oscillator with three panels:
1. Wave function psi_n(x) plotted against position, stacked at energy E_n inside
   the parabolic potential well V(x) = (1/2) m omega^2 x^2.
2. Probability density |psi(x,t)|^2 as a filled region.
3. A small phase-space inset showing <x>(t) vs <p>(t) for the active state.

Three modes selectable via radio buttons or tabs:
- Eigenstate n: pick n in 0..5, watch the static probability density.
- Coherent state alpha: complex alpha via |alpha| and arg(alpha) sliders;
  watch the wave packet slosh.
- Two-state superposition: pick n1, n2 and complex c1, c2; watch the
  interference beat at frequency (E_{n2} - E_{n1})/hbar.

Sliders: omega (0.5 to 5.0), n (0 to 5), |alpha| (0 to 3), arg(alpha) (0 to 2pi).
Buttons: play / pause / reset.
Toggles: show / hide energy levels, classical turning points, phase-space inset.

Natural units: hbar = m = 1. Length unit = sqrt(hbar/(m omega)).
Time unit = 1/omega. Render frame rate 60 fps via requestAnimationFrame.
```

### Part 2 — The CLAUDE.md amendment

```
Append to CLAUDE.md (coding constitution) the following physics rules for
Chapter 3 simulations:

HARMONIC OSCILLATOR PHYSICS RULES

1. Hermite polynomials are computed by recursion:
     H_{n+1}(xi) = 2 xi H_n(xi) - 2 n H_{n-1}(xi)
   with H_0 = 1, H_1 = 2 xi. Cache H_n across the spatial grid for each
   active n. Cap n at 15 for numerical stability; the naive recursion
   overflows double precision above this near the turning points.

2. Normalization: psi_n(x) = (m omega / pi hbar)^(1/4) * (1 / sqrt(2^n n!))
   * H_n(xi) * exp(-xi^2 / 2), where xi = sqrt(m omega / hbar) x.
   Precompute n! by lookup for n <= 15.

3. When omega slider changes, the natural length unit changes. Recompute
   the spatial grid in units of sqrt(hbar / (m omega)) AND renormalize.
   Failing to renormalize after an omega change is failure mode #2 below.

4. Time evolution: psi(x, t) = sum_n c_n psi_n(x) exp(-i E_n t / hbar)
   with E_n = (n + 1/2) hbar omega. Store complex c_n as {re, im} pairs;
   multiply by phase each frame; sum to get psi(x, t); compute |psi|^2.

5. For coherent states, c_n = exp(-|alpha|^2 / 2) * alpha^n / sqrt(n!).
   Truncate at n_max = ceil(|alpha|^2 + 5 sqrt(|alpha|^2)). Verify
   sum |c_n|^2 = 1 within 1e-4 as a runtime sanity check.

6. Animate |psi|^2 in the probability-density panel. Animate Re(psi) in
   the wave-function panel if "show real part" is toggled; otherwise show
   the static psi_n(x) for the eigenstate mode. Always label which is which.

7. Time step dt: choose dt such that omega * dt <= 0.05 per frame.
   If omega slides to 5, dt should be at most 0.01. Otherwise the phase
   per frame is too large and the visualization teleports.

KNOWN FAILURE MODES to avoid:
(a) Hermite overflow at large n. Mitigation: cap n; use scaled Hermites.
(b) Forgetting to renormalize on omega change.
(c) Phase sign errors in psi_n for odd n. Verify against H_1 = 2 xi
    (positive at xi > 0), H_3 = 8 xi^3 - 12 xi (verify the -12 xi term).
(d) Coherent-state truncation mismatched to |alpha|^2.
(e) Time step too large.
(f) Confusing animation of psi vs |psi|^2 (label both axes; show both
    when the user toggles between them).
```

### Part 3 — The simulation prompt

```
You are working in my directory which contains CLAUDE.md, DESIGN.md, and
PROJECT.md. Read all three first.

Build 03-harmonic-oscillator.html: a single self-contained HTML file using
D3 v7 from a CDN, no other dependencies, that implements the Chapter 3
simulation as specified in PROJECT.md and following the physics rules in
CLAUDE.md and the visual constitution in DESIGN.md.

The simulation has three panels arranged horizontally in one SVG of 1100 x 600:
- Panel A (left, 500 wide): wave function psi_n(x) or Re(psi(x, t)), plotted
  as a line. Y-axis: amplitude in natural units, ranging roughly -1 to +1.
  Behind the wave function: parabolic potential V(x) drawn as a dashed
  curve, energy levels E_n = (n + 1/2) hbar omega as horizontal lines for
  n = 0..5, classical turning points at xi_n = sqrt(2n+1) marked as small
  vertical ticks for the active n.
- Panel B (middle, 400 wide): probability density |psi(x, t)|^2, plotted
  as a filled area beneath a darker stroked outline.
- Panel C (right, 200 wide): phase-space inset, a square plot of <x>(t)
  vs <p>(t), with the orbit traced as a fading line and the current point
  marked. For an eigenstate the orbit is a single point at the origin;
  for a coherent state it is a circle of radius proportional to |alpha|.

Mode selector at the top: three buttons - "Eigenstate", "Coherent state",
"Superposition". Below them, the appropriate sliders for the active mode.
Play / pause / reset button below the panels.

Spatial grid: 401 points from -6 to +6 in natural units of sqrt(hbar/(m omega)).
Update <x> and <p> each frame as discrete sums over the grid:
  <x>(t) = sum_i x_i * |psi(x_i, t)|^2 * dx
  <p>(t) = Im(integral psi* dpsi/dx) computed as a finite difference.

Runtime sanity checks (write to console):
- Sum |psi(x_i, t)|^2 * dx should equal 1 within 0.001 at every frame.
- For an eigenstate, <x> and <p> should remain within 0.01 of zero.
- For a coherent state with |alpha| = 1 at t = 0 and arg(alpha) = 0, the
  initial <x> should be sqrt(2 hbar / (m omega)) (i.e., sqrt(2) in
  natural units).

Do NOT use any 3D library. Do NOT use math.js or numeric.js. Pure D3 +
vanilla JS arithmetic. Comments at every non-trivial physics step.
```

### Part 4 — Exploration tasks and extension prompt

Run the simulation and answer the following:

1. With $\omega = 1$, set the mode to "Eigenstate" and toggle $n$ from 0 to 5. Watch the probability density. Confirm: it does not move. Now switch to "Coherent state" with $|\alpha| = 1$. Watch the probability density slosh. Note the period $T = 2\pi/\omega$.

2. Increase $|\alpha|$ from $0$ to $3$ slowly. What happens to the amplitude of the orbit in phase space? What happens to the width of the wave packet? Predict before sliding; check after.

3. Set $|\alpha| = 0$. What state does the coherent state reduce to? Compare the wave function to the eigenstate $n = 0$.

4. Set the mode to "Superposition" with $n_1 = 0, n_2 = 1$, equal coefficients. Watch $|\psi|^2$. At what frequency does it slosh? Now try $n_1 = 0, n_2 = 2$. Does it slosh? Why or why not? (Hint: think about parity.)

5. Slide $\omega$ from 1 to 3 while the simulation is running in coherent-state mode. What happens to the spatial extent of the wave packet? What happens to the period of oscillation?

**Extension prompt:**

```
Modify 03-harmonic-oscillator.html to add a fourth panel showing a
Wigner-function pseudo-image of the current state: a heatmap on the
(x, p) plane where bright spots correspond to high quasi-probability.
For coherent states, the Wigner function is a positive Gaussian centered
at (<x>, <p>) and rotating around the origin at frequency omega. For
eigenstates n >= 1, the Wigner function has negative regions (non-classical
signature). Compute the Wigner function as

  W(x, p) = (1 / (pi hbar)) integral psi*(x + y) psi(x - y) exp(2 i p y / hbar) dy

discretized on a 51 x 51 grid in (x, p). Use d3.contour() to render
the contours; show negative regions in a different color from positive.
Update PROJECT.md to mark Chapter 03 as complete and note the Wigner
extension as the bridge to Chapter 4 (where phase-space representation
of operators becomes central).
```

---

## Still puzzling

The infinity that disappears when you compute Casimir differences is one of the most well-behaved infinities in physics. You take the zero-point energy sum with plates minus without, and the difference is finite and measurable. The infinity that does not disappear — the vacuum energy density of the universe, computed by summing zero-point energies of all quantum fields up to the Planck scale — exceeds the observed cosmological constant by roughly 120 orders of magnitude. The same harmonic-oscillator machinery, applied to two different problems, gives one of physics' cleanest predictions and one of its deepest open questions. I do not know what fixes the second case. Neither does anyone else.

---

## Exercises

**Warm-up**

1. *[Tests: commutator algebra, ladder operator definition]* Starting from $[\hat{x}, \hat{p}] = i\hbar$ and the definitions $\hat{a}_\pm = (1/\sqrt{2\hbar m\omega})(\mp i\hat{p} + m\omega\hat{x})$, verify $[\hat{a}_-, \hat{a}_+] = 1$ explicitly by writing out the product $\hat{a}_-\hat{a}_+ - \hat{a}_+\hat{a}_-$ and substituting. Show every step. *Difficulty: warm-up.*

2. *[Tests: Hermite polynomial recursion, node counting]* Using the recursion $H_{n+1}(\xi) = 2\xi H_n(\xi) - 2n H_{n-1}(\xi)$ with $H_0 = 1$, $H_1 = 2\xi$, compute $H_2$, $H_3$, and $H_4$ explicitly. For each, count the number of real roots and verify it matches $n$. *Difficulty: warm-up.*

3. *[Tests: stationary state, time evolution of probability density]* Write down $|\Psi_n(x,t)|^2$ for the harmonic oscillator eigenstate. Show algebraically that it is independent of time. Then explain in one sentence what "stationary state" means physically — not mathematically. *Difficulty: warm-up.*

**Application**

4. *[Tests: zero-point energy, uncertainty principle connection]* A diatomic nitrogen molecule N₂ has a vibrational frequency of approximately $\omega \approx 4.45 \times 10^{14}$ rad/s. (a) Compute the zero-point vibrational energy $E_0 = \hbar\omega/2$ in eV. (b) Compute the thermal energy $k_BT$ at room temperature (300 K). (c) Are most N₂ molecules in the vibrational ground state at room temperature? Justify by comparing $E_0$ and $k_BT$ to the level spacing $\hbar\omega$. *Difficulty: application.*

5. *[Tests: ladder algebra for expectation values]* Using $\hat{x} = \sqrt{\hbar/2m\omega}(\hat{a}_+ + \hat{a}_-)$ and the normalized ladder relations $\hat{a}_+|n\rangle = \sqrt{n+1}|n+1\rangle$, $\hat{a}_-|n\rangle = \sqrt{n}|n-1\rangle$: (a) Compute $\langle n|\hat{x}^3|n\rangle$ without integrals. (b) Compute the matrix element $\langle m|\hat{x}|n\rangle$ for general $m, n$ and state which values of $m-n$ give non-zero results. *Difficulty: application.*

6. *[Tests: coherent state structure, Poisson distribution]* For the coherent state $|\alpha\rangle = e^{-|\alpha|^2/2}\sum_n (\alpha^n/\sqrt{n!})|n\rangle$: (a) Compute $\langle \hat{n}\rangle = \langle\alpha|\hat{a}_+\hat{a}_-|\alpha\rangle$ and show it equals $|\alpha|^2$. (b) Compute $\langle\hat{n}^2\rangle$ using $\hat{n}^2 = \hat{a}_+\hat{a}_-\hat{a}_+\hat{a}_-$ and the commutator. (c) Show the variance $\langle\hat{n}^2\rangle - \langle\hat{n}\rangle^2 = |\alpha|^2$, the Poisson signature. *Difficulty: application.*

**Synthesis**

7. *[Tests: tunneling fraction, connecting algebra to position-space integrals]* The classical turning points for the ground state are $x = \pm x_0$ where $x_0 = \sqrt{\hbar/m\omega}$. Show that the probability of finding the particle outside the classical turning points is $1 - \mathrm{erf}(1)$. Evaluate this numerically and check it against the 16% claim in the text. (You will need $\int_0^1 e^{-u^2}\,du = (\sqrt{\pi}/2)\mathrm{erf}(1) \approx 0.747$.) *Difficulty: synthesis.*

8. *[Tests: correspondence principle, classical vs. quantum distributions]* For the $n$-th eigenstate, the classical probability density for a harmonic oscillator with energy $E_n$ is $P_\mathrm{cl}(x) = 1/(\pi\sqrt{x_n^2 - x^2})$ where $x_n = \sqrt{2E_n/m\omega^2}$ is the classical turning point. (a) Sketch $|\psi_n(x)|^2$ and $P_\mathrm{cl}(x)$ on the same axes for $n = 1$ and $n = 5$. Where does the quantum density peak? Where does the classical density peak? (b) Explain in two sentences why the quantum and classical distributions agree on average at large $n$ even though they disagree pointwise. *Difficulty: synthesis.*

**Challenge**

9. *[Tests: time evolution of coherent states, phase-space orbit]* Show that a coherent state $|\alpha\rangle$ evolved under $\hat{H}$ for time $t$ gives $e^{-i\omega t/2}|\alpha e^{-i\omega t}\rangle$ — a coherent state with amplitude $\alpha$ rotated in the complex plane by $-\omega t$, up to a global phase. (Hint: substitute the energy eigenstate expansion of $|\alpha\rangle$ and act with $e^{-i\hat{H}t/\hbar}$; resum the resulting series.) What does this say about the shape of the wave packet over time? *Difficulty: challenge.*

10. *[Tests: generalization of ladder algebra, connection to QFT]* The commutator $[\hat{a}_-, \hat{a}_+] = 1$ is the entire algebraic content of the harmonic oscillator. Consider a system with two independent oscillator modes described by operators $\hat{a}_\pm$ and $\hat{b}_\pm$ satisfying $[\hat{a}_-, \hat{a}_+] = [\hat{b}_-, \hat{b}_+] = 1$ and $[\hat{a}_\pm, \hat{b}_\pm] = 0$. (a) Write down the total Hamiltonian $\hat{H} = \hbar\omega_a(\hat{a}_+\hat{a}_- + 1/2) + \hbar\omega_b(\hat{b}_+\hat{b}_- + 1/2)$ and show the energy eigenvalues are $(n_a + 1/2)\hbar\omega_a + (n_b + 1/2)\hbar\omega_b$. (b) Without calculation, explain why a photon in a cavity mode with frequency $\omega$ corresponds to a single quantum of the associated harmonic oscillator — and what "the vacuum" means in this picture. *Difficulty: challenge.*

---

*Chapter 4: The ladder operators $\hat{a}_\pm$ introduced here are the first example of something general — using algebra rather than differential equations to extract physical content. The next chapter formalizes that move into the full operator language of quantum mechanics, where states become vectors in Hilbert space, observables become Hermitian operators, and the Schrödinger equation becomes a statement about unitary evolution.*
