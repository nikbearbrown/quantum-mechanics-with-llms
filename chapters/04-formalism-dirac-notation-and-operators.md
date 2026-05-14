# Chapter 4 — Formalism: Dirac Notation and Operators
*The State Is Not the Wave Function.*

> The chapter where the book stops doing wave-function problems and starts doing *quantum mechanics* — the same physics in basis-free language, with the qubit as the pedagogical anchor.

---

Here is a thing that should bother you.

The wave function $\psi(x)$ tells you the probability amplitude for finding the particle at position $x$. Its Fourier transform $\tilde{\psi}(p)$ tells you the probability amplitude for finding the particle with momentum $p$. These two functions contain identical physical information — one is a complete description of the state — and yet they look nothing alike. One oscillates in position; the other oscillates in momentum. One spreads when the other is narrow.

So which one is "the state"?

The answer is neither. The state is the *object* that has $\psi(x)$ as its position-space components and $\tilde{\psi}(p)$ as its momentum-space components. The same way a vector in three-dimensional space is not its $(x, y, z)$ Cartesian coordinates — it is the abstract arrow, whose components depend on which basis you project it onto — the quantum state is not the wave function. The wave function is a list of components in one chosen basis. The state is the vector.

This is not philosophy. It is the difference between a calculation you have to redo every time you change basis and one you write down once and evaluate anywhere. This chapter introduces the language — Dirac notation, Hilbert space, Hermitian operators — that lets you do the second thing.

---

## The abstract state

A **quantum state** is a unit vector $|\psi\rangle$ in a complex inner-product space, defined up to an overall phase. The angle-bracket notation is due to Dirac — he called these "ket" vectors. Their duals, linear functionals that map kets to complex numbers, are "bra" vectors $\langle\phi|$. The inner product of $\langle\phi|$ with $|\psi\rangle$ is the complex number $\langle\phi|\psi\rangle$, sometimes written as a "bracket." The product in the other order — $|\psi\rangle\langle\phi|$ — is not a number but an *operator*, the linear map that takes any $|\chi\rangle$ to $\langle\phi|\chi\rangle\,|\psi\rangle$.

The position-space wave function is the projection of $|\psi\rangle$ onto the position eigenket $|x\rangle$:

$$\psi(x) = \langle x|\psi\rangle.$$

The momentum-space wave function is the projection onto $|p\rangle$:

$$\tilde{\psi}(p) = \langle p|\psi\rangle.$$

Same state. Different projections. The Fourier-transform relationship between $\psi(x)$ and $\tilde{\psi}(p)$ is simply the statement $\langle x|p\rangle = e^{ipx/\hbar}/\sqrt{2\pi\hbar}$ — the overlap of two different basis kets.

Three identities do most of the computational work. The first is **completeness**, also called the resolution of the identity. If $\{|n\rangle\}$ is any orthonormal basis, then

$$\sum_n |n\rangle\langle n| = \hat{I}.$$

This is just the number 1, written in a way you can insert into any expression. Insert it between $\langle\phi|$ and $|\psi\rangle$:

$$\langle\phi|\psi\rangle = \sum_n \langle\phi|n\rangle\langle n|\psi\rangle.$$

The inner product becomes a sum of products of components. For the continuous position basis, the sum becomes $\int |x\rangle\langle x|\,dx = \hat{I}$, and $\langle\phi|\psi\rangle = \int\phi^*(x)\psi(x)\,dx$ — the ordinary wave-function inner product you have been computing for three chapters.

The second identity is **orthonormality**: $\langle m|n\rangle = \delta_{mn}$.

The third is **expansion**: $|\psi\rangle = \sum_n c_n|n\rangle$ with $c_n = \langle n|\psi\rangle$. The components in any basis are just inner products with the basis vectors. Change the basis, change the components. The vector does not move.

<!-- → [INFOGRAPHIC: three-panel diagram of the three identities side by side — left panel: completeness, showing Σ|n⟩⟨n| = Î as the identity being "inserted" between ⟨φ| and |ψ⟩ with an arrow; center panel: orthonormality, showing a 3×3 grid of inner products ⟨m|n⟩ with 1s on the diagonal and 0s off it; right panel: expansion, showing |ψ⟩ decomposed into a sum of basis-vector arrows c₁|1⟩ + c₂|2⟩ + ...; caption: "Three identities that do all the computational work in any basis"] -->

What does Dirac notation do that the wave function notation does not? Two things. First, it is shorter and does not commit to a basis: $\langle\phi|\hat{A}|\psi\rangle$ is a single expression that means the same thing in position space, momentum space, and the energy basis; the corresponding integral looks different in each representation and has to be rewritten each time. Second, it makes the dual structure visible. In $\psi(x)$ notation, both $\psi(x)$ and $\psi^*(x)$ look like complex-valued functions; the fact that they belong to different vector spaces — one the primal, one the dual — is hidden in the integration measure. In Dirac notation, $|\psi\rangle$ and $\langle\psi|$ are explicitly different kinds of objects. Students who miss this categorical distinction get confused when they encounter adjoints of operators, and they tend to write things like $|\psi\rangle^\dagger = \langle\psi|$ without understanding what the dagger operation is actually doing.

---

## Operators and Hermiticity

A linear operator $\hat{A}$ on Hilbert space is a linear map from the space to itself. That is the whole definition. Operators are abstract — they do not care which basis you are using.

In any chosen basis $\{|n\rangle\}$, an operator has a **matrix representation**:

$$A_{mn} = \langle m|\hat{A}|n\rangle.$$

Different basis, different matrix. Same operator. This distinction — the operator is not the matrix — is the most important single idea in the chapter, and it is the one students most reliably miss. The operator $\hat{x}$ in the position basis acts by multiplication: $\hat{x}|x\rangle = x|x\rangle$, so its matrix is diagonal. The same operator $\hat{x}$ in the energy basis of the harmonic oscillator is tridiagonal, with entries involving $\sqrt{n}$, because $\hat{x} = \sqrt{\hbar/2m\omega}(\hat{a}_+ + \hat{a}_-)$. One operator, two different-looking matrices. The matrix is incidental to the basis. The operator is not. You should be able to switch between representations without feeling like you have changed the problem.

<!-- → [TABLE: two-column comparison of the operator x̂ in two bases — left column: position basis (diagonal matrix, entry x at position indexed by x, eigenvalue equation x̂|x⟩ = x|x⟩); right column: harmonic oscillator energy basis (tridiagonal matrix with √n entries, derived from x̂ = √(ℏ/2mω)(â₊ + â₋)); header row: "Same operator x̂, two bases"; footer: "The matrix depends on the basis. The operator does not. Verify: ⟨0|x̂|0⟩ = 0 in both representations"] -->

For any operator $\hat{A}$, its **adjoint** $\hat{A}^\dagger$ is the operator defined by

$$\langle\phi|\hat{A}\psi\rangle = \langle\hat{A}^\dagger\phi|\psi\rangle \quad \text{for all }|\psi\rangle, |\phi\rangle.$$

In matrix form, the adjoint is the **conjugate transpose**: $(A^\dagger)_{mn} = A_{nm}^*$. For real matrices this is the ordinary transpose. For complex matrices it is not — the complex conjugation matters, and it is where sign errors live.

The Pauli matrix $\sigma_y = \bigl(\begin{smallmatrix} 0 & -i \\ i & 0 \end{smallmatrix}\bigr)$ is the typical failure case. Its transpose is $\bigl(\begin{smallmatrix} 0 & i \\ -i & 0 \end{smallmatrix}\bigr) = -\sigma_y$, so $\sigma_y$ is *anti-symmetric* as a matrix. But its conjugate transpose is $\bigl(\begin{smallmatrix} 0 & -i \\ i & 0 \end{smallmatrix}\bigr) = \sigma_y$, so it is Hermitian. Students who learned "Hermitian means symmetric" in real linear algebra write $\sigma_y$ with both off-diagonal entries equal to $i$ — producing a non-Hermitian matrix — often enough that any code doing qubit calculations should include a runtime check.

An operator is **Hermitian** (self-adjoint) if $\hat{A}^\dagger = \hat{A}$. Three things follow:

First, the eigenvalues are real. If $\hat{A}|a\rangle = a|a\rangle$, take the inner product of both sides with $\langle a|$ and use the Hermitian property to show $a = a^*$. Measurement outcomes are real numbers, so observables must be Hermitian operators. This is not a convention; it is the reason the framework is built this way.

Second, eigenstates with distinct eigenvalues are orthogonal. If $\hat{A}|a\rangle = a|a\rangle$ and $\hat{A}|a'\rangle = a'|a'\rangle$ with $a \neq a'$, then $\langle a|a'\rangle = 0$.

Third, the **spectral theorem**: the eigenstates of any Hermitian operator form a complete orthonormal basis. You can write

$$\hat{A} = \sum_n a_n\,|a_n\rangle\langle a_n|.$$

Every Hermitian operator comes with its own natural basis — its eigenbasis. The probability of getting outcome $a_n$ when you measure $\hat{A}$ on a state $|\psi\rangle$ is $|\langle a_n|\psi\rangle|^2$ — the Born rule, stated as a geometric projection.

One worked example to verify the Hermitian property for a continuous operator. In position representation, $\hat{p} = -i\hbar\,\partial_x$. Compute $\langle\phi|\hat{p}\psi\rangle$:

$$\langle\phi|\hat{p}\psi\rangle = \int_{-\infty}^\infty \phi^*(x)(-i\hbar)\partial_x\psi(x)\,dx.$$

Integrate by parts. The boundary term vanishes because both $\psi$ and $\phi$ go to zero at $\pm\infty$:

$$= \int_{-\infty}^\infty (i\hbar)\partial_x\phi^*(x)\cdot\psi(x)\,dx = \int_{-\infty}^\infty (-i\hbar\partial_x\phi)^*\psi\,dx = \langle\hat{p}\phi|\psi\rangle.$$

Hermitian. The factor of $i$ in the definition $\hat{p} = -i\hbar\partial_x$ is exactly what makes it work. Without the $i$, the partial derivative would be anti-Hermitian, and its eigenvalues would be imaginary — not what you want for a measurable momentum.

<!-- → [INFOGRAPHIC: two-column diagram contrasting Hermitian vs anti-Hermitian operators — left: p̂ = −iℏ∂ₓ, label "Hermitian", shows the integration-by-parts step producing ⟨p̂φ|ψ⟩, eigenvalues real (momentum observable); right: ∂ₓ alone (no −i factor), label "anti-Hermitian: ∂ₓ† = −∂ₓ", shows the boundary term sign flip, eigenvalues imaginary (not observable); caption: "The factor of i in p̂ = −iℏ∂ₓ is not a convention. It is what makes momentum Hermitian and its eigenvalues real"] -->

---

## Commutators and why they matter

Two operators **commute** if $\hat{A}\hat{B} - \hat{B}\hat{A} = 0$. If they commute, they share a common eigenbasis, and you can simultaneously assign definite values to both observables. If they do not commute, no common eigenbasis exists, and the two observables cannot both be sharp on the same state. The commutator $[\hat{A}, \hat{B}] = \hat{A}\hat{B} - \hat{B}\hat{A}$ is the measure of their incompatibility.

The central commutator of quantum mechanics is $[\hat{x}, \hat{p}]$. Apply it to a test function:

$$[\hat{x}, \hat{p}]\psi = \hat{x}(-i\hbar\partial_x\psi) - (-i\hbar\partial_x)(x\psi).$$

The first term is $-i\hbar x\partial_x\psi$. The second, by the product rule, is $-(-i\hbar)(\psi + x\partial_x\psi) = i\hbar\psi + i\hbar x\partial_x\psi$. Sum:

$$[\hat{x}, \hat{p}]\psi = i\hbar\psi.$$

Since this holds for any $\psi$:

$$\boxed{[\hat{x}, \hat{p}] = i\hbar.}$$

This is the **canonical commutation relation**. It is the algebraic statement that distinguishes a quantum theory from a classical one, and every result about position-momentum incompatibility — including the uncertainty principle — follows from it.

Here is the uncertainty principle, done correctly. Most students first encounter it as Heisenberg's 1927 microscope story: the photon used to locate an electron kicks it, so you cannot know both position and momentum simultaneously. That story gives the right intuition and the wrong derivation. The actual theorem, proved by H. P. Robertson in 1929, says nothing about measurement disturbance. It says:

For any two Hermitian operators $\hat{A}, \hat{B}$ and any state $|\psi\rangle$,

$$\sigma_A\sigma_B \geq \frac{1}{2}\bigl|\langle[\hat{A}, \hat{B}]\rangle\bigr|$$

where $\sigma_A$ is the standard deviation of outcomes when $\hat{A}$ is measured on many independently prepared copies of $|\psi\rangle$.

Here is the derivation, stripped to its bones. Define shifted operators $\hat{A}' = \hat{A} - \langle\hat{A}\rangle$ and $\hat{B}' = \hat{B} - \langle\hat{B}\rangle$. Their variances are $\sigma_A^2 = \langle\hat{A}'^2\rangle = \|\hat{A}'|\psi\rangle\|^2$ and $\sigma_B^2 = \|\hat{B}'|\psi\rangle\|^2$. The Cauchy-Schwarz inequality gives

$$\sigma_A^2\sigma_B^2 \geq |\langle\psi|\hat{A}'\hat{B}'|\psi\rangle|^2.$$

Decompose $\hat{A}'\hat{B}'$ into its symmetric and antisymmetric parts: $\hat{A}'\hat{B}' = \frac{1}{2}\{\hat{A}', \hat{B}'\} + \frac{1}{2}[\hat{A}', \hat{B}']$. The symmetric part is Hermitian with a real expectation value; the antisymmetric part is anti-Hermitian with a purely imaginary expectation value. Their modulus squares add:

$$|\langle\hat{A}'\hat{B}'\rangle|^2 = \tfrac{1}{4}\langle\{\hat{A}', \hat{B}'\}\rangle^2 + \tfrac{1}{4}|\langle[\hat{A}, \hat{B}]\rangle|^2.$$

Drop the first (non-negative) term on the right, take the square root:

$$\sigma_A\sigma_B \geq \tfrac{1}{2}|\langle[\hat{A}, \hat{B}]\rangle|.$$

Substituting $\hat{A} = \hat{x}$, $\hat{B} = \hat{p}$, and $[\hat{x}, \hat{p}] = i\hbar$: $\sigma_x\sigma_p \geq \hbar/2$. Robertson. No microscope. No photon. No disturbance.

The operational meaning: prepare a million copies of $|\psi\rangle$. Measure $\hat{A}$ on half and $\hat{B}$ on the other half. Compute the standard deviations of the two histograms. Their product satisfies the Robertson bound. No copy is measured twice. The bound is a property of the state, set before any measurement takes place.

<!-- → [INFOGRAPHIC: ensemble-measurement diagram illustrating the Robertson protocol — top: a single state |ψ⟩ branching into N/2 copies going to "Measure Â" and N/2 copies going to "Measure B̂"; bottom: two histograms of +1/−1 outcomes with sample standard deviations σ_A and σ_B labeled; below the histograms: "σ_A · σ_B ≥ |⟨[Â,B̂]⟩|/2" with a ✓ mark; caption: "No copy is measured twice. The bound is set by the state before measurement begins — it is not caused by measurement disturbance"] -->

---

## The qubit

The simplest non-trivial quantum system has a two-dimensional Hilbert space. Pick a basis $\{|0\rangle, |1\rangle\}$. Any normalized state is

$$|\psi\rangle = \cos(\theta/2)\,|0\rangle + e^{i\phi}\sin(\theta/2)\,|1\rangle$$

with $\theta \in [0, \pi]$ and $\phi \in [0, 2\pi)$. Two real parameters. Every state of a qubit lives on a sphere.

This is the **Bloch sphere**. The north pole ($\theta = 0$) is $|0\rangle$; the south pole ($\theta = \pi$) is $|1\rangle$; the equator ($\theta = \pi/2$) is the equal superpositions $(|0\rangle + e^{i\phi}|1\rangle)/\sqrt{2}$. The **Bloch vector** is

$$\vec{r} = \bigl(\langle\sigma_x\rangle, \langle\sigma_y\rangle, \langle\sigma_z\rangle\bigr)$$

where $\sigma_x, \sigma_y, \sigma_z$ are the Pauli matrices:

$$\sigma_x = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}, \qquad \sigma_y = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}, \qquad \sigma_z = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}.$$

For a pure state with the parametrization above, a direct computation gives $\vec{r} = (\sin\theta\cos\phi, \sin\theta\sin\phi, \cos\theta)$ — the unit vector in the direction $(\theta, \phi)$. For pure states $|\vec{r}| = 1$ exactly; the state is on the surface of the sphere. Their algebra: $[\sigma_i, \sigma_j] = 2i\epsilon_{ijk}\sigma_k$ and $\{\sigma_i, \sigma_j\} = 2\delta_{ij}\hat{I}$.

<!-- → [IMAGE: labeled Bloch sphere diagram — a unit sphere with three labeled axes (x, y, z); north pole labeled |0⟩; south pole labeled |1⟩; a point on the equator at φ=0 labeled (|0⟩+|1⟩)/√2; a point on the equator at φ=π/2 labeled (|0⟩+i|1⟩)/√2; an arrow from the origin to a general point (θ,φ) labeled |ψ⟩ = cos(θ/2)|0⟩ + e^{iφ}sin(θ/2)|1⟩; the Bloch vector (r_x, r_y, r_z) labeled as the tip; caption: "Every pure qubit state is a point on the unit sphere. The angles θ/2 in the state become θ on the sphere via double-angle formulas"] -->

The factor of $\theta/2$ in the state rather than $\theta$ is not an aesthetic choice. Slide $\theta$ from $0$ to $2\pi$. On the Bloch sphere, the state returns to $|0\rangle$ when $\theta = 2\pi$. In the state itself, $\cos(\theta/2)$ goes from $1$ to $-1$ and back — the state accumulates a sign. The sign is invisible in $|\vec{r}|$, which depends on $\langle\sigma_i\rangle$ and therefore on $|\text{components}|^2$, but it is observable in interference experiments. A full loop around the sphere acquires a phase of $-1$. To return the state to itself, you need two loops: $\theta = 4\pi$. This is the spinor double cover of $SO(3)$ — the state space of a qubit is not the sphere $S^2$ but its double cover. The Bloch sphere is the *image* of the state space under the map to expectation values, not the state space itself.

The computation of the Bloch vector is worth doing once in full, because it is the chapter. For $\langle\sigma_z\rangle$:

$$\langle\sigma_z\rangle = \begin{pmatrix}\cos(\theta/2) & e^{-i\phi}\sin(\theta/2)\end{pmatrix}\begin{pmatrix}1 & 0\\0 & -1\end{pmatrix}\begin{pmatrix}\cos(\theta/2)\\e^{i\phi}\sin(\theta/2)\end{pmatrix} = \cos^2(\theta/2) - \sin^2(\theta/2) = \cos\theta.$$

For $\langle\sigma_x\rangle$:

$$\langle\sigma_x\rangle = \begin{pmatrix}\cos(\theta/2) & e^{-i\phi}\sin(\theta/2)\end{pmatrix}\begin{pmatrix}e^{i\phi}\sin(\theta/2)\\\cos(\theta/2)\end{pmatrix} = 2\cos(\theta/2)\sin(\theta/2)\cos\phi = \sin\theta\cos\phi.$$

Similarly $\langle\sigma_y\rangle = \sin\theta\sin\phi$. The half-angles in the state become full angles on the sphere because $\cos\theta = \cos^2(\theta/2) - \sin^2(\theta/2)$ — the double-angle formula is the geometric statement of the double cover.

Now apply Robertson. Let $\hat{A} = \sigma_x$ and $\hat{B} = \sigma_z$. Their commutator is $[\sigma_x, \sigma_z] = -2i\sigma_y$. Robertson says:

$$\sigma_{\sigma_x}\sigma_{\sigma_z} \geq |\langle\sigma_y\rangle| = |\sin\theta\sin\phi|.$$

At the north pole ($\theta = 0$): the state is a $\sigma_z$ eigenstate, $\sigma_{\sigma_z} = 0$, and the right-hand side is also $0$ — the inequality permits anything. On the equator at $\phi = \pi/2$ ($\sigma_y$ eigenstate): $\langle\sigma_y\rangle = 1$, $\sigma_{\sigma_x} = \sigma_{\sigma_z} = 1$, product is $1 \geq 1$. The bound is saturated.

There is something worth pausing on here. The $\sigma_y$ eigenstate has definite $\sigma_y$ — it is the state that, measured along $y$, always returns $+1$. The same state, measured along $x$, returns $+1$ or $-1$ with equal probability. Measured along $z$, the same: 50/50. The Robertson bound is telling you that a state which is as certain as it can be in the $y$ direction must be maximally uncertain in the $x$ and $z$ directions. The state is not uncertain because the measurement disturbs it. The state is uncertain because the eigenstates of $\sigma_y$ are superpositions in the $\sigma_x$ and $\sigma_z$ eigenbases, and superpositions have spread. The spread is in the state before the measurement begins.

<!-- → [TABLE: Robertson bound evaluated at key qubit states — rows: |0⟩ (north pole θ=0), |+x⟩ (equator φ=0), |+y⟩ (equator φ=π/2), |+⟩=(|0⟩+|1⟩)/√2 (equator φ=0 same as +x); columns: state, ⟨σ_y⟩, σ_{σ_x}, σ_{σ_z}, σ_{σ_x}·σ_{σ_z}, Robertson bound |⟨σ_y⟩|; footer: "Bound is saturated (ratio = 1) exactly at the σ_y eigenstate. At the σ_z eigenstate the bound is 0 and is trivially satisfied" — student sees the bound is state-dependent, not a fixed number] -->

---

## Time evolution as rotation

Under a Hamiltonian $\hat{H} = (\hbar\omega/2)\,\hat{n}\cdot\vec{\sigma}$ — a magnetic-field-like interaction along a unit vector $\hat{n}$ — time evolution is

$$|\psi(t)\rangle = e^{-i\hat{H}t/\hbar}|\psi(0)\rangle.$$

Using the Pauli anticommutation relation $(\hat{n}\cdot\vec{\sigma})^2 = \hat{I}$, the matrix exponential evaluates in closed form:

$$e^{-i(\omega t/2)\hat{n}\cdot\vec{\sigma}} = \cos(\omega t/2)\,\hat{I} - i\sin(\omega t/2)\,\hat{n}\cdot\vec{\sigma}.$$

Acting on the Bloch vector, this is a rotation: the Bloch vector precesses about $\hat{n}$ at angular velocity $\omega$. The orbit is a circle on the sphere. In NMR and MRI, this is Larmor precession — the spin precesses around the static magnetic field at the Larmor frequency $\omega = \gamma|\vec{B}|$, and precisely timed RF pulses rotate the Bloch vector to any desired orientation. In quantum computing, controlled pulses implement the single-qubit gates of a quantum circuit. The geometry is the engineering.

The qubit is small enough to compute everything by hand and rich enough to illustrate every abstract idea in the chapter. The Hilbert-space structure, the operator-as-abstract-object, the distinction between eigenvalues (which are invariant) and matrix elements (which change with basis), the Robertson bound as a property of states rather than measurements — all of it is visible in two-dimensional complex vector space, where you can draw pictures and check every step.

This is why the qubit is the chapter's anchor. Everything that follows in the book — perturbation theory, angular momentum, entanglement — uses the same formalism. The qubit is where you learn to use it.

---

## Exercises

**Warm-up**

**4.1** For each of the following, state whether the object is a ket, a bra, an operator, or a scalar: $|\psi\rangle$, $\langle\phi|\psi\rangle$, $|\psi\rangle\langle\phi|$, $\hat{A}|\psi\rangle$, $\langle\phi|\hat{A}|\psi\rangle$, $\sum_n|n\rangle\langle n|$. For each operator in the list, describe what it does when applied to an arbitrary ket $|\chi\rangle$. *(Tests: can distinguish the categorical types in Dirac notation; can read operator expressions without confusing them with scalars or vectors)*

**4.2** Verify that $\sigma_y^\dagger = \sigma_y$ explicitly by computing the conjugate transpose of $\sigma_y = \bigl(\begin{smallmatrix}0&-i\\i&0\end{smallmatrix}\bigr)$. Then verify $\sigma_y^2 = \hat{I}$. State why the transpose alone (without conjugation) would give the wrong answer, and identify which physical property of $\sigma_y$ would be lost if you used the transpose instead of the conjugate transpose. *(Tests: can compute the adjoint of a complex matrix; understands why Hermitian ≠ symmetric for complex matrices)*

**4.3** Derive $[\hat{x}, \hat{p}] = i\hbar$ by applying both sides to a test function $\psi(x)$. Show each step of the product rule explicitly. At which step does the constant $i\hbar$ emerge, and what would the commutator be if $\hat{p}$ were defined without the factor of $-i$ (i.e., as $\hat{p} = \hbar\partial_x$)? *(Tests: can execute the canonical commutation derivation; understands the role of the factor of i)*

---

**Application**

**4.4** The state $|\psi\rangle = \cos(\theta/2)|0\rangle + e^{i\phi}\sin(\theta/2)|1\rangle$ with $(\theta, \phi) = (\pi/3, \pi/4)$. Compute: (a) $\langle\sigma_z\rangle$; (b) $\langle\sigma_x\rangle$; (c) the Bloch vector $\vec{r}$; (d) $|\vec{r}|^2$, and verify it equals 1. *(Tests: can execute the Bloch-vector calculation numerically for a specific state; verifies the pure-state condition)*

**4.5** A qubit is in the state $|\!\uparrow_x\rangle = (|0\rangle + |1\rangle)/\sqrt{2}$. (a) Compute $P(\sigma_z = +1)$ and $P(\sigma_z = -1)$ using the Born rule $P = |\langle\text{eigenstate}|\psi\rangle|^2$. (b) Compute $\sigma_{\sigma_z}$, the standard deviation of $\sigma_z$ outcomes. (c) Compute $\sigma_{\sigma_x}$. (d) Verify the Robertson bound $\sigma_{\sigma_x}\sigma_{\sigma_z} \geq |\langle\sigma_y\rangle|$. *(Tests: can apply the Born rule to compute measurement probabilities; can verify Robertson numerically for a specific state)*

**4.6** Show that $\hat{p} = -i\hbar\partial_x$ is Hermitian using integration by parts. State explicitly what property of the wave functions you need at $\pm\infty$, and explain why this property is required for any physically normalizable state. What would go wrong with the Hermitian proof if you applied $\hat{p}$ to a plane wave $e^{ikx}$ (which is not normalizable)? *(Tests: can execute the integration-by-parts argument; understands the role of boundary conditions in Hermiticity)*

**4.7** Time-evolve the state $|0\rangle$ under $\hat{H} = (\hbar\omega/2)\sigma_x$ using the closed-form unitary $U(t) = \cos(\omega t/2)\hat{I} - i\sin(\omega t/2)\sigma_x$. Compute $|\psi(t)\rangle$ and the Bloch vector $\vec{r}(t)$. Describe the precession geometrically: what axis does the Bloch vector rotate around, and at what angular velocity? *(Tests: can apply the closed-form time-evolution operator; can interpret precession on the Bloch sphere)*

---

**Synthesis**

**4.8** The chapter claims that $\psi(x) = \langle x|\psi\rangle$ and $\tilde{\psi}(p) = \langle p|\psi\rangle$ are related by the Fourier transform because $\langle x|p\rangle = e^{ipx/\hbar}/\sqrt{2\pi\hbar}$. Derive this: starting from $\tilde{\psi}(p) = \langle p|\psi\rangle$, insert the completeness relation $\int|x\rangle\langle x|\,dx = \hat{I}$, and show that the result is the standard Fourier transform $\tilde{\psi}(p) = \int\langle p|x\rangle\psi(x)\,dx$ provided $\langle p|x\rangle = e^{-ipx/\hbar}/\sqrt{2\pi\hbar}$. This means the Fourier transform is a change-of-basis formula, not an independent mathematical operation. *(Tests: can use the completeness relation to derive a representation-change formula; connects the abstract formalism to a familiar operation)*

**4.9** Prove that eigenstates of a Hermitian operator with *distinct* eigenvalues are orthogonal. Then explain why orthogonality is not automatic for eigenstates with the *same* eigenvalue (degeneracy), and state what additional procedure restores an orthonormal basis in the degenerate case. Give a concrete example of a degenerate Hermitian operator from the chapter's material. *(Tests: can reproduce the orthogonality proof; understands degeneracy as the case where the proof fails and knows the remedy)*

---

**Challenge**

**4.10** The Robertson bound $\sigma_A\sigma_B \geq \frac{1}{2}|\langle[\hat{A},\hat{B}]\rangle|$ was derived by dropping the anticommutator term $\frac{1}{4}\langle\{\hat{A}',\hat{B}'\}\rangle^2$ in the Cauchy-Schwarz step. (a) Show that the dropped term is non-negative. (b) The tighter bound that retains this term is the Schrödinger uncertainty relation: $\sigma_A^2\sigma_B^2 \geq \frac{1}{4}|\langle\{\hat{A}',\hat{B}'\}\rangle|^2 + \frac{1}{4}|\langle[\hat{A},\hat{B}]\rangle|^2$. For the qubit with $\hat{A} = \sigma_x$, $\hat{B} = \sigma_z$, and a general state with Bloch vector $(\sin\theta\cos\phi, \sin\theta\sin\phi, \cos\theta)$, evaluate both the Robertson bound and the Schrödinger bound. Find a state where they differ by the largest amount, and explain geometrically on the Bloch sphere why that state maximizes the anticommutator term. *(Tests: requires carrying the dropped term through the derivation and evaluating both bounds explicitly; geometric reasoning on the Bloch sphere)*

---

## LLM Exercise — the Bloch sphere with measurement statistics

The chapter's deliverable is `04-bloch-sphere.html`: a Bloch sphere in three modes — static state, time evolution (Larmor precession), and measurement-statistics (operationalizing the Robertson bound by simulating ensemble measurements on independently prepared copies).

### Part 1 — Update `PROJECT.md`

```
Append a new entry to PROJECT.md describing the Chapter 4 simulation:

Chapter 04 — Formalism: Dirac Notation and Operators
Deliverable: 04-bloch-sphere.html
Status: in progress

The simulation displays a single-qubit state on the Bloch sphere with three modes:

1. Static state mode. The user sets theta (0 to pi) and phi (0 to 2 pi) sliders,
   or the four real components (Re alpha, Im alpha, Re beta, Im beta) with
   automatic normalization. The Bloch vector r = (sin theta cos phi, sin theta
   cos phi, cos theta) is drawn as an arrow from the origin to the surface of a
   translucent unit sphere. The three Pauli expectation values <sigma_x>,
   <sigma_y>, <sigma_z> are displayed as a bar chart in a side panel.

2. Time evolution mode. The user sets H = (hbar omega / 2)(B_x sigma_x +
   B_y sigma_y + B_z sigma_z) via sliders for B_x, B_y, B_z. The Bloch
   vector precesses about B-hat at angular velocity omega = |B|. The orbit
   is drawn as a fading trail on the sphere.

3. Measurement statistics mode. The user picks two Pauli operators. The
   simulation generates N = 1000 (slider 100 to 10000) independent copies
   of the current state, measures the first operator on half and the second
   on the other half, and draws histograms of +1 and -1 outcomes. The product
   of sample standard deviations is compared in real time to the Robertson
   bound |<[A, B]>| / 2. A label reads: "These are N independent measurements
   on N independent copies of the same state. No copy is measured twice."

3D rendering uses orthographic projection of (x, y, z) to 2D screen coordinates.
View angles draggable. Hidden portions of the arrow drawn dashed.
```

### Part 2 — The CLAUDE.md amendment

```
Append to CLAUDE.md the following physics rules for Chapter 4 simulations:

QUBIT AND BLOCH-SPHERE PHYSICS RULES

1. Pauli matrices (verify at startup):
     sigma_x = [[0, 1], [1, 0]]
     sigma_y = [[0, -i], [i, 0]]   <-- note the SIGN of the off-diagonal i
     sigma_z = [[1, 0], [0, -1]]
   Runtime check: for each M in [sigma_x, sigma_y, sigma_z],
   verify M.dagger() === M (Hermitian) and M @ M === I (squares to identity).
   Sign errors in sigma_y are common LLM failure mode #1.

2. State parametrization:
     |psi> = cos(theta / 2) |0> + exp(i phi) sin(theta / 2) |1>
   The factor of theta/2 (NOT theta) is mandatory. Verify:
     theta = 0 -> |0> (Bloch vector +z)
     theta = pi -> |1> (Bloch vector -z)
     theta = pi/2, phi = 0 -> (|0> + |1>) / sqrt(2) (Bloch vector +x)

3. Bloch vector:
     r = (sin theta cos phi, sin theta sin phi, cos theta)
   For pure states, |r|^2 = 1 exactly; runtime check |r|^2 within 1e-6 of 1.

4. Time evolution under H = (hbar / 2)(B_x sigma_x + B_y sigma_y + B_z sigma_z):
   Use CLOSED-FORM unitary, NOT numerical integration.
     omega = sqrt(B_x^2 + B_y^2 + B_z^2)
     n = (B_x, B_y, B_z) / omega
     U(t) = cos(omega t / 2) I - i sin(omega t / 2) (n . sigma)
   Or equivalently rotate the Bloch vector via Rodrigues' formula:
     r(t) = r cos(omega t) + (n cross r) sin(omega t) + n (n . r)(1 - cos(omega t))
   Either method; use one consistently. Closed form conserves normalization exactly.

5. Born-rule probabilities (eigenstates known analytically):
     sigma_z: |+> = |0>, |-> = |1>
     sigma_x: |+> = (|0> + |1>) / sqrt(2), |-> = (|0> - |1>) / sqrt(2)
     sigma_y: |+> = (|0> + i |1>) / sqrt(2), |-> = (|0> - i |1>) / sqrt(2)
   Compute P(+1) = |<+|psi>|^2, P(-1) = |<-|psi>|^2.
   Sanity: P(+1) + P(-1) = 1; for theta = pi/2 in sigma_z, both = 0.5.

6. Measurement statistics: sample N outcomes per operator using inverse CDF
   (uniform u in [0,1); record +1 if u < P(+1), else -1). Compute sample
   standard deviations; compare product to Robertson bound |<[A,B]>| / 2
   computed analytically.

KNOWN FAILURE MODES:
(a) Sign error in sigma_y — Hermitian check catches it.
(b) Missing theta/2 factor — Bloch-vector test catches it.
(c) Wrong Larmor precession direction — document sign convention explicitly.
(d) Normalization drift in time evolution — use closed-form U(t).
(e) Hidden-surface ordering wrong — depth-check each segment of the arrow.
(f) Born-rule probability mistakes — always derive from inner products with
    the operator's eigenstates, never guess.
```

### Part 3 — The simulation prompt

```
You are working in my directory which contains CLAUDE.md, DESIGN.md, and
PROJECT.md (with the Chapter 4 entry just added). Read all three first.

Build 04-bloch-sphere.html: a single self-contained HTML file using D3 v7
from a CDN, no other dependencies, implementing the Chapter 4 simulation
specified in PROJECT.md following the physics rules in CLAUDE.md and the
visual constitution in DESIGN.md.

Layout: one SVG of 1200 x 700, divided as follows:

- Top-left (sphere panel, 600 x 600): the Bloch sphere as a translucent
  dashed-outline circle (silhouette). Three orthogonal axes labeled x, y, z
  with tick marks at +/- 1. The state-vector arrow from origin to the Bloch
  vector, drawn solid in front of the sphere center plane and dashed behind.
  In time-evolution mode, a fading trail traces the recent Bloch vector history.
  View angles (azimuth, elevation) draggable via mouse.

- Top-right (numerics panel, 600 x 300): readouts for theta, phi, Re(alpha),
  Im(alpha), Re(beta), Im(beta). <sigma_x>, <sigma_y>, <sigma_z> as a horizontal
  bar chart with bars centered on zero, range [-1, 1].

- Bottom (measurement panel, 1200 x 400): two histograms side by side for
  the two chosen Pauli operators, each with bars at +1 and -1 showing counts.
  Below the histograms:
    sigma_A, sigma_B, sigma_A * sigma_B, Robertson bound = |<[A,B]>| / 2,
    Ratio = (sigma_A * sigma_B) / Robertson bound  (should be >= 1)
  Label: "These are N independent measurements on N independent copies
  of the same state. No copy is measured twice. The bound is a property
  of the state, not the apparatus."

Controls (top edge):
- Mode selector: three radio buttons — Static / Time evolution / Measurement.
- theta slider (0 to pi, default pi/4), phi slider (0 to 2 pi, default pi/3).
- Time-evolution mode: B_x, B_y, B_z sliders (-1 to 1 each), play/pause/reset.
- Measurement mode: operator pickers (sigma_x, sigma_y, sigma_z for each),
  N slider (100 to 10000), Run button.

Mathematical implementation:
- State as a 2-element complex array [{re, im}, {re, im}].
- Pauli matrices as 2x2 complex arrays.
- Matrix-vector multiplication and inner products as helper functions.
- Bloch vector from <psi| sigma_i |psi> at each update.

Runtime sanity checks (console at startup and every update):
- Each Pauli matrix satisfies M.dagger == M.
- |Bloch vector|^2 - 1 < 1e-6.
- P(+1) + P(-1) = 1 within 1e-6.
- For theta = 0 (sigma_z eigenstate), sigma_sigma_z near 0; sigma_sigma_x near 1.

Do NOT use any 3D library (no three.js, no babylon). Pure D3 SVG with
hand-rolled orthographic projection. Comments at every non-trivial physics step.
```

### Part 4 — Exploration tasks

1. **Operator vs matrix.** Set the state to $(\theta, \phi) = (\pi/2, 0)$ — the $\sigma_x$ eigenstate. Note all three expectation values. Now drag the sphere view 90° around the $y$-axis. The point on the sphere has not moved. Imagine the basis rotating, not the view: the expectation values $\langle\sigma_i\rangle$ are basis-dependent, but the state is not. This is the operator-vs-matrix distinction made visual.

2. **Eigenvalues do not depend on basis.** In static mode, vary $(\theta, \phi)$ freely. For every state, the eigenvalues of $\sigma_z$ remain $\pm 1$. What changes is the *probability* of getting each one. Confirm $P(\sigma_z = +1) = \cos^2(\theta/2)$ from the bar chart.

3. **Robertson is about the state, not the apparatus.** Switch to measurement-statistics mode, $\sigma_x$ and $\sigma_z$, $N = 1000$. Set $\theta = 0$: the $\sigma_z$ eigenstate. The $\sigma_z$ histogram should be all $+1$; the $\sigma_x$ histogram should be 50/50. Product $= 0$. Robertson bound $= 0$. Both zero, no disturbance involved. Now set $\theta = \pi/2, \phi = \pi/2$ (the $\sigma_y$ eigenstate): both histograms 50/50, product $= 1$, Robertson bound $= 1/2$. The inequality holds as $1 \geq 1/2$. No copy was measured twice.

4. **Larmor precession.** Time-evolution mode, $\vec{B} = (0, 0, 1)$, initial state $\theta = \pi/2$, $\phi = 0$. Press play. The Bloch vector traces the equatorial circle. Period $= 2\pi$ in units where $|\vec{B}| = 1$. Now set $\vec{B} = (1, 0, 1)/\sqrt{2}$: the Bloch vector precesses around the tilted axis. Precession is always around the field direction.

5. **The double cover.** Static mode, hold $\phi$ fixed, slide $\theta$ from $0$ to $2\pi$. The Bloch vector returns to the north pole at $\theta = 2\pi$ — the sphere closes. But the state has accumulated a sign: $\cos(2\pi/2) = \cos\pi = -1$. The sphere cannot see this. To return to $+|0\rangle$ rather than $-|0\rangle$, you need $\theta = 4\pi$.

**Extension prompt:**

```
Modify 04-bloch-sphere.html to add a "two-qubit Bloch correlations" mode.
The state is a two-qubit state |psi> in a 4-dimensional Hilbert space.
Default state: the Bell pair (|00> + |11>) / sqrt(2). Slider controls let
the user interpolate between |00>, the Bell pair, and other entangled states.

For each qubit, compute the reduced Bloch vector (length < 1 for the
maximally entangled state). Draw both vectors on separate Bloch spheres.
Display the entanglement entropy S(rho_A) = -Tr(rho_A log rho_A) where
rho_A is the reduced density matrix of qubit A.

Update PROJECT.md to mark Chapter 04 complete and note the entanglement
extension as the bridge to Chapter 13.
```

---

*Bridge to Chapter 5: The formalism of Chapter 4 is general — it applies to any quantum system. Chapter 5 applies it to the simplest system with an unbounded spectrum and continuous eigenvalues: position and momentum in free space. The Fourier transform emerges not as a mathematical tool but as the statement that $|x\rangle$ and $|p\rangle$ are two different bases for the same Hilbert space, and the inner product $\langle x|p\rangle = e^{ipx/\hbar}/\sqrt{2\pi\hbar}$ is the change-of-basis matrix.*
