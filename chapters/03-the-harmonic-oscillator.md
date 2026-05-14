# Chapter 3 — The Harmonic Oscillator

> The most important exactly solvable system in quantum mechanics — the one that appears wherever something vibrates near equilibrium, and the gateway to the operator formalism that takes over in Chapter 4.

---

## 1. What this chapter is doing

You have already solved the infinite square well. That problem had hard walls, oscillating eigenfunctions, and a tidy $n^2$ spectrum. The chapter you are reading now does something different. It takes the *smoothest possible* confining potential — a parabola — and shows that the spectrum becomes evenly spaced, that the eigenfunctions are Gaussian-damped oscillations, and that a single piece of algebra ($[\hat{a}_-, \hat{a}_+] = 1$) generates the entire structure without solving a differential equation. Then it shows you the wave packet that *does* oscillate the way you wanted it to — the coherent state — and lets you watch it slosh.

We are closing Act One here. After this chapter, the book pivots from concrete wave-function calculations to the abstract operator formalism. The harmonic oscillator is the bridge. Its ladder operators are the first encounter with the kind of algebraic move that, in Chapter 4, becomes a worldview.

## 2. Learning objectives

By the end of this chapter you should be able to:

- Write down the harmonic-oscillator Hamiltonian and explain why it shows up in almost every physical system.
- Derive $[\hat{a}_-, \hat{a}_+] = 1$ from $[\hat{x}, \hat{p}] = i\hbar$ explicitly.
- Use the commutator $[\hat{H}, \hat{a}_\pm] = \pm\hbar\omega\,\hat{a}_\pm$ to climb and descend the energy ladder.
- Construct the ground-state wave function $\psi_0(x)$ by solving $\hat{a}_-|0\rangle = 0$ as a first-order ODE.
- Recognize the Hermite-polynomial form of the eigenstates and identify nodes, classical turning points, and tunneling into the classically forbidden region.
- Distinguish a stationary eigenstate (static probability density) from a coherent state (Gaussian sloshing without spreading).
- Build a D3 simulation that displays $\psi_n(x)$, $|\psi_n|^2$, and the time evolution of a coherent state.

## 3. Motivating problem

A diatomic molecule — say hydrogen chloride — sits in a vibrational mode. The bond stretches and contracts. Infrared spectroscopy measures the energy required to bump the molecule from one vibrational state to the next, and the answer is a single, sharply defined photon energy: for HCl, transitions cluster near 2886 cm$^{-1}$ in the gas phase [verify against NIST WebBook]. Not a continuous spectrum. A line.

Classical mechanics is comfortable with this much: a mass on a spring oscillates at $\omega = \sqrt{k/m}$ regardless of amplitude. Quantum mechanics is *not* comfortable. A quantum system that can only absorb photons of one energy must have an evenly spaced ladder of levels separated by $\hbar\omega$. Where does that ladder come from? Why is the lowest rung *not* at zero — why is the molecule moving even at absolute zero, when classical physics says it should be sitting still at the bottom of the well? And once we have the spectrum, can we make it slosh, like a classical oscillator?

These three questions are the chapter. The Hamiltonian:

$$\hat{H} = \frac{\hat{p}^2}{2m} + \frac{1}{2}m\omega^2\hat{x}^2$$

is the simplest non-trivial expression in quantum mechanics. Two terms. One kinetic, one quadratic in position. Nothing fancy. And yet this object is everywhere — molecular vibrations, lattice phonons, photons in a cavity, every small-oscillation problem near equilibrium. The reason is simple. Expand any smooth potential $V(x)$ about a stable minimum $x_0$:

$$V(x) \approx V(x_0) + \tfrac{1}{2}V''(x_0)(x - x_0)^2 + \cdots$$

The linear term vanishes at a minimum. The quadratic term is what is left. Set $m\omega^2 = V''(x_0)$ and you have the harmonic oscillator. That is why this Hamiltonian governs a generic system held near equilibrium. Feynman called it "the most important problem"; he was not exaggerating. The harmonic approximation is the *reason* small oscillations are tractable in any physical system you will meet for the rest of your career.

## 4. Concept block — the algebraic move

### 4.1 Factor the Hamiltonian

Here is the trick. Define two operators:

$$\hat{a}_\pm = \frac{1}{\sqrt{2\hbar m\omega}}\bigl(\mp i\hat{p} + m\omega\hat{x}\bigr)$$

These look ugly. Bear with the bookkeeping. We are going to multiply them out and discover something clean.

Compute $\hat{a}_-\hat{a}_+$:

$$\hat{a}_-\hat{a}_+ = \frac{1}{2\hbar m\omega}\bigl(i\hat{p} + m\omega\hat{x}\bigr)\bigl(-i\hat{p} + m\omega\hat{x}\bigr)$$

$$= \frac{1}{2\hbar m\omega}\bigl(\hat{p}^2 + m^2\omega^2\hat{x}^2 + im\omega(\hat{p}\hat{x} - \hat{x}\hat{p})\bigr)$$

$$= \frac{1}{2\hbar m\omega}\bigl(\hat{p}^2 + m^2\omega^2\hat{x}^2 - im\omega \cdot i\hbar\bigr)$$

where the last step used $[\hat{x}, \hat{p}] = i\hbar$, so $\hat{p}\hat{x} - \hat{x}\hat{p} = -i\hbar$. Clean up:

$$\hat{a}_-\hat{a}_+ = \frac{\hat{H}}{\hbar\omega} + \tfrac{1}{2}$$

Equivalently,

$$\hat{H} = \hbar\omega\bigl(\hat{a}_-\hat{a}_+ - \tfrac{1}{2}\bigr) = \hbar\omega\bigl(\hat{a}_+\hat{a}_- + \tfrac{1}{2}\bigr)$$

The two forms differ because $\hat{a}_-$ and $\hat{a}_+$ do not commute. Subtract them:

$$[\hat{a}_-, \hat{a}_+] = \hat{a}_-\hat{a}_+ - \hat{a}_+\hat{a}_- = 1$$

This is the *only* algebraic input we need. The entire spectrum of the harmonic oscillator falls out of this single commutator. (Griffiths §2.3.1; Liboff §7.3.)

### 4.2 The ladder

Compute $[\hat{H}, \hat{a}_+]$. Use $\hat{H} = \hbar\omega(\hat{a}_+\hat{a}_- + 1/2)$:

$$[\hat{H}, \hat{a}_+] = \hbar\omega[\hat{a}_+\hat{a}_-, \hat{a}_+] = \hbar\omega\,\hat{a}_+[\hat{a}_-, \hat{a}_+] = \hbar\omega\,\hat{a}_+$$

Similarly $[\hat{H}, \hat{a}_-] = -\hbar\omega\,\hat{a}_-$. Now suppose $|n\rangle$ is an eigenstate of $\hat{H}$ with energy $E_n$: $\hat{H}|n\rangle = E_n|n\rangle$. What is $\hat{H}(\hat{a}_+|n\rangle)$? Use the commutator:

$$\hat{H}\hat{a}_+|n\rangle = (\hat{a}_+\hat{H} + [\hat{H}, \hat{a}_+])|n\rangle = \hat{a}_+E_n|n\rangle + \hbar\omega\,\hat{a}_+|n\rangle = (E_n + \hbar\omega)\hat{a}_+|n\rangle$$

So $\hat{a}_+|n\rangle$ is an eigenstate of $\hat{H}$ with energy $E_n + \hbar\omega$. The operator $\hat{a}_+$ raises the energy by one quantum. By the same argument $\hat{a}_-$ lowers it by one quantum. They are *ladder operators*: a raising operator and a lowering operator.

### 4.3 The ground state — why the ladder terminates downward

The descent cannot go on forever. The Hamiltonian $\hat{H} = \hat{p}^2/2m + (1/2)m\omega^2\hat{x}^2$ is a sum of squares of Hermitian operators, so $\langle\psi|\hat{H}|\psi\rangle \geq 0$ for any state. Energies cannot be negative. The lowering must stop somewhere. The only way it stops is if some state $|0\rangle$ exists with

$$\hat{a}_-|0\rangle = 0$$

Apply $\hat{a}_+$ to both sides and use $\hat{H} = \hbar\omega(\hat{a}_+\hat{a}_- + 1/2)$:

$$\hat{H}|0\rangle = \hbar\omega\bigl(\hat{a}_+\hat{a}_- + \tfrac{1}{2}\bigr)|0\rangle = \tfrac{1}{2}\hbar\omega|0\rangle$$

The ground-state energy is $E_0 = \hbar\omega/2$. This is the **zero-point energy** — and it is not an artifact. Try to set $E_0 = 0$ by demanding a state with $\sigma_x = 0$ and $\sigma_p = 0$ simultaneously: the uncertainty principle forbids it. The ground state is the minimum-uncertainty compromise — a Gaussian wide enough in $x$ to spread $p$ just enough to satisfy $\sigma_x\sigma_p \geq \hbar/2$, with $\langle\hat{H}\rangle = \hbar\omega/2$ as the price.

This is not a calculation you can argue with. The Casimir force between conducting plates, measured by Lamoreaux in 1997 ([*Phys. Rev. Lett.* 78, 5](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.78.5)) to within roughly 5% of theory, is a macroscopic consequence of summed zero-point energies. Liquid helium does not freeze at atmospheric pressure even as $T \to 0$ because zero-point motion is enough to keep it fluid. Zero-point energy is real, and it has a bill you can read.

### 4.4 The whole ladder

From $|0\rangle$, apply $\hat{a}_+$ repeatedly. Each application raises the energy by $\hbar\omega$:

$$E_n = \bigl(n + \tfrac{1}{2}\bigr)\hbar\omega, \quad n = 0, 1, 2, \ldots$$

The normalized ladder relations (which we will not derive in full but you can verify) are:

$$\hat{a}_+|n\rangle = \sqrt{n+1}\,|n+1\rangle, \quad \hat{a}_-|n\rangle = \sqrt{n}\,|n-1\rangle$$

Notice what just happened. We did no differential equations. We solved no boundary-value problem. From $[\hat{a}_-, \hat{a}_+] = 1$ and the non-negativity of $\hat{H}$, the entire spectrum dropped out. This is the algebraic method.

**Misconception 1.** *"Ladder operators are a slick trick. The real way to solve this is power series."* No. The algebra generalizes. In quantum field theory, $\hat{a}_+$ and $\hat{a}_-$ become creation and annihilation operators for photons; a state with $n$ excitations of a mode is a state with $n$ photons. In Chapter 6 the same algebra reappears as $\hat{J}_\pm$ for angular momentum. The Hamiltonian $\hat{H} = \hbar\omega(\hat{a}_+\hat{a}_- + 1/2)$ is the same expression — number operator plus zero-point — in every context where harmonic structure appears. The trick is the structure.

**Misconception 2.** *"$E_0 = \hbar\omega/2$ is a convention; you can subtract it off."* Sometimes you do, when only energy *differences* matter. But the absolute value is real and observable in the cases listed above. Subtraction is bookkeeping, not physics.

## 5. Concept block — the analytic confirmation

### 5.1 The ground state explicitly

Solve $\hat{a}_-|0\rangle = 0$ in the position representation. Substituting $\hat{p} = -i\hbar\,\partial_x$:

$$\hat{a}_-\psi_0(x) = \frac{1}{\sqrt{2\hbar m\omega}}\bigl(\hbar\,\partial_x + m\omega x\bigr)\psi_0(x) = 0$$

This is a first-order ODE: $\psi_0'(x) = -(m\omega/\hbar)x\,\psi_0(x)$. Separate variables:

$$\frac{d\psi_0}{\psi_0} = -\frac{m\omega}{\hbar}x\,dx \;\Longrightarrow\; \psi_0(x) = A\,e^{-m\omega x^2/(2\hbar)}$$

A Gaussian. Normalize $\int|\psi_0|^2\,dx = 1$ to fix $A = (m\omega/\pi\hbar)^{1/4}$. The ground state of the harmonic oscillator is just a Gaussian — the simplest non-trivial wave function you have seen.

### 5.2 Excited states by ladder

Higher states follow by applying $\hat{a}_+$. The first excited state:

$$\psi_1(x) = \hat{a}_+\psi_0(x) = \frac{1}{\sqrt{2\hbar m\omega}}\bigl(-\hbar\,\partial_x + m\omega x\bigr)\,A\,e^{-m\omega x^2/(2\hbar)} = A\sqrt{\frac{2m\omega}{\hbar}}\,x\,e^{-m\omega x^2/(2\hbar)}$$

Each application of $\hat{a}_+$ multiplies the Gaussian by a polynomial of degree one higher. Those polynomials are the **Hermite polynomials**. Introducing $\xi = \sqrt{m\omega/\hbar}\,x$, the eigenstates take the form:

$$\psi_n(x) = \biggl(\frac{m\omega}{\pi\hbar}\biggr)^{1/4}\frac{1}{\sqrt{2^n n!}}\,H_n(\xi)\,e^{-\xi^2/2}$$

with $H_0 = 1$, $H_1 = 2\xi$, $H_2 = 4\xi^2 - 2$, $H_3 = 8\xi^3 - 12\xi$, generated by the recursion $H_{n+1}(\xi) = 2\xi H_n(\xi) - 2n H_{n-1}(\xi)$. (Griffiths §2.3.2; Liboff §7.3.)

### 5.3 What the eigenstates look like

Two facts to internalize:

1. The $n$-th eigenstate has exactly $n$ nodes (zero crossings, not counting $\pm\infty$). The ground state has none. The first excited state crosses zero once at $x = 0$.

2. The classical turning points for energy $E_n = (n+1/2)\hbar\omega$ sit at $\xi_n = \sqrt{2n+1}$. For small $n$, $|\psi_n|^2$ piles up at the center — the *opposite* of where a classical particle spends most of its time (a classical particle moves fastest at the bottom of the well and spends most of its time near the turning points). For large $n$, the probability density oscillates rapidly and *averages* to the classical distribution. That is the **correspondence principle** in action: the quantum description, smoothed, recovers the classical one in the high-$n$ limit.

About 16% [verify against Griffiths Problem 2.15] of the ground-state probability sits *outside* the classical turning points — the wave function tunnels into the classically forbidden region. The classical particle of energy $\hbar\omega/2$ is rigorously confined; the quantum particle is not.

### 5.4 Eigenstates do not oscillate

This is the single biggest source of confusion fresh from classical mechanics, and the simulation must make it visible immediately. The time-dependent eigenstate is:

$$\Psi_n(x,t) = \psi_n(x)\,e^{-iE_n t/\hbar}$$

so

$$|\Psi_n(x,t)|^2 = |\psi_n(x)|^2$$

The probability density is *static*. The phase rotates in the complex plane, but the magnitude does not. An energy eigenstate of the harmonic oscillator is, in every observable way, sitting still. Nothing sloshes. If the harmonic oscillator were only its eigenstates, classical oscillation would never emerge.

## 6. Concept block — coherent states, the bridge to classical motion

### 6.1 What does oscillate?

If eigenstates do not, what does? *Superpositions* of eigenstates do. The simplest demonstration: take $\Psi(x,0) = (\psi_0 + \psi_1)/\sqrt{2}$. Then

$$\Psi(x,t) = \frac{1}{\sqrt{2}}\bigl(\psi_0\,e^{-iE_0t/\hbar} + \psi_1\,e^{-iE_1t/\hbar}\bigr)$$

and

$$|\Psi(x,t)|^2 = \tfrac{1}{2}\bigl(|\psi_0|^2 + |\psi_1|^2\bigr) + \mathrm{Re}\bigl[\psi_0\psi_1^*\,e^{-i(E_0 - E_1)t/\hbar}\bigr]$$

The cross-term beats at frequency $(E_1 - E_0)/\hbar = \omega$. The probability density sloshes back and forth. But — and this is the catch — it also distorts. A general two-state superposition does not maintain its shape.

### 6.2 The coherent state

A **coherent state** $|\alpha\rangle$ is defined by being an eigenstate of $\hat{a}_-$:

$$\hat{a}_-|\alpha\rangle = \alpha\,|\alpha\rangle$$

for any complex number $\alpha$. Expanded in the energy basis:

$$|\alpha\rangle = e^{-|\alpha|^2/2}\sum_{n=0}^\infty \frac{\alpha^n}{\sqrt{n!}}\,|n\rangle$$

This is *not* an eigenstate of $\hat{H}$. Its energy is uncertain — the probability of finding $n$ quanta is Poisson with mean $\langle n\rangle = |\alpha|^2$. But:

- $\langle\hat{x}(t)\rangle = \sqrt{2\hbar/m\omega}\,|\alpha|\cos(\omega t - \arg\alpha)$
- $\langle\hat{p}(t)\rangle = -\sqrt{2m\hbar\omega}\,|\alpha|\sin(\omega t - \arg\alpha)$
- $\sigma_x\sigma_p = \hbar/2$ at all times — the coherent state saturates the uncertainty principle.
- The wave-packet shape is a Gaussian with the *same width as the ground state, forever*.

The packet just orbits. Position oscillates classically, momentum oscillates classically, and the wave packet rides the orbit without spreading. This is the quantum state that most resembles a classical particle in a harmonic well.

Roy Glauber introduced these in his 1963 paper "[Coherent and Incoherent States of the Radiation Field](https://journals.aps.org/pr/abstract/10.1103/PhysRev.131.2766)" (*Physical Review* 131, 2766), in the context of laser light. He shared the 2005 Nobel for this work. Coherent states are the *physical* states of the electromagnetic field that interact with classical detectors. The output of an ideal laser is a coherent state of the cavity mode.

**Misconception.** *"Coherent states are classical states."* They are quantum states with classical-like expectation values. They still carry quantum signatures — the Poisson photon-number distribution is the giveaway. Squeezed light, used by LIGO to push below the standard quantum limit [verify exact 2019 *PRL* citation], is a *different* minimum-uncertainty state that trades reduced noise in one quadrature for increased noise in the other. The classical limit is not "coherent state"; it is a hierarchy of nearly-classical objects, of which coherent states are the most symmetric.

## 7. Worked examples

### 7.1 Building $\psi_0$ from $\hat{a}_-|0\rangle = 0$ — start to finish

The defining condition:

$$\bigl(\hbar\,\partial_x + m\omega x\bigr)\psi_0(x) = 0$$

This is separable:

$$\frac{d\psi_0}{\psi_0} = -\frac{m\omega}{\hbar}x\,dx$$

Integrate:

$$\ln\psi_0 = -\frac{m\omega}{2\hbar}x^2 + \mathrm{const} \;\Longrightarrow\; \psi_0(x) = A\exp\!\biggl(-\frac{m\omega x^2}{2\hbar}\biggr)$$

Normalize using $\int_{-\infty}^\infty e^{-x^2/\sigma^2}\,dx = \sigma\sqrt{\pi}$ with $\sigma = \sqrt{\hbar/m\omega}$:

$$1 = |A|^2\sigma\sqrt{\pi} \;\Longrightarrow\; A = (m\omega/\pi\hbar)^{1/4}$$

Compute the energy:

$$\langle\hat{H}\rangle_0 = \hbar\omega\bigl(\langle\hat{a}_+\hat{a}_-\rangle + \tfrac{1}{2}\bigr) = \tfrac{1}{2}\hbar\omega$$

because $\hat{a}_-|0\rangle = 0$. The ground-state energy is exactly $\hbar\omega/2$.

### 7.2 The energy of the $n$-th state by induction

Claim: $E_n = (n + 1/2)\hbar\omega$. Proof by induction on $n$.

Base case: $E_0 = \hbar\omega/2$, established above.

Inductive step: suppose $\hat{H}|n\rangle = (n + 1/2)\hbar\omega|n\rangle$. Then

$$\hat{H}\bigl(\hat{a}_+|n\rangle\bigr) = \bigl(\hat{a}_+\hat{H} + [\hat{H}, \hat{a}_+]\bigr)|n\rangle = \hat{a}_+(n+\tfrac{1}{2})\hbar\omega|n\rangle + \hbar\omega\,\hat{a}_+|n\rangle = (n+\tfrac{3}{2})\hbar\omega\,\hat{a}_+|n\rangle$$

So $\hat{a}_+|n\rangle$ is an eigenstate with energy $(n+1+1/2)\hbar\omega$. Normalize: $\hat{a}_+|n\rangle = \sqrt{n+1}\,|n+1\rangle$ (we will not derive the prefactor here; it follows from computing $\langle n|\hat{a}_-\hat{a}_+|n\rangle = n+1$). The induction closes. The whole spectrum is $E_n = (n+1/2)\hbar\omega$.

### 7.3 Expectation values without integrals

Express position and momentum in terms of ladder operators:

$$\hat{x} = \sqrt{\frac{\hbar}{2m\omega}}\,(\hat{a}_+ + \hat{a}_-), \quad \hat{p} = i\sqrt{\frac{m\hbar\omega}{2}}\,(\hat{a}_+ - \hat{a}_-)$$

Then $\langle n|\hat{x}|n\rangle = 0$ and $\langle n|\hat{p}|n\rangle = 0$ — the ladder ops shift the basis state, and orthogonality kills the inner product. For the variance:

$$\langle n|\hat{x}^2|n\rangle = \frac{\hbar}{2m\omega}\langle n|(\hat{a}_+ + \hat{a}_-)^2|n\rangle = \frac{\hbar}{2m\omega}(2n+1)$$

(The cross terms $\hat{a}_+\hat{a}_+$ and $\hat{a}_-\hat{a}_-$ vanish on diagonal matrix elements; $\hat{a}_+\hat{a}_- + \hat{a}_-\hat{a}_+ = 2\hat{a}_+\hat{a}_- + 1 = 2n + 1$ on $|n\rangle$.) Similarly $\langle n|\hat{p}^2|n\rangle = (m\hbar\omega/2)(2n+1)$. The product:

$$\sigma_x\sigma_p = \bigl(n + \tfrac{1}{2}\bigr)\hbar$$

For $n = 0$ this saturates Heisenberg at $\hbar/2$. For higher $n$, the product grows linearly. No integrals were needed. This is the payoff of the ladder algebra.

## 8. Exercises

**Warm-up.**

1. Verify $[\hat{a}_-, \hat{a}_+] = 1$ explicitly from $[\hat{x}, \hat{p}] = i\hbar$ by writing out both operators in terms of $\hat{x}$ and $\hat{p}$.

2. Write down the first four Hermite polynomials and check the recursion $H_{n+1}(\xi) = 2\xi H_n - 2n H_{n-1}$ for $n = 1, 2$.

3. Sketch $\psi_0, \psi_1, \psi_2, \psi_3$ and mark each zero crossing. Count nodes.

**Application.**

4. A diatomic molecule has reduced mass $\mu$ and a bond with spring constant $k$. The vibrational frequency is $\omega = \sqrt{k/\mu}$. Estimate the ground-state vibrational energy of HCl using $\omega \approx 5.4 \times 10^{14}$ rad/s [verify], express it in eV, and compare to thermal energy $k_BT$ at room temperature. Are most HCl molecules in the vibrational ground state at room temperature?

5. Compute $\langle n|\hat{x}^4|n\rangle$ using ladder operators. (Hint: $\hat{x}^2 = (\hbar/2m\omega)(\hat{a}_+ + \hat{a}_-)^2$; expand and keep only terms that return to $|n\rangle$.)

6. For the coherent state $|\alpha\rangle$, show that $\langle\alpha|\hat{n}|\alpha\rangle = |\alpha|^2$ where $\hat{n} = \hat{a}_+\hat{a}_-$ is the number operator. Show that the variance $\langle\hat{n}^2\rangle - \langle\hat{n}\rangle^2 = |\alpha|^2$ — the Poisson signature.

**Synthesis.**

7. Show that the ground-state probability of being outside the classical turning points $|x| > \sqrt{\hbar/m\omega}$ is $1 - \mathrm{erf}(1)$. Evaluate numerically and compare to the 16% [verify] claim in the text.

8. Two coherent states $|\alpha\rangle$ and $|\beta\rangle$ are *not* orthogonal in general. Compute $|\langle\alpha|\beta\rangle|^2$. (Hint: use the expansion in $|n\rangle$ and sum the series.) Show that the overlap is large when $\alpha$ and $\beta$ are close in the complex plane and exponentially small when they are far apart.

**Challenge.**

9. Time-evolve $|\alpha\rangle$ under the harmonic Hamiltonian. Show that $|\alpha(t)\rangle = e^{-i\omega t/2}|\alpha e^{-i\omega t}\rangle$ — the coherent state remains coherent, with its $\alpha$ rotating in the complex plane at frequency $\omega$. The wave packet orbits in phase space.

10. The Casimir force between two parallel conducting plates of area $A$ separated by distance $d$ is, to leading order, $F = -(\pi^2\hbar c A)/(240 d^4)$. The sign is *attractive*. Trace the origin: it comes from the *difference* between the zero-point energies of EM modes with and without the plates. Without computing the full sum, explain why the difference is finite even though each sum is infinite, and why zero-point motion of a single oscillator generalizes to this many-mode result.

## 9. What would change my mind

If a precision measurement of the Casimir force at high accuracy disagreed with the QED prediction by more than the theoretical uncertainty, or if measured vibrational energy levels in a clean diatomic system consistently failed to match $(n+1/2)\hbar\omega$ to leading order without an obvious anharmonic explanation, the chapter's framing — that the harmonic oscillator is exactly the right model for small-oscillation problems and that zero-point energy is a real, observable consequence — would be in trouble. So far, both checks have come back in the theory's favor.

## 10. Still puzzling

The infinity that disappears when you compute Casimir differences is one of the most well-behaved infinities in physics. The infinity that *does not* disappear — the vacuum energy density of the universe, predicted by summing zero-point energies of all fields up to the Planck scale and exceeding the observed cosmological constant by something like 120 orders of magnitude — is one of the worst. The same harmonic-oscillator machinery, applied to two different problems, gives one of physics' cleanest predictions and one of its biggest open questions. I do not know what fixes this, and neither does anyone else.

## 11. LLM Exercise — the harmonic oscillator simulation

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

1. With $\omega = 1$, set the mode to "Eigenstate" and toggle $n$ from 0 to 5. Watch the probability density. Confirm: it does not move. (The phase rotates, but $|\psi|^2$ does not change in time.) Now switch to "Coherent state" with $|\alpha| = 1$. Watch the probability density slosh. Note the period $T = 2\pi/\omega$.

2. Increase $|\alpha|$ from $0$ to $3$ slowly. What happens to the *amplitude* of the orbit in phase space? What happens to the *width* of the wave packet? Predict before sliding; check after.

3. Set $|\alpha| = 0$. What state does the coherent state reduce to? Check by comparing the wave function to the eigenstate $n = 0$.

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

*Sources consulted: Griffiths §2.3 (algebraic and analytic methods, Hermite polynomials, problems 2.10–2.20); Liboff §7.2–7.3 (classical setup, eigenfunctions, p. 190–211); Lahiri & Pal *A First Book of Quantum Field Theory* (ladder operators as creation/annihilation operators in QFT, pantry); Glauber, "[Coherent and Incoherent States of the Radiation Field](https://journals.aps.org/pr/abstract/10.1103/PhysRev.131.2766)", *Physical Review* 131, 2766 (1963); Lamoreaux, "Demonstration of the Casimir Force in the 0.6 to 6 μm Range", *Physical Review Letters* 78, 5 (1997).*

*Tags: harmonic-oscillator, ladder-operators, hermite-polynomials, coherent-states, zero-point-energy, casimir-effect, d3-simulation*

*Status: draft for Nik's review. Voice-anchor check pending — root `style/` and `books/quantum-mechanics-with-llms/style/` not yet inspected. Flag: voice-unanchored if both empty. Several `[verify]` flags throughout — see specifically CO/HCl vibrational frequencies, 16% tunneling fraction, LIGO squeezed-light PRL date.*
