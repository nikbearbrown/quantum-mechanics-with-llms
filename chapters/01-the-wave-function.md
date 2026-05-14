# Chapter 1 — The Wave Function
*What the blob is actually telling you.*

---

You watched a blue filled curve drift across a screen in Chapter 0. You dragged a slider and the curve spread. You noticed an orange line inside it, oscillating, going negative. You probably had a feeling — something between understanding and confusion — that you were looking at *something*, but you were not told what.

Now I want to tell you what it is. Not by giving you a definition to memorize. By actually figuring it out.

---

## What are we even looking at?

<!-- → [IMAGE: Side-by-side comparison of a population density map (people/km²) and a wave function probability density |ψ(x)|² — visual analogy showing that neither gives you "a location," both require integration over a region to yield a countable quantity] -->

Here is the first thing to notice about the blue curve: it has units, and you probably did not display them. If the particle is moving along a line measured in nanometers, the blue curve is a number *per nanometer*. It is a density — like population per square kilometer, not a total population. You cannot read off "the particle is here" from its value at a single point, any more than you can read off the number of people in a city from a population density at one address. To get a probability, you have to integrate over a region.

That is the **Born rule**. Max Born introduced it in 1926, in a paper on quantum scattering. The rule says: given a wave function $\psi(x, t)$, the probability of finding the particle in the interval $[a, b]$ at time $t$ is

$$\mathrm{Prob}\bigl(\text{particle in } [a, b]\bigr) = \int_a^b |\psi(x, t)|^2 \, dx.$$

<!-- → [INFOGRAPHIC: Annotated diagram of |ψ(x)|² curve with a shaded region [a,b] beneath it, arrow pointing to the shaded area labeled "this is the probability," arrow pointing to the curve's peak value labeled "this is NOT a probability — it is a density (units: nm⁻¹)"] -->

The density $|\psi(x,t)|^2$ can be larger than 1 — it is per unit length, not a probability itself. Probability is what you get after you multiply by $dx$ and integrate. Forgetting the integration is the most common first mistake; I am telling you about it now so you make it consciously rather than accidentally.

Born's original paper actually said the probability was proportional to $\psi$. In a footnote added in proof, he changed it to $|\psi|^2$. That footnote is one of the most consequential edits in the history of physics. He received the Nobel Prize in 1954 for the statistical interpretation the footnote introduced.

---

## Why is $\psi$ complex at all?

If what we measure is $|\psi|^2$, and $|\psi|^2$ is real and non-negative, why not just work with a real function? Why drag in complex numbers?

The answer is not conventional — it is forced. The time-dependent Schrödinger equation is

$$i\hbar \frac{\partial \psi}{\partial t} = \hat{H} \psi.$$

That $i$ on the left is not optional. Suppose $\psi$ were purely real. Then $\partial \psi / \partial t$ would be real. But $i\hbar$ times something real is purely imaginary. The equation cannot balance — a real left side would have to equal a purely imaginary right side, which it can't unless everything is zero. The dynamics themselves force $\psi$ to be complex.

You saw this in Chapter 0. The orange curve — Re $\psi$ — and the gray dashed curve — Im $\psi$ — were both non-trivial, with Im $\psi$ leading Re $\psi$ by a quarter cycle. If you tried to set Im $\psi = 0$ and run a time step, the Schrödinger equation would rebuild the imaginary part immediately. The phase is intrinsic to the motion.

<!-- → [IMAGE: Three-panel time sequence showing a Gaussian wave packet at t=0, t=T/4, t=T/2 — each panel overlaying Re ψ (orange), Im ψ (gray dashed), and |ψ|² (blue filled) — student should see the 90° phase relationship between Re and Im while |ψ|² drifts smoothly] -->

This is the answer to the first question I asked at the start of Chapter 0: the orange curve is the real part of a complex amplitude whose modulus-squared gives the probability density. Its sign carries phase information — information about momentum, about interference, about everything that makes quantum mechanics different from classical probability theory. Throwing away the imaginary part is not a simplification; it is destroying the physics.

---

## The most persistent misconception

Let me say something carefully, because this mistake survives from freshman physics all the way into research groups.

$\psi$ is not the particle. The particle, in any single run of the experiment, is at one definite place when you measure its position. $\psi$ tells you about the *distribution* of those places across many identically prepared experiments. Narrow $\psi$: when you run the experiment many times, the results cluster tightly. Wide $\psi$: they spread out.

This sounds like a small distinction. It is not. The blob you watched spreading in Chapter 0 — the blue curve growing wider — was not a particle physically spreading out. It was the probability distribution of position measurements becoming more uncertain. If you had one actual particle and you measured its position at time $t = 1000$ (after the blob had spread), you would get one number. That number would be somewhere in the wide blue distribution. Run the experiment ten thousand times with identical initial conditions; you get a histogram. The histogram matches $|\psi|^2$.

<!-- → [INFOGRAPHIC: Two-column diagram. Left: single run — one particle, one measurement, one dot on a number line. Right: 10,000 runs — histogram of measurement outcomes building up to match the shape of |ψ|². Caption: "ψ describes the histogram, not the dot."] -->

That is the Born rule in practice. That is what the blob was telling you.

---

## Normalization, and a calculation worth doing in full

Since $|\psi|^2$ is a probability density, the particle has to be *somewhere*. The integral over all space must equal 1:

$$\int_{-\infty}^{\infty} |\psi(x, t)|^2 \, dx = 1.$$

A wave function satisfying this is called normalized.

Now here is something that needs to be shown, not just asserted: if you normalize $\psi$ at $t = 0$, does it *stay* normalized as it evolves under the Schrödinger equation? It had better. If the probability of finding the particle somewhere drifted away from 1 as time passed, the formalism would be inconsistent. But it is not obvious from looking at the Schrödinger equation that this is preserved. Let me show you the calculation, because the argument produces a beautiful byproduct.

Differentiate the total probability with respect to time:

$$\frac{d}{dt}\int_{-\infty}^{\infty} |\psi|^2 \, dx = \int_{-\infty}^{\infty} \frac{\partial}{\partial t}(\psi^* \psi) \, dx.$$

Using the product rule, $\partial_t(\psi^*\psi) = (\partial_t \psi^*)\psi + \psi^*(\partial_t \psi)$. Now substitute the Schrödinger equation for $\partial_t \psi$ and its complex conjugate for $\partial_t \psi^*$. With Hamiltonian $\hat{H} = -(\hbar^2/2m)\,\partial_x^2 + V(x)$:

$$\partial_t \psi = \frac{1}{i\hbar}\hat{H}\psi, \qquad \partial_t \psi^* = -\frac{1}{i\hbar}\hat{H}\psi^*.$$

Plug in. The two terms involving the real potential $V(x)\psi^*\psi$ cancel — they enter with opposite signs. All that survives is the kinetic part:

$$\frac{\partial}{\partial t}(\psi^*\psi) = \frac{i\hbar}{2m}\!\left(\frac{\partial^2 \psi^*}{\partial x^2}\,\psi - \psi^* \frac{\partial^2 \psi}{\partial x^2}\right).$$

Here is the trick that makes everything work. The right side is a perfect derivative in $x$:

$$\frac{\partial^2 \psi^*}{\partial x^2}\,\psi - \psi^*\frac{\partial^2 \psi}{\partial x^2} = \frac{\partial}{\partial x}\!\left(\frac{\partial \psi^*}{\partial x}\,\psi - \psi^* \frac{\partial \psi}{\partial x}\right).$$

(Differentiate the right side yourself to verify — it takes thirty seconds.) So we can write

$$\frac{\partial |\psi|^2}{\partial t} = -\frac{\partial J}{\partial x},$$

where we have defined the **probability current**

$$J(x, t) \equiv \frac{\hbar}{m}\,\mathrm{Im}\!\left(\psi^* \frac{\partial \psi}{\partial x}\right).$$

<!-- → [INFOGRAPHIC: Pipe-flow analogy for the continuity equation ∂ρ/∂t + ∂J/∂x = 0 — a horizontal tube with probability density ρ = |ψ|² shown as fluid, arrows indicating J flowing right; annotation showing that what drains from one region fills the next — probability is neither created nor destroyed] -->

This is the **continuity equation** — the same equation that governs the flow of any conserved quantity in physics. Mass, charge, energy: they all satisfy $\partial \rho / \partial t + \partial J / \partial x = 0$. Probability satisfies it too.

To finish the proof, integrate over all $x$:

$$\frac{d}{dt}\int_{-\infty}^{\infty}|\psi|^2 \, dx = -\bigl[J(x,t)\bigr]_{-\infty}^{\infty}.$$

For a physically realizable (normalizable) wave function, $\psi \to 0$ fast enough as $|x| \to \infty$ that $J$ vanishes at both limits. So the right side is zero, and the total probability is constant.

The proof has a lesson beyond its own conclusion: it tells you why $J$ matters. The probability current is not an accessory definition — it is the *structural reason* normalization is preserved. If your simulation shows $\int |\psi|^2\,dx$ drifting away from 1, either the Schrödinger equation is being solved incorrectly (an explicit Euler scheme is not unitary and will drift), or probability is leaking at the grid boundaries. The normalization indicator catches both errors.

---

## What do you actually measure?

The Born rule gives you the probability distribution for position. But position is not the only observable. You might want the average position across many experiments, or the average momentum, or how much either quantity fluctuates. These are **expectation values**.

The average position is simply the centroid of the probability distribution:

$$\langle x \rangle = \int_{-\infty}^{\infty} x\, |\psi(x, t)|^2 \, dx.$$

Each possible position is weighted by how probable it is. This is the same arithmetic as the mean of any probability distribution.

The average momentum is where things get interesting, and where most students first get stuck.

You cannot write $\langle p \rangle = \int p\, |\psi|^2 \, dp$ in the same way, because in position space you do not have a function of $p$ to integrate against — you have a function of $x$. The momentum operator in position space is a derivative:

$$\hat{p} = -i\hbar\frac{\partial}{\partial x}.$$

So the expectation value of momentum is

$$\langle p \rangle = \int_{-\infty}^{\infty} \psi^*(x, t)\,\left(-i\hbar\frac{\partial}{\partial x}\right)\psi(x, t)\,dx.$$

Why a derivative? The cleanest reason is the Fourier transform. Define $\phi(p,t)$ as the Fourier transform of $\psi(x,t)$. Then $|\phi(p,t)|^2$ is the probability density for momentum measurements — the Born rule applied in momentum space. In momentum space, $\langle p \rangle = \int p\, |\phi|^2\, dp$ by the same logic as position. Translate back to position space using Parseval's theorem, and you get the derivative operator. Momentum is differentiation because differentiation is what Fourier transform does to oscillation frequency.

<!-- → [INFOGRAPHIC: Fourier duality diagram — left panel shows ψ(x) as a narrow Gaussian in position space; right panel shows φ(p) as a broad Gaussian in momentum space; double-headed arrow labeled "Fourier transform" connecting them; caption: "narrow in x ↔ broad in p. You cannot localize both simultaneously."] -->

The minus sign matters. $\hat{p} = -i\hbar\,\partial_x$, not $+i\hbar\,\partial_x$. Get the sign wrong and $\langle p \rangle$ flips direction. A wave packet moving to the right (positive $k_0$) must give $\langle p \rangle > 0$. The simulation in the LLM exercise will catch a sign error immediately.

---

## The uncertainty principle, properly

Here is the statement:

$$\sigma_x\,\sigma_p \geq \frac{\hbar}{2},$$

where $\sigma_x = \sqrt{\langle x^2\rangle - \langle x\rangle^2}$ is the standard deviation of position measurements across many identical experiments, and $\sigma_p$ is the same for momentum.

The misconception to clear up immediately: this is not about measurement disturbing the particle. Heisenberg's original 1927 paper used a thought experiment with a gamma-ray microscope in which observing the electron kicked its momentum. That is a physically interesting statement, but it is a *different* statement from the inequality above.

The Kennard inequality — this is what the formula above is called, after E. H. Kennard who proved it in 1927 — is a statement about *preparation*, not disturbance. Prepare ten thousand copies of the same state $\psi$. Measure position on five thousand of them; get a distribution with standard deviation $\sigma_x$. Measure momentum on the other five thousand; get a distribution with standard deviation $\sigma_p$. The product $\sigma_x \sigma_p \geq \hbar/2$. No single measurement disturbs anything in this statement. It is a property of the shape of $\psi$.

<!-- → [INFOGRAPHIC: Two-group experimental protocol diagram — 10,000 identical preparations split into two groups of 5,000; left group: position measurements → histogram → σ_x; right group: momentum measurements → histogram → σ_p; bottom: σ_x · σ_p ≥ ℏ/2. Caption: "No particle is measured twice. No disturbance occurs. The inequality is about the shape of ψ."] -->

The reason it holds is Fourier analysis. A wave function narrow in $x$ must be broad in $p$, and a wave function narrow in $p$ must be broad in $x$ — they are Fourier conjugates, and you cannot make both transforms narrow simultaneously. The inequality $\sigma_x \sigma_p \geq \hbar/2$ is the precise quantification of that unavoidable Fourier-pair relationship.

There is a separate measurement-disturbance inequality, formalized by Ozawa in 2003, with a different bound and different experimental tests (Erhart et al. 2012, Rozema et al. 2012). It is a different animal. The chapter mentions this distinction here and does not revisit it.

---

## The Gaussian saturates the bound

The Gaussian wave packet is the minimum-uncertainty state: it achieves $\sigma_x\sigma_p = \hbar/2$ exactly, and every other normalizable wave function does strictly worse. Let me show you why.

Take $\psi(x) = (1/(\pi a^2))^{1/4}\,\exp(-x^2/(2a^2))\,\exp(ik_0 x)$ at a fixed time.

**Position.** $|\psi|^2 = (1/(\pi a^2))^{1/2}\,e^{-x^2/a^2}$, a Gaussian with standard deviation $a/\sqrt{2}$. So $\sigma_x = a/\sqrt{2}$.

**Momentum.** Differentiate $\psi$:

$$\frac{\partial \psi}{\partial x} = \psi\!\left(-\frac{x}{a^2} + ik_0\right).$$

Apply $\hat{p} = -i\hbar\,\partial_x$:

$$\hat{p}\psi = \psi\left(\frac{i\hbar x}{a^2} + \hbar k_0\right).$$

Then $\langle p\rangle = \int \psi^*\hat{p}\psi\,dx$. The $i\hbar x/a^2$ term integrates to zero (it is an odd function times the symmetric density $|\psi|^2$). The $\hbar k_0$ term gives $\hbar k_0\int|\psi|^2\,dx = \hbar k_0$. So $\langle p\rangle = \hbar k_0$.

For $\langle p^2\rangle$, apply $\hat{p}^2 = -\hbar^2\,\partial_x^2$ and collect terms. After the odd-function integrals vanish, you get $\langle p^2\rangle = \hbar^2(1/(2a^2) + k_0^2)$. The variance is $\sigma_p^2 = \langle p^2\rangle - \langle p\rangle^2 = \hbar^2/(2a^2)$, so $\sigma_p = \hbar/(\sqrt{2}\,a)$.

**The product.**

$$\sigma_x\,\sigma_p = \frac{a}{\sqrt{2}} \cdot \frac{\hbar}{\sqrt{2}\,a} = \frac{\hbar}{2}.$$

Equality. The Gaussian is the tightest possible state — the one where position and momentum uncertainties are balanced as evenly as quantum mechanics permits. Every other wave function you can write down gives a larger product.

<!-- → [CHART: Two-panel plot. Left: σ_x vs. a (linear, slope 1/√2). Right: σ_p vs. a (hyperbola, proportional to 1/a). Both panels share the same x-axis range a ∈ [0.2, 4] nm. Inset box: σ_x · σ_p = ℏ/2 for all a — student should see the product is constant even as each factor varies] -->

Notice the relationship: $\sigma_x \propto a$, $\sigma_p \propto 1/a$. Make the wave packet narrower in space ($a$ smaller) and it becomes broader in momentum ($\sigma_p$ grows). Make it broader in space and it becomes narrower in momentum. The product stays at $\hbar/2$. This is the Fourier relationship, made concrete.

The simulation you build next lets you watch this numerically, for the Gaussian and for every other wave function in the gallery.

---

## LLM Exercise — the probability explorer

The deliverable: `01-probability-explorer.html`. A wave-function gallery with three stacked SVG panels — Re $\psi$, Im $\psi$, $|\psi|^2$ — and a live numerics panel that shows $\langle x\rangle$, $\langle p\rangle$, $\sigma_x$, $\sigma_p$, and the ratio $\sigma_x\sigma_p/(\hbar/2)$ that reads $1.000$ for the Gaussian.

### Part A — Updated `CLAUDE.md` snippet for this chapter

Add this stanza to your existing `CLAUDE.md`:

````markdown
## Chapter 1 — Probability and observables

- Complex storage: every ψ array is two parallel Float64Arrays (re, im) OR
  an array of {re, im}. NEVER drop the imaginary part.
- Momentum operator p̂ = −i ℏ ∂/∂x. Sign is critical. For a Gaussian with
  k₀ > 0, ⟨p⟩ must be positive.
- ⟨x⟩, ⟨x²⟩ computed via Simpson's rule on the x grid (N ≥ 500).
- ⟨p⟩, ⟨p²⟩ computed via FFT to momentum space, then integrate p|φ|²
  and p²|φ|². Use fft-js from CDN (https://cdn.jsdelivr.net/npm/fft-js).
  FFT convention: forward = sum_n ψ_n e^(−i k_m x_n) · Δx / √(2πℏ).
  Document the convention in code comments.
- The σ_x σ_p / (ℏ/2) display must read 1.000 for the Gaussian.
  If it reads 0.500, you divided by ℏ instead of ℏ/2 — fix.
- Every numerical display has units (nm, nm⁻¹, kg·m/s).
- Normalization indicator: ∫|ψ|² dx via Simpson's rule, displayed top-right.
````

### Part B — The simulation prompt

````markdown
SHOW.
The Born rule for a one-dimensional particle:
  P(x, t) dx = |ψ(x, t)|² dx,  with ∫ |ψ|² dx = 1.
Position and momentum expectation values:
  ⟨x⟩  = ∫ x |ψ|² dx
  ⟨x²⟩ = ∫ x² |ψ|² dx
  ⟨p⟩  = ∫ ψ* (−i ℏ ∂/∂x) ψ dx
  ⟨p²⟩ = ∫ ψ* (−ℏ² ∂²/∂x²) ψ dx
  σ_x = √(⟨x²⟩ − ⟨x⟩²),  σ_p = √(⟨p²⟩ − ⟨p⟩²).
Uncertainty principle: σ_x σ_p ≥ ℏ/2, saturated by the Gaussian.

Wave function gallery (selectable by dropdown):
  1. Gaussian: ψ(x) = (1/(πa²))^(1/4) exp(−x²/(2a²)) exp(i k₀ x)
     — sliders: a (0.1 to 5 nm), k₀ (−20 to +20 nm⁻¹)
  2. Infinite-well eigenstate n (within 0 ≤ x ≤ L):
     ψ_n(x) = √(2/L) sin(nπx/L) for n = 1..10
     — sliders: n (1..10 integer), L (1 to 20 nm)
  3. Double Gaussian:
     ψ(x) ∝ exp(−(x−d)²/(2σ²)) + exp(−(x+d)²/(2σ²))
     — sliders: d (separation, 0.5 to 5 nm), σ (0.2 to 2 nm)
  4. Square pulse: ψ(x) = 1/√w for −w/2 < x < w/2, else 0
     — slider: w (0.5 to 10 nm)

Use the existing CLAUDE.md and DESIGN.md as context.

SAY.
Produce a single file `01-probability-explorer.html`.

Layout:
  Left column (700 px wide):
    Three stacked SVG panels (each 130 px tall) sharing an x-axis:
      Top:    Re ψ(x)   in orange
      Middle: Im ψ(x)   in gray dashed
      Bottom: |ψ(x)|²   in blue filled
  Right column (300 px wide), live numerical readouts:
      ∫|ψ|² dx       (normalization indicator, must read 1.000)
      ⟨x⟩            (in nm)
      ⟨x²⟩           (in nm²)
      σ_x            (in nm)
      ⟨p⟩            (in ℏ/nm)
      ⟨p²⟩           (in (ℏ/nm)²)
      σ_p            (in ℏ/nm)
      σ_x σ_p / (ℏ/2)   (DIMENSIONLESS, prominent, large font)
  Below: wave-function dropdown + sliders that update based on selection.
  Optional: a time slider for free-particle evolution (Gaussian only).

CONSTRAIN.
- D3 v7 from CDN. SVG only. Vanilla JS.
- N = 500 grid points on x ∈ [−20 nm, +20 nm].
- ⟨x⟩, ⟨x²⟩, ∫|ψ|² via Simpson's rule.
- ⟨p⟩, ⟨p²⟩, σ_p via FFT (fft-js from CDN). FFT convention documented.
- Display σ_x σ_p / (ℏ/2) — the Gaussian must read 1.000. The infinite-well
  n=1 in L=10 nm must read approximately 1.136. The square pulse must read
  ∞ (or "undefined") because σ_p diverges for a discontinuous ψ — handle
  gracefully with a label.
- Re ψ and Im ψ must both be drawn from the complex ψ. Do not collapse
  to a real-only function.
- Color scheme from DESIGN.md.

VERIFY.
After writing the file, give me four checks:
(a) Gaussian with a = 1 nm, k₀ = 10 nm⁻¹: σ_x = 1/√2 ≈ 0.707 nm;
    σ_p = ℏ/(√2 · 1 nm) ≈ 0.707 ℏ/nm; product = ℏ/2; ratio = 1.000.
(b) Gaussian with a = 0.5 nm, k₀ = 10 nm⁻¹: σ_x = 0.354 nm; σ_p doubles;
    product unchanged; ratio = 1.000.  (a halved, σ_p doubled, product same.)
(c) Infinite-well n=1 in L=10 nm: ⟨x⟩ = 5 nm by symmetry;
    σ_x = L · √(1/12 − 1/(2π²)) ≈ 1.81 nm; σ_p = (π ℏ)/L ≈ 0.314 ℏ/nm;
    ratio ≈ 1.136.
(d) Double Gaussian with d = 2 nm, σ = 0.5 nm: ⟨x⟩ = 0 by symmetry, BUT
    the probability of finding the particle in [−0.5 nm, +0.5 nm] is small
    (peaks are at ±2 nm). Display this in a side panel as a teaching note.

Then list known LLM failure modes for this code and confirm which you have
guarded against:
  - ψ-vs-|ψ|² render swap (the |ψ|² panel showing a signed curve, or the
    Re ψ panel showing a non-negative one).
  - Lost imaginary part (Im ψ identically zero for a wave packet with
    k₀ ≠ 0).
  - Sign error in p̂ (⟨p⟩ negative for k₀ > 0).
  - Simpson's rule on a coarse grid drifting ⟨x⟩ from its analytical value.
  - FFT convention mismatch producing σ_p off by a factor of √(2π) or √ℏ.
  - Missing units on numerical readouts.
  - σ_x σ_p / (ℏ/2) = 0.500 for a Gaussian (dividing by ℏ instead of ℏ/2).
````

### Part C — Exploration tasks

**Saturate the bound.** Select the Gaussian. Vary $a$ from $0.2$ nm to $4$ nm. Watch $\sigma_x$ change. Watch $\sigma_p$ change inversely. Watch the ratio $\sigma_x \sigma_p / (\hbar/2)$ stay locked at $1.000$. Write down what this confirms.

**Exceed the bound.** Switch to the infinite-well eigenstate, $n = 1$, $L = 10$ nm. The ratio reads about $1.136$. Now try $n = 2$ through $n = 10$. As $n$ grows, $\sigma_p$ grows (higher energy means larger momentum spread) while $\sigma_x$ changes little (the wave function fills the same well regardless of $n$). Does $\sigma_x \sigma_p / (\hbar/2)$ grow without bound, approach a limit, or oscillate?

**The double-peaked case.** Select the double Gaussian with $d = 2$ nm, $\sigma = 0.3$ nm. $\langle x \rangle$ reads $0$. Look at $|\psi|^2$: the probability of finding the particle within $\pm 0.5$ nm of $x = 0$ is tiny — the peaks are at $\pm 2$ nm. Write one sentence explaining what this tells you about using $\langle x\rangle$ as a prediction for a single measurement.

**The square pulse.** Select the square pulse, width $w = 2$ nm. $\sigma_x$ is finite. $\sigma_p$ should be infinite (or, on a finite grid, very large) because the Fourier transform of a discontinuous square pulse decays like $1/p$ and $\int p^2 \cdot (1/p)^2\,dp$ diverges. The ratio panel should label this "undefined." This is not a bug — it is a feature of the discontinuity at $\pm w/2$.

**Free-particle time evolution (Gaussian only).** Run time evolution. Watch $\sigma_x$ grow. Watch $\sigma_p$ stay constant. Watch the ratio $\sigma_x\sigma_p / (\hbar/2)$ exceed $1.000$ as time advances. The Gaussian saturates the bound only at $t = 0$. Under free evolution, $\sigma_x(t)^2 = \sigma_x(0)^2 + (\hbar t / (2m\sigma_x(0)))^2$. Explain in two sentences why $\sigma_p$ stays constant while $\sigma_x$ grows.

### Part D — Extension prompt

````markdown
Add a momentum-space panel below the existing three panels:
  Fourth panel: |φ(p)|² (the momentum-space probability density), blue filled.

φ(p) is the spatial Fourier transform of ψ(x), already computed for the
⟨p⟩ readout — reuse it; do not recompute.

For the Gaussian with a = 1 nm, k₀ = 10 nm⁻¹, the momentum-space density
is a Gaussian centered at p = ℏ k₀ with width σ_p = ℏ/(a√2). Verify by
fitting a Gaussian to the displayed |φ(p)|² and reading off the centroid
and width — they must match σ_p to within 1%.

For the infinite-well n = 1 state, |φ(p)|² has TWO main peaks at p ≈ ±πℏ/L
(the de Broglie momenta of the left- and right-moving components of the
standing wave). Verify the two peaks appear in the momentum panel.

Add a label below the panel reading: "The position–momentum Fourier pair:
σ_x and σ_p cannot both be made small at once."

Do not regress any existing panel.
````

When you watch the momentum-space panel of the infinite-well eigenstate split into two peaks, you have a concrete picture for why the energy eigenstates of a confined particle are standing waves. Chapter 2 will name this.

---

## Still puzzling

The Born rule is a postulate in this book. I have flagged that other research programs — Zurek's envariance argument, many-worlds branch-counting — try to derive it from other axioms. I do not know with confidence whether any of those derivations should be called settled, and I have chosen not to take a position. The chapter would be cleaner if I did.

The probability current $J$ has a beautiful interpretation as a flow of probability density. For a single particle in one dimension it works elegantly. For many particles in three dimensions the generalization holds, but the geometric intuition is harder, and this chapter has not shown it. Chapters 5 and 6 will.

The square pulse's divergent $\sigma_p$ is real physics, but most students first encounter it as a numerical artifact. Labeling it "undefined" is honest; it may not be the most pedagogically satisfying move.

---

## Exercises

**Warm-up**

1. *[Tests: Born rule as density vs. probability]* A particle has wave function $\psi(x) = A e^{-|x|/a}$ for some real constant $a > 0$. (a) Find the normalization constant $A$ such that $\int_{-\infty}^{\infty}|\psi|^2\,dx = 1$. (b) What is the probability of finding the particle in the interval $[-a, a]$? (c) The peak value of $|\psi(0)|^2$ is $|A|^2$. For $a = 0.5$ nm, compute this value and confirm it is greater than 1 — then explain why that does not violate anything. *Difficulty: warm-up.*

2. *[Tests: complex structure of ψ, sign of momentum operator]* Let $\psi(x) = N\,e^{-x^2/(2a^2)}\,e^{ik_0 x}$ with $a = 1$ nm and $k_0 = -5$ nm$^{-1}$. (a) Sketch Re $\psi$, Im $\psi$, and $|\psi|^2$ on the same axis. Which is symmetric? Which oscillates? (b) Without computing the full integral, determine the sign of $\langle p \rangle$ and the value of $\langle x \rangle$. Justify both answers in one sentence each. *Difficulty: warm-up.*

3. *[Tests: normalization preservation, probability current]* The probability current for a real-valued wave function is $J(x,t) = 0$ everywhere. Prove this directly from the definition $J = (\hbar/m)\,\mathrm{Im}(\psi^*\,\partial_x\psi)$. Then state what this means physically: can a real-valued $\psi$ describe a particle with net momentum in one direction? *Difficulty: warm-up.*

**Application**

4. *[Tests: expectation values for a non-Gaussian state]* For the infinite-well ground state $\psi_1(x) = \sqrt{2/L}\,\sin(\pi x/L)$ on $[0, L]$: (a) Compute $\langle x \rangle$ and $\langle x^2 \rangle$ by direct integration. (b) Compute $\sigma_x$. (c) Compute $\langle p \rangle$ using $\hat{p} = -i\hbar\,\partial_x$. Does the answer surprise you? Explain why it makes physical sense for a standing wave. *Difficulty: application.*

5. *[Tests: Kennard inequality, preparation vs. disturbance]* A professor claims: "If I measure a particle's position very precisely, I must have disturbed its momentum — that is what the uncertainty principle says." Write a two-paragraph response. In the first paragraph, identify what is physically correct in the claim. In the second, explain what is wrong with it and state the correct formulation of the Kennard inequality. *Difficulty: application.*

6. *[Tests: units and dimensional reasoning with probability density]* A wave function is given numerically on a grid with $x$ in meters. The peak value of $|\psi|^2$ at $t = 0$ is $3.2 \times 10^9$ m$^{-1}$. (a) Is this a valid probability density value? Why? (b) Estimate the probability of finding the particle within $\pm 0.1$ nm of the peak, assuming $|\psi|^2$ is roughly constant over that interval. (c) Suppose someone reports that the wave function is "unnormalized by a factor of 2." What does this mean precisely, and what is the corrected peak density? *Difficulty: application.*

7. *[Tests: Born rule applied to the momentum-space wave function]* Define $\phi(p) = (1/\sqrt{2\pi\hbar})\int_{-\infty}^{\infty}\psi(x)\,e^{-ipx/\hbar}\,dx$. For the Gaussian $\psi(x) = (\pi a^2)^{-1/4}\,e^{-x^2/(2a^2)}\,e^{ik_0 x}$, show by direct Fourier transform that $\phi(p)$ is itself a Gaussian centered at $p = \hbar k_0$ with width $\hbar/a$. Then compute $\int_{-\infty}^{\infty}|\phi(p)|^2\,dp$ and verify it equals 1 — confirming the Born rule holds in momentum space. *Difficulty: application.*

**Synthesis**

8. *[Tests: combining normalization proof with physical interpretation]* The continuity equation says $\partial_t |\psi|^2 = -\partial_x J$. (a) Suppose $J(x,t) > 0$ for all $x$ in some interval $[a,b]$ and $J = 0$ outside. Sketch how $|\psi|^2$ evolves in and near $[a,b]$ over a short time $\delta t$. (b) Now suppose $J$ is positive on the left half of the interval and negative on the right half. Where does $|\psi|^2$ increase and where does it decrease? (c) Use this reasoning to explain, without equations, why a wave packet moving to the right has $J > 0$ in the region of high probability density. *Difficulty: synthesis.*

9. *[Tests: uncertainty principle across multiple wave function types]* You have four wave functions: a Gaussian ($a = 1$ nm), an infinite-well ground state ($L = 4$ nm), a double Gaussian ($d = 1.5$ nm, $\sigma = 0.4$ nm), and a Gaussian with $a = 1$ nm evolved for a long time under free propagation. Rank them in order of increasing $\sigma_x \sigma_p / (\hbar/2)$ and justify each ranking. You may use the simulation to check your predictions, but state the prediction first. *Difficulty: synthesis.*

**Challenge**

10. *[Tests: limits of the formalism, connection to Chapter 2]* The plane wave $\psi(x) = e^{ikx}$ has $|\psi|^2 = 1$ everywhere. (a) Show it cannot be normalized on $(-\infty, \infty)$. (b) Nevertheless, compute $\langle p \rangle$ formally using $\hat{p} = -i\hbar\,\partial_x$ — what do you get? (c) The plane wave is often described as a particle with "definite momentum $\hbar k$." In light of the Born rule's requirement that $\int|\psi|^2\,dx = 1$, what is the precise sense in which this statement is and is not true? (d) Propose a way to use plane waves as building blocks for normalizable wave functions — this is the direction Chapter 2 will develop. *Difficulty: challenge.*

---

*Chapter 2: You now know what $\psi$ means and how to extract position and momentum statistics from it. But what determines $\psi(x)$ in the first place? The answer requires a potential $V(x)$ and an eigenvalue equation. Next: the time-independent Schrödinger equation.*
