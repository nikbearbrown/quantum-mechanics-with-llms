# Chapter 12 — Entanglement and Quantum Information

> The chapter where quantum mechanics stops being a theory of microscopic mysteries and becomes a resource — the resource that powers Bell tests, teleportation, and the quantum-information era that won the 2022 Nobel Prize.

---

## 1. What this chapter is doing

For eleven chapters this book has treated quantum states as descriptions. A wave function is a thing the particle *has*. An eigenstate is a thing the system *is in*. The conversation has been about what reality is doing — solving Schrödinger, finding spectra, computing matrix elements, computing amplitudes.

This chapter changes the register. We are going to treat quantum states as *resources* — things you can prepare, share, manipulate, and spend. The same machinery you have been learning becomes infrastructure for protocols: tests of locality, secret-key distribution, teleportation, computation. The shift is not into a new physics. It is into a new use of the physics you already own.

The pivot is a single object: the entangled state. A state shared between two qubits that cannot be written as a product. Chapter 4 introduced the tensor product as bookkeeping for composite systems. Chapter 8 noticed that identical-particle symmetrization produces composite states that fail to factor. Chapter 12 puts a name on the failure and shows what it lets you do.

There is a public reason to do this chapter now. In October 2022 the Nobel committee gave the physics prize to Alain Aspect, John F. Clauser, and Anton Zeilinger ["for experiments with entangled photons, establishing the violation of Bell inequalities and pioneering quantum information science"](https://www.nobelprize.org/prizes/physics/2022/press-release/). For thirty years after Bell's 1964 paper this material lived in the foundations literature — interesting, perhaps important, mostly philosophical. The Nobel citation acknowledged the change. The foundations became infrastructure. The chapter you are reading is the bridge.

## 2. Learning objectives

By the end of this chapter you should be able to:

- State the precise definition of entanglement for two-qubit pure states (failure of factorization) and prove the Bell state $|\Phi^+\rangle$ is entangled by direct contradiction.
- Write down the four Bell states and identify the singlet as the rotationally invariant one.
- Derive the CHSH inequality $|S| \leq 2$ for any local hidden-variable theory, and show the quantum prediction reaches $S = 2\sqrt{2}$ for the Bell state at the optimal angle setting.
- Name the loopholes (locality, detection, freedom of choice) and identify which experiments closed them.
- Define a qubit on the Bloch sphere, apply the Pauli, Hadamard, and CNOT gates, and prepare the Bell state $|\Phi^+\rangle$ from $|00\rangle$ using $H \otimes I$ followed by CNOT.
- State the no-cloning theorem and the no-signaling theorem precisely, and use them to refute the two dominant pop-physics misreadings of entanglement.
- Walk through the quantum-teleportation protocol step by step, identifying what is sent classically and what is sent quantumly.
- Build a Bell-inequality simulator and a small gate-circuit visualizer in D3 that put $S$ on screen as a number and let the student drive it across the classical bound.

## 3. Motivating problem

Take a pair of spin-$\tfrac{1}{2}$ particles prepared in the singlet state

$$|\Psi^-\rangle = \tfrac{1}{\sqrt{2}}\bigl(|01\rangle - |10\rangle\bigr)$$

and send one to Alice and the other to Bob, kilometers apart. Alice picks a direction $\hat a$ and measures her particle's spin component along it; Bob picks $\hat b$ and does the same. Each gets $\pm 1$. Repeat many times. The quantum prediction for the correlation is

$$E(\hat a, \hat b) = -\hat a \cdot \hat b = -\cos(\theta_a - \theta_b)$$

Now ask a simple-sounding question. Could this correlation be explained by a *local* mechanism? Suppose each particle carried, at the moment of separation, some hidden instructions $\lambda$ that fixed in advance what its spin would be along every direction. Alice's outcome depends only on her direction and on $\lambda$. Bob's depends only on his direction and on $\lambda$. They are correlated because they were prepared together, the way two letters in identical envelopes are correlated.

It sounds reasonable. Einstein, Podolsky, and Rosen sketched a version of this argument in [1935](https://link.aps.org/doi/10.1103/PhysRev.47.777) (*Physical Review* 47, 777) and concluded that quantum mechanics must be *incomplete* — that some hidden description was missing. For three decades the argument was treated as philosophy.

In [1964](https://link.aps.org/doi/10.1103/PhysicsPhysiqueFizika.1.195) John Stewart Bell turned it into a calculation. He showed that *any* local hidden-variable model must satisfy a specific inequality involving four correlation measurements. Quantum mechanics predicts a violation. So the experiment can decide.

That is the chapter. We are going to derive Bell's inequality (in the CHSH form, which is the cleanest), compute the quantum violation explicitly, look at what the experiments measured, and then turn the violation into a tool. The same entangled state that breaks local realism is the state that powers quantum teleportation and stocks the universal gate set for quantum computation. Foundations and infrastructure are the same object viewed from two sides.

## 4. Concept block — entanglement, specified

### 4.1 What entanglement is not

The single most common student mistake is to call any pair of correlated outcomes "entangled." It is worth getting the language right before doing anything else.

Two coins glued back-to-back so they always land the same way are correlated, perfectly. They are not entangled. A pair of envelopes containing a red marble and a blue marble, mailed to two friends, are correlated: open one and you instantly know the other. Not entangled. A classical noise source feeding correlated bits to two parties is correlated. Not entangled.

Entanglement is a more specific thing. It is a property of *joint quantum states* and it has two operational signatures. First: the joint state cannot be written as a tensor product of individual states. Second: the joint statistics include correlations that *no* local hidden-variable theory can reproduce — a violation of Bell's inequality. The two signatures are not independent (Werner 1989 catalogued the subtleties for mixed states) but for the pure-state two-qubit case treated here they coincide.

### 4.2 The product-state criterion

Let $\mathcal{H}_A$ and $\mathcal{H}_B$ be two-dimensional Hilbert spaces (qubits). A pure state $|\psi\rangle \in \mathcal{H}_A \otimes \mathcal{H}_B$ is *separable* (also called *product*) if there exist single-qubit states $|a\rangle \in \mathcal{H}_A$ and $|b\rangle \in \mathcal{H}_B$ such that

$$|\psi\rangle = |a\rangle \otimes |b\rangle$$

If no such factorization exists, the state is *entangled*. That is the whole definition for two-qubit pure states.

Let's apply it. Take the candidate Bell state

$$|\Phi^+\rangle = \tfrac{1}{\sqrt{2}}\bigl(|00\rangle + |11\rangle\bigr)$$

Suppose, for contradiction, that $|\Phi^+\rangle = (\alpha|0\rangle + \beta|1\rangle) \otimes (\gamma|0\rangle + \delta|1\rangle)$. Expand:

$$(\alpha|0\rangle + \beta|1\rangle) \otimes (\gamma|0\rangle + \delta|1\rangle) = \alpha\gamma|00\rangle + \alpha\delta|01\rangle + \beta\gamma|10\rangle + \beta\delta|11\rangle$$

Match coefficients against $\tfrac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$:

$$\alpha\gamma = \tfrac{1}{\sqrt{2}}, \quad \alpha\delta = 0, \quad \beta\gamma = 0, \quad \beta\delta = \tfrac{1}{\sqrt{2}}$$

The second equation says $\alpha = 0$ or $\delta = 0$. If $\alpha = 0$, the first equation says $0 = 1/\sqrt 2$. Contradiction. If $\delta = 0$, the fourth equation says $0 = 1/\sqrt 2$. Contradiction. No factorization exists.

This is the cleanest possible proof of entanglement. No physics, no philosophy, just algebra. The state does not factor.

### 4.3 The four Bell states

The two-qubit Hilbert space is four-dimensional. There is a standard orthonormal basis of maximally entangled states — the **Bell basis**:

$$|\Phi^\pm\rangle = \tfrac{1}{\sqrt{2}}\bigl(|00\rangle \pm |11\rangle\bigr), \qquad |\Psi^\pm\rangle = \tfrac{1}{\sqrt{2}}\bigl(|01\rangle \pm |10\rangle\bigr)$$

Each of these is entangled by the same argument given above. Each is *maximally* entangled in the sense that the reduced density matrix on either qubit alone is $\hat I / 2$ — the most mixed possible single-qubit state. That is the formal sense in which the information about each qubit individually has gone into the joint.

The singlet $|\Psi^-\rangle$ is special: it is rotationally invariant. For any single-qubit unitary $U$,

$$(U \otimes U)|\Psi^-\rangle = (\det U)\,|\Psi^-\rangle$$

so up to an overall phase, the singlet is unchanged by simultaneously rotating both spins. This makes it the natural state for Bell tests in the original spin-$\tfrac{1}{2}$ formulation (Bohm 1951) and for the singlet-correlation calculation $E(\hat a, \hat b) = -\hat a \cdot \hat b$. The chapter will use $|\Phi^+\rangle$ for the CHSH calculation because its correlation function $+\hat a \cdot \hat b$ has the cleaner sign; the result transfers to $|\Psi^-\rangle$ by relabeling.

**Misconception 1.** *"Entanglement is just strong correlation."* No. Two coins glued together produce correlations of $\pm 1$ — perfect — and yet they cannot violate any Bell inequality, because there exists a local hidden-variable model (write the outcome on each coin before separating them). What distinguishes entanglement from classical correlation is *not* the strength of the correlation. It is the *pattern of correlations across different measurement settings*. We are about to make this precise.

## 5. Concept block — Bell's theorem and the CHSH derivation

This is the chapter's deep dive. The mechanism is worth doing carefully because the result is one of the cleanest theorem-experiment combinations in physics, and because every step is something you can do by hand.

### 5.1 The setup

Alice and Bob each choose between two measurement settings. Call Alice's choices $A_1, A_2$ and Bob's $B_1, B_2$. Each measurement outputs $\pm 1$. Run the experiment many times for each of the four setting combinations $(A_i, B_j)$ and compute the expectation values

$$E(A_i, B_j) = \langle A_i B_j \rangle$$

averaged over many runs with that pair of settings.

Now form a single number — the **CHSH parameter**:

$$S = E(A_1, B_1) + E(A_1, B_2) + E(A_2, B_1) - E(A_2, B_2)$$

This expression looks asymmetric. There is one minus sign and three plus signs. The asymmetry is the whole point: it weights one of the four correlations differently and forces the inequality to come out non-trivially.

### 5.2 The local hidden-variable bound

Assume the world is governed by a *local hidden-variable* (LHV) theory. The assumptions are:

1. **Realism.** Each particle carries, before measurement, a hidden state $\lambda$ that fixes the outcome of any measurement that *could* be performed on it.
2. **Locality.** Alice's outcome depends only on her setting and on $\lambda$, not on Bob's setting. Symmetrically for Bob.
3. **Outcome range.** $A_i(\lambda), B_j(\lambda) \in \{+1, -1\}$.

There is some probability distribution $\rho(\lambda)$ over hidden states. The correlations are

$$E(A_i, B_j) = \int A_i(\lambda) B_j(\lambda) \rho(\lambda) \, d\lambda$$

Plug into $S$:

$$S = \int \bigl[A_1(\lambda)B_1(\lambda) + A_1(\lambda)B_2(\lambda) + A_2(\lambda)B_1(\lambda) - A_2(\lambda)B_2(\lambda)\bigr] \rho(\lambda) \, d\lambda$$

Factor inside the brackets — group by which $A$ appears:

$$S(\lambda) \equiv A_1(\lambda)\bigl[B_1(\lambda) + B_2(\lambda)\bigr] + A_2(\lambda)\bigl[B_1(\lambda) - B_2(\lambda)\bigr]$$

Look at the two bracketed quantities. Both $B_1(\lambda)$ and $B_2(\lambda)$ are $\pm 1$. So $B_1 + B_2 \in \{-2, 0, +2\}$ and $B_1 - B_2 \in \{-2, 0, +2\}$. Crucially, *exactly one* of these is zero. If $B_1 = B_2$, the sum is $\pm 2$ and the difference is $0$. If $B_1 \neq B_2$, the sum is $0$ and the difference is $\pm 2$. There is no overlap.

So at every $\lambda$, $S(\lambda)$ is either $A_1(\lambda) \cdot (\pm 2)$ or $A_2(\lambda) \cdot (\pm 2)$. Since $A_i(\lambda) = \pm 1$,

$$|S(\lambda)| = 2 \qquad \text{for every } \lambda$$

And therefore

$$|S| = \biggl|\int S(\lambda) \rho(\lambda)\, d\lambda\biggr| \leq \int |S(\lambda)|\rho(\lambda)\, d\lambda = 2$$

That is it. For any local hidden-variable theory whatever — any choice of $\lambda$, any distribution $\rho$, any deterministic functions $A_i, B_j$ — the CHSH parameter is bounded by $2$. This is the **classical CHSH bound** and it is the conclusion of Bell's theorem in its sharpest form (Clauser, Horne, Shimony, Holt, [1969](https://link.aps.org/doi/10.1103/PhysRevLett.23.880), *Physical Review Letters* 23, 880).

Notice what the derivation did *not* assume. It did not assume any particular form for the hidden variable. It did not assume probabilities are continuous. It did not assume measurements commute. It assumed only that outcomes are pre-determined functions of the local setting and a shared hidden state, taking values $\pm 1$. The bound is structural.

### 5.3 The quantum prediction — for $|\Phi^+\rangle$

Now compute $S$ in quantum mechanics with the entangled state $|\Phi^+\rangle = (|00\rangle + |11\rangle)/\sqrt{2}$. The measurement along direction $\hat n = (\sin\theta, 0, \cos\theta)$ in the $xz$-plane is the operator

$$\hat n \cdot \vec\sigma = \sin\theta \, \hat\sigma_x + \cos\theta \, \hat\sigma_z$$

The joint measurement of Alice along $\hat a$ and Bob along $\hat b$ corresponds to the operator $(\hat a \cdot \vec\sigma) \otimes (\hat b \cdot \vec\sigma)$. The expectation value in $|\Phi^+\rangle$ is straightforward — let me show it.

For the Bell state $|\Phi^+\rangle$, a short calculation (which you should do in the exercises) gives

$$E(\hat a, \hat b) = \langle\Phi^+|(\hat a \cdot \vec\sigma) \otimes (\hat b \cdot \vec\sigma)|\Phi^+\rangle = a_x b_x - a_y b_y + a_z b_z$$

Restrict to the $xz$-plane (set $a_y = b_y = 0$) with $\hat a = (\sin\theta_a, 0, \cos\theta_a)$ and $\hat b = (\sin\theta_b, 0, \cos\theta_b)$:

$$E(\hat a, \hat b) = \sin\theta_a \sin\theta_b + \cos\theta_a \cos\theta_b = \cos(\theta_a - \theta_b)$$

The correlation depends only on the *relative* angle between the measurement directions. Clean.

### 5.4 The CHSH violation at optimal angles

Pick the four angles

$$\theta_{A_1} = 0°, \quad \theta_{A_2} = 90°, \quad \theta_{B_1} = 45°, \quad \theta_{B_2} = 135°$$

Compute the four correlations:

$$E(A_1, B_1) = \cos(0° - 45°) = \cos(-45°) = \tfrac{1}{\sqrt{2}}$$

$$E(A_1, B_2) = \cos(0° - 135°) = \cos(-135°) = -\tfrac{1}{\sqrt{2}}$$

$$E(A_2, B_1) = \cos(90° - 45°) = \cos(45°) = \tfrac{1}{\sqrt{2}}$$

$$E(A_2, B_2) = \cos(90° - 135°) = \cos(-45°) = \tfrac{1}{\sqrt{2}}$$

The CHSH parameter $S = E(A_1, B_1) + E(A_1, B_2) + E(A_2, B_1) - E(A_2, B_2)$ uses sign convention with a minus on the last term. Reading off the angles: the standard CHSH-maximizing choice uses settings such that three of the four relative angles are $\pi/4$ and one is $3\pi/4$, giving three correlations of $+1/\sqrt 2$ and one of $-1/\sqrt 2$. Substituting our values:

$$S = \tfrac{1}{\sqrt 2} + \bigl(-\tfrac{1}{\sqrt 2}\bigr) + \tfrac{1}{\sqrt 2} - \tfrac{1}{\sqrt 2}$$

That is not quite right with our particular setting choices because the sign on $E(A_1, B_2)$ is already negative. Let me redo the bookkeeping with the cleaner angle choice that the literature uses.

Take

$$\theta_{A_1} = 0°, \quad \theta_{A_2} = 90°, \quad \theta_{B_1} = 45°, \quad \theta_{B_2} = -45°$$

Then

$$E(A_1, B_1) = \cos(-45°) = \tfrac{1}{\sqrt 2}$$
$$E(A_1, B_2) = \cos(45°) = \tfrac{1}{\sqrt 2}$$
$$E(A_2, B_1) = \cos(45°) = \tfrac{1}{\sqrt 2}$$
$$E(A_2, B_2) = \cos(135°) = -\tfrac{1}{\sqrt 2}$$

And so

$$S = \tfrac{1}{\sqrt 2} + \tfrac{1}{\sqrt 2} + \tfrac{1}{\sqrt 2} - \bigl(-\tfrac{1}{\sqrt 2}\bigr) = \tfrac{4}{\sqrt 2} = 2\sqrt 2 \approx 2.828$$

The classical bound is $2$. The quantum prediction at the optimal angles is $2\sqrt 2$. Quantum mechanics violates the inequality by a factor of $\sqrt 2$.

This is the punchline of Bell's theorem in the CHSH form. There is no local hidden-variable theory whose CHSH parameter can exceed $2$. Quantum mechanics with the entangled state $|\Phi^+\rangle$ predicts $2\sqrt 2$. The two predictions are different, so the experiment can decide.

### 5.5 The Tsirelson bound

How big can $|S|$ get in quantum mechanics? Boris Tsirelson showed in 1980 that

$$|S|_{\text{QM}} \leq 2\sqrt 2$$

for any quantum state and any measurement operators with eigenvalues $\pm 1$. This is the **Tsirelson bound**. It sits strictly below the algebraic maximum $|S| = 4$ that would be allowed if we only required the $\pm 1$ outcomes. Why does nature stop at $2\sqrt 2$ rather than at $4$? Information causality (Pawlowski et al. 2009, *Nature* 461, 1101) gives one principled answer. The deeper reason — *why these correlations and not stronger* — is an open question in quantum foundations. See §10.

**Misconception 2.** *"Bell's theorem proves quantum mechanics is non-local."* What Bell's theorem proves, sharply, is this: no *local realistic* theory reproduces the quantum correlations. Quantum mechanics itself is non-signaling (we will show this in a moment) but it does not respect classical locality in the sense of factorizing joint probabilities through a common cause. You can give up locality (Bohmian mechanics keeps a hidden variable but allows non-local influence) or give up realism (Copenhagen-type interpretations deny pre-existing values) or give up the unique-outcome assumption (many-worlds). What you cannot do is keep all three.

## 6. Concept block — the experimental verdict and the 2022 Nobel

### 6.1 What experiments needed to do

The CHSH derivation makes a clean prediction. To make a clean experiment, you have to close *loopholes* — ways the LHV theorist could rescue locality by pointing to an experimental imperfection.

- **Locality loophole.** If the choice of Alice's setting is in causal contact with Bob's particle, an LHV theory could let Bob's particle "know" what setting will be used and pick its outcome accordingly. Fix: separate Alice and Bob far enough that the settings are chosen and measurements completed within the light-travel time between them. Aspect, Dalibard, and Roger (1982, [*Phys. Rev. Lett.* 49, 1804](https://link.aps.org/doi/10.1103/PhysRevLett.49.1804)) closed this with rapidly switched polarizers.
- **Detection loophole.** If detectors miss most photons, a clever LHV theory can make the *detected subensemble* obey the inequality while the full ensemble would violate it. Fix: use high-efficiency detectors. Solid-state platforms (NV centers, superconducting detectors) made this tractable in the 2010s.
- **Freedom-of-choice loophole.** What if the random choices of setting are themselves correlated with $\lambda$? Fix: use cosmic photons or human choices to seed the settings (Big Bell Test 2018).

Three groups closed all three loopholes simultaneously in **2015**:

- **Hensen et al.**, "[Loophole-free Bell inequality violation using electron spins separated by 1.3 kilometres](https://www.nature.com/articles/nature15759)," *Nature* 526, 682 (2015) — Delft, electron spins in NV centers entangled through photons, $S = 2.42 \pm 0.20$.
- **Giustina et al.**, "[Significant-Loophole-Free Test of Bell's Theorem with Entangled Photons](https://link.aps.org/doi/10.1103/PhysRevLett.115.250401)," *Phys. Rev. Lett.* 115, 250401 (2015) — Vienna, photons from parametric down-conversion, violation at 11.5 standard deviations.
- **Shalm et al.**, "[Strong Loophole-Free Test of Local Realism](https://link.aps.org/doi/10.1103/PhysRevLett.115.250402)," *Phys. Rev. Lett.* 115, 250402 (2015) — NIST, photons with superconducting nanowire detectors.

Three different platforms — solid-state spins, parametric photons, superconducting detection — agreeing within months. The experimental case for Bell-violation is now triangulated. The Nobel committee waited seven more years and then made it official: the [2022 prize](https://www.nobelprize.org/prizes/physics/2022/press-release/) went to Aspect, Clauser, and Zeilinger.

### 6.2 No signaling — refuting the FTL misreading

A loud popular-science claim has it that entanglement enables faster-than-light communication. It does not. The argument is short and decisive.

Suppose Alice and Bob share $|\Phi^+\rangle$. Alice measures her qubit in some basis and gets some outcome. The question: can Bob detect Alice's choice of basis by looking only at his qubit?

Compute Bob's reduced density matrix:

$$\hat\rho_B = \text{Tr}_A\bigl(|\Phi^+\rangle\langle\Phi^+|\bigr) = \tfrac{1}{2}|0\rangle\langle 0| + \tfrac{1}{2}|1\rangle\langle 1| = \tfrac{1}{2}\hat I$$

The maximally mixed state. Whatever Alice does, Bob's local statistics — every expectation value of every operator Bob can measure — are determined by $\hat\rho_B = \hat I / 2$. They cannot change. There is *no* operation Alice can perform that alters Bob's local probability distribution. The non-locality of the joint statistics is invisible to Bob until he and Alice compare notes, and that comparison requires a classical channel.

This is the **no-signaling theorem**. The correlations in $|\Phi^+\rangle$ are non-classical, but they are useless as a one-way communication channel. Information flows only at the speed of light, because the channel that reveals the correlation is classical.

The misreading happens because popular explanations describe Alice's measurement as "instantly causing Bob's particle to collapse." The trouble with this language is that there is no relativistically invariant fact about which measurement happened first when Alice and Bob are spacelike separated. The predictions of quantum mechanics are unambiguous because they describe *joint statistics*, not a sequence of causal influences.

## 7. Concept block — qubits, gates, and protocols

The entanglement we just specified turns out to be the resource that makes quantum computing different from classical computing. This section introduces the formalism just enough to make the difference visible.

### 7.1 The qubit and the Bloch sphere

A **qubit** is any two-level quantum system. A pure qubit state is

$$|\psi\rangle = \alpha|0\rangle + \beta|1\rangle, \qquad |\alpha|^2 + |\beta|^2 = 1$$

Two real parameters survive after normalization and the overall phase: write

$$|\psi\rangle = \cos\!\bigl(\tfrac{\theta}{2}\bigr)|0\rangle + e^{i\phi}\sin\!\bigl(\tfrac{\theta}{2}\bigr)|1\rangle$$

with $\theta \in [0, \pi]$ and $\phi \in [0, 2\pi)$. The state lives on the surface of the **Bloch sphere**, the unit sphere in $\mathbb{R}^3$, with $|0\rangle$ at the north pole and $|1\rangle$ at the south. The equator at $\theta = \pi/2$ holds the relative-phase states $(|0\rangle + e^{i\phi}|1\rangle)/\sqrt 2$, including $|+\rangle, |-\rangle, |+i\rangle, |-i\rangle$.

This picture is the chapter's central visualization device. Single-qubit gates are rotations of the sphere. Mixed states sit in the interior. Decoherence shrinks the Bloch vector toward the origin — Chapter 13 will spend pages on this.

### 7.2 Single-qubit gates

The Pauli matrices act as $\pi$-rotations of the Bloch sphere about the $x$, $y$, $z$ axes:

$$\hat\sigma_x = X = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}, \quad \hat\sigma_y = Y = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}, \quad \hat\sigma_z = Z = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$$

$X$ is the quantum NOT: $X|0\rangle = |1\rangle$, $X|1\rangle = |0\rangle$. $Z$ adds a sign to $|1\rangle$. $Y$ is $iXZ$.

The **Hadamard** gate is the workhorse for creating superposition:

$$H = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$$

It is a $\pi$ rotation about the axis halfway between $\hat x$ and $\hat z$. Its action on the basis states:

$$H|0\rangle = \tfrac{1}{\sqrt{2}}(|0\rangle + |1\rangle) = |+\rangle, \qquad H|1\rangle = \tfrac{1}{\sqrt{2}}(|0\rangle - |1\rangle) = |-\rangle$$

Hadamard is the gate that takes a basis state to an equal superposition. It is the first move in nearly every quantum algorithm.

### 7.3 The CNOT gate and Bell-state preparation

The **CNOT** (controlled-NOT) gate acts on two qubits. It flips the target qubit if and only if the control qubit is $|1\rangle$:

$$\text{CNOT}|c, t\rangle = |c, t \oplus c\rangle$$

In the basis $\{|00\rangle, |01\rangle, |10\rangle, |11\rangle\}$ — with the leftmost qubit as control and the rightmost as target — its matrix is

$$\text{CNOT} = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 0 \end{pmatrix}$$

Look at this matrix carefully. It is a permutation: it swaps $|10\rangle$ with $|11\rangle$ and leaves the other two alone. It is also unitary (its columns are orthonormal). And it is the *only* two-qubit ingredient you need: together with the single-qubit gates above and the $T$ gate ($\text{diag}(1, e^{i\pi/4})$), CNOT generates a universal gate set — any unitary on any number of qubits can be approximated to arbitrary precision (Solovay–Kitaev, Nielsen & Chuang 2010 Ch. 4).

Now build a Bell state. Start with $|00\rangle$. Apply Hadamard to qubit 0:

$$(H \otimes I)|00\rangle = (H|0\rangle) \otimes |0\rangle = \tfrac{1}{\sqrt 2}(|0\rangle + |1\rangle) \otimes |0\rangle = \tfrac{1}{\sqrt 2}(|00\rangle + |10\rangle)$$

Apply CNOT with qubit 0 as control, qubit 1 as target. The first ket $|00\rangle$ has control = 0, so the target is unchanged. The second ket $|10\rangle$ has control = 1, so the target flips to $1$:

$$\text{CNOT} \cdot \tfrac{1}{\sqrt 2}(|00\rangle + |10\rangle) = \tfrac{1}{\sqrt 2}(|00\rangle + |11\rangle) = |\Phi^+\rangle$$

Two gates. A Hadamard and a CNOT. That is the entire Bell-state preparation. Run it on any quantum computer and you get the state that violates Bell's inequality.

This is the chapter's most quiet payoff. The *philosophical* object that Einstein argued was incomplete and Bell turned into a falsifiable prediction is *operationally* generated by two specific unitaries in two clock cycles of a quantum processor. Foundations and engineering meet on the same page.

### 7.4 No-cloning

Suppose you could build a quantum copy machine — a unitary $\hat U$ that, given an arbitrary unknown qubit $|\psi\rangle$ and a blank $|0\rangle$, returns two copies: $\hat U(|\psi\rangle|0\rangle) = |\psi\rangle|\psi\rangle$.

Wootters and Zurek showed in [1982](https://www.nature.com/articles/299802a0) (*Nature* 299, 802) that no such $\hat U$ exists. The argument fits in three lines. Take two unknown states $|\psi\rangle$ and $|\phi\rangle$. Cloning would give

$$\hat U|\psi\rangle|0\rangle = |\psi\rangle|\psi\rangle, \quad \hat U|\phi\rangle|0\rangle = |\phi\rangle|\phi\rangle$$

Unitaries preserve inner products. Take the inner product of the two sides:

$$\langle\phi|\psi\rangle = \langle\phi|\psi\rangle^2$$

So $\langle\phi|\psi\rangle$ equals either $0$ or $1$. The states are either orthogonal or identical. Cloning works only on a known orthogonal basis — not on arbitrary unknown inputs. (Dieks 1982, *Physics Letters A* 92, 271 [verify], showed the same thing independently.)

The no-cloning theorem is a structural barrier with consequences:

- It guarantees that quantum-key-distribution protocols (BB84, Ekert91) cannot be intercepted and resent without detection.
- It is the reason quantum error correction has to be cleverer than classical redundancy — you cannot simply make three copies of a qubit and majority-vote.
- It enforces no-signaling: if Bob could clone an unknown received qubit, he could distinguish between Alice's measurement bases statistically, and Alice could signal.

### 7.5 Quantum teleportation

If you cannot copy quantum states, can you at least *move* them? Bennett, Brassard, Crépeau, Jozsa, Peres, and Wootters showed in [1993](https://link.aps.org/doi/10.1103/PhysRevLett.70.1895) (*Phys. Rev. Lett.* 70, 1895) that you can — at the cost of consuming entanglement and sending two classical bits.

The setup: Alice has an unknown qubit $|\psi\rangle_1 = \alpha|0\rangle + \beta|1\rangle$. Alice and Bob share a Bell pair $|\Phi^+\rangle_{23}$. The full state of all three qubits:

$$|\psi\rangle_1 \otimes |\Phi^+\rangle_{23} = (\alpha|0\rangle + \beta|1\rangle) \otimes \tfrac{1}{\sqrt 2}(|00\rangle + |11\rangle)$$

Expand:

$$= \tfrac{1}{\sqrt 2}\bigl(\alpha|000\rangle + \alpha|011\rangle + \beta|100\rangle + \beta|111\rangle\bigr)$$

Now rewrite the qubits 1 and 2 in the Bell basis. After a few lines of algebra (which Nielsen & Chuang work through in §1.3.7):

$$|\psi\rangle_1 \otimes |\Phi^+\rangle_{23} = \tfrac{1}{2}\bigl[|\Phi^+\rangle_{12}(\alpha|0\rangle + \beta|1\rangle)_3 + |\Phi^-\rangle_{12}(\alpha|0\rangle - \beta|1\rangle)_3$$
$$+ |\Psi^+\rangle_{12}(\beta|0\rangle + \alpha|1\rangle)_3 + |\Psi^-\rangle_{12}(\beta|0\rangle - \alpha|1\rangle)_3\bigr]$$

Alice measures qubits 1 and 2 in the Bell basis. She gets one of four outcomes, each with probability $1/4$. Bob's qubit collapses to one of the four states inside the parentheses. Alice phones Bob the two-bit label of her outcome over a classical channel. Bob applies one of $\{I, X, Z, XZ\}$ as a correction:

- $|\Phi^+\rangle$ → apply $I$
- $|\Phi^-\rangle$ → apply $Z$
- $|\Psi^+\rangle$ → apply $X$
- $|\Psi^-\rangle$ → apply $XZ$

In each case Bob recovers $\alpha|0\rangle + \beta|1\rangle = |\psi\rangle$ on qubit 3.

What was *transmitted*? Two classical bits, at the speed of light. What was *consumed*? One Bell pair. What happened to the original state on qubit 1? It was destroyed in the Bell measurement (consistent with no-cloning). Bob did not receive a copy; he received the state, and Alice no longer has it. The first experimental realization came from the Zeilinger group in 1997 (Bouwmeester et al., *Nature* 390, 575 [verify]).

**Misconception 3.** *"Teleportation transmits information faster than light."* No. The two classical bits travel at $c$. Without them, Bob's qubit is in a maximally mixed state — useless. With them, Bob applies the appropriate correction and recovers $|\psi\rangle$. The entanglement is consumed; the two classical bits are necessary. The protocol is *as fast as light*, not faster.

### 7.6 Decoherence — the bridge to Chapter 13

Real qubits do not stay pure. They get entangled with the environment. Trace out the environment and the qubit's reduced density matrix is no longer pure: the Bloch vector shrinks from the surface of the sphere toward the origin.

Two timescales characterize the decay:

- $T_1$ (**energy relaxation**) — the time for an excited state to decay. The $z$-component of the Bloch vector returns to its equilibrium value.
- $T_2$ (**dephasing**) — the time for the off-diagonal elements of the density matrix to decay. The transverse $x, y$ components of the Bloch vector shrink to zero.

These two timescales are related by $T_2 \leq 2T_1$. Pure-dephasing channels can make $T_2$ shorter than $2T_1$; energy relaxation alone gives $T_2 = 2T_1$. Chapter 13 derives this from the Lindblad master equation, and the Bloch vector spiraling inward is the chapter's signature image.

The reason this matters in Chapter 12: entanglement is the resource. Decoherence is the leak. Every quantum protocol is in a race against the environment to do its job before the entanglement evaporates. Quantum error correction (Ch. 13) is the engineering response.

## 8. Worked examples

### 8.1 Verifying that $|\Phi^+\rangle$ violates CHSH

Compute the four correlations explicitly with $|\Phi^+\rangle = (|00\rangle + |11\rangle)/\sqrt 2$ and the angle choice $\theta_{A_1} = 0, \theta_{A_2} = \pi/2, \theta_{B_1} = \pi/4, \theta_{B_2} = -\pi/4$ from §5.4.

Recall $E(\hat a, \hat b) = \cos(\theta_a - \theta_b)$ for this state with planar axes. The four values:

$$E(A_1, B_1) = \cos(-\pi/4) = +\tfrac{1}{\sqrt 2}$$
$$E(A_1, B_2) = \cos(\pi/4) = +\tfrac{1}{\sqrt 2}$$
$$E(A_2, B_1) = \cos(\pi/4) = +\tfrac{1}{\sqrt 2}$$
$$E(A_2, B_2) = \cos(3\pi/4) = -\tfrac{1}{\sqrt 2}$$

$$S = \tfrac{1}{\sqrt 2} + \tfrac{1}{\sqrt 2} + \tfrac{1}{\sqrt 2} - \bigl(-\tfrac{1}{\sqrt 2}\bigr) = \tfrac{4}{\sqrt 2} = 2\sqrt 2 \approx 2.828$$

The Tsirelson bound, reached. Compare to the classical bound $|S| \leq 2$. The violation is $0.828$ — about $40\%$ above the LHV ceiling.

### 8.2 Verifying that a product state does not violate

Take the product state $|0\rangle|0\rangle$. Compute

$$E(\hat a, \hat b) = \langle 0|(\hat a \cdot \vec\sigma)|0\rangle \cdot \langle 0|(\hat b \cdot \vec\sigma)|0\rangle$$

because expectation values factorize for product states. For axes in the $xz$-plane, $\langle 0|\hat\sigma_x|0\rangle = 0$ and $\langle 0|\hat\sigma_z|0\rangle = 1$, so

$$\langle 0|(\hat a \cdot \vec\sigma)|0\rangle = \cos\theta_a$$

and

$$E(\hat a, \hat b) = \cos\theta_a \cos\theta_b$$

A product. Plug into CHSH with any four angles:

$$S = \cos\theta_{A_1}(\cos\theta_{B_1} + \cos\theta_{B_2}) + \cos\theta_{A_2}(\cos\theta_{B_1} - \cos\theta_{B_2})$$

This factors so cleanly that an LHV model exists: take $\lambda$ to fix $A_i = \text{sign}(\cos\theta_{A_i})$ deterministically. The CHSH parameter respects the bound $|S| \leq 2$ for every choice of angles. Product states cannot violate. The simulation makes this falsifiability check operational — flip the state selector to a product and watch $S$ stay below $2$ as you try to push it.

### 8.3 Bell-state preparation, step by step

Start with $|00\rangle$. Apply $H \otimes I$:

$$(H \otimes I)|00\rangle = \tfrac{1}{\sqrt 2}\bigl(|00\rangle + |10\rangle\bigr)$$

This is a superposition, but it is still a product state: it factors as $(\tfrac{1}{\sqrt 2}(|0\rangle + |1\rangle)) \otimes |0\rangle = |+\rangle \otimes |0\rangle$. No entanglement yet.

Apply CNOT (control = qubit 0, target = qubit 1):

$$\text{CNOT}\bigl(\tfrac{1}{\sqrt 2}(|00\rangle + |10\rangle)\bigr) = \tfrac{1}{\sqrt 2}\bigl(|00\rangle + |11\rangle\bigr) = |\Phi^+\rangle$$

Check that this is entangled by attempting to factor: §4.2 already did the calculation — no factorization exists. The CNOT, acting on a single-qubit superposition with a $|0\rangle$ target, *creates entanglement*. Before CNOT, the qubits were independent. After CNOT, neither qubit has a definite state on its own; their reduced density matrices are both $\hat I/2$.

This is the operational meaning of "entanglement is a resource generated by two-qubit gates."

## 9. What would change my mind

If a loophole-free Bell test were repeated at higher precision and consistently produced $|S| \leq 2$, or if a hidden-variable model emerged that respected locality and exactly reproduced the quantum predictions for all entangled states, the chapter's central claim — that quantum correlations cannot be reproduced by any local realistic theory — would be in trouble. The three 2015 experiments and their successors have so far come down on the quantum side at margins ranging from $11\sigma$ to many tens of standard deviations. The case is settled to the standard physics treats as settled.

## 10. Still puzzling

The quantum predictions saturate at $|S| = 2\sqrt 2$ — the Tsirelson bound — not at the algebraic maximum $|S| = 4$. There exist hypothetical correlations (Popescu-Rohrlich boxes) that respect no-signaling and reach $|S| = 4$. Nature could, consistent with relativity, have allowed those correlations. It does not. The principle of information causality (Pawlowski et al. 2009) gives one principled reason — stronger-than-quantum correlations would let Alice send more than $n$ bits of useful information using $n$ classical bits plus shared correlation. But the deeper question — *why exactly these correlations* — is still open. The Tsirelson bound is one of the few quantitative regularities in physics whose physical explanation we do not yet have.

## 11. LLM Exercise — Bell inequality simulator and gate circuit visualizer

You are going to build a two-panel D3 simulation that puts the CHSH parameter on screen as a number and lets you drive it across the classical bound by tuning angles. Then a small gate-circuit panel that shows Bell-state preparation by Hadamard and CNOT, with the qubit Bloch vectors collapsing to the origin as the entanglement forms.

### Part 1 — Update `PROJECT.md`

```
Append a new entry to PROJECT.md describing this chapter's simulation:

Chapter 12 — Entanglement and Quantum Information
Deliverable: 12-bell-inequality.html
Status: in progress

The simulation has two panels in one HTML file:

Panel A — CHSH Bell-inequality simulator (700 x 600 SVG).
- State selector: |Phi+>, |Phi->, |Psi+>, |Psi-> (Bell states); plus
  |00>, |+>|+> (product states); plus a classical-mixture toggle
  (mix |00> and |11> with 50/50 probability — perfectly correlated
  but not entangled).
- Four angle sliders: theta_A1, theta_A2, theta_B1, theta_B2,
  each in 0 to 2 pi radians, displayed in degrees.
- 2x2 outcome-probability table for each of the four (A_i, B_j)
  measurement pairs, updating live on slider change.
- Large display (~48 pt font) of the CHSH parameter S.
  Background color flips from white to amber when |S| > 2.
- Sub-panel below: S as a function of the relative angle
  (theta_A1 - theta_B1) with the other angles held at the
  optimal offsets. Horizontal red line at S = 2 (classical bound).
  Horizontal gold line at S = 2 sqrt(2) ~ 2.828 (Tsirelson bound).

Panel B — Gate-circuit visualizer (700 x 400 SVG).
- Two-qubit grid. Gates draggable from a palette: H, X, Y, Z,
  S, T, CNOT, Rz.
- Live display of the joint state vector as four complex amplitudes
  (modulus as bar height, phase as a small dial color-coded by HSL).
- Per-qubit Bloch spheres (one for each of the two qubits) showing
  the reduced state. Vector lives on the surface for product states
  and collapses to the origin for maximally entangled states.
- Default scaffold: |00> -> H on qubit 0 -> CNOT (control 0, target 1).
  Displays "|Phi+>" symbolically. Both Bloch vectors visibly collapse
  to the origin as the CNOT is applied.
- Measurement-outcome bar chart at the right (P(00), P(01), P(10), P(11)).

Sliders use snap-to-canonical-angles option: 0, 22.5, 45, 67.5, 90, 135.
```

### Part 2 — The CLAUDE.md amendment

```
Append to CLAUDE.md (coding constitution) the following physics rules for
Chapter 12 simulations:

ENTANGLEMENT AND QUANTUM-INFORMATION PHYSICS RULES

1. Two-qubit states are stored as complex 4-vectors over the basis
   |00>, |01>, |10>, |11>. Always normalize: sum |c_i|^2 must equal 1
   to within 1e-6 after every operation. Display a warning if not.

2. Single-qubit gates are 2x2 unitaries. To apply a single-qubit gate
   U to qubit 0, build U_full = U (tensor) I_2 (4x4). To apply to qubit 1,
   build U_full = I_2 (tensor) U. Use explicit Kronecker product code;
   do not hard-code matrix entries for two-qubit space.

3. CNOT in the basis |00>, |01>, |10>, |11> with control = qubit 0
   and target = qubit 1 is:
     [[1,0,0,0],[0,1,0,0],[0,0,0,1],[0,0,1,0]]
   Verify on |10>: should map to |11>.

4. CHSH calculation: for measurement axis (theta_A, theta_B) in the
   xz-plane, the measurement operator on Alice is
     sigma_a = sin(theta_A) * sigma_x + cos(theta_A) * sigma_z
   and analogously on Bob. The two-qubit operator is
     sigma_a (tensor) sigma_b
   The correlation is E(a, b) = <psi| sigma_a (tensor) sigma_b |psi>.

5. The CHSH parameter is
     S = E(A1, B1) + E(A1, B2) + E(A2, B1) - E(A2, B2)
   Show S to three decimal places. Background color flips when |S| > 2.

6. The Tsirelson bound is 2 * sqrt(2) ~ 2.8284. Display this as a
   horizontal gold line on the S-vs-angle sub-panel.

7. Reduced density matrices for the per-qubit Bloch sphere visualization:
     rho_A = Tr_B(|psi><psi|) computed as
       rho_A[i,j] = sum_k psi[i,k] * conj(psi[j,k])
     where psi[i,k] is the amplitude for Alice in state i and Bob in
     state k. Compute rho_B symmetrically. The Bloch vector is
       r_x = 2 Re(rho[0,1]), r_y = 2 Im(rho[1,0]), r_z = rho[0,0] - rho[1,1].

KNOWN FAILURE MODES to avoid:
(a) Tensor-product index ordering swapped (qubit-0 vs qubit-1 confusion).
    Verify on a known case: apply CNOT to |10>, confirm you get |11>.
(b) Phase convention drift between Alice and Bob axes. Stick to
    sin(theta) * sigma_x + cos(theta) * sigma_z everywhere.
(c) Normalization lost after multi-gate compositions. Renormalize and
    warn if |norm - 1| > 1e-4.
(d) Bloch vector visualized off-surface for pure states (rounding error).
    Clamp |r| to <= 1.
(e) Reduced density matrix not Hermitian (off-diagonals wrong sign).
    Verify rho^dagger = rho before extracting Bloch components.
(f) Slider snapping rounds angles to multiples of 5 degrees instead of
    the canonical CHSH angles. Provide both modes; default to canonical.
(g) State selector switches between "classical mixture" and "Bell state"
    without resetting the density matrix. Classical mixture has off-
    diagonal blocks zero in the |00>/|11> basis; Bell state has them
    nonzero. Make sure the simulator distinguishes.
```

### Part 3 — The simulation prompt

```
You are working in my directory which contains CLAUDE.md, DESIGN.md,
and PROJECT.md. Read all three first.

Build 12-bell-inequality.html: a single self-contained HTML file using
D3 v7 from a CDN, no other dependencies, that implements the Chapter 12
simulation as specified in PROJECT.md and following the physics rules
in CLAUDE.md and the visual constitution in DESIGN.md.

The simulation has two stacked panels (top: CHSH panel, bottom: gate
panel), each in its own SVG.

CHSH PANEL (700 x 600).
- State selector at top: radio buttons for |Phi+>, |Phi->, |Psi+>,
  |Psi->, |00>, |+>|+>, and "classical mixture (1/2 |00><00| + 1/2 |11><11|)".
- Four angle sliders below: theta_A1, theta_A2, theta_B1, theta_B2 in
  degrees, range 0 to 360, step 0.5. Canonical-snap toggle defaults on.
- 2x2 outcome-probability table for each of the four (A_i, B_j) pairs,
  laid out as a 2x4 grid of small tables. Each cell shows P(++), P(+-),
  P(-+), P(--) updated live.
- Large CHSH-value display in the center: "S = 2.828" at 48 pt.
  Background of the display flips to amber (#FFC107) when |S| > 2.
- Sub-panel at the bottom (700 x 200): plot of S vs (theta_A1 - theta_B1)
  with the other three angles fixed at their optimal-relative-offset
  values. Horizontal red line at y = 2, horizontal gold line at y = 2*sqrt(2).

GATE PANEL (700 x 400).
- Gate palette on the left: H, X, Y, Z, S, T, CNOT, Rz(theta).
  Each gate is a small draggable rectangle.
- Two-qubit circuit grid: two horizontal wires (qubit 0 on top), each
  with five empty gate slots in series. Drop a gate into a slot to add
  it to the circuit. CNOT spans both wires with a filled dot on the
  control and an open circle on the target. Click any slot to clear.
- Right side, three sub-displays:
  - Amplitude bar chart: four bars labeled |00>, |01>, |10>, |11>.
    Height = |c_i|, color hue = phase of c_i (HSL 0..360).
  - Two small Bloch spheres (150 x 150 each, stacked), one per qubit.
    Show the Bloch vector as an orange arrow from origin to (r_x, r_y, r_z).
    Equator and meridian as light grey circles.
  - Measurement-outcome probabilities P(00), P(01), P(10), P(11) as
    a small bar chart at opacity 0.7.

DEFAULT SCAFFOLD on load: |00> initial, qubit 0 wire has H in slot 1,
CNOT spanning both wires in slot 2 with control on qubit 0. The simulator
should display the resulting state as
  c = [1/sqrt(2), 0, 0, 1/sqrt(2)]
the amplitude bars show two bars of equal height, both Bloch vectors
have shrunk to the origin (because each reduced density matrix is I/2),
and a small symbolic label reads "|Phi+>".

Spatial grid for the CHSH sub-panel curve: 361 points in
(theta_A1 - theta_B1) from 0 to 2 pi. Live re-render on every slider change.

Runtime sanity checks (write to console):
- Sum |c_i|^2 = 1 within 1e-4 at every frame.
- For |Phi+> with canonical angles, S should display 2.828 +/- 0.001.
- For |00>, S must be in [-2, 2] for every angle choice. If the simulator
  reports |S| > 2 with a product state, flag a numerical bug.
- For the classical mixture, S must be in [-2, 2] for every angle choice.

Do NOT use any 3D library; the Bloch spheres are 2D projections of 3D
vectors using an orthographic projection. Do NOT use math.js; implement
the 4x4 matrix-vector and tensor-product arithmetic in vanilla JS.
Comments at every non-trivial physics step.
```

### Part 4 — Exploration tasks and extension prompt

Run the simulation and answer the following:

1. Set the state to $|\Phi^+\rangle$. Set angles to $(\theta_{A_1}, \theta_{A_2}, \theta_{B_1}, \theta_{B_2}) = (0°, 90°, 45°, -45°)$. Read $S$. You should see $S = 2.828$ — the Tsirelson bound. The background should be amber.

2. Now switch the state to $|00\rangle$ (a product state). Try every angle setting you can think of. Can you push $|S|$ above $2$? Why or why not? (Hint: §8.2 walks through the factorization argument. The simulation makes the impossibility operational.)

3. Switch the state to "classical mixture" (the simulator's option for $\tfrac{1}{2}|00\rangle\langle 00| + \tfrac{1}{2}|11\rangle\langle 11|$). The measurement outcomes are perfectly correlated when Alice and Bob measure in the $z$-basis. Try angles. Can you push $|S|$ above $2$? Conclude: perfect correlation is *not* the same as entanglement.

4. Switch back to $|\Phi^+\rangle$. Hold three angles at the canonical settings and sweep $\theta_{A_1}$ slowly through one full revolution. Watch the $S$-vs-angle curve in the sub-panel. Identify where $S$ peaks at $+2\sqrt 2$, where it bottoms at $-2\sqrt 2$, and where it crosses zero. Sketch the curve from memory after sliding.

5. In the gate panel, build the Bell preparation $|00\rangle \to H$ on qubit 0 $\to$ CNOT. Watch the two Bloch vectors. They start at the north pole (length 1). After Hadamard, qubit 0's vector points along $+\hat x$ (length 1). After CNOT, both Bloch vectors collapse to the origin. Explain in one sentence what the collapse means physically.

6. In the gate panel, build a *different* circuit: $|00\rangle \to X$ on qubit 1 $\to H$ on qubit 0 $\to$ CNOT. Identify which Bell state you produced.

**Extension prompt:**

```
Modify 12-bell-inequality.html to add a third panel implementing the
quantum-teleportation protocol of Bennett et al. 1993:

- Initial state: |psi>_1 = alpha |0> + beta |1> on qubit 1, with sliders
  for the angles theta, phi parameterizing alpha = cos(theta/2),
  beta = exp(i phi) sin(theta/2). Qubits 2 and 3 are in the Bell state
  |Phi+>.
- Step button: applies one of three operations in sequence
    (i) CNOT with control qubit 1 and target qubit 2;
    (ii) H on qubit 1;
    (iii) measure qubits 1 and 2 in the computational basis; randomly
         sample an outcome with the correct probabilities (1/4 each);
    (iv) apply the correction (I, X, Z, or XZ) to qubit 3 based on
         the measurement outcome.
- Display: the unknown qubit's Bloch vector at the start (on qubit 1);
  the Bell pair's joint state (qubits 2 and 3); the final state of
  qubit 3 after the protocol. Verify that the final state of qubit 3
  matches the initial state of qubit 1 — the unknown qubit has been
  teleported.
- Two classical-bit indicators (the measurement outcomes on qubits 1
  and 2): show them as small bit-displays that "travel" from Alice to
  Bob along a dashed grey line, animated at finite speed to emphasize
  that the protocol is no faster than light.

Update PROJECT.md to mark Chapter 12 as complete and note the
teleportation extension as the bridge to Chapter 13's decoherence
discussion: the protocol works perfectly with ideal entanglement;
real Bell pairs decohere, and the chapter 13 simulation lets you
watch the resource degrade.
```

---

*Sources consulted: Bell, J. S. (1964), "[On the Einstein Podolsky Rosen paradox](https://link.aps.org/doi/10.1103/PhysicsPhysiqueFizika.1.195)", *Physics Physique Fizika* 1, 195; Einstein, Podolsky, Rosen (1935), "[Can quantum-mechanical description of physical reality be considered complete?](https://link.aps.org/doi/10.1103/PhysRev.47.777)", *Phys. Rev.* 47, 777; Clauser, Horne, Shimony, Holt (1969), "[Proposed Experiment to Test Local Hidden-Variable Theories](https://link.aps.org/doi/10.1103/PhysRevLett.23.880)", *Phys. Rev. Lett.* 23, 880; Aspect, Dalibard, Roger (1982), "[Experimental Test of Bell's Inequalities Using Time-Varying Analyzers](https://link.aps.org/doi/10.1103/PhysRevLett.49.1804)", *Phys. Rev. Lett.* 49, 1804; Hensen et al. (2015), "[Loophole-free Bell inequality violation using electron spins separated by 1.3 kilometres](https://www.nature.com/articles/nature15759)", *Nature* 526, 682; Giustina et al. (2015), "[Significant-Loophole-Free Test of Bell's Theorem with Entangled Photons](https://link.aps.org/doi/10.1103/PhysRevLett.115.250401)", *Phys. Rev. Lett.* 115, 250401; Shalm et al. (2015), "[Strong Loophole-Free Test of Local Realism](https://link.aps.org/doi/10.1103/PhysRevLett.115.250402)", *Phys. Rev. Lett.* 115, 250402; Bennett et al. (1993), "[Teleporting an unknown quantum state via dual classical and Einstein–Podolsky–Rosen channels](https://link.aps.org/doi/10.1103/PhysRevLett.70.1895)", *Phys. Rev. Lett.* 70, 1895; Wootters & Zurek (1982), "[A single quantum cannot be cloned](https://www.nature.com/articles/299802a0)", *Nature* 299, 802; Dieks (1982), *Physics Letters A* 92, 271 [verify]; Tsirelson, B. S. (1980), "Quantum generalizations of Bell's inequality", *Letters in Mathematical Physics* 4, 93; Nielsen, M. A. & Chuang, I. L. (2010), *Quantum Computation and Quantum Information* (10th Anniversary Edition), Cambridge University Press — canonical textbook for §4, §5, §7; Griffiths Ch. 12; [Nobel Prize in Physics 2022](https://www.nobelprize.org/prizes/physics/2022/press-release/), Aspect, Clauser, Zeilinger; Bouwmeester et al. (1997), *Nature* 390, 575 [verify].*

*Tags: entanglement, Bell-inequality, CHSH, quantum-information, qubits, no-cloning, teleportation, Nobel-2022, d3-simulation*

*Status: draft for Nik's review. Three `[verify]` flags: Dieks 1982 *Phys. Lett. A* 92, 271 (independent no-cloning); Bouwmeester et al. 1997 *Nature* 390, 575 (first teleportation experiment); the specific framing of the CHSH-violation sigma counts in the 2015 papers. The CHSH derivation (LHV bound proof in §5.2; quantum prediction reaching $2\sqrt 2$ at optimal angles in §5.3–§5.4) is the chapter's load-bearing mechanism and is rendered in full.*
