# Chapter 4 — Formalism: Dirac Notation and Operators

> The chapter where the book stops doing wave-function problems and starts doing *quantum mechanics* — the same physics in basis-free language, with the qubit as the pedagogical anchor.

---

## 1. What this chapter is doing

You have spent three chapters computing with wave functions $\psi(x)$. You have solved the infinite square well, the harmonic oscillator, and a handful of expectation-value integrals. Now we change languages.

The change is not because $\psi(x)$ is wrong. It is because $\psi(x)$ is *one representation* of an object — the quantum state — that has many representations, and writing down only one of them hides what is actually going on. The state itself is more fundamental than the position-space components you have been computing. This chapter introduces the formalism that lets you write the state directly, derive its rules from a small set of axioms, and recover any representation (position, momentum, energy basis) as a corollary.

The pivot has a price. The math goes abstract for a stretch. Hilbert spaces, dual vectors, Hermitian operators, the spectral theorem — these are the structural skeleton of every quantum calculation you will ever do, and they have to be introduced as such. The chapter pays this cost up front, then earns it back by making everything that follows easier.

The qubit — the simplest non-trivial quantum system, a state living in a two-dimensional complex vector space — is the worked example throughout. It is small enough to compute every quantity by hand, rich enough to demonstrate every abstract concept, and important enough on its own (NMR, photon polarization, quantum computing) that the chapter doubles as a working introduction to single-qubit physics.

## 2. Learning objectives

By the end of this chapter you should be able to:

- Distinguish between a state $|\psi\rangle$, its dual $\langle\psi|$, and its position-space wave function $\psi(x) = \langle x|\psi\rangle$.
- Write down and use the completeness relation $\sum_n|n\rangle\langle n| = \hat{I}$ to insert into expressions and convert between bases.
- Compute the Hermitian conjugate (adjoint) of an operator and check whether an operator is Hermitian.
- State and apply the spectral theorem: every Hermitian operator's eigenstates form a complete orthonormal basis.
- Derive $[\hat{x}, \hat{p}] = i\hbar$ in the position representation, and use it to prove the Robertson uncertainty principle from Cauchy-Schwarz.
- Set up a two-level system, compute the Pauli matrices, and locate a state on the Bloch sphere.
- Distinguish the *operator* $\hat{S}_z$ as an abstract entity from its matrix representation in a chosen basis.
- Distinguish ensemble-statistical uncertainty (Robertson) from single-shot measurement disturbance — and explain why the first does not require the second.
- Build a D3 Bloch-sphere simulator with a measurement-statistics mode that displays the Robertson bound as a function of the state.

## 3. Motivating problem

Here is a thing that should bother you. A wave function $\psi(x)$ in the position representation, and the same physical state in momentum representation $\tilde{\psi}(p)$, are different functions. They are related by a Fourier transform. They contain identical information, but they look nothing alike. Which one is "the state"?

The answer is neither. The state is the *object* whose position-space components are $\psi(x)$ and whose momentum-space components are $\tilde{\psi}(p)$. Just as a vector in three-dimensional Euclidean space is *not* its $(x, y, z)$ Cartesian coordinates — it is the abstract vector that *has* those coordinates in that basis — a quantum state is *not* its wave function. The wave function is a list of components in one chosen basis. The state is the vector.

This is more than philosophy. Compute the expectation value of position in the harmonic-oscillator ground state. In position representation it is an integral $\int x|\psi_0(x)|^2 dx$. In the energy basis it is $\langle 0|\hat{x}|0\rangle$. Same physical quantity. Different-looking calculations. If you want to compute expectation values in *any* basis without rewriting your whole apparatus each time, you need a basis-free way to express the operator and the state. That is what Dirac notation does.

A second motivating reason. Quantum information — every quantum computer, every quantum communication protocol, every entanglement experiment — lives in *abstract* Hilbert space. There is no "position" of a qubit. A qubit is two complex numbers and the rules that govern how they evolve and are measured. The whole field would be unintelligible if you insisted on writing everything as a wave function in some pretended position space. Dirac notation is the lingua franca. This chapter is the gate.

A third reason. The uncertainty principle, as you encountered it in introductory quantum mechanics, was probably presented as Heisenberg's 1927 thought experiment about a microscope: the photon used to locate an electron also kicks the electron, so you cannot know both position and momentum. That story is useful as a first picture and *wrong* as a description of why $\sigma_x\sigma_p \geq \hbar/2$. The actual statement is a theorem about Hermitian operators in Hilbert space, due to H. P. Robertson in 1929 ([*Phys. Rev.* 34, 163](https://journals.aps.org/pr/abstract/10.1103/PhysRev.34.163)). It is about the spread of outcomes when you measure incompatible observables on independently prepared copies of the same state. No measurement disturbance is invoked. This chapter proves it.

## 4. Concept block — Hilbert space and Dirac notation

### 4.1 What a state is

A **quantum state** is a unit vector $|\psi\rangle$ in a complex inner-product space called **Hilbert space**, defined up to an overall phase. The properties of Hilbert space:

- *Linear:* if $|\psi\rangle$ and $|\phi\rangle$ are states, then $\alpha|\psi\rangle + \beta|\phi\rangle$ is also in the space, for any complex $\alpha, \beta$. This is the superposition principle.
- *Complex inner product:* there is an operation $(|\phi\rangle, |\psi\rangle) \mapsto \langle\phi|\psi\rangle \in \mathbb{C}$ satisfying conjugate symmetry $\langle\phi|\psi\rangle = \langle\psi|\phi\rangle^*$ and positivity $\langle\psi|\psi\rangle \geq 0$ with equality only when $|\psi\rangle = 0$.
- *Normalizable:* physical states obey $\langle\psi|\psi\rangle = 1$.
- *Complete:* every Cauchy sequence converges. This matters for the infinite-dimensional case (harmonic oscillator, hydrogen atom). For finite-dimensional cases (qubits) completeness is automatic.

Liboff's framing in §4.4 (pantry, lines 5294+) is that Hilbert space is "the analogy of Cartesian 3-space" — the arena in which quantum objects live. The geometric moves you know from $\mathbb{R}^3$ — decompose a vector into components, project onto an axis, change basis — all work here, just with complex numbers.

**Specification move.** *State* is one of the most overloaded words in physics. In this chapter it means a unit vector $|\psi\rangle \in \mathcal{H}$ defined up to an overall phase. It is *not* the wave function (the wave function is one representation), *not* the probability distribution $|\psi(x)|^2$ (that is the squared modulus of one representation), and *not* the density matrix (a mixed-state generalization we will not need until Chapter 13).

### 4.2 The notation

Vectors get angle-bracket kets:

$$|\psi\rangle \in \mathcal{H}$$

Linear functionals on $\mathcal{H}$ — that is, linear maps from $\mathcal{H}$ to $\mathbb{C}$ — form a dual space $\mathcal{H}^*$. Its elements get angle-bracket bras:

$$\langle\phi| \in \mathcal{H}^*$$

Apply a bra to a ket and you get a complex number: $\langle\phi|\psi\rangle \in \mathbb{C}$ — the inner product. Multiply a ket and a bra in the other order and you get an *operator*: $|\psi\rangle\langle\phi|$ is the linear map that takes a vector $|\chi\rangle$ to $\langle\phi|\chi\rangle\,|\psi\rangle$.

The position-space wave function is the projection of $|\psi\rangle$ onto the (improper) position eigenket $|x\rangle$:

$$\psi(x) = \langle x|\psi\rangle$$

The momentum-space wave function is the projection onto $|p\rangle$:

$$\tilde{\psi}(p) = \langle p|\psi\rangle$$

Same state, different projections.

### 4.3 The three identities that do all the work

**Completeness (resolution of the identity).** If $\{|n\rangle\}$ is an orthonormal basis,

$$\sum_n |n\rangle\langle n| = \hat{I}$$

You can insert this anywhere — it is just multiplying by 1 — and use it to convert between representations. For example,

$$\langle\phi|\psi\rangle = \langle\phi|\hat{I}|\psi\rangle = \sum_n \langle\phi|n\rangle\langle n|\psi\rangle$$

The inner product becomes a sum over the basis. For continuous bases like position, the sum becomes an integral with Dirac-delta normalization: $\int |x\rangle\langle x|\,dx = \hat{I}$ and $\langle\phi|\psi\rangle = \int\phi^*(x)\psi(x)\,dx$.

**Orthonormality.** $\langle m|n\rangle = \delta_{mn}$ for discrete bases, $\langle x|x'\rangle = \delta(x - x')$ for continuous.

**Expansion.** $|\psi\rangle = \sum_n c_n|n\rangle$ with $c_n = \langle n|\psi\rangle$. The components in the basis are just the inner products with the basis vectors.

### 4.4 Why Dirac notation is more than shorthand

Two reasons. The first is bookkeeping: $\langle\phi|\hat{A}|\psi\rangle$ is shorter than $\int\phi^*(x)\hat{A}\psi(x)\,dx$ and does not commit to a basis. Switch to momentum representation and the integral has to be rewritten; the Dirac expression does not change.

The second is categorical. In Dirac notation, $|\psi\rangle$ and $\langle\psi|$ live in *different* vector spaces — the primal and the dual. They have different transformation properties. They are not the same kind of object. In position-rep wave-function notation, $\psi(x)$ and $\psi^*(x)$ both look like complex-valued functions, and the dual structure is hidden in the integration measure. Dirac notation makes the dual visible. Students who treat it as just shorthand — without recognizing the categorical distinction — get confused later when they meet adjoints of operators, or when they try to take the dual of a sum.

## 5. Concept block — operators and Hermiticity

### 5.1 What an operator is

A linear operator $\hat{A}$ on $\mathcal{H}$ is a map $\hat{A}: \mathcal{H} \to \mathcal{H}$ that is linear: $\hat{A}(\alpha|\psi\rangle + \beta|\phi\rangle) = \alpha\hat{A}|\psi\rangle + \beta\hat{A}|\phi\rangle$. That is the entire definition. Operators are abstract — they live on the Hilbert space without reference to any basis.

In any chosen basis $\{|n\rangle\}$, an operator $\hat{A}$ has a **matrix representation**

$$A_{mn} = \langle m|\hat{A}|n\rangle$$

Different basis, different matrix. *Same operator.* This is the most important distinction in the chapter. The operator is the abstract object; the matrix is one representation of it.

**Misconception.** *"Operators are matrices."* They are *represented by* matrices in any chosen basis. The same operator $\hat{x}$ in the position basis acts by multiplication: $\hat{x}|x\rangle = x|x\rangle$, so the matrix is diagonal (with eigenvalue $x$ at the diagonal entry indexed by $x$). The same operator in the energy basis of the QHO is tridiagonal, with entries involving $\sqrt{n}$, because $\hat{x} = \sqrt{\hbar/2m\omega}(\hat{a}_+ + \hat{a}_-)$. The matrix is incidental to the basis. The operator is not.

Marshman and Singh ([2017, *European Journal of Physics* 38, 025705](https://iopscience.iop.org/article/10.1088/1361-6404/aa8e73)) document this confusion as one of the most persistent in upper-division quantum mechanics. Students learn matrix mechanics by computing matrix elements, then conflate the matrix with the operator, and lose the ability to switch bases. The chapter must hit this explicitly.

### 5.2 The adjoint

For any linear operator $\hat{A}$, its **adjoint** $\hat{A}^\dagger$ is defined by

$$\langle\phi|\hat{A}\psi\rangle = \langle\hat{A}^\dagger\phi|\psi\rangle \quad \text{for all }|\psi\rangle, |\phi\rangle$$

In matrix form, the adjoint is the **conjugate transpose**: $(A^\dagger)_{mn} = A_{nm}^*$. Note the conjugation. For real matrices the adjoint is the transpose, but for complex matrices it is *not*. This is the next misconception.

**Misconception.** *"Hermitian means symmetric matrix."* False for complex matrices. Hermitian means $A_{mn}^* = A_{nm}$ — conjugate transpose, not just transpose. The Pauli matrix

$$\sigma_y = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}$$

is Hermitian but *not* symmetric. Check: $\sigma_y^T = \begin{pmatrix}0 & i \\ -i & 0\end{pmatrix} \neq \sigma_y$, but $\sigma_y^\dagger = (\sigma_y^T)^* = \begin{pmatrix}0 & -i \\ i & 0\end{pmatrix} = \sigma_y$. Students fresh from real linear algebra get this wrong — and write $\sigma_y$ as $\begin{pmatrix}0 & i \\ i & 0\end{pmatrix}$ (a sign error producing a non-Hermitian matrix) often enough that any working code should include a runtime check that $\sigma_y^\dagger = \sigma_y$.

### 5.3 Hermitian operators are the observables

An operator is **Hermitian** (or self-adjoint, with technical caveats for infinite dimensions we will not dwell on) if $\hat{A}^\dagger = \hat{A}$. Hermitian operators have three properties that make them *the* operators in quantum mechanics:

1. **Eigenvalues are real.** If $\hat{A}|a\rangle = a|a\rangle$ with $\hat{A}$ Hermitian, then $a = a^*$, so $a \in \mathbb{R}$. Because measurement outcomes are real numbers, observables must be Hermitian operators. This is the *reason* QM uses them.

2. **Eigenstates with distinct eigenvalues are orthogonal.** If $\hat{A}|a\rangle = a|a\rangle$ and $\hat{A}|a'\rangle = a'|a'\rangle$ with $a \neq a'$, then $\langle a|a'\rangle = 0$.

3. **Spectral theorem.** Any Hermitian operator (on a finite-dimensional Hilbert space, and with appropriate technical assumptions in the infinite-dimensional case) can be written

$$\hat{A} = \sum_n a_n\,|a_n\rangle\langle a_n|$$

The eigenstates form a complete orthonormal basis.

The spectral theorem is the workhorse. It says every observable comes with its own natural basis — its eigenbasis. Measurement of $\hat{A}$ projects the state onto one of those eigenstates and returns the corresponding eigenvalue. The probability of getting outcome $a_n$ is

$$P(a_n) = |\langle a_n|\psi\rangle|^2$$

— the **Born rule**, stated geometrically. The expansion coefficient in the eigenbasis is the probability amplitude.

**Worked example: $\hat{p}$ is Hermitian.** In position representation, $\hat{p} = -i\hbar\,\partial_x$. Check:

$$\langle\phi|\hat{p}\psi\rangle = \int_{-\infty}^\infty \phi^*(x)(-i\hbar)\partial_x\psi(x)\,dx$$

Integrate by parts. Boundary terms vanish for normalizable $\psi, \phi$ (both go to zero at $\pm\infty$):

$$= \int_{-\infty}^\infty (i\hbar)\partial_x\phi^*(x) \cdot \psi(x)\,dx = \int_{-\infty}^\infty \bigl(-i\hbar\partial_x\phi(x)\bigr)^* \psi(x)\,dx = \langle\hat{p}\phi|\psi\rangle$$

The factor of $i$ in the definition $\hat{p} = -i\hbar\partial_x$ is exactly what makes it Hermitian. Without the $i$, $\partial_x$ would be anti-Hermitian.

## 6. Concept block — commutators, compatibility, Robertson uncertainty

### 6.1 Commutators

Two operators may or may not commute. Their **commutator** is

$$[\hat{A}, \hat{B}] = \hat{A}\hat{B} - \hat{B}\hat{A}$$

If $[\hat{A}, \hat{B}] = 0$, the operators are **compatible** — they share a common eigenbasis, and the corresponding observables can be simultaneously assigned definite values. If $[\hat{A}, \hat{B}] \neq 0$, they are **incompatible** — no common eigenbasis exists, and the two observables cannot both be sharp on the same state.

The canonical commutator in QM is $[\hat{x}, \hat{p}]$. Derive it in position representation. Apply to a test function $\psi(x)$:

$$[\hat{x}, \hat{p}]\psi(x) = \hat{x}(-i\hbar\partial_x\psi) - (-i\hbar\partial_x)(x\psi)$$

The first term is $-i\hbar x\partial_x\psi$. The second term uses the product rule:

$$-(-i\hbar\partial_x)(x\psi) = i\hbar(\psi + x\partial_x\psi)$$

Combine:

$$[\hat{x}, \hat{p}]\psi(x) = -i\hbar x\partial_x\psi + i\hbar\psi + i\hbar x\partial_x\psi = i\hbar\psi$$

Since this holds for any $\psi$:

$$\boxed{[\hat{x}, \hat{p}] = i\hbar\hat{I}}$$

This is the **canonical commutation relation**. It is the algebraic statement at the heart of quantum mechanics — the equation that distinguishes a quantum theory from a classical one. (Liboff §5.4 derives the same result; the pantry text confirms at lines 6097+.)

### 6.2 Robertson uncertainty — the theorem

The Heisenberg uncertainty principle, as you probably first met it, was a hand-wave about microscopes and photons. The modern formulation is a clean theorem about Hermitian operators in Hilbert space. **For any two Hermitian operators $\hat{A}, \hat{B}$ and any state $|\psi\rangle$:**

$$\sigma_A\sigma_B \geq \frac{1}{2}\bigl|\langle[\hat{A}, \hat{B}]\rangle\bigr|$$

where $\sigma_A = \sqrt{\langle\hat{A}^2\rangle - \langle\hat{A}\rangle^2}$ and analogously for $B$, with all expectation values taken in the state $|\psi\rangle$.

This was proved by H. P. Robertson in 1929 ([*Physical Review* 34, 163](https://journals.aps.org/pr/abstract/10.1103/PhysRev.34.163)), generalizing Heisenberg's 1927 *Zeitschrift für Physik* 43, 172 argument. Substituting $\hat{A} = \hat{x}, \hat{B} = \hat{p}$, and $[\hat{x}, \hat{p}] = i\hbar$:

$$\sigma_x\sigma_p \geq \frac{1}{2}|i\hbar| = \frac{\hbar}{2}$$

Heisenberg's original bound is a special case of Robertson's theorem.

### 6.3 Proof outline — Cauchy-Schwarz on shifted operators

Here is the derivation. Define shifted operators centered on their means:

$$\hat{A}' = \hat{A} - \langle\hat{A}\rangle, \quad \hat{B}' = \hat{B} - \langle\hat{B}\rangle$$

These are Hermitian (the means are real numbers) and have $\sigma_A^2 = \langle\hat{A}'^2\rangle = \||\hat{A}'\psi\rangle\|^2$ and $\sigma_B^2 = \||\hat{B}'\psi\rangle\|^2$.

The Cauchy-Schwarz inequality, $|\langle u|v\rangle|^2 \leq \langle u|u\rangle\langle v|v\rangle$, applied to $|u\rangle = \hat{A}'|\psi\rangle$ and $|v\rangle = \hat{B}'|\psi\rangle$:

$$|\langle\psi|\hat{A}'\hat{B}'|\psi\rangle|^2 \leq \sigma_A^2\sigma_B^2$$

Now decompose $\hat{A}'\hat{B}'$ into symmetric and antisymmetric parts:

$$\hat{A}'\hat{B}' = \tfrac{1}{2}\{\hat{A}', \hat{B}'\} + \tfrac{1}{2}[\hat{A}', \hat{B}']$$

where $\{\hat{A}', \hat{B}'\} = \hat{A}'\hat{B}' + \hat{B}'\hat{A}'$ is the anticommutator (Hermitian, real expectation value) and $[\hat{A}', \hat{B}']$ is the commutator (anti-Hermitian, pure imaginary expectation value). The expectation value is therefore

$$\langle\hat{A}'\hat{B}'\rangle = \underbrace{\tfrac{1}{2}\langle\{\hat{A}', \hat{B}'\}\rangle}_{\text{real}} + \underbrace{\tfrac{1}{2}\langle[\hat{A}', \hat{B}']\rangle}_{\text{imaginary}}$$

Taking the modulus squared, the cross term vanishes:

$$|\langle\hat{A}'\hat{B}'\rangle|^2 = \tfrac{1}{4}\langle\{\hat{A}', \hat{B}'\}\rangle^2 + \tfrac{1}{4}|\langle[\hat{A}', \hat{B}']\rangle|^2$$

Combined with Cauchy-Schwarz and using $[\hat{A}', \hat{B}'] = [\hat{A}, \hat{B}]$ (the constant shifts drop out):

$$\sigma_A^2\sigma_B^2 \geq \tfrac{1}{4}|\langle[\hat{A}, \hat{B}]\rangle|^2$$

Take the square root and you have Robertson. The whole proof rests on Cauchy-Schwarz and the algebra of Hermitian operators. No microscope. No photon. No measurement.

### 6.4 The misconception this undoes

Most students arrive at this chapter having been told some version of: "You can't simultaneously know position and momentum because measuring one disturbs the other." That story is Heisenberg's 1927 heuristic, and it is misleading as a foundational explanation. The Robertson uncertainty principle is a **statement about the statistical spread of outcomes in identically-prepared states.**

Here is the operational statement. Prepare a million copies of $|\psi\rangle$. Measure $\hat{A}$ on half a million; measure $\hat{B}$ on the other half million. The standard deviations of the two histograms satisfy $\sigma_A\sigma_B \geq |\langle[\hat{A}, \hat{B}]\rangle|/2$. *No copy is measured twice.* The bound exists before any measurement takes place. It is a property of the state, not of the measurement apparatus.

The "measurement disturbance" framing is not wrong as a *separate* phenomenon — measurements do disturb states, and there is a separate inequality (Ozawa's, [2003](https://journals.aps.org/pra/abstract/10.1103/PhysRevA.67.042105) [verify]) bounding measurement-disturbance trade-offs. But that is a different theorem. The Robertson bound is what every textbook means when it writes "$\sigma_x\sigma_p \geq \hbar/2$", and it is *not* about disturbance. The chapter's simulation will operationalize this distinction in Part 4.

## 7. Concept block — the two-level system

### 7.1 The qubit

The smallest non-trivial Hilbert space has $\dim\mathcal{H} = 2$. Pick a basis $\{|0\rangle, |1\rangle\}$, often called the **computational basis** in quantum information. Any normalized state is

$$|\psi\rangle = \alpha|0\rangle + \beta|1\rangle, \quad |\alpha|^2 + |\beta|^2 = 1$$

Two complex numbers, one normalization constraint, one overall phase that is unobservable. That leaves two real degrees of freedom — exactly the dimension of a sphere. The parametrization is

$$|\psi\rangle = \cos(\theta/2)\,|0\rangle + e^{i\phi}\sin(\theta/2)\,|1\rangle$$

with $\theta \in [0, \pi]$, $\phi \in [0, 2\pi)$. This is the **Bloch sphere** — every pure qubit state is a point on the unit sphere in $\mathbb{R}^3$, with the north pole $\hat{z}$ being $|0\rangle$, the south pole $-\hat{z}$ being $|1\rangle$, and the equator the equal superpositions $(|0\rangle + e^{i\phi}|1\rangle)/\sqrt{2}$.

The factor of $\theta/2$ matters. A full rotation of $\theta$ from $0$ to $2\pi$ takes the state $|0\rangle \mapsto -|0\rangle$ — a phase flip, observable only via interference. To return the state to itself, you need $\theta = 4\pi$. This is the famous spinor double cover of SO(3): the state space is *not* just the sphere but its double cover. Bloch-sphere parameterizations using $\theta$ instead of $\theta/2$ make this invisible and are common LLM errors.

### 7.2 The Pauli matrices

In the $\{|0\rangle, |1\rangle\}$ basis:

$$\sigma_x = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}, \quad \sigma_y = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}, \quad \sigma_z = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$$

Each is Hermitian and has eigenvalues $\pm 1$. Their algebra:

$$[\sigma_i, \sigma_j] = 2i\,\epsilon_{ijk}\,\sigma_k$$

$$\{\sigma_i, \sigma_j\} = 2\delta_{ij}\hat{I}$$

The **Bloch vector** of a state $|\psi\rangle$ is

$$\vec{r} = (\langle\sigma_x\rangle, \langle\sigma_y\rangle, \langle\sigma_z\rangle)$$

For pure states, $|\vec{r}| = 1$ — the vector reaches the surface of the sphere. For mixed states (defer to Chapter 13), $|\vec{r}| < 1$.

For the parametrization above, a direct computation gives

$$\vec{r} = (\sin\theta\cos\phi, \sin\theta\sin\phi, \cos\theta)$$

— the unit vector in the direction $(\theta, \phi)$ in spherical coordinates. The state is the point. This calculation, done once, *is* the chapter — see the worked example in Section 8.

### 7.3 Time evolution as rotation

Consider a Hamiltonian

$$\hat{H} = \frac{\hbar\omega}{2}\,\hat{n}\cdot\vec{\sigma}$$

for some unit vector $\hat{n}$. Time evolution is

$$|\psi(t)\rangle = e^{-i\hat{H}t/\hbar}|\psi(0)\rangle$$

Using $(\hat{n}\cdot\vec{\sigma})^2 = \hat{I}$ (from the anticommutation relation):

$$e^{-i\hat{H}t/\hbar} = \cos(\omega t/2)\,\hat{I} - i\sin(\omega t/2)\,\hat{n}\cdot\vec{\sigma}$$

The action on the Bloch vector is a **rotation about the axis $\hat{n}$ at angular velocity $\omega$**. This is Larmor precession. It is the universal description of single-qubit dynamics: every two-level system, evolving under any Hamiltonian, has its Bloch vector tracing a circle on the sphere.

In NMR and MRI, $\hat{n}$ is along the static magnetic field $\vec{B}$, and $\omega = \gamma|\vec{B}|$ is the Larmor frequency. In quantum computing, controlled magnetic-field pulses implement arbitrary $\hat{n}$ to compose single-qubit gates. The geometry is the engineering.

**Misconception.** *"The Bloch sphere is a literal picture of where the spin is pointing."* Half right. For a spin-1/2 magnetic moment in a real magnetic field, the Bloch vector's direction *does* coincide with the direction of the magnetic moment's expectation value. But the Bloch sphere applies equally to *any* two-level system — photon polarization, energy levels of an atom, two-path interferometer — where $|0\rangle$ and $|1\rangle$ have no spatial meaning. The sphere is an abstract *state space*, not real 3D space. The coincidence for spin-1/2 is genuine but not generic.

Recent education research (Glaser et al. 2024 *European Journal of Physics* [verify exact DOI](https://iopscience.iop.org/article/10.1088/1361-6404/ad2393)) found that students readily compute on the Bloch sphere but struggle to articulate what it represents. The simulation in this chapter directly addresses this: by tying every point on the sphere to a live set of expectation values and to an explicit ensemble of measurement outcomes, the geometry-to-physics link becomes operational rather than decorative.

## 8. Worked examples

### 8.1 Diagonalizing $\sigma_z$

Trivial but worth doing: the eigenvalue equation $\sigma_z|s\rangle = s|s\rangle$ gives a 2x2 system. With $\sigma_z = \mathrm{diag}(1, -1)$, the eigenvalues are $s = \pm 1$ and the eigenvectors are

$$|\!\uparrow_z\rangle = \begin{pmatrix}1\\0\end{pmatrix} = |0\rangle, \quad |\!\downarrow_z\rangle = \begin{pmatrix}0\\1\end{pmatrix} = |1\rangle$$

The notation $|\!\uparrow_z\rangle$ is conventional for spin-1/2; for the qubit context, the computational basis $|0\rangle, |1\rangle$ is the same pair of states with a different label.

### 8.2 $\sigma_x|\!\uparrow_z\rangle$ — the preview of measurement

In the $\sigma_z$ basis,

$$\sigma_x|\!\uparrow_z\rangle = \begin{pmatrix}0 & 1\\1 & 0\end{pmatrix}\begin{pmatrix}1\\0\end{pmatrix} = \begin{pmatrix}0\\1\end{pmatrix} = |\!\downarrow_z\rangle$$

So $\sigma_x$ flips $|\!\uparrow_z\rangle$ to $|\!\downarrow_z\rangle$. Its eigenvectors are *not* $|\!\uparrow_z\rangle$ and $|\!\downarrow_z\rangle$ — they are

$$|\!\uparrow_x\rangle = \frac{1}{\sqrt{2}}\bigl(|\!\uparrow_z\rangle + |\!\downarrow_z\rangle\bigr), \quad |\!\downarrow_x\rangle = \frac{1}{\sqrt{2}}\bigl(|\!\uparrow_z\rangle - |\!\downarrow_z\rangle\bigr)$$

— equal-weight superpositions in the $\sigma_z$ basis. *The same physical state* $|\!\uparrow_x\rangle$ is a pure energy eigenstate from $\sigma_x$'s point of view (definite eigenvalue $+1$) and a perfectly indefinite state from $\sigma_z$'s point of view (50/50 probability of getting $\pm 1$). The state is one thing; what it looks like depends on which operator you are about to apply.

This is the punchline of Section 5.3: an operator comes with its eigenbasis, and the state's relationship to that operator is determined entirely by how the state decomposes into that eigenbasis. The "$50/50$ probability" is just $|\langle\!\uparrow_z|\!\uparrow_x\rangle|^2 = 1/2$.

### 8.3 The Bloch vector of $|\psi\rangle = \cos(\theta/2)|0\rangle + e^{i\phi}\sin(\theta/2)|1\rangle$

Compute $\langle\sigma_z\rangle$:

$$\langle\sigma_z\rangle = \begin{pmatrix}\cos(\theta/2) & e^{-i\phi}\sin(\theta/2)\end{pmatrix}\begin{pmatrix}1 & 0\\0 & -1\end{pmatrix}\begin{pmatrix}\cos(\theta/2)\\e^{i\phi}\sin(\theta/2)\end{pmatrix}$$

$$= \cos^2(\theta/2) - \sin^2(\theta/2) = \cos\theta$$

Compute $\langle\sigma_x\rangle$:

$$\langle\sigma_x\rangle = \begin{pmatrix}\cos(\theta/2) & e^{-i\phi}\sin(\theta/2)\end{pmatrix}\begin{pmatrix}e^{i\phi}\sin(\theta/2)\\\cos(\theta/2)\end{pmatrix}$$

$$= 2\cos(\theta/2)\sin(\theta/2)\,\mathrm{Re}(e^{i\phi}) = \sin\theta\cos\phi$$

Similarly $\langle\sigma_y\rangle = \sin\theta\sin\phi$. So

$$\vec{r} = (\sin\theta\cos\phi, \sin\theta\sin\phi, \cos\theta)$$

— the unit vector in the direction $(\theta, \phi)$. The state-to-sphere map is geometry. The factor of $\theta/2$ in the state becomes $\theta$ on the sphere because the half-angles square to full angles via $\cos\theta = \cos^2(\theta/2) - \sin^2(\theta/2)$.

### 8.4 Robertson on the qubit

Pick $\hat{A} = \sigma_x, \hat{B} = \sigma_z$. Their commutator is $[\sigma_x, \sigma_z] = -2i\sigma_y$. Robertson:

$$\sigma_{\sigma_x}\sigma_{\sigma_z} \geq \frac{1}{2}|\langle -2i\sigma_y\rangle| = |\langle\sigma_y\rangle|$$

For the state $|\psi\rangle = \cos(\theta/2)|0\rangle + e^{i\phi}\sin(\theta/2)|1\rangle$:

- $\sigma_{\sigma_x}^2 = 1 - \langle\sigma_x\rangle^2 = 1 - \sin^2\theta\cos^2\phi$ (since $\sigma_x^2 = \hat{I}$ gives $\langle\sigma_x^2\rangle = 1$)
- $\sigma_{\sigma_z}^2 = 1 - \cos^2\theta = \sin^2\theta$
- $\sigma_{\sigma_x}\sigma_{\sigma_z} = \sqrt{(1 - \sin^2\theta\cos^2\phi)\sin^2\theta}$
- $|\langle\sigma_y\rangle| = |\sin\theta\sin\phi|$

You can verify the inequality holds for any $(\theta, \phi)$. Special cases: at the north pole $(\theta = 0)$, the state $|0\rangle$ is a $\sigma_z$ eigenstate; $\sigma_{\sigma_z} = 0$, and Robertson permits $\sigma_{\sigma_x}$ to be anything (the right-hand side is also zero). On the equator at $\phi = \pi/2$ — the state $(|0\rangle + i|1\rangle)/\sqrt{2}$, which is the $\sigma_y$ eigenstate — both $\sigma_{\sigma_x} = 1$ and $\sigma_{\sigma_z} = 1$, saturating the bound $|\langle\sigma_y\rangle| = 1$.

## 9. Exercises

**Warm-up.**

1. Verify that $\sigma_y^\dagger = \sigma_y$ explicitly. Then verify that $\sigma_y^2 = \hat{I}$.

2. Compute $[\sigma_x, \sigma_y]$, $[\sigma_y, \sigma_z]$, $[\sigma_z, \sigma_x]$ directly from the matrices. Confirm the structure constant: $[\sigma_i, \sigma_j] = 2i\epsilon_{ijk}\sigma_k$.

3. Write the state $|\psi\rangle = \cos(\theta/2)|0\rangle + e^{i\phi}\sin(\theta/2)|1\rangle$ for $(\theta, \phi) = (\pi/2, 0)$ in the $\sigma_z$ basis. What is its Bloch vector? Which Pauli operator has this state as an eigenstate, with what eigenvalue?

**Application.**

4. A spin-1/2 particle is in state $|\!\uparrow_x\rangle$. Compute the probability of measuring $\sigma_z = +1$ and the probability of measuring $\sigma_z = -1$. Repeat for $\sigma_y$. Repeat for $\sigma_x$.

5. Verify $[\hat{a}_-, \hat{a}_+] = 1$ from the canonical commutator $[\hat{x}, \hat{p}] = i\hbar$ using the definitions of $\hat{a}_\pm$ from Chapter 3. (Closes the loop: the algebraic structure of Chapter 3 was the position-momentum commutator wearing different clothes.)

6. Compute the matrix representation of $\hat{x}$ in the harmonic-oscillator energy basis $\{|n\rangle\}$. (Use $\hat{x} = \sqrt{\hbar/2m\omega}(\hat{a}_+ + \hat{a}_-)$.) Verify it is Hermitian and infinite-dimensional. Now compute its matrix in the position basis $\{|x\rangle\}$. Verify that the two matrices represent the same operator by computing $\langle 0|\hat{x}|0\rangle$ in both representations and getting the same answer.

**Synthesis.**

7. Show that for any two Pauli matrices, $\sigma_i\sigma_j = \delta_{ij}\hat{I} + i\epsilon_{ijk}\sigma_k$. Use this to compute $(\hat{n}\cdot\vec{\sigma})^2$ for a unit vector $\hat{n}$, and confirm it equals $\hat{I}$.

8. Prove the Cauchy-Schwarz inequality $|\langle u|v\rangle|^2 \leq \langle u|u\rangle\langle v|v\rangle$ in a complex inner-product space. (Hint: consider $|u\rangle - \lambda|v\rangle$ for $\lambda = \langle v|u\rangle/\langle v|v\rangle$ and use $\langle u - \lambda v|u - \lambda v\rangle \geq 0$.)

9. A qubit is in state $(|0\rangle + i|1\rangle)/\sqrt{2}$. Time-evolve under $\hat{H} = (\hbar\omega/2)\sigma_z$. Compute $|\psi(t)\rangle$ and the Bloch vector $\vec{r}(t)$. Describe the motion geometrically.

**Challenge.**

10. Show that any unitary operator $\hat{U}$ on a two-dimensional Hilbert space can be written, up to an overall phase, as $\hat{U} = \exp(-i(\omega t/2)\hat{n}\cdot\vec{\sigma})$ for some unit vector $\hat{n}$ and some real $\omega t$. This is the statement that the group SU(2) is the double cover of SO(3). (Hint: any 2x2 unitary has determinant of unit modulus, so we can factor out a phase; the remaining SU(2) element decomposes via the Pauli expansion.)

11. The state of the photon polarization out of a polarizing beam splitter aligned at angle $\theta$ to the horizontal is $\cos\theta|H\rangle + \sin\theta|V\rangle$. A subsequent polarizer at angle $\theta'$ transmits with probability $\cos^2(\theta' - \theta)$ — Malus's law. Derive Malus's law from the Born rule in this two-state system.

12. Build the operator $\hat{S}_z = (\hbar/2)\sigma_z$ for spin-1/2 in three forms: (a) abstract, defined by $\hat{S}_z|\!\uparrow\rangle = +(\hbar/2)|\!\uparrow\rangle$ and $\hat{S}_z|\!\downarrow\rangle = -(\hbar/2)|\!\downarrow\rangle$; (b) matrix, in the $\sigma_z$ basis; (c) spectral, $\hat{S}_z = (\hbar/2)(|\!\uparrow\rangle\langle\!\uparrow| - |\!\downarrow\rangle\langle\!\downarrow|)$. Verify all three give the same expectation value $\langle\hat{S}_z\rangle$ for the state $|\!\uparrow_x\rangle$.

## 10. What would change my mind

If a precision experiment found measurement statistics on independently prepared identical states that *violated* Robertson's bound — that is, observed $\sigma_A\sigma_B < |\langle[\hat{A}, \hat{B}]\rangle|/2$ in a clean setup with controlled state preparation — the chapter's central theorem and the formalism that derives it would be falsified. No such experiment has reported a violation. Tests of the Robertson bound (and the related Maccone-Pati bounds [verify]) are now standard practice in quantum-optics laboratories; they consistently confirm the inequality.

If, conversely, a foundational result derived a more restrictive inequality from a smaller set of axioms — say, an inequality that did not require the full apparatus of Hilbert space and Hermitian operators — the chapter's *justification* for that apparatus would need rewriting. Information-theoretic reconstructions of quantum mechanics (Hardy, Chiribella-D'Ariano-Perinotti, and others) attempt this; so far they recover the same formalism from operational axioms rather than replace it.

## 11. Still puzzling

I understand how to compute on the Bloch sphere. I do not understand, in any deep sense, why the state space of a single two-level quantum system is the sphere $S^2$ (more precisely, the double cover SU(2)) and not, say, a circle or a torus or some entirely different topological object. The formalism prescribes complex Hilbert spaces by axiom. Why complex? Why not real, why not quaternionic? There are partial answers — complex Hilbert spaces are the unique structure that supports continuous reversible dynamics, certain composition rules, and tomography — but none of them feel like *the* answer. The question is alive, and I do not have a satisfying resolution.

## 12. LLM Exercise — the Bloch sphere with measurement statistics

You are going to build a single-file D3 simulation that displays a qubit on the Bloch sphere, lets you rotate the state under any Hamiltonian, and runs a *measurement-statistics mode* that operationally demonstrates the Robertson uncertainty bound by simulating ensemble measurements. The deliverable is `04-bloch-sphere.html`.

### Part 1 — Update `PROJECT.md`

```
Append a new entry to PROJECT.md describing the Chapter 4 simulation:

Chapter 04 — Formalism: Dirac Notation and Operators
Deliverable: 04-bloch-sphere.html
Status: in progress

The simulation displays a single-qubit state on the Bloch sphere with three
modes:

1. Static state mode. The user sets theta (0 to pi) and phi (0 to 2 pi)
   sliders, or alternatively sets the four complex-amplitude components
   (Re alpha, Im alpha, Re beta, Im beta) with automatic normalization.
   The Bloch vector r = (sin theta cos phi, sin theta sin phi, cos theta)
   is drawn as an arrow from the origin to the surface of a translucent
   unit sphere. The three Pauli expectation values <sigma_x>, <sigma_y>,
   <sigma_z> are displayed as a bar chart in a side panel.

2. Time evolution mode. The user sets a Hamiltonian H = (hbar omega / 2)
   (B_x sigma_x + B_y sigma_y + B_z sigma_z) via sliders for B_x, B_y, B_z.
   The Bloch vector precesses about the unit vector B-hat at angular
   velocity omega = |B|. The orbit is drawn as a fading trail on the sphere.

3. Measurement statistics mode. The user picks two Pauli operators (any
   pair: sigma_x and sigma_z, sigma_x and sigma_y, etc.). The simulation
   generates N = 1000 (slider 100 to 10000) independent copies of the
   current state, then "measures" the first operator on half the copies
   and the second operator on the other half. Histograms of the +1 and
   -1 outcomes are drawn for each operator. The product of standard
   deviations is computed from the histograms and compared in real time
   to the Robertson bound |<[A, B]>| / 2. A live display reports both
   numbers and the ratio. As theta and phi change, both numbers update.

3D rendering uses orthographic projection of (x, y, z) on the unit sphere
to 2D screen coordinates. View angles (alpha, beta) are draggable. Hidden
surfaces (parts of the arrow behind the sphere) are drawn with dashed
lines or reduced opacity using a depth check.
```

### Part 2 — The CLAUDE.md amendment

```
Append to CLAUDE.md the following physics rules for Chapter 4 simulations:

QUBIT AND BLOCH-SPHERE PHYSICS RULES

1. Pauli matrices (verify at startup):
     sigma_x = [[0, 1], [1, 0]]
     sigma_y = [[0, -i], [i, 0]]   <-- note the SIGN of the off-diagonal i
     sigma_z = [[1, 0], [0, -1]]
   Runtime check: for each matrix M in [sigma_x, sigma_y, sigma_z],
   verify M.dagger() === M (Hermitian) and M @ M === I (squares to identity).
   Failure to verify is failure mode #1; sign errors in sigma_y are common.

2. State parametrization:
     |psi> = cos(theta / 2) |0> + exp(i phi) sin(theta / 2) |1>
   The factor of theta/2 (NOT theta) is mandatory. Half-angles in the state,
   full angles on the sphere. Verify by checking:
     theta = 0 -> |0> (Bloch vector pointing +z)
     theta = pi -> |1> (Bloch vector pointing -z)
     theta = pi/2, phi = 0 -> (|0> + |1>) / sqrt(2) (Bloch vector +x)

3. Bloch vector:
     r = (sin theta cos phi, sin theta sin phi, cos theta)
   Equivalently: r_x = <sigma_x>, r_y = <sigma_y>, r_z = <sigma_z>.
   For pure states, |r| = 1 exactly; runtime check |r|^2 within 1e-6 of 1.

4. Time evolution under H = (hbar / 2) (B_x sigma_x + B_y sigma_y + B_z sigma_z):
   Use CLOSED-FORM unitary, NOT numerical integration. Define:
     omega = sqrt(B_x^2 + B_y^2 + B_z^2)
     n = (B_x, B_y, B_z) / omega
     U(t) = cos(omega t / 2) I - i sin(omega t / 2) (n . sigma)
   Apply U(t) to the initial state by matrix-vector multiplication, then
   recompute the Bloch vector. This conserves normalization exactly.

5. Equivalently, rotate the Bloch vector directly using Rodrigues' formula:
     r(t) = r cos(omega t) + (n cross r) sin(omega t)
            + n (n . r) (1 - cos(omega t))
   Either method is fine; use one and stick with it.

6. Born-rule probabilities:
     P(sigma_z = +1) = |<0|psi>|^2 = cos^2(theta / 2)
     P(sigma_z = -1) = |<1|psi>|^2 = sin^2(theta / 2)
   The HALF-ANGLE matters. Sanity check: theta = pi/2 must give 50/50.

   For a general operator A with eigenstates |a+>, |a->, probabilities are
   |<a+|psi>|^2 and |<a-|psi>|^2.

7. Measurement statistics mode generates N independent random outcomes per
   operator using inverse-CDF sampling: draw u in [0, 1) uniformly; if
   u < P(+1), record +1, else -1. After N samples, compute sample variance
   and product. Compare to Robertson bound |<[A, B]>| / 2.

KNOWN FAILURE MODES to avoid:
(a) Sign error in sigma_y (Hermitian check catches this).
(b) Missing half-angle factor in state parametrization (Bloch test catches).
(c) Wrong sign for Larmor precession direction. Document the convention;
    Griffiths uses the convention that positive B_z rotates the Bloch vector
    counterclockwise when viewed from the +z direction (right-hand rule
    around +z).
(d) Numerical normalization drift in time evolution. Use closed-form U(t).
(e) Hidden-surface ordering wrong in 3D projection. For the state-vector
    arrow, sample 20 points along the arrow length; for each, check whether
    its projected depth (signed distance from viewer) puts it in front of
    or behind the sphere; draw front segments solid and back segments dashed.
(f) Born-rule probability mistakes. Always derive from inner products with
    eigenstates of the operator being measured, never guess.
```

### Part 3 — The simulation prompt

```
You are working in my directory which contains CLAUDE.md, DESIGN.md, and
PROJECT.md (with the Chapter 4 entry just added). Read all three first.

Build 04-bloch-sphere.html: a single self-contained HTML file using D3 v7
from a CDN, no other dependencies, that implements the Chapter 4 simulation
specified in PROJECT.md following the physics rules in CLAUDE.md and the
visual constitution in DESIGN.md.

Layout: one SVG of 1200 x 700, divided as follows:

- Top-left (sphere panel, 600 x 600): the Bloch sphere as a translucent
  dashed-outline circle (the silhouette). Three orthogonal axes labeled
  x, y, z with tick marks at +/- 1. The state-vector arrow from origin
  to the Bloch vector position on the sphere, drawn solid for the portion
  in front of the sphere center plane and dashed for the portion behind.
  When in time-evolution mode, a fading trail traces the recent history
  of the Bloch vector. View angles (alpha for azimuth, beta for elevation)
  draggable via mouse on this panel.

- Top-right (numerics panel, 600 x 300): readouts for
  theta, phi, alpha = cos(theta / 2), beta = exp(i phi) sin(theta / 2)
  (Re and Im parts shown separately), <sigma_x>, <sigma_y>, <sigma_z>
  as a horizontal bar chart with bars centered on zero and extending to
  the corresponding expectation value, range [-1, 1] for each.

- Bottom (measurement panel, 1200 x 400): two histograms side by side,
  labeled with the two chosen Pauli operators. Each histogram has two
  bars at +1 and -1, showing counts from N independent simulated
  measurements. Below the histograms: a row of computed numbers:
    sigma_A (sample standard deviation of the A measurements)
    sigma_B (sample standard deviation of the B measurements)
    sigma_A * sigma_B (the product)
    Robertson bound = |<[A, B]>| / 2 (computed analytically for the
                                       current theta, phi)
    Ratio = (sigma_A * sigma_B) / Robertson bound
  The ratio should be >= 1 (with small statistical fluctuations).
  Annotate the panel with the explanation: "These are N independent
  measurements on N independent copies of the same state. No copy is
  measured twice. The bound is a property of the state, not the apparatus."

Controls (along the top edge above the sphere panel):
- Mode selector: three radio buttons - "Static" / "Time evolution" / "Measurement"
- theta slider (0 to pi, default pi/4)
- phi slider (0 to 2 pi, default pi/3)
- For time-evolution mode: B_x, B_y, B_z sliders (-1 to 1 each) and
  play / pause / reset buttons.
- For measurement mode: a pair of operator pickers (each cycling through
  sigma_x, sigma_y, sigma_z), an N slider (100 to 10000), and a "Run"
  button that re-samples the histograms.

Mathematical implementation:
- State as a 2-element complex array [{re, im}, {re, im}].
- Pauli matrices as 2x2 complex arrays.
- Matrix-vector multiplication and inner products as small helper functions.
- Bloch vector computed from the state via <psi| sigma_i |psi> at each
  update.
- For the measurement mode, eigenstates of each Pauli operator are known
  analytically:
    sigma_z: |+> = |0>, |-> = |1>
    sigma_x: |+> = (|0> + |1>) / sqrt(2), |-> = (|0> - |1>) / sqrt(2)
    sigma_y: |+> = (|0> + i |1>) / sqrt(2), |-> = (|0> - i |1>) / sqrt(2)
  Compute probabilities, then sample.

Runtime sanity checks (write to console at startup and on every update):
- Pauli matrices are Hermitian (M.dagger == M).
- |Bloch vector|^2 - 1 < 1e-6.
- Sum of Born-rule probabilities = 1 within 1e-6.
- For measurement mode with N = 1000 and a sigma_z eigenstate (theta = 0),
  sigma_sigma_z should come out within 0.05 of 0 (the eigenstate has no
  spread); sigma_sigma_x will be near 1.

Do NOT use any 3D library (no three.js, no babylon). Pure D3 SVG with
hand-rolled orthographic projection. Comments at every non-trivial physics
step.
```

### Part 4 — Exploration tasks and extension prompt

Run the simulation and answer the following:

1. **Operator vs matrix.** Set the state to $(\theta, \phi) = (\pi/2, 0)$ — the $\sigma_x$ eigenstate. Note all three expectation values $\langle\sigma_x\rangle, \langle\sigma_y\rangle, \langle\sigma_z\rangle$. Now rotate the view of the sphere (drag the panel) by 90° around the $y$-axis so what *was* the $x$-axis is now pointing toward you. The point on the sphere has not moved relative to the sphere — it is still on the same physical state. But your perception of "where it is" has changed. Now imagine the basis is what you rotated, not the view. The expectation values $\langle\sigma_x\rangle, \langle\sigma_y\rangle, \langle\sigma_z\rangle$ depend on the basis choice; the state does not.

2. **Eigenvalues do not depend on basis.** In static mode, set $(\theta, \phi)$ to several different values. For each, the *eigenvalues* of $\sigma_z$ are still $\pm 1$ — that is the operator's invariant property. What changes is the *probability* of getting each eigenvalue. Confirm in the simulation that $P(\sigma_z = +1) = \cos^2(\theta/2)$ for the parametrized state, by reading the bar chart and the angles.

3. **Robertson is about the state, not the apparatus.** Switch to measurement-statistics mode with $N = 1000$. Pick $\sigma_x$ and $\sigma_z$. Set the state to the $\sigma_z$ eigenstate ($\theta = 0$). The $\sigma_z$ histogram should be all $+1$ (no spread, $\sigma_{\sigma_z} = 0$). The $\sigma_x$ histogram should be 50/50 ($\sigma_{\sigma_x} = 1$). Product is $0$. The Robertson bound $|\langle\sigma_y\rangle|/2$ is also $0$ (since the $\sigma_z$ eigenstate has $\langle\sigma_y\rangle = 0$). The inequality is saturated as $0 = 0$, with no measurements interfering with each other. Now rotate the state to $\theta = \pi/2, \phi = \pi/2$ — the $\sigma_y$ eigenstate. Both histograms are now 50/50. Product is $1$. Robertson bound $|\langle\sigma_y\rangle|/2 = 1/2$ (since $\langle\sigma_y\rangle = 1$). The inequality holds with $1 \geq 1/2$. Confirm that *no copy was measured twice* — the bound emerges from independent measurements on identically prepared copies.

4. **Larmor precession.** Switch to time-evolution mode. Set $\vec{B} = (0, 0, 1)$ — magnetic field along $z$. Set the initial state to $\theta = \pi/2, \phi = 0$ — the $\sigma_x$ eigenstate. Press play. The Bloch vector should trace a circle on the equator (the $xy$-plane). What is the period? Confirm: $T = 2\pi/\omega = 2\pi$ in your units (since $|\vec{B}| = 1$). Now set $\vec{B} = (1, 0, 1)/\sqrt{2}$ — a field tilted 45° from $z$ toward $x$. Restart from the same initial state. Now the Bloch vector traces a circle *around the tilted $\vec{B}$ axis*, not around $z$. The geometry is general: precession is *always* around the field direction.

5. **The double cover.** Static mode. Hold $\phi$ fixed and slide $\theta$ from $0$ to $2\pi$. Notice: in the parametrization $\cos(\theta/2)|0\rangle + e^{i\phi}\sin(\theta/2)|1\rangle$, sliding $\theta$ past $\pi$ takes $\cos(\theta/2)$ negative — the state acquires a relative sign. On the sphere (which sees only $\langle\sigma_i\rangle$), this overall sign is invisible. The state space, properly described, is $S^3/\mathbb{Z}_2$ (the unit sphere in $\mathbb{C}^2$ modulo overall phase), which is *not* $S^2$. The Bloch sphere is the *image* of the state space under the map to expectation values, not the state space itself.

**Extension prompt:**

```
Modify 04-bloch-sphere.html to add a "two-qubit Bloch correlations" mode.
The state is a two-qubit state |psi> in a 4-dimensional Hilbert space.
Default state: the Bell pair (|00> + |11>) / sqrt(2). Slider controls
let the user dial the state between |00>, the Bell pair, and (|0+> + |1->) etc.

For each qubit, compute the reduced Bloch vector (length < 1 for the
maximally entangled state). Draw both vectors on separate Bloch spheres.
Display the entanglement entropy S(rho_A) = -Tr(rho_A log rho_A) where
rho_A is the reduced density matrix of qubit A.

This previews Chapter 13's material on entanglement and mixed states.
Update PROJECT.md to mark Chapter 04 complete and note the entanglement
extension as the bridge to Chapter 13.
```

---

*Sources consulted: Griffiths §3.1–3.6, Ch. 4 (qubit/spin material); Liboff §4.3–4.4 (Dirac notation and Hilbert space, pantry lines 5221–5305), Ch. 5 (commutators, pantry lines 6097+), Ch. 11 (angular momentum matrices); Sakurai & Napolitano *Modern Quantum Mechanics* Ch. 1; Shankar *Principles of Quantum Mechanics* §1; Nielsen & Chuang *Quantum Computation and Quantum Information* §1.2–1.4 [verify edition]; Robertson, "[The Uncertainty Principle](https://journals.aps.org/pr/abstract/10.1103/PhysRev.34.163)", *Physical Review* 34, 163 (1929); Heisenberg, *Zeitschrift für Physik* 43, 172 (1927); Marshman & Singh, "[Investigating student understanding of basic quantum mechanics: position and momentum probabilities](https://iopscience.iop.org/article/10.1088/1361-6404/aa8e73)", *European Journal of Physics* 38, 025705 (2017); Glaser et al. on Bloch-sphere education [verify 2024 EJP DOI](https://iopscience.iop.org/article/10.1088/1361-6404/ad2393); Lahiri & Pal *A First Book of Quantum Field Theory* (pantry, for the formalism's QFT extension); Gordon, Zeiger, & Townes ammonia-maser paper [verify *Phys. Rev.* 99, 1264 (1955)].*

*Tags: dirac-notation, hilbert-space, hermitian-operators, robertson-uncertainty, bloch-sphere, pauli-matrices, qubit, d3-simulation*

*Status: draft for Nik's review. Voice-anchor check pending — root `style/` and `books/quantum-mechanics-with-llms/style/` not yet inspected. Flag: voice-unanchored if both empty. Several `[verify]` flags throughout — see specifically Ozawa 2003 PRA citation, Nielsen & Chuang edition, Glaser et al. 2024 EJP DOI, ammonia-maser citation, Maccone-Pati bounds reference.*
