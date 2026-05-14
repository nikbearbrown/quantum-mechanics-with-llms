# Chapter 1 — The Wave Function

> You watched a Gaussian blob spread on screen in Chapter 0. This chapter answers the question you have not yet been allowed to ask: what was that blob actually telling you about a particle?

---

## 1. What this chapter is doing

In Chapter 0 you produced a free-particle wave packet and ran it. You saw $|\psi(x, t)|^2$ drift and spread. You did not yet have permission to call it a probability density, because you did not yet have a definition of probability density in the quantum sense. This chapter supplies the definition. It states the Born rule, proves that normalization is preserved under Schrödinger evolution, introduces expectation values of position and momentum, and shows that the uncertainty principle $\sigma_x \sigma_p \geq \hbar/2$ is saturated by the Gaussian you have been watching. The simulation this chapter produces is the *probability explorer*: a gallery of wave functions with live numerical readouts for $\langle x \rangle$, $\langle p \rangle$, $\sigma_x$, $\sigma_p$, and — the chapter's punchline — the ratio $\sigma_x \sigma_p / (\hbar/2)$ that reads exactly $1.000$ for a Gaussian and strictly greater than $1.000$ for everything else.

The mechanism deep-dived here is the proof that the Born rule's probability is *conserved*: $\int |\psi|^2 \,dx$ stays $1$ for all time, by a calculation that produces the *probability current* as a byproduct. This is the chapter's gift and the place where most undergraduate texts mumble. We are going to do the integration by parts in full view.

## 2. Learning objectives

- **(Understand)** Distinguish the wave function $\psi(x, t)$ from the probability density $|\psi(x, t)|^2$ — and the probability density from a probability.
- **(Apply)** State the Born rule and compute the probability of finding a particle in a finite interval $[a, b]$ from a given $\psi$.
- **(Apply)** Compute $\langle x \rangle$, $\langle x^2 \rangle$, $\sigma_x$, and the analogous momentum quantities for a Gaussian and for the infinite-well ground state.
- **(Analyze)** Prove that normalization is preserved under Schrödinger evolution, identifying where each move (integration by parts, the Schrödinger equation, the boundary condition at infinity) enters.
- **(Evaluate)** State the uncertainty principle as a statement about identically prepared ensembles, *not* about measurement disturbance, and identify the empirical claim that would settle the distinction.
- **(Create)** Produce `01-probability-explorer.html`, a gallery-and-readout visualizer that confirms $\sigma_x \sigma_p / (\hbar/2) \geq 1$ for any wave function in the gallery.

## 3. The motivating problem

Here is what you saw in Chapter 0. A blue filled curve, centered at $x = 0$, narrow. You dragged a slider. The curve drifted right and grew wider. You also saw an orange curve and a gray dashed one, oscillating inside the blue blob.

Now I ask you four questions Chapter 0 did not let you answer.

**One.** The blue curve has units. What are they? Is it dimensionless? Per meter? Per nanometer? You probably don't know, because you were not told. (If the curve is a probability density and $x$ is in nanometers, the units are nm$^{-1}$. If you were not displaying units, you have already made the mistake this chapter is going to name.)

**Two.** Suppose the blue curve, at $t = 0$, has its peak value at $0.4$ nm$^{-1}$ at $x = 0$. The classical question "where is the particle?" wants a number. What does $0.4$ nm$^{-1}$ tell you about where the particle is? Hint: it is not "the particle is at $x = 0$ with strength $0.4$."

**Three.** The orange curve goes negative. The blue curve never does. The orange curve is the real part of something whose absolute square is the blue curve. What is the orange curve a real part *of*, and how does its sign carry physical content?

**Four.** You dragged the time slider. The blue curve drifted at one speed and the wave crests inside it moved at half that speed. Drag the slider for a long time. The blob spreads until it covers ten times its initial width. Has the *particle* spread? Or has something else?

The chapter answers all four, in order. The first three are answered by the Born rule and the structural fact that $\psi$ is a complex amplitude. The fourth is answered by saying clearly that $\psi$ describes the distribution of measurement outcomes across identically prepared experiments, not the position of a single particle.

## 4. The Born rule and what it costs

### 4.1 Plain-language setup

A particle's quantum state is captured by a complex-valued function $\psi(x, t)$. You do not observe $\psi$ directly. The instrument on your bench does not have a needle that reads $\psi$. What you observe — when you measure the particle's position — is a number $x_i$ for that one experiment. Repeat the preparation many times with identical setups, plot a histogram of the $x_i$'s, and the *density* of that histogram (in the limit of infinitely many trials) is

$$P(x, t) = |\psi(x, t)|^2.$$

That is the **Born rule**. It is the bridge between $\psi$ (calculable, in the formalism) and $x_i$ (measured, on the bench).

Max Born introduced this in 1926, in a paper on quantum scattering ([Born, M. (1926), *Zur Quantenmechanik der Stoßvorgänge*, *Zeitschrift für Physik* 37, 863–867](https://link.springer.com/article/10.1007/BF01397477)). The footnote you should know about: in the original submission, Born wrote that the probability was proportional to $\psi$. In a footnote added in proof, he changed it to $|\psi|^2$. That footnote is one of the most consequential edits in physics. Born received the 1954 Nobel Prize ([nobelprize.org](https://www.nobelprize.org/prizes/physics/1954/born/facts/)) specifically for the statistical interpretation of the wave function.

### 4.2 Formal statement

For a particle in one dimension, the probability of finding it between $x$ and $x + dx$ at time $t$ is

$$P(x, t)\,dx = |\psi(x, t)|^2\,dx.$$

For an interval $[a, b]$,

$$\mathrm{Prob}\bigl(\text{particle in } [a, b] \text{ at time } t\bigr) = \int_a^b |\psi(x, t)|^2\,dx.$$

Three things are happening in the equation that you should not let slip past.

First, $|\psi|^2 = \psi^*\psi$ is real and non-negative. Probability had better be non-negative. The modulus-squared is *what makes the complex $\psi$ produce a real probability*. (Griffiths *Introduction to Quantum Mechanics* 3rd ed., §1.3.)

Second, $|\psi|^2$ has units. If $x$ is measured in meters, $|\psi|^2$ has units of m$^{-1}$. It is a *density*. Multiplying by $dx$ (in meters) gives a dimensionless probability. **Misconception, addressed inline.** *"$|\psi|^2$ is a probability."* No. $|\psi|^2$ is a probability *per unit length*. The probability is $|\psi|^2 \,dx$, or the integral over an interval. Forget the $dx$ and you will forget that probability density can be larger than $1$. (A Gaussian with $\sigma = 0.1$ nm has peak density $\sim 4$ nm$^{-1}$; this is not a 400% probability.)

Third, the Born rule is a *postulate*. It is not derived from the Schrödinger equation. It is the assumption that takes you from the calculable object $\psi$ to the measurable distribution of $x_i$. There are research programs (Zurek's envariance argument, [arXiv:quant-ph/0405161](https://arxiv.org/abs/quant-ph/0405161); the many-worlds branch-counting arguments — Wallace 2012, *The Emergent Multiverse*) that try to derive the Born rule from other axioms. They are not settled. The textbook position — the one this book takes — is that the Born rule is the operational definition that links formalism to experiment, and the foundations are a live research program you should know exists but do not have to settle to do quantum mechanics.

**Misconception, addressed inline.** *"$\psi$ is the particle."* No. $\psi$ is a *device for computing probability densities of measurement outcomes for identically prepared particles*. The particle, on a given run of the experiment, is at one place when you measure. $\psi$ tells you the distribution of places it might be found across many runs. The wave-function-is-the-particle mistake is the most persistent misconception in upper-division QM ([McKagan, Perkins & Wieman 2010, *Phys. Rev. ST PER* 6, 020121](https://journals.aps.org/prper/abstract/10.1103/PhysRevSTPER.6.020121); [Singh 2001, *Am. J. Phys.* 69, 885–895](https://aapt.scitation.org/doi/10.1119/1.1365404)). The chapter spends its first section killing it.

### 4.3 Why complex, not real

You might ask: if what we measure is $|\psi|^2$, why is $\psi$ complex at all? Why not stipulate $\psi$ to be real and avoid the imaginary unit?

The answer is in the dynamical law. The time-dependent Schrödinger equation is

$$i\hbar \frac{\partial \psi}{\partial t} = \hat{H} \psi.$$

The $i$ on the left is not optional. A real-only $\psi$ has a real $\partial \psi / \partial t$; the right side $\hat{H}\psi$ is real-or-complex depending on $\hat{H}$, but $i\hbar \partial_t \psi$ on a real $\psi$ is purely imaginary. The equation cannot be satisfied with a real $\psi$ unless the wave function is identically zero. The complex-valuedness is forced by the dynamics. (Griffiths §1.4 makes this point explicitly.)

You can see this in your Chapter 0 simulation. The orange Re $\psi$ and the gray dashed Im $\psi$ are *both* non-trivial, and Im $\psi$ leads Re $\psi$ by $\pi/2$ (for $k_0 > 0$). If you tried to set Im $\psi = 0$ and evolve, the Schrödinger equation would generate the imaginary part for you on the first time step. The phase is intrinsic.

## 5. Normalization, and its preservation — the deep-dive

This is the chapter's main mechanism. Three moves: state the requirement, prove it is preserved, see the probability current fall out as a byproduct. Each move on the page.

### 5.1 The requirement

If $|\psi|^2$ is a probability density, the total probability of the particle being *somewhere* is $1$:

$$\int_{-\infty}^{\infty} |\psi(x, t)|^2\,dx = 1.$$

A wave function satisfying this is **normalized**. Not every solution of the Schrödinger equation is normalizable. The plane wave $e^{ikx}$ has $|\psi|^2 = 1$ everywhere, and $\int_{-\infty}^{\infty} 1\,dx$ diverges. Plane waves are useful as components but are not physical states by themselves. Physical states are normalizable.

### 5.2 Schrödinger evolution preserves normalization — the proof

Let $\psi$ be a solution of the time-dependent Schrödinger equation with Hamiltonian $\hat{H} = -(\hbar^2 / (2m))\,\partial^2/\partial x^2 + V(x)$. Assume $\int |\psi|^2 \,dx = 1$ at $t = 0$. Claim: the integral remains $1$ for all $t > 0$.

Compute the time derivative:

$$\frac{d}{dt}\int_{-\infty}^{\infty} |\psi|^2\,dx = \int_{-\infty}^{\infty} \frac{\partial}{\partial t}(\psi^* \psi)\,dx = \int_{-\infty}^{\infty} \left(\frac{\partial \psi^*}{\partial t}\,\psi + \psi^* \frac{\partial \psi}{\partial t}\right) dx.$$

Substitute the Schrödinger equation $\partial_t \psi = (1/(i\hbar)) \hat{H}\psi$ and its complex conjugate $\partial_t \psi^* = -(1/(i\hbar))\hat{H}\psi^*$ (the $V(x)$ is real, so $\hat{H}^* = \hat{H}$ as an operator on real-valued $x$). Then

$$\frac{\partial \psi^*}{\partial t}\,\psi + \psi^* \frac{\partial \psi}{\partial t} = -\frac{1}{i\hbar}(\hat{H}\psi^*) \psi + \frac{1}{i\hbar} \psi^* (\hat{H}\psi).$$

The two $V(x)\psi^*\psi$ terms (one from each $\hat{H}$) cancel — they enter with opposite signs and are real. What remains is the kinetic part:

$$\frac{\partial}{\partial t}(\psi^* \psi) = -\frac{1}{i\hbar}\left(-\frac{\hbar^2}{2m}\right) \frac{\partial^2 \psi^*}{\partial x^2}\,\psi + \frac{1}{i\hbar}\left(-\frac{\hbar^2}{2m}\right) \psi^* \frac{\partial^2 \psi}{\partial x^2}.$$

Collect:

$$\frac{\partial}{\partial t}(\psi^* \psi) = \frac{i\hbar}{2m}\left(\frac{\partial^2 \psi^*}{\partial x^2}\,\psi - \psi^* \frac{\partial^2 \psi}{\partial x^2}\right).$$

Here is the trick. The right side is a *total derivative* in $x$:

$$\frac{\partial^2 \psi^*}{\partial x^2}\,\psi - \psi^* \frac{\partial^2 \psi}{\partial x^2} = \frac{\partial}{\partial x}\!\left(\frac{\partial \psi^*}{\partial x}\,\psi - \psi^* \frac{\partial \psi}{\partial x}\right).$$

(Differentiate the right-hand side product to verify.) So

$$\frac{\partial}{\partial t}|\psi|^2 = \frac{i\hbar}{2m}\,\frac{\partial}{\partial x}\!\left(\frac{\partial \psi^*}{\partial x}\,\psi - \psi^* \frac{\partial \psi}{\partial x}\right) = -\frac{\partial J}{\partial x},$$

where we have defined the **probability current**

$$J(x, t) \equiv \frac{i\hbar}{2m}\!\left(\psi \frac{\partial \psi^*}{\partial x} - \psi^* \frac{\partial \psi}{\partial x}\right) = \frac{\hbar}{m}\,\mathrm{Im}\!\left(\psi^* \frac{\partial \psi}{\partial x}\right).$$

(The two forms are equal; the second is the form most textbooks quote.) We have just derived the **continuity equation**

$$\frac{\partial |\psi|^2}{\partial t} + \frac{\partial J}{\partial x} = 0.$$

This is the same equation that governs the flow of any conserved density (mass, charge, energy) in continuum physics. *Probability is locally conserved*.

To finish the proof, integrate over all $x$:

$$\frac{d}{dt}\int_{-\infty}^{\infty}|\psi|^2\,dx = -\int_{-\infty}^{\infty} \frac{\partial J}{\partial x}\,dx = -\left[J(x, t)\right]_{-\infty}^{\infty}.$$

For a normalizable $\psi$, $\psi \to 0$ as $|x| \to \infty$ (faster than $1/\sqrt{|x|}$, otherwise $\int|\psi|^2$ would not converge). Therefore $J(\pm\infty, t) = 0$, and

$$\frac{d}{dt}\int_{-\infty}^{\infty}|\psi|^2\,dx = 0.$$

$\blacksquare$

The clever part: a quantity defined globally ($\int |\psi|^2$) turns out to be conserved because of a *local* statement ($\partial_t |\psi|^2 = -\partial_x J$). The current $J$ is not an accessory; it is the structural reason normalization is preserved. **The lesson.** If your simulation shows $\int |\psi|^2 \,dx$ drifting, either the Schrödinger equation is not being solved correctly (numerical drift from a non-unitary scheme like explicit Euler), or the boundary conditions are wrong (probability "leaking" at the grid edge), or both. The normalization indicator catches both. **The limit.** The proof requires $\psi \to 0$ at infinity. For unnormalizable solutions (plane waves), normalization is not defined and the argument does not apply directly.

## 6. Expectation values

### 6.1 Position

For a position measurement, the average over many identically prepared experiments is

$$\langle x \rangle = \int_{-\infty}^{\infty} x\, |\psi(x, t)|^2 \, dx.$$

Each value of $x$ is weighted by the probability density of finding the particle there. This is just the centroid of $|\psi|^2$ — the same arithmetic as the mean of a probability distribution in any statistics course.

**Misconception, addressed inline.** *"$\langle x \rangle$ is where the particle is."* No. It is the average of many measurements on identically prepared states. Consider a double-peaked $\psi$, with $|\psi|^2$ symmetric around $x = 0$: $|\psi|^2 \propto e^{-(x-a)^2/\sigma^2} + e^{-(x+a)^2/\sigma^2}$. By symmetry $\langle x \rangle = 0$. But the probability of finding the particle near $x = 0$ is small — the density is suppressed between the peaks. The average is *not* a likely location. The average is the expected value of many measurements; for a bimodal distribution it can be far from any single high-probability region.

### 6.2 Momentum

This is where students stick. Momentum's expectation value is

$$\langle p \rangle = \int_{-\infty}^{\infty} \psi^*(x, t)\,\hat{p}\,\psi(x, t)\,dx, \quad \text{with}\quad \hat{p} = -i\hbar\frac{\partial}{\partial x}.$$

You cannot replace $\hat{p}$ with a number and integrate against $|\psi|^2$. The momentum is not multiplication; it is *differentiation*. Why?

The cleanest reason is the Fourier transform. Define

$$\phi(p, t) \equiv \frac{1}{\sqrt{2\pi\hbar}} \int_{-\infty}^{\infty} \psi(x, t)\, e^{-ipx/\hbar}\,dx.$$

Then $|\phi(p, t)|^2$ is the probability density for momentum measurements (this is the Born rule applied in momentum space — it follows from the structural symmetry of position and momentum in the canonical commutation relation). In momentum space, $\langle p \rangle = \int p\, |\phi|^2\, dp$, perfectly analogous to position. Translate back to position space using Parseval and integration by parts (Griffiths §1.5, §3.2):

$$\int p\, |\phi|^2\,dp = \int \psi^*(x)\, \left(-i\hbar\frac{\partial}{\partial x}\right) \psi(x)\,dx.$$

The differential operator is what position-space momentum looks like. The minus sign matters: $\hat{p} = -i\hbar\,\partial_x$, not $+i\hbar\,\partial_x$. **Misconception, addressed inline.** *"$\hat{p} = +i\hbar\,\partial_x$, surely the sign doesn't matter because we take an absolute square."* The sign matters for $\langle p \rangle$, which is not absolute-squared — it is an integral of $\psi^*\,\hat{p}\,\psi$ that is linear in $\hat{p}$. Get the sign wrong and $\langle p \rangle$ flips. Your simulation in Section 9 will catch this: a Gaussian with $k_0 > 0$ must give $\langle p \rangle > 0$.

### 6.3 Variances

$$\sigma_x^2 = \langle x^2 \rangle - \langle x \rangle^2, \quad \sigma_p^2 = \langle p^2 \rangle - \langle p \rangle^2.$$

The variance of position is the second central moment of $|\psi|^2$. The variance of momentum is the second central moment of $|\phi|^2$, equivalently $\int \psi^*\, \hat{p}^2 \psi\, dx - \langle p \rangle^2$ with $\hat{p}^2 = -\hbar^2\,\partial^2/\partial x^2$.

## 7. The uncertainty principle, properly stated

$$\sigma_x\, \sigma_p \geq \frac{\hbar}{2}.$$

Heisenberg's original 1927 paper ([*Über den anschaulichen Inhalt der quantentheoretischen Kinematik und Mechanik*, *Z. Phys.* 43, 172–198](http://dx.doi.org/10.1007/BF01397280)) presented a microscope thought experiment in which observing a particle's position with a photon necessarily kicked its momentum. This is the "measurement disturbance" reading, and it is the wrong reading. The sharper bound $\sigma_x \sigma_p \geq \hbar/2$ is from [Kennard, E. H. (1927), *Z. Phys.* 44, 326–352](https://link.springer.com/article/10.1007/BF01391200) [verify exact pagination], and the generalized version $\sigma_A \sigma_B \geq |\langle [\hat{A}, \hat{B}] \rangle| / 2$ from [Robertson, H. P. (1929), *Phys. Rev.* 34, 163](https://journals.aps.org/pr/abstract/10.1103/PhysRev.34.163) [verify].

**Misconception, addressed inline.** *"The uncertainty principle is about measurement disturbance — the photon kicks the electron."* It is not. The Kennard/Robertson inequality is a statistical statement about identically prepared ensembles. Prepare $10\,000$ copies of the same state $\psi$. Measure position on $5\,000$ of them; you get a distribution with standard deviation $\sigma_x$. Measure momentum on the other $5\,000$; you get a distribution with standard deviation $\sigma_p$. The inequality says the product $\sigma_x \sigma_p$ is at least $\hbar/2$. *No single measurement disturbs anything in this statement.* The inequality is a property of the shape of $\psi$ — a narrow $\psi$ in $x$ is necessarily a broad $\phi$ in $p$ by Fourier inversion, and the bound is the unavoidable Fourier-pair relation made quantitative.

There is a separate, distinct statement about how a position measurement *disturbs subsequent momentum measurements* on the same system — the so-called "measurement-disturbance" inequality, formalized by [Ozawa 2003, *Phys. Rev. A* 67, 042105](https://journals.aps.org/pra/abstract/10.1103/PhysRevA.67.042105). This is a different inequality with a different proof and different experimental tests ([Erhart et al. 2012, *Nature Physics* 8, 185–189](https://www.nature.com/articles/nphys2194)). The chapter mentions this distinction once, in this paragraph, and otherwise sticks to the Kennard inequality.

The Gaussian wave packet saturates the bound: $\sigma_x \sigma_p = \hbar/2$ exactly. This is the chapter's main worked example.

## 8. Worked example — the Gaussian saturates the bound

Let $\psi(x) = (1/(\pi a^2))^{1/4} \exp(-x^2/(2a^2)) \exp(i k_0 x)$. (We work at a single time and drop the $t$.) Compute each quantity on the page.

**Normalization check.** $|\psi|^2 = (1/(\pi a^2))^{1/2} \exp(-x^2/a^2)$, so $\int |\psi|^2\,dx = (1/(\pi a^2))^{1/2} \cdot a\sqrt{\pi} = 1$. ✓

**Position.** $\langle x \rangle = \int x\, |\psi|^2\,dx = 0$ (odd integrand). $\langle x^2 \rangle = \int x^2\, |\psi|^2\,dx = a^2/2$ (standard Gaussian second moment: $\int x^2 e^{-x^2/a^2}\,dx = (a^2/2)\cdot a\sqrt{\pi}$, divide by $(1/(\pi a^2))^{-1/2} = a\sqrt{\pi}$). Therefore

$$\sigma_x = \sqrt{\langle x^2 \rangle - \langle x \rangle^2} = \frac{a}{\sqrt{2}}.$$

**Momentum.** Compute $\hat{p}\psi = -i\hbar\,\partial_x \psi$. Differentiate:

$$\frac{\partial \psi}{\partial x} = \psi\,\left(-\frac{x}{a^2} + i k_0\right),$$

so

$$\hat{p}\psi = -i\hbar\, \psi\,\left(-\frac{x}{a^2} + i k_0\right) = \psi\left(\frac{i\hbar x}{a^2} + \hbar k_0\right).$$

Then

$$\psi^*\,\hat{p}\,\psi = |\psi|^2\left(\frac{i\hbar x}{a^2} + \hbar k_0\right).$$

Integrate. The first term is purely imaginary times an odd integrand ($x \cdot |\psi|^2$) — both odd, product even, but it carries a factor of $i$. Hmm — let's be careful. $x|\psi|^2$ is odd, so its integral is zero, and the imaginary part vanishes. The second term gives $\hbar k_0 \int |\psi|^2 \,dx = \hbar k_0$. Therefore

$$\langle p \rangle = \hbar k_0.$$

For $\langle p^2 \rangle$, apply $\hat{p}^2 = -\hbar^2\,\partial_x^2$:

$$\frac{\partial^2 \psi}{\partial x^2} = \psi\left(-\frac{1}{a^2} + \left(-\frac{x}{a^2} + i k_0\right)^2\right) = \psi\left(-\frac{1}{a^2} + \frac{x^2}{a^4} - \frac{2 i k_0 x}{a^2} - k_0^2\right).$$

So

$$\hat{p}^2 \psi = -\hbar^2 \psi\left(-\frac{1}{a^2} + \frac{x^2}{a^4} - \frac{2 i k_0 x}{a^2} - k_0^2\right) = \hbar^2 \psi \left(\frac{1}{a^2} - \frac{x^2}{a^4} + \frac{2 i k_0 x}{a^2} + k_0^2\right).$$

Multiply by $\psi^*$ and integrate. The $|\psi|^2 \cdot x$ term is odd and vanishes. We are left with

$$\langle p^2 \rangle = \hbar^2 \left(\frac{1}{a^2} - \frac{\langle x^2 \rangle}{a^4} + k_0^2\right) = \hbar^2\left(\frac{1}{a^2} - \frac{a^2/2}{a^4} + k_0^2\right) = \hbar^2\left(\frac{1}{2 a^2} + k_0^2\right).$$

The variance:

$$\sigma_p^2 = \langle p^2 \rangle - \langle p \rangle^2 = \hbar^2\left(\frac{1}{2 a^2} + k_0^2\right) - \hbar^2 k_0^2 = \frac{\hbar^2}{2 a^2}.$$

$$\sigma_p = \frac{\hbar}{\sqrt{2}\, a}.$$

**The product.**

$$\sigma_x \sigma_p = \frac{a}{\sqrt{2}} \cdot \frac{\hbar}{\sqrt{2}\, a} = \frac{\hbar}{2}.$$

Equality. The Gaussian saturates the Kennard bound. Every other normalizable wave function gives $\sigma_x \sigma_p > \hbar/2$. The Gaussian is the *minimum-uncertainty state*.

**The lesson.** The relationship $\sigma_x \propto a$ and $\sigma_p \propto 1/a$ is the Fourier-pair relation made concrete: narrow $\psi$ in $x$ means broad $\psi$ in $p$, with the proportionality constants tuned so the product is exactly $\hbar/2$. **The limit.** Other states (square pulses, double Gaussians, infinite-well eigenstates) give strictly $\sigma_x \sigma_p > \hbar/2$. The simulation in Section 9 lets you verify this for every wave function in the gallery, by displaying $\sigma_x \sigma_p / (\hbar/2)$ live.

## 9. LLM Exercise — the probability explorer

The signature deliverable: `01-probability-explorer.html`. A wave-function gallery with three stacked SVG panels (Re $\psi$, Im $\psi$, $|\psi|^2$), a live numerics panel that shows $\langle x \rangle$, $\langle p \rangle$, $\sigma_x$, $\sigma_p$, and the ratio $\sigma_x \sigma_p / (\hbar/2)$ that reads $1.000$ for the Gaussian.

### Part A — Updated `CLAUDE.md` snippet for this chapter

Add this stanza to your existing `CLAUDE.md` (or paste alongside it as a chapter-specific extension):

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

1. **Saturate the bound.** Select the Gaussian. Vary $a$ from $0.2$ nm to $4$ nm. Watch $\sigma_x$ change. Watch $\sigma_p$ change inversely. Watch the ratio $\sigma_x \sigma_p / (\hbar/2)$ stay locked at $1.000$. Write down what this confirms about the Gaussian.

2. **Exceed the bound.** Switch to the infinite-well eigenstate, $n = 1$, $L = 10$ nm. The ratio reads about $1.136$. Now $n = 2$. Watch $\sigma_x$ change very little (the wave function fills the same well) while $\sigma_p$ grows. The ratio increases. State the trend: as $n$ grows, does $\sigma_x \sigma_p / (\hbar/2)$ approach a limit, grow without bound, or oscillate? Try $n = 1$ through $n = 10$.

3. **The double-peaked case.** Select the double Gaussian. $d = 2$ nm, $\sigma = 0.3$ nm. $\langle x \rangle$ reads $0$. Now look at $|\psi|^2$: the probability of finding the particle within $\pm 0.5$ nm of $x = 0$ is tiny. Write one sentence saying what this tells you about $\langle x \rangle$ as a "prediction" for a single measurement.

4. **The square pulse.** Select the square pulse, width $w = 2$ nm. $\sigma_x$ is finite ($w/\sqrt{12}$). $\sigma_p$ should be infinite (or, on a finite grid, very large) because the Fourier transform of a square pulse decays like $1/p$ and $\int p^2 / p^2 \,dp$ diverges. The ratio panel should label this as "undefined" or display a very large number with a warning. *State why this is a feature of the wave function's discontinuity at $\pm w/2$, not a bug in the simulation.*

5. **Free-particle time evolution (Gaussian only).** Run time evolution. Watch $\sigma_x$ grow. Watch $\sigma_p$ stay constant (free particle conserves momentum). Watch the ratio $\sigma_x \sigma_p / (\hbar/2)$ grow above $1.000$ as time advances. The Gaussian saturates the bound only at $t = 0$; under free evolution it does not stay minimum-uncertainty. Explain in two sentences using $\sigma_x(t)^2 = \sigma_x(0)^2 + (\hbar t / (2 m \sigma_x(0)))^2$.

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

When you watch the momentum-space panel of the infinite-well eigenstate split into two peaks, you have a concrete picture for *why* the energy eigenstates of a confined particle are standing waves rather than running waves. Chapter 2 will name this.

## 10. What would change my mind

The chapter's interpretive position is that $\sigma_x \sigma_p \geq \hbar/2$ is a *structural* statement about the shape of $\psi$, not a statement about measurement disturbance. Ozawa's 2003 reformulation ([*Phys. Rev. A* 67, 042105](https://journals.aps.org/pra/abstract/10.1103/PhysRevA.67.042105)) showed there are two distinct inequalities — Kennard's (preparation) and Ozawa's (measurement-disturbance) — and they have different bounds. Erhart et al. 2012 ([*Nature Physics* 8, 185–189](https://www.nature.com/articles/nphys2194)) and Rozema et al. 2012 ([*Phys. Rev. Lett.* 109, 100404](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.109.100404)) measured experimental violations of Heisenberg's original measurement-disturbance form while leaving the Kennard preparation form intact. If a careful experiment found a violation of Kennard's $\sigma_x \sigma_p \geq \hbar/2$ for a preparation-only protocol on identically prepared states, the chapter's framing — and most of standard QM — would have to revise. None has been seen.

## 11. Still puzzling

- The Born rule is a postulate in this book. I have flagged that other research programs (Zurek's envariance, many-worlds branch-counting) try to derive it from other axioms. I do not know with confidence whether any derivation should be called "settled," and I have chosen not to take a position. The chapter would be cleaner if I did.
- The probability current $J$ has a beautiful interpretation as a *flow* of probability density. It works for a single particle in 1D. For many particles in 3D it generalizes, but the geometric intuition is harder, and the chapter does not yet show that generalization. (Chapters 5 and 6 will.)
- The square pulse's divergent $\sigma_p$ is real but felt as a numerical artifact by most students. I am not sure the best way to teach it. The current move — label it "undefined" with a warning — is honest but unsatisfying.
- The choice to compute $\langle p \rangle$ via FFT is pedagogically motivated (it shows the position-momentum Fourier duality directly) but it introduces grid-edge artifacts that real-space integration of $\psi^* \hat{p} \psi$ would not. The chapter has not yet decided whether to teach this as a feature or a footnote.

**Tags:** Born-rule, normalization, probability-current, expectation-value, uncertainty-principle, Fourier-duality, Kennard, McKagan

---

*Bridge to Chapter 2: You now know what $\psi$ means and how to extract physics from it. But what determines $\psi(x)$ in the first place? The answer requires a potential $V(x)$ and an eigenvalue equation. Next chapter, the time-independent Schrödinger equation.*
