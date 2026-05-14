# Chapter 6 — Spin

> An angular momentum with no classical analog: the two-state Hilbert space, the Pauli matrices, and the experiment that found something quantum theory hadn't yet imagined.

---

## 1. The 1922 puzzle

In February 1922, Otto Stern and Walther Gerlach sent a thin beam of neutral silver atoms through the gap between a sharp pole piece and a flat one — an inhomogeneous magnetic field — and let the beam strike a glass plate. The classical prediction was clean. A silver atom carries a magnetic moment $\vec{\mu}$; the field exerts a force $\vec{F} = \nabla(\vec{\mu}\cdot\vec{B})$; atoms entering with $\vec{\mu}$ at every possible angle to $\hat{z}$ would deposit in a continuous smear along the plate.

When Stern developed the plate (famously aided by sulfur from his cheap cigar, which reacted with silver to make the faint trace visible), he found two spots. Not a smear. Two.

That is the empirical fact this chapter has to explain. Whatever a silver atom carries, the component along whichever axis you choose to measure takes exactly two values, never three, never a continuum. The deflection is proportional to $\mu_z$, so two deflections means two $\mu_z$ values. Always. For any axis you point.

A subtlety the chapter has to honor up front: Stern and Gerlach in 1922 did *not* discover electron spin. Spin did not exist as a concept until late 1925, when George Uhlenbeck and Samuel Goudsmit proposed it in *Die Naturwissenschaften* 13, 953. Stern and Gerlach believed they were observing the "space quantization" of orbital angular momentum predicted by the old Bohr–Sommerfeld theory. Silver has the configuration [Kr] $4d^{10} 5s^1$; its lone valence electron sits in an $s$ orbital with $\ell = 0$ and contributes zero orbital angular momentum. The two-spot pattern is in fact the projection of the *spin* of that single $5s^1$ valence electron. The 1922 experiment is the right answer to the wrong question, and the right answer only became readable three years later.

I find this is worth telling honestly because it is exactly how physics often goes. An experiment is robust; its interpretation depends on which concepts have been invented yet.

**Learning objectives.** By the end of this chapter, you should be able to:

- State what spin is and what it isn't (it is not a small ball rotating, and you will see why with a number).
- Write the three Pauli matrices from memory and verify four algebraic facts about them.
- Build the eigenstates of $\hat{S}_{\hat{n}}$ — spin along an arbitrary direction — and apply the Born rule to compute outcome probabilities.
- Solve the time-dependent Schrödinger equation for a spin in a uniform magnetic field and recover Larmor precession.
- Explain why a sequential Stern–Gerlach experiment ($SG_z \to SG_x \to SG_z$) gives 50/50 on the third stage, and why this is not "measurement disturbance" in the classical sense.
- Build a three-panel interactive simulation that lets you drag spin states on the Bloch sphere, watch SG outcome probabilities update, and visualize Larmor precession.

**Prerequisites.** Wave functions and the Born rule (Ch. 1–2). Dirac notation and Hermitian operators on a finite-dimensional Hilbert space (Ch. 4). Orbital angular momentum and the commutator $[\hat{L}_i, \hat{L}_j] = i\hbar \epsilon_{ijk} \hat{L}_k$ (Ch. 5). Calculus through partial derivatives. Matrix multiplication for $2\times 2$ matrices.

---

## 2. The two-state Hilbert space and the Pauli matrices

### 2.1 Why two

The empirical wedge is "always two values." Whatever Hilbert space spin lives in, that space must be such that any Hermitian operator representing a spin component has exactly two eigenvalues. The smallest space that does this is $\mathbb{C}^2$ — two-dimensional, complex.

Choose a basis. Conventionally, the eigenstates of $\hat{S}_z$:

$$ |\!\uparrow\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \qquad |\!\downarrow\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}. $$

You should read these as "spin-up along $z$" and "spin-down along $z$." Up to an overall phase, the general spin state is

$$ |\psi\rangle = \alpha |\!\uparrow\rangle + \beta |\!\downarrow\rangle, \qquad |\alpha|^2 + |\beta|^2 = 1. $$

Two complex numbers, minus one normalization, minus one global phase: two real parameters. That is the dimension of a sphere.

### 2.2 The Pauli matrices

The spin operators are $\hat{S}_i = (\hbar/2) \sigma_i$ where $\sigma_x, \sigma_y, \sigma_z$ are the three **Pauli matrices**. Write them out — every later identity in this chapter depends on them:

$$ \sigma_x = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}, \qquad \sigma_y = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}, \qquad \sigma_z = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}. $$

Four facts about these matrices, all checkable by direct multiplication. Get a piece of paper and verify each one before moving on; it pays off later.

**Fact 1: $\sigma_i^2 = I$ for each $i$.** Compute, for instance,

$$ \sigma_x^2 = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}\begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix} = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} = I. $$

**Fact 2: $\mathrm{Tr}(\sigma_i) = 0$.** Read off the diagonal entries: $0+0$, $0+0$, $1+(-1) = 0$.

**Fact 3: Anticommutation.** $\{\sigma_i, \sigma_j\} = \sigma_i \sigma_j + \sigma_j \sigma_i = 2 \delta_{ij} I$. For $i = j$ this is just Fact 1 doubled. For $i \neq j$, you can check $\sigma_x \sigma_y + \sigma_y \sigma_x = 0$:

$$ \sigma_x \sigma_y = \begin{pmatrix} i & 0 \\ 0 & -i \end{pmatrix}, \qquad \sigma_y \sigma_x = \begin{pmatrix} -i & 0 \\ 0 & i \end{pmatrix}, $$

sum to zero. Different Pauli matrices anticommute.

**Fact 4: Commutation.** $[\sigma_i, \sigma_j] = 2i \epsilon_{ijk} \sigma_k$. From the calculation above, $\sigma_x \sigma_y - \sigma_y \sigma_x = 2i \sigma_z$. Equivalently, $[\hat{S}_i, \hat{S}_j] = i\hbar \epsilon_{ijk} \hat{S}_k$ — the same angular-momentum algebra you derived for orbital $\hat{L}$ in Chapter 5.

Combine Facts 3 and 4: $\sigma_i \sigma_j = \delta_{ij} I + i \epsilon_{ijk} \sigma_k$. This single identity is the multiplication table for the Pauli algebra, and it shows up everywhere — in QED Feynman rules, in NMR pulse sequences, in qubit gates. Memorize it.

The Pauli matrices are not arbitrary. They are forced by four requirements: (a) Hermitian (so the eigenvalues are real); (b) traceless (so the eigenvalues are $\pm \hbar/2$, summing to zero); (c) squaring to $I$ (so $\hat{S}_i^2 = (\hbar/2)^2 I$); (d) satisfying the angular-momentum commutator. Up to a unitary change of basis, no other $2 \times 2$ matrices do all four. Together they generate $SU(2)$, the group of $2 \times 2$ unitary matrices with determinant 1 — the natural rotation group for objects living in $\mathbb{C}^2$.

### 2.3 Spin is not rotation — the numerical takedown

Many students arrive with the picture that an electron is a tiny ball physically rotating on its axis, and "spin" is the angular momentum of that rotation. Kill this picture now, with a number, not a hand-wave. We will compute the equatorial speed required if it were true, and find it embarrassing.

Give the electron the most generous size you can — the *classical electron radius*

$$ r_e = \frac{e^2}{4\pi\epsilon_0 m_e c^2} \approx 2.82 \times 10^{-15} \text{ m}, $$

defined by setting the electrostatic self-energy equal to $m_e c^2$. (Modern experimental bounds place the actual electron size below $10^{-18}$ m, but we want the most generous possible radius, since a smaller radius makes the picture fail worse.)

Demand angular momentum $\hbar/2$. The moment of inertia of a uniform solid sphere is $I = \frac{2}{5} m_e r_e^2$, and $L = I \omega$, so the equatorial speed is $v = \omega r_e = L r_e / I = 5 \hbar / (4 m_e r_e)$:

$$ v = \frac{5 \times 1.055 \times 10^{-34} \text{ J s}}{4 \times 9.11 \times 10^{-31} \text{ kg} \times 2.82 \times 10^{-15} \text{ m}} \approx 5.1 \times 10^{10} \text{ m/s}. $$

The speed of light is $c \approx 3.0 \times 10^8$ m/s. The required equatorial speed is roughly $170 c$. The picture is not wrong by a few percent; it is wrong by more than two orders of magnitude.

Give the electron a smaller radius (truer to experiment) and the speed gets worse. Give it a larger radius and the required angular momentum drops, but you have to argue the electron is bigger than $10^{-15}$ m — which experiment forbids. There is no escape inside the "spinning ball" picture.

So what *is* spin? An internal degree of freedom that transforms as a representation of $SU(2)$ under rotations. It is not a description of any motion in space. It is a label the electron carries — a label that takes two values when you measure it, that obeys the same operator algebra as orbital angular momentum (so it deserves the name "angular momentum" in the operator-algebra sense), and that has no classical analog whatsoever. Paul Dirac (1928, *Proceedings of the Royal Society A* 117, 610 [verify]) derived spin-1/2 from the requirement that the wave equation be Lorentz-invariant and first-order in time. Spin falls out of relativity plus quantum mechanics; you do not put it in by hand.

You will sometimes hear "spin is intrinsic angular momentum." That is true but vacuous unless you say what *intrinsic* means. Intrinsic means: the algebra is angular momentum, the carrier is a representation of $SU(2)$, and the underlying degree of freedom does not correspond to any motion in physical space.

---

## 3. The Bloch sphere — the chapter's deep dive

### 3.1 Spin along an arbitrary direction

Pick a unit vector $\hat{n} = (\sin\theta \cos\phi, \sin\theta \sin\phi, \cos\theta)$. The spin operator along $\hat{n}$ is

$$ \hat{S}_{\hat{n}} = \frac{\hbar}{2} \hat{n}\cdot\vec{\sigma} = \frac{\hbar}{2}(n_x \sigma_x + n_y \sigma_y + n_z \sigma_z). $$

Substituting the Pauli matrices and the components of $\hat{n}$:

$$ \hat{n}\cdot\vec{\sigma} = \begin{pmatrix} \cos\theta & \sin\theta \, e^{-i\phi} \\ \sin\theta \, e^{i\phi} & -\cos\theta \end{pmatrix}. $$

Two questions. What are the eigenvalues? What are the eigenvectors?

**Eigenvalues.** The determinant is $-\cos^2\theta - \sin^2\theta = -1$, and the trace is $0$. The characteristic polynomial is $\lambda^2 - 1 = 0$, giving $\lambda = \pm 1$. The eigenvalues of $\hat{S}_{\hat{n}} = (\hbar/2) \hat{n}\cdot\vec{\sigma}$ are therefore $\pm \hbar/2$. This is the formal statement of "always two spots, any axis you point."

**Eigenvectors.** Solve $(\hat{n}\cdot\vec{\sigma}) |\hat{n}, +\rangle = +|\hat{n}, +\rangle$:

$$ \begin{pmatrix} \cos\theta - 1 & \sin\theta \, e^{-i\phi} \\ \sin\theta \, e^{i\phi} & -\cos\theta - 1 \end{pmatrix} \begin{pmatrix} a \\ b \end{pmatrix} = 0. $$

Use the half-angle identities $1 - \cos\theta = 2\sin^2(\theta/2)$ and $\sin\theta = 2\sin(\theta/2)\cos(\theta/2)$. The top row gives

$$ -2\sin^2(\theta/2) \, a + 2\sin(\theta/2)\cos(\theta/2) e^{-i\phi} \, b = 0, $$

so $a/b = \cos(\theta/2)/(\sin(\theta/2) e^{i\phi}) \cdot e^{i\phi}/e^{i\phi}$, cleaning up to $a = \cos(\theta/2)$ and $b = e^{i\phi} \sin(\theta/2)$ (after fixing the overall phase). The normalized eigenstate is

$$ \boxed{ |\hat{n}, +\rangle = \cos(\theta/2) |\!\uparrow\rangle + e^{i\phi} \sin(\theta/2) |\!\downarrow\rangle. } $$

The orthogonal "minus" eigenstate is

$$ |\hat{n}, -\rangle = \sin(\theta/2) |\!\uparrow\rangle - e^{i\phi} \cos(\theta/2) |\!\downarrow\rangle. $$

Stop and look at the half-angle. A state pointing along $+\hat{x}$ corresponds to $\theta = \pi/2, \phi = 0$, so $|\hat{x}, +\rangle = \frac{1}{\sqrt{2}}(|\!\uparrow\rangle + |\!\downarrow\rangle)$. Equal weights on $|\!\uparrow\rangle$ and $|\!\downarrow\rangle$ — which is right, because a spin pointing along $+\hat{x}$ should give 50/50 outcomes when measured along $\hat{z}$. A state pointing along $-\hat{z}$ corresponds to $\theta = \pi$, so $|\hat{z}, -\rangle = e^{i\phi}\sin(\pi/2) |\!\downarrow\rangle = e^{i\phi} |\!\downarrow\rangle$ — equal to $|\!\downarrow\rangle$ up to an overall phase, as it should.

The deeper consequence of the half-angle: rotating the analyzer by $2\pi$ (a full turn in physical space) sends $\theta \to \theta + 2\pi$, which sends $\cos(\theta/2) \to -\cos(\theta/2)$ and $\sin(\theta/2) \to -\sin(\theta/2)$. The spin state acquires an overall minus sign. Only at $4\pi$ — a full turn twice — does the state return to itself. This is the famous "spinors transform under the double cover $SU(2)$ of $SO(3)$" property. You can demonstrate it physically in tabletop experiments (the "Dirac belt trick") but for now keep it as a fact: spin states are not vectors in space; they are objects in $\mathbb{C}^2$ that transform under $SU(2)$.

### 3.2 The Bloch sphere

The parameterization $(\theta, \phi)$ makes the spin state a point on a unit sphere — the **Bloch sphere**:

- North pole ($\theta = 0$): $|\!\uparrow\rangle$.
- South pole ($\theta = \pi$): $|\!\downarrow\rangle$.
- Equator ($\theta = \pi/2$): equal superposition $\frac{1}{\sqrt{2}}(|\!\uparrow\rangle + e^{i\phi} |\!\downarrow\rangle)$, where $\phi$ runs around the equator.

Every two-state quantum system — a spin-1/2 particle, a two-level atom, a single qubit — has its state space the Bloch sphere. This is the picture that connects Chapter 6 to the modern applications in Chapter 13.

### 3.3 The Born rule on the Bloch sphere

Suppose a system is prepared in state $|\psi\rangle$ at Bloch angles $(\theta_\psi, \phi_\psi)$, and you measure $\hat{S}_{\hat{n}}$ along an analyzer axis $\hat{n}$ at Bloch angles $(\theta_n, \phi_n)$. The Born rule gives the probability of outcome $+\hbar/2$:

$$ P(+) = |\langle \hat{n}, + | \psi \rangle|^2. $$

Compute the inner product:

$$ \langle \hat{n}, + | \psi\rangle = \cos(\theta_n/2)\cos(\theta_\psi/2) + e^{i(\phi_\psi - \phi_n)} \sin(\theta_n/2)\sin(\theta_\psi/2). $$

Take the modulus squared and use the identity $\cos^2(\gamma/2) = (1 + \cos\gamma)/2$, where $\gamma$ is the angle on the Bloch sphere between the state vector and the analyzer axis:

$$ \cos\gamma = \cos\theta_\psi \cos\theta_n + \sin\theta_\psi \sin\theta_n \cos(\phi_\psi - \phi_n). $$

The probability collapses to

$$ \boxed{ P(+) = \cos^2(\gamma/2) }, \qquad P(-) = \sin^2(\gamma/2). $$

This is the formula the simulation in §9 animates. Three sanity checks:

- $\gamma = 0$ (analyzer aligned with state): $P(+) = 1$, $P(-) = 0$. Definite outcome.
- $\gamma = \pi$ (anti-aligned): $P(+) = 0$, $P(-) = 1$. Definite, opposite.
- $\gamma = \pi/2$ (perpendicular): $P(+) = P(-) = 1/2$. Maximally uncertain.

Three numbers from one formula, all matching what an experimentalist would call common sense — and all derived, not asserted.

---

## 4. Larmor precession — spin in a magnetic field

### 4.1 The Hamiltonian

The magnetic moment of an electron is $\vec{\mu} = -\gamma \vec{S}$, where $\gamma = g_e (e / 2 m_e)$ is the gyromagnetic ratio and $g_e \approx 2.00232$ is the electron g-factor. (The deviation of $g_e$ from 2 is the famous $(g-2)$ anomaly — Dirac theory predicts $g = 2$ exactly, and QED radiative corrections account for the deviation. The agreement between theory and experiment, currently at parts in $10^{13}$, is one of the most precise tests of any physical theory; see Fan, Myers, Sukra, and Gabrielse 2023, *Physical Review Letters* 130, 071801 [verify].)

The Hamiltonian for a spin in a uniform field $\vec{B} = B_0 \hat{z}$ is

$$ \hat{H} = -\vec{\mu}\cdot\vec{B} = \gamma B_0 \hat{S}_z = \frac{\gamma B_0 \hbar}{2} \sigma_z. $$

This is diagonal in the $\hat{S}_z$ basis with eigenvalues $\pm (\hbar \omega_L / 2)$, where the **Larmor frequency** is

$$ \boxed{ \omega_L = \gamma B_0. } $$

### 4.2 Time evolution

The time-evolution operator is $\hat{U}(t) = e^{-i\hat{H}t/\hbar}$. In the $\hat{S}_z$ basis, $\hat{H}$ is diagonal, so

$$ \hat{U}(t) = \begin{pmatrix} e^{-i\omega_L t/2} & 0 \\ 0 & e^{+i\omega_L t/2} \end{pmatrix}. $$

Take an initial state on the Bloch sphere at angle $\theta_0$ and azimuth $\phi_0 = 0$: $|\psi(0)\rangle = \cos(\theta_0/2)|\!\uparrow\rangle + \sin(\theta_0/2)|\!\downarrow\rangle$. Apply $\hat{U}(t)$:

$$ |\psi(t)\rangle = e^{-i\omega_L t/2}\cos(\theta_0/2)|\!\uparrow\rangle + e^{+i\omega_L t/2}\sin(\theta_0/2)|\!\downarrow\rangle. $$

Factor out the overall phase $e^{-i\omega_L t/2}$ (it has no physical consequence):

$$ |\psi(t)\rangle = \cos(\theta_0/2)|\!\uparrow\rangle + e^{+i\omega_L t}\sin(\theta_0/2)|\!\downarrow\rangle. $$

The polar angle stays fixed at $\theta_0$. The azimuth advances linearly: $\phi(t) = \omega_L t$. The Bloch vector rotates around $\hat{z}$ at angular frequency $\omega_L$.

### 4.3 Expectation values

Compute the expectation values of the spin components in the time-evolved state. The matrix elements of $\sigma_x, \sigma_y$ between $|\!\uparrow\rangle$ and $|\!\downarrow\rangle$ are off-diagonal; carrying out the calculation:

$$ \langle \hat{S}_x \rangle(t) = (\hbar/2)\sin\theta_0 \cos(\omega_L t), $$
$$ \langle \hat{S}_y \rangle(t) = (\hbar/2)\sin\theta_0 \sin(\omega_L t), $$
$$ \langle \hat{S}_z \rangle(t) = (\hbar/2)\cos\theta_0. $$

The vector $(\langle \hat{S}_x \rangle, \langle \hat{S}_y \rangle, \langle \hat{S}_z \rangle)$ has constant magnitude $\hbar/2$ and rotates in the $xy$-plane at frequency $\omega_L$. This is Larmor precession — the same equation you would write for a classical magnetic moment in a field. The expectation values precess classically; the underlying state, of course, is a quantum superposition that is not "the spin pointing in a definite direction." What rotates is the probability distribution over measurement outcomes.

### 4.4 The numbers

Real numbers turn the formula into instruments.

- **Proton in 1 T:** $\gamma_p / (2\pi) \approx 42.58$ MHz/T [verify CODATA]. Larmor period $T = 1/(42.58 \text{ MHz}) \approx 23.5$ ns. This is the resonance frequency exploited in nuclear magnetic resonance.
- **Clinical MRI at 1.5 T:** $f_L = 42.58 \times 1.5 \approx 63.87$ MHz [verify]. Every MRI scanner is tuned to this frequency for hydrogen — the protons in your body's water.
- **Electron in 1 mT:** $\gamma_e / (2\pi) \approx 28.025$ GHz/T [verify]. Larmor period $\approx 35.7$ ns. Electron spin resonance lives in the microwave regime.

These are not decoration. They are why magnetic resonance technology exists.

---

## 5. The sequential Stern–Gerlach experiment

Prepare a beam of silver atoms and send it through an $SG_z$ apparatus. Block the lower output. The surviving beam is in the state $|\!\uparrow\rangle = |\hat{z}, +\rangle$.

Now send that beam through an $SG_x$ apparatus. Express $|\!\uparrow\rangle$ in the $\hat{S}_x$ basis. The eigenstates of $\sigma_x$ are

$$ |\hat{x}, +\rangle = \frac{1}{\sqrt{2}}(|\!\uparrow\rangle + |\!\downarrow\rangle), \qquad |\hat{x}, -\rangle = \frac{1}{\sqrt{2}}(|\!\uparrow\rangle - |\!\downarrow\rangle). $$

Invert:

$$ |\!\uparrow\rangle = \frac{1}{\sqrt{2}}(|\hat{x}, +\rangle + |\hat{x}, -\rangle). $$

By the Born rule, $P(\hat{x}, +) = P(\hat{x}, -) = 1/2$. The beam splits 50/50 at $SG_x$.

Block the $|\hat{x}, -\rangle$ output. The surviving beam is in $|\hat{x}, +\rangle$. Now send *that* through a third apparatus, $SG_z$ again. Invert the relation:

$$ |\hat{x}, +\rangle = \frac{1}{\sqrt{2}}(|\!\uparrow\rangle + |\!\downarrow\rangle). $$

So $P(\hat{z}, +) = P(\hat{z}, -) = 1/2$. The beam splits 50/50 at the third stage — even though we started with a beam that was definitively $|\!\uparrow\rangle$ and never measured $\hat{S}_z$ directly between the two $SG_z$ stages.

The intermediate $SG_x$ measurement "destroyed" the $\hat{S}_z$ information. Here is the lazy way to describe it — "the $SG_x$ device kicked the atom around" — and here is why that description is wrong.

The operators $\hat{S}_x$ and $\hat{S}_z$ do not commute: $[\hat{S}_x, \hat{S}_z] = -i\hbar \hat{S}_y \neq 0$. No state can be a simultaneous eigenstate of both. After $SG_x$, the atom is in $|\hat{x}, +\rangle$, which is a superposition in the $\hat{z}$ basis — there is no "true" $\hat{S}_z$ value being disturbed by clumsy measurement. There is simply no definite $\hat{S}_z$ value to disturb. The 50/50 outcome at the third $SG_z$ is not a measurement artifact; it is the Born rule applied to a state that is not a $\hat{z}$ eigenstate.

This is the moment where students must let go of an implicit classical picture. A naïve "hidden-variable" model would say: each silver atom carries pre-existing values of $\mu_x, \mu_y, \mu_z$, and the analyzers sort by those labels. Such a model could explain the two-spot pattern at any single $SG$ axis. But it would predict that if you sort atoms to have $\mu_z = +\mu_B$ at $SG_1$ and $\mu_x = +\mu_B$ at $SG_2$, the third stage at $SG_z$ should re-find $\mu_z = +\mu_B$ with probability 1 — the labels are stable. Experiment says 50/50. Pre-existing definite labels for non-commuting observables are not consistent with the data.

(Bell-type arguments tighten this: *any* local hidden-variable theory consistent with all measurement outcomes can be ruled out, not just the simplest one. That machinery belongs to Ch. 13.)

---

## 6. Worked example — measuring $\hat{S}_z$ on a state prepared along $\hat{x}$

Take a state prepared in the $\hat{S}_x = +\hbar/2$ eigenstate: $|\psi\rangle = |\hat{x}, +\rangle = \frac{1}{\sqrt{2}}(|\!\uparrow\rangle + |\!\downarrow\rangle)$.

**Question 1:** What is $\langle \hat{S}_z \rangle$?

Using $\hat{S}_z = (\hbar/2)\sigma_z$, $\hat{S}_z |\!\uparrow\rangle = +(\hbar/2)|\!\uparrow\rangle$, $\hat{S}_z |\!\downarrow\rangle = -(\hbar/2)|\!\downarrow\rangle$:

$$ \hat{S}_z |\psi\rangle = \frac{\hbar}{2}\frac{1}{\sqrt{2}}(|\!\uparrow\rangle - |\!\downarrow\rangle). $$

$$ \langle\psi|\hat{S}_z|\psi\rangle = \frac{\hbar}{2}\cdot\frac{1}{2}(1 - 1) = 0. $$

The expectation value is zero — as it must be, by symmetry, for a state pointing along $\hat{x}$.

**Question 2:** What is the probability of measuring $\hat{S}_z = +\hbar/2$?

$P(+) = |\langle\!\uparrow|\psi\rangle|^2 = |1/\sqrt{2}|^2 = 1/2$. Half. Same for $P(-)$.

**Question 3:** What is the uncertainty $\Delta S_z = \sqrt{\langle \hat{S}_z^2 \rangle - \langle \hat{S}_z \rangle^2}$?

$\hat{S}_z^2 = (\hbar/2)^2 I$ (since $\sigma_z^2 = I$), so $\langle \hat{S}_z^2 \rangle = (\hbar/2)^2$ for any state. With $\langle \hat{S}_z\rangle = 0$, $\Delta S_z = \hbar/2$ — maximal. A state with definite $\hat{S}_x$ has maximally uncertain $\hat{S}_z$. This is the spin-version of the position-momentum uncertainty principle, and it follows from the same commutator structure.

---

## 7. Three misconceptions worth confronting

**Misconception 1: "Spin is the particle spinning on its axis."** Killed by the equator-speed-greater-than-$c$ calculation in §2.3. The picture is wrong by orders of magnitude, not by a small approximation. Spin is an internal degree of freedom that transforms as a representation of $SU(2)$ — full stop.

**Misconception 2: "Measuring one component of spin disturbs the others by the action of the measuring device."** Tempting language; wrong physics. The disturbance reading imports a classical picture where the system "had" a value all along. The cleaner statement: non-commuting observables cannot have simultaneous definite values. Measuring $\hat{S}_x$ projects the state into an $\hat{S}_x$ eigenstate; that state is a superposition in the $\hat{S}_z$ basis; a subsequent $\hat{S}_z$ measurement is probabilistic. No disturbance is needed — the previous state simply did not have a definite $\hat{S}_z$ to disturb.

**Misconception 3: "The electron g-factor is exactly 2, and the Dirac equation predicts this."** Half right. Dirac's equation predicts $g = 2$ exactly at tree level. Experiment finds $g_e \approx 2.00232$. The deviation, $a_e = (g-2)/2 \approx 0.00116$, is *not* a problem with Dirac — it is the QED radiative correction from virtual photons dressing the bare electron. The agreement between QED theory and experiment for $a_e$ extends to 13 significant figures [verify]. The deviation is a feature, not a bug.

---

## 8. Synthesis — what you can now do

Spin is the chapter where quantum mechanics stops imitating classical intuition and walks somewhere new. You now have:

- A two-dimensional complex Hilbert space whose unit vectors are spin states.
- Three Hermitian operators (the Pauli matrices, scaled by $\hbar/2$) representing components of spin along orthogonal axes.
- A way to specify spin along any direction $\hat{n}$ — the half-angle parameterization $|\hat{n}, +\rangle = \cos(\theta/2)|\!\uparrow\rangle + e^{i\phi}\sin(\theta/2)|\!\downarrow\rangle$ — and a geometric picture of the state space (the Bloch sphere).
- A Born-rule formula for measurement outcome probabilities along any analyzer axis: $P(+) = \cos^2(\gamma/2)$, where $\gamma$ is the angle between the state and the analyzer on the Bloch sphere.
- A solution of the time-dependent Schrödinger equation for a spin in a uniform field: Larmor precession at $\omega_L = \gamma B$.
- An honest account of why sequential Stern–Gerlach measurements give the outcomes they do, with the "measurement disturbance" framing replaced by the structural fact that $[\hat{S}_x, \hat{S}_z] \neq 0$.

The Stern–Gerlach pattern from 1922 is no longer a puzzle. The empirical fact — two spots, always, with angle-dependent probabilities — falls out of a two-state Hilbert space and the operator algebra. The deeper question — *why* nature put each fundamental particle into either the bosonic or fermionic family — is the spin-statistics theorem, which requires relativistic QFT to prove (Pauli 1940, *Physical Review* 58, 716 [verify]). For now, accept it: integer spin → bosons, half-integer → fermions. We will use this fact in Chapter 8.

**Connection forward.** Chapter 7 will introduce spin as the fourth quantum number $m_s = \pm 1/2$ in the hydrogen atom. The factor of 2 in the $2n^2$ degeneracy and the entire electron count of the periodic table both depend on the two-state structure you just built.

---

## 9. LLM Exercise — Building the Stern–Gerlach Simulator

You are going to build a working interactive simulation that visualizes everything in this chapter: drag a state arrow on the Bloch sphere, drag an analyzer axis, watch the Stern–Gerlach beam split with correct probabilities, and turn on a magnetic field to see Larmor precession in real time.

### 9.1 The CLAUDE.md prompt — extending the coding constitution

Open your project's `CLAUDE.md` (from Chapter 0) and append this block:

```
## Chapter 6 — Stern–Gerlach Simulator Rules

- Single HTML file, single SVG canvas, no external assets.
- Three coupled panels stacked vertically inside the SVG:
  (1) Bloch sphere view (top, ~360 × 360 px),
  (2) Stern–Gerlach apparatus side view (middle, ~600 × 200 px),
  (3) Larmor precession panel + control sidebar (bottom + side).
- D3 v7 only. No three.js, no WebGL.
- Parameter sliders live in a right-hand sidebar; never inside the SVG.
- Numeric readouts: monospaced font, ≤ 3 significant figures, no animation
  on number changes.
- All probability arithmetic uses the half-angle Born rule:
  P(+) = cos²(γ/2), with γ = angle between state and analyzer Bloch vectors.
- The state and analyzer are dragged on the Bloch sphere by mouse.
- Larmor precession increments φ_state by ω_L · dt each animation frame,
  with ω_L = γ · B₀ and γ chosen by a particle-species dropdown
  (electron, proton).
- All redraws go through a single redraw() function. No DOM mutation outside.
```

### 9.2 The simulation prompt — four-move structure

Paste the following into Claude:

```
Build me a D3 v7 Stern–Gerlach simulator following CLAUDE.md.

HOOK. Render the 1922 Stern–Gerlach experiment in one HTML page,
but let the user rotate the analyzer.

UNFOLD. The spin state is a unit vector on the Bloch sphere at
(θ_ψ, φ_ψ). The analyzer is a unit vector at (θ_n, φ_n). The Born-rule
probability of outcome +ℏ/2 is P(+) = cos²(γ/2), where
cos γ = cos θ_ψ cos θ_n + sin θ_ψ sin θ_n cos(φ_ψ − φ_n).

MECHANISM. Three panels.
  (1) Bloch sphere: isometric projection of latitude/longitude lines, with
      two draggable arrows — one for the state |ψ⟩ (blue), one for the
      analyzer axis n̂ (orange). Numeric readouts of (θ_ψ, φ_ψ) and (θ_n, φ_n).
  (2) Stern–Gerlach apparatus: beam enters from the left, encounters the
      magnet, splits into upper and lower trajectories. Stroke widths of
      the two output beams are proportional to P(+) = cos²(γ/2) and
      P(−) = sin²(γ/2). A bar chart at the right shows the same probabilities
      numerically.
  (3) Larmor precession panel: when a B-field slider is nonzero, the state
      arrow on the Bloch sphere precesses around ẑ at ω_L = γ · B₀, with
      γ set by a particle dropdown (electron γ_e/2π = 28.025 GHz/T,
      proton γ_p/2π = 42.58 MHz/T). A digital readout shows ω_L/(2π) in
      Hz, kHz, MHz, or GHz as appropriate.

SYNTHESIZE. Add a "Sequential SG mode" toggle. When on, render a second
SG apparatus downstream of the first. The user picks which branch from
SG₁ survives (+ or −) and sets the SG₂ axis independently. Show
conditional probabilities P(SG₂=+ | SG₁=+) and P(SG₂=− | SG₁=+).

Output a single self-contained HTML file. No external dependencies except
the D3 v7 CDN. The file should be runnable by saving and double-clicking.
```

### 9.3 Exploration tasks

Once your simulation is working, do these in order. Each is a small experiment that builds your intuition.

1. **Verify the antipode.** Set the state to $\theta_\psi = 0$ (north pole, $|\!\uparrow\rangle$). Set the analyzer to $\theta_n = 0$. Read $P(+)$ — it should be $1.00$. Now rotate the analyzer to $\theta_n = \pi$. Read $P(+)$ — it should be $0.00$. The probability is continuous; rotate the analyzer to $\theta_n = \pi/3$ and predict $P(+) = \cos^2(\pi/6) = 3/4$. Check against the readout.

2. **Verify the half-angle.** Set $\theta_\psi = \pi/2$ (the state lies on the equator). The Bloch-sphere half of the formula says this state is $(|\!\uparrow\rangle + |\!\downarrow\rangle)/\sqrt{2}$. Confirm by checking that for analyzer $\theta_n = 0$ (the $\hat{z}$-axis), $P(+) = 1/2$. Verify the prediction at three other angles.

3. **Larmor period.** Turn on the B-field. Set the particle species to "proton" and $B_0 = 1$ T. Read off the precession period from the on-screen timer. Confirm it equals $1/(42.58 \text{ MHz}) \approx 23.5$ ns. Now set $B_0 = 0.5$ T. Confirm the period doubles. Confirm $\omega_L \propto B$ by plotting period vs. $1/B$ for three field strengths.

4. **The sequential SG headline.** Turn on Sequential SG mode. Prepare the initial state as $|\!\uparrow\rangle$. Set $SG_1$ along $\hat{z}$. Keep only the $+$ branch. Set $SG_2$ along $\hat{x}$ — confirm the $SG_2$ outcome is 50/50. Keep the $+$ branch of $SG_2$. Mentally chain a third (you can chain stages by re-using $SG_2$ along $\hat{z}$). Confirm the outcome is 50/50 — the original "definitely up along $\hat{z}$" state has been re-randomized by the intermediate $\hat{x}$ measurement.

5. **The misconception trap.** Predict, before running: if you remove the intermediate $SG_x$ (so you go $SG_z \to SG_z$ with both stages along $\hat{z}$), what do you expect at the second $SG_z$? Now configure the simulation to do this and verify. The contrast with task 4 is the empirical signature of measurement incompatibility.

### 9.4 Extension prompt — Monte Carlo mode

The simulation above shows continuous *probabilities*. A real Stern–Gerlach experiment fires one atom at a time, each going into one branch or the other. The $\cos^2(\gamma/2)$ law emerges as a frequency over many atoms. Add this layer:

```
Extend the Stern–Gerlach simulator to include a Monte Carlo mode.

When the user clicks "Fire atom," generate a uniform random number u in [0, 1].
If u < P(+), the atom goes up; else it goes down. Animate the atom traveling
through the SG apparatus and landing on one of the two output collectors.

Maintain running tallies n_+ and n_- of the two outcomes. Display the
empirical frequencies n_+ / (n_+ + n_-) and n_- / (n_+ + n_-) alongside
the theoretical probabilities P(+) and P(-).

Add a "Fire 1000" button that fires 1000 atoms in rapid succession (with
shortened animation per atom) and shows the running frequencies converging
toward the theoretical values. Plot a small histogram of the running
deviation |empirical − theoretical| against atom number.
```

Run the extension. Watch the empirical frequencies wander before settling within a few percent of the theoretical value after ~100 atoms, and within fractions of a percent after ~1000. This is the empirical foundation of the Born rule: probabilities are predictions about frequencies in long runs of identically prepared systems, not about any single atom.

### 9.5 Six failure modes to watch for

When your simulation misbehaves, the bug is usually in one of these places. Check them in order:

1. **Half-angle dropped.** If $|\hat{x}, +\rangle$ comes out as $\cos(\pi/2)|\!\uparrow\rangle + \sin(\pi/2)|\!\downarrow\rangle = |\!\downarrow\rangle$, you forgot the half in $\cos(\theta/2)$. The state along $+\hat{x}$ should have *equal* weights, not all weight on $|\!\downarrow\rangle$.
2. **$\gamma$ formula wrong.** Some students compute $\gamma$ as the angle between the state vector and analyzer in 3D space, but use the *full* angle in $\cos^2\gamma$ instead of $\cos^2(\gamma/2)$. Easy to spot: at $\gamma = \pi/2$ you'll get $P(+) = 0$ instead of $1/2$.
3. **Larmor frequency in wrong units.** $\gamma_p/(2\pi) = 42.58$ MHz/T means $\omega_L = 2\pi \times 42.58 \times 10^6 \times B_0$ rad/s. If the precession looks $2\pi$ times too slow, you used $\gamma_p$ instead of $2\pi \gamma_p$ in the angular frequency.
4. **Sign of the precession direction.** A positively charged proton's magnetic moment is along its spin; for an electron it is opposite. The two species precess in opposite senses for a given field. If both look the same in your simulation, check the sign of $\gamma$.
5. **State drifts during animation.** If the polar angle $\theta_\psi$ wanders during Larmor precession, your time-evolution operator is wrong — only $\phi$ should advance. Verify $\langle \hat{S}_z \rangle$ is constant in time.
6. **Probability normalization fails.** Check that $P(+) + P(-) = 1$ to within floating-point tolerance for every analyzer setting. If it's off by more than $10^{-9}$, you have an arithmetic bug.

When you can drag the state to any point on the Bloch sphere, rotate the analyzer freely, watch the beam widths update continuously, and toggle on Larmor precession to see the state drift around $\hat{z}$ — at that moment the formalism of this chapter is no longer in the page. It is on your screen, in your hands.

---

**What would change my mind:** a demonstration that some particle species in 3+1 dimensions does not fall cleanly into either the integer-spin/boson or half-integer-spin/fermion family, contradicting the spin-statistics theorem within experimental precision.

**Still puzzling:** I can tell you what spin algebra does and how to compute every observable consequence; I cannot tell you, at the level of an undergraduate course, *why* the universe contains a $\mathbb{C}^2$ degree of freedom that transforms as a fundamental representation of $SU(2)$. The Dirac derivation answers this from "be Lorentz-invariant"; that answer pushes the question one layer deeper without dissolving it.

**Tags:** spin-1/2, Pauli matrices, Stern–Gerlach experiment, Bloch sphere, Larmor precession, sequential measurement, $SU(2)$, quantum measurement, D3.js, Born rule
