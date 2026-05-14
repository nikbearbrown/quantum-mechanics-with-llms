# Chapter 6 — Spin
*Two Spots, No Explanation, Three Years.*

An angular momentum with no classical analog: the two-state Hilbert space, the Pauli matrices, and the experiment that found something quantum theory hadn't yet imagined.


In February 1922, Otto Stern and Walther Gerlach sent a beam of neutral silver atoms through an inhomogeneous magnetic field and caught them on a glass plate. The field exerts a force on any magnetic moment — the gradient of $\vec{\mu}\cdot\vec{B}$ — and atoms with different moment orientations should deflect by different amounts. Classical physics says the magnetic moments can point in any direction, so the plate should show a continuous smear of silver. Stern developed the plate. He found two spots.
Not a smear. Two distinct spots. One above, one below. Nothing in between.
Whatever silver atoms are doing, the component of their magnetic moment along the field axis takes exactly two values, never three, never a continuum. And this turns out to be true for any axis you point: two spots, always. The experiment is unambiguous and strange, and it sat unexplained for three years.
Here is what makes the story more interesting: Stern and Gerlach in 1922 did not know what they had found. They believed they were confirming the old Bohr–Sommerfeld "space quantization" of orbital angular momentum. Silver has the electron configuration $[\text{Kr}]\,4d^{10}5s^1$, with a single valence electron in an $s$ orbital. An $s$ orbital has zero orbital angular momentum — $\ell = 0$ — so it contributes nothing to the magnetic moment. The two spots came from something nobody had proposed yet: the intrinsic spin of the electron, hypothesized by Uhlenbeck and Goudsmit in 1925. Stern and Gerlach got the right answer before the right question had been asked.
I find this worth saying honestly, because it is how physics often goes. The experiment was right. The interpretation waited for a new concept.
This chapter builds that concept.

<!-- → [IMAGE: reproduction of the original 1922 Stern–Gerlach glass plate photograph alongside a schematic of the apparatus — magnet poles top and bottom, silver beam entering horizontally, two discrete impact spots visible on the plate; caption: "The original result: two spots where classical physics predicts a continuous smear. The image should make viscerally clear that the split is discrete, not broadened"] -->

## Two values means two dimensions
The empirical fact — always two values, any axis — points directly to the Hilbert space. Whatever spin lives in, that space must be such that any spin-component operator has exactly two eigenvalues. The smallest complex vector space that supports this is $\mathbb{C}^2$, two-dimensional and complex. This is not a guess; it is the minimal structure forced by "two and only two."
Choose the eigenstates of the $z$-component of spin as the basis:
$$|\!\uparrow\rangle = \begin{pmatrix}1\\0\end{pmatrix}, \qquad |\!\downarrow\rangle = \begin{pmatrix}0\\1\end{pmatrix}.$$
Any normalized spin state is a linear combination of these:
$$|\psi\rangle = \alpha|\!\uparrow\rangle + \beta|\!\downarrow\rangle, \qquad |\alpha|^2 + |\beta|^2 = 1.$$
Two complex numbers, one normalization constraint, one overall phase that is unobservable: two real degrees of freedom. That is the dimension of a sphere. We will come back to the sphere.
The spin operators are $\hat{S}_i = (\hbar/2)\sigma_i$, where $\sigma_x, \sigma_y, \sigma_z$ are the Pauli matrices:
$$\sigma_x = \begin{pmatrix}0&1\\1&0\end{pmatrix}, \qquad \sigma_y = \begin{pmatrix}0&-i\\i&0\end{pmatrix}, \qquad \sigma_z = \begin{pmatrix}1&0\\0&-1\end{pmatrix}.$$
Four facts about these matrices, all verifiable by direct multiplication. The computation is mechanical but the facts are structural — they recur everywhere from NMR pulse sequences to qubit gates to the Feynman rules of QED.

$\sigma_i^2 = I$ for each $i$. Check: $\sigma_x^2 = \bigl(\begin{smallmatrix}0&1\\1&0\end{smallmatrix}\bigr)^2 = \bigl(\begin{smallmatrix}1&0\\0&1\end{smallmatrix}\bigr)$. ✓

$\mathrm{Tr}(\sigma_i) = 0$ for each $i$. Read off the diagonals.

Different Pauli matrices anticommute: $\sigma_i\sigma_j + \sigma_j\sigma_i = 0$ for $i \neq j$. Compute $\sigma_x\sigma_y = \bigl(\begin{smallmatrix}i&0\\0&-i\end{smallmatrix}\bigr)$ and $\sigma_y\sigma_x = \bigl(\begin{smallmatrix}-i&0\\0&i\end{smallmatrix}\bigr)$; they sum to zero.

They satisfy the angular-momentum commutation relations: $[\sigma_i, \sigma_j] = 2i\epsilon_{ijk}\sigma_k$. From the calculation above, $[\sigma_x, \sigma_y] = \sigma_x\sigma_y - \sigma_y\sigma_x = 2i\sigma_z$. Which means $[\hat{S}_i, \hat{S}_j] = i\hbar\epsilon_{ijk}\hat{S}_k$ — the same algebra you derived for orbital angular momentum $\hat{L}$ in Chapter 5. That algebraic coincidence is not an accident. It is the reason "spin" deserves to be called angular momentum.

The four facts combine into one multiplication table: $\sigma_i\sigma_j = \delta_{ij}I + i\epsilon_{ijk}\sigma_k$. This single identity is the entire Pauli algebra. Memorize it.

<!-- → [TABLE: Pauli multiplication table — 3×3 grid with rows and columns labeled σ_x, σ_y, σ_z; each cell shows the product σ_i σ_j as either I (diagonal), +iσ_k, or −iσ_k (off-diagonal, with signs following the right-hand rule); footer row: "σ_i² = I for all i; σ_i σ_j = −σ_j σ_i for i≠j"; caption: "The entire Pauli algebra in one table. Every NMR calculation, qubit gate, and Feynman rule involving spin reduces to entries here"] -->

## Why spin is not rotation
Many students arrive with a picture: the electron is a tiny ball physically rotating on its own axis, and "spin" names that rotation's angular momentum. Let us kill this picture now with a number, not a hand-wave.
Assume the electron has angular momentum $\hbar/2$ and the "spinning ball" picture is true. We need a radius to work with. Use the most generous possible estimate — the classical electron radius:
$$r_e = \frac{e^2}{4\pi\epsilon_0 m_e c^2} \approx 2.82 \times 10^{-15}\ \text{m},$$
defined by setting the electrostatic self-energy equal to $m_e c^2$. Real experiment bounds the electron's actual size below $10^{-18}$ m, but we want the most generous radius, since a smaller one makes the picture fail worse.
The moment of inertia of a uniform solid sphere is $I = \frac{2}{5}m_e r_e^2$, and $L = I\omega$, so the equatorial surface speed is $v = \omega r_e = L r_e/I = 5\hbar/(4m_e r_e)$:
$$v = \frac{5 \times 1.055 \times 10^{-34}}{4 \times 9.11 \times 10^{-31} \times 2.82 \times 10^{-15}} \approx 5.1 \times 10^{10}\ \text{m/s}.$$
The speed of light is $c \approx 3.0 \times 10^8$ m/s. The required equatorial speed is roughly $170c$. The picture is not wrong by a small margin. It is wrong by more than two orders of magnitude, and using a smaller, more realistic electron radius makes it worse.

<!-- → [CHART: log-scale bar chart comparing v_equator to c for three assumed electron radii — classical electron radius r_e ≈ 2.82×10⁻¹⁵ m (gives ~170c), experimental upper bound r < 10⁻¹⁸ m (gives ~5×10⁴ c), proton radius r_p ≈ 0.85×10⁻¹⁵ m (gives ~630c); horizontal dashed line at v = c labeled "speed of light"; caption: "The spinning-ball picture requires superluminal surface speeds at every plausible electron radius. Smaller radii make it worse, not better"] -->

So what is spin? An internal degree of freedom that transforms as a representation of $\mathrm{SU}(2)$ — the group of $2\times2$ unitary matrices with determinant 1 — under rotations. It is not any motion in physical space. It is a label the electron carries, a label that takes two values when you measure it, that obeys the angular-momentum operator algebra, and that has no classical analog. Paul Dirac derived spin-1/2 in 1928 from the requirement that the wave equation be Lorentz-covariant and first-order in time: spin falls out of relativity plus quantum mechanics. You do not put it in by hand; you find it already there when you insist on the right symmetries.
"Spin is intrinsic angular momentum" is true but incomplete unless you say what *intrinsic* means. Intrinsic means: the algebra is that of angular momentum, the carrier is an $\mathrm{SU}(2)$ representation, and the underlying degree of freedom does not correspond to any motion in physical space.

## Spin along any axis — the Bloch sphere
Pick a unit vector $\hat{n} = (\sin\theta\cos\phi, \sin\theta\sin\phi, \cos\theta)$. The spin operator along $\hat{n}$ is
$$\hat{S}_{\hat{n}} = \frac{\hbar}{2}\hat{n}\cdot\vec{\sigma} = \frac{\hbar}{2}\begin{pmatrix}\cos\theta & \sin\theta\,e^{-i\phi}\\\sin\theta\,e^{i\phi} & -\cos\theta\end{pmatrix}.$$
The eigenvalues: the matrix has trace zero and determinant $-1$, so the characteristic polynomial is $\lambda^2 - 1 = 0$, giving $\lambda = \pm 1$. The eigenvalues of $\hat{S}_{\hat{n}}$ are $\pm\hbar/2$. For every axis you point, two values. The formalism delivers what the 1922 experiment found.
The eigenvectors require more work. Solving $(\hat{n}\cdot\vec{\sigma})|\hat{n},+\rangle = +|\hat{n},+\rangle$ using the half-angle identities $1 - \cos\theta = 2\sin^2(\theta/2)$ and $\sin\theta = 2\sin(\theta/2)\cos(\theta/2)$, the normalized result is
$$|\hat{n},+\rangle = \cos(\theta/2)|\!\uparrow\rangle + e^{i\phi}\sin(\theta/2)|\!\downarrow\rangle.$$
The orthogonal eigenstate is $|\hat{n},-\rangle = \sin(\theta/2)|\!\uparrow\rangle - e^{i\phi}\cos(\theta/2)|\!\downarrow\rangle$.
Notice the half-angle. A spin pointing along $+\hat{x}$ is $\theta = \pi/2$, $\phi = 0$, so $|\hat{x},+\rangle = (|\!\uparrow\rangle + |\!\downarrow\rangle)/\sqrt{2}$ — equal weights on $|\!\uparrow\rangle$ and $|\!\downarrow\rangle$. This is right: a spin definitely pointing along $\hat{x}$ should give 50/50 when measured along $\hat{z}$. Check it as a Born rule calculation and you get exactly that.
The half-angle has a deeper consequence. Rotate the analyzer by $2\pi$ — a full turn in physical space. The angle $\theta$ goes to $\theta + 2\pi$, and $\cos(\theta/2)$ goes to $\cos(\theta/2 + \pi) = -\cos(\theta/2)$; similarly for the sine. The spin state acquires an overall minus sign. Only at $4\pi$ — two full turns — does the state return to itself. This is the spinor double cover: spin states live in $\mathrm{SU}(2)$, not in the ordinary rotation group $\mathrm{SO}(3)$. A $2\pi$ rotation that takes every vector in space back to itself takes a spinor to its negative. This is observable in interference experiments and in the "Dirac belt trick."
The parameterization $(\theta, \phi)$ maps every pure spin state to a point on a unit sphere — the Bloch sphere. North pole: $|\!\uparrow\rangle$. South pole: $|\!\downarrow\rangle$. Equator: equal superpositions $(|\!\uparrow\rangle + e^{i\phi}|\!\downarrow\rangle)/\sqrt{2}$, with $\phi$ varying around the equator. Every point on the sphere is a spin state; every spin state is a point on the sphere.
Now the Born rule takes a clean geometric form. Suppose the state is at Bloch angles $(\theta_\psi, \phi_\psi)$ and the analyzer points at $(\theta_n, \phi_n)$. Let $\gamma$ be the angle between the two unit vectors on the Bloch sphere:
$$\cos\gamma = \cos\theta_\psi\cos\theta_n + \sin\theta_\psi\sin\theta_n\cos(\phi_\psi - \phi_n).$$
The probability of outcome $+\hbar/2$ is
$$P(+) = \cos^2(\gamma/2), \qquad P(-) = \sin^2(\gamma/2).$$
Three checks. State aligned with analyzer ($\gamma = 0$): $P(+) = 1$. Anti-aligned ($\gamma = \pi$): $P(+) = 0$. Perpendicular ($\gamma = \pi/2$): $P(+) = 1/2$. Three correct limits from one formula.

<!-- → [IMAGE: Bloch sphere diagram annotated for the Born-rule geometry — a unit sphere with labeled north pole |↑⟩, south pole |↓⟩, and equatorial ring; two arrows from the origin: a blue arrow to a state point (θ_ψ, φ_ψ) and an orange arrow to an analyzer point (θ_n, φ_n); the angle γ between them labeled on the sphere surface; a small inset shows the P(+) = cos²(γ/2) curve plotted against γ from 0 to π, with the three sanity-check values marked; caption: "The Born rule on the Bloch sphere: probability depends only on the angle γ between state and analyzer, not on their absolute positions"] -->

## Spin in a magnetic field — Larmor precession
A spin in a uniform magnetic field $\vec{B} = B_0\hat{z}$ has Hamiltonian
$$\hat{H} = -\vec{\mu}\cdot\vec{B} = \gamma B_0\hat{S}_z = \frac{\gamma B_0\hbar}{2}\sigma_z,$$
where $\gamma$ is the gyromagnetic ratio — $\gamma_e/2\pi \approx 28.025$ GHz/T for the electron, $\gamma_p/2\pi \approx 42.58$ MHz/T for the proton.
The Hamiltonian is diagonal in the $\hat{S}_z$ basis. The time-evolution operator is therefore diagonal too:
$$\hat{U}(t) = \begin{pmatrix}e^{-i\omega_L t/2}&0\\0&e^{+i\omega_L t/2}\end{pmatrix},$$
where $\omega_L = \gamma B_0$ is the Larmor frequency. Starting from a general state at polar angle $\theta_0$ and azimuth $\phi_0 = 0$:
$$|\psi(t)\rangle = \cos(\theta_0/2)|\!\uparrow\rangle + e^{i\omega_L t}\sin(\theta_0/2)|\!\downarrow\rangle.$$
The polar angle $\theta_0$ does not change. The azimuth advances at rate $\omega_L$: $\phi(t) = \omega_L t$. On the Bloch sphere, the state precesses around the $\hat{z}$-axis at the Larmor frequency. The expectation values follow:
$$\langle\hat{S}_x\rangle(t) = \frac{\hbar}{2}\sin\theta_0\cos(\omega_L t), \qquad \langle\hat{S}_y\rangle(t) = \frac{\hbar}{2}\sin\theta_0\sin(\omega_L t), \qquad \langle\hat{S}_z\rangle(t) = \frac{\hbar}{2}\cos\theta_0.$$
The vector $(\langle\hat{S}_x\rangle, \langle\hat{S}_y\rangle, \langle\hat{S}_z\rangle)$ has constant magnitude $\hbar/2$ and rotates in the $xy$-plane. This is Larmor precession — formally identical to the precession of a classical magnetic moment, except that the underlying object is a quantum superposition, not a vector in space. What precesses is the probability distribution over outcomes, not any physical pointer.
The numbers make this real. A proton in a 1 T field has $\omega_L/(2\pi) \approx 42.58$ MHz, so a period of about 23.5 ns. This is the resonance frequency exploited in nuclear magnetic resonance: every MRI scanner operating on hydrogen is tuned to this frequency times the field strength. The formula $\omega_L = \gamma B_0$ is not textbook background; it is the operating equation of a medical instrument.

<!-- → [TABLE: Larmor frequencies for different particles and field strengths — rows: electron at 1 mT, proton at 0.5 T (low-field MRI), proton at 1.5 T (clinical MRI), proton at 3 T (research MRI), proton at 7 T (ultra-high field); columns: particle, B₀ (T), γ/(2π) (MHz/T or GHz/T), f_L = ω_L/(2π), T_L = 1/f_L; caption: "Every MRI scanner is a Larmor precession detector. The operating frequency is set by ω_L = γB₀ for hydrogen protons in the applied field"] -->

<!-- → [IMAGE: Bloch sphere showing Larmor precession — a spin state arrow at polar angle θ₀ from the north pole, tracing a circular path around the ẑ axis; dashed circle shows the precession cone; labels: θ₀ (tilt angle, unchanged), φ(t) = ω_L t (advancing azimuth), ω_L (precession rate arrow curving around ẑ); caption: "Larmor precession: θ₀ is frozen, φ advances at ω_L = γB₀. The state traces a latitude circle on the Bloch sphere"] -->

## What the sequential experiment is really telling you
Prepare a beam of silver atoms and send it through an $\mathrm{SG}_z$ apparatus. Block the lower output. The surviving atoms are in state $|\!\uparrow\rangle$.
Send that beam through an $\mathrm{SG}_x$ apparatus. The $\hat{S}_x$ eigenstates are $|\hat{x},\pm\rangle = (|\!\uparrow\rangle \pm |\!\downarrow\rangle)/\sqrt{2}$, so $|\!\uparrow\rangle = (|\hat{x},+\rangle + |\hat{x},-\rangle)/\sqrt{2}$. Born rule gives $P(\hat{x},+) = P(\hat{x},-) = 1/2$. The beam splits equally.
Block the $|\hat{x},-\rangle$ output. The surviving atoms are in $|\hat{x},+\rangle = (|\!\uparrow\rangle + |\!\downarrow\rangle)/\sqrt{2}$. Now send them through a second $\mathrm{SG}_z$. Express $|\hat{x},+\rangle$ in the $\hat{z}$ basis: it is already written as an equal superposition of $|\!\uparrow\rangle$ and $|\!\downarrow\rangle$. Born rule: $P(\hat{z},+) = P(\hat{z},-) = 1/2$. The beam splits equally again.
The atoms started definitively spin-up along $\hat{z}$. After an intermediate $\hat{x}$ measurement, they are 50/50 along $\hat{z}$ again. The tempting description is: the $\mathrm{SG}_x$ device disturbed the atoms, scrambling their $z$-component. This is the wrong picture, and it matters to get it right.
The operators $\hat{S}_x$ and $\hat{S}_z$ do not commute: $[\hat{S}_x, \hat{S}_z] = -i\hbar\hat{S}_y \neq 0$. No state can be simultaneously an eigenstate of both. After the $\mathrm{SG}_x$ measurement selects $|\hat{x},+\rangle$, that state is not an eigenstate of $\hat{S}_z$ — it has no definite $\hat{z}$ value, not a definite value that was obscured by a clumsy apparatus. There is nothing there to disturb. The 50/50 outcome at the third stage is the Born rule applied to a state that simply does not have a definite $\hat{S}_z$. The noncommutativity of the operators is structural, not a measurement artifact.
Here is the sharpest way to see this. A naive picture where each silver atom carries pre-existing definite values $(\mu_x, \mu_y, \mu_z)$ — labels that the SG apparatuses read off without disturbing — would predict that selecting $\mu_z = +\mu_B$ at stage one and then $\mu_x = +\mu_B$ at stage two should leave $\mu_z$ unchanged: the labels are stable. So stage three should return $\mu_z = +\mu_B$ with probability 1. Experiment gives 50/50. Pre-existing definite values for non-commuting observables are not consistent with the data.
This is the point where students have to let go of the hidden-variable picture. The spin component along $\hat{z}$ does not exist as a pre-existing property when the system is prepared in a $\hat{x}$ eigenstate. It comes into being at the moment of the measurement. The algebra forces this.

<!-- → [INFOGRAPHIC: three-stage sequential SG diagram — left: beam enters SG_z, splits to |↑⟩ (upper, kept) and |↓⟩ (lower, blocked); center: |↑⟩ beam enters SG_x, splits 50/50 to |x,+⟩ (kept) and |x,−⟩ (blocked); right: |x,+⟩ beam enters SG_z again, splits 50/50; below, a contrast diagram showing SG_z → SG_z with no intermediate stage, where the second SG_z gives P(+)=1; caption: "The intermediate SG_x measurement does not disturb a pre-existing z-value. It produces a state that has no definite z-value. The 50/50 outcome is structural, not accidental"] -->

## The g-factor, and what "exactly 2" actually means
Before leaving spin, one number deserves attention. The Hamiltonian $\hat{H} = -\vec{\mu}\cdot\vec{B}$ used the magnetic moment $\vec{\mu} = -\gamma\vec{S}$ with $\gamma = g_e(e/2m_e)$. The Dirac equation predicts $g_e = 2$ exactly. The measured value is
$$g_e \approx 2.00232.$$
The deviation $a_e = (g_e - 2)/2 \approx 0.00116$ is not a failure of Dirac. It is the QED radiative correction from virtual photons dressing the bare electron — the leading term is $a_e \approx \alpha/(2\pi)$, where $\alpha \approx 1/137$ is the fine-structure constant. The agreement between QED theory and experiment extends to 13 significant figures, making it one of the most precisely tested predictions in all of physics. The deviation is a feature, not a bug.
The relevant lesson here is smaller: when we write $\hat{H} = \gamma B_0\hat{S}_z$, we use the experimental $\gamma$, which includes the anomalous correction. For most of what follows in the course, this distinction does not matter. But it is worth knowing that "spin" already pointed beyond Dirac before Dirac had finished writing the paper.

<!-- → [INFOGRAPHIC: conceptual diagram showing the layered structure of the electron g-factor — three horizontal bands labeled "Classical expectation: g = 1 (orbital analogy)", "Dirac equation prediction: g = 2 (relativistic QM)", "QED correction: g ≈ 2.00232 (virtual photon loops)"; each band has a brief annotation: the Dirac result as the baseline, the deviation a_e = (g−2)/2 ≈ α/(2π) with a small Feynman diagram icon of a vertex correction; caption: "The anomalous magnetic moment a_e is not an error. It is a precision test: QED and experiment agree to 13 significant figures"] -->

## What you now have
The 1922 experiment found two spots because silver has one unpaired spin-1/2 electron, and that electron lives in a two-dimensional complex Hilbert space. The formalism built in this chapter — the Pauli matrices, the half-angle eigenstates, the Bloch sphere, the Larmor precession, the Born-rule formula $P(+) = \cos^2(\gamma/2)$ — is the complete machinery for any spin-1/2 system. The same machinery governs the NMR resonances used in MRI, the qubit states used in quantum computers, and the photon polarization states used in quantum cryptography. The chapter is not about a specialized subject. It is about the simplest non-trivial quantum system, and that system is everywhere.
The deeper question — why nature puts each fundamental particle into either the bosonic or fermionic family, with integer or half-integer spin respectively — is the spin-statistics theorem. Its proof requires relativistic quantum field theory. Accept it as a fact for now: half-integer spin means fermions, integer spin means bosons. Chapter 8 will use this when it counts the states available to electrons in an atom.

## Exercises

### Warm-up

**6.1** Write down the three Pauli matrices from memory. Verify, by direct matrix multiplication, that (a) $\sigma_x^2 = I$; (b) $\sigma_x\sigma_y = i\sigma_z$; (c) $\sigma_x\sigma_y + \sigma_y\sigma_x = 0$. State which of these verifies the anticommutation relation and which verifies the commutation relation. *(Tests: can reproduce the Pauli matrices and execute the four algebraic facts by direct computation)*

**6.2** The chapter refutes the spinning-ball picture by calculating the required equatorial speed. Redo the calculation for a proton ($m_p = 1.673 \times 10^{-27}$ kg) with spin $\hbar/2$ and radius equal to the measured proton charge radius $r_p \approx 0.85 \times 10^{-15}$ m. Use $I = \frac{2}{5}m_p r_p^2$. Express the result as a multiple of $c$ and compare to the electron case. What does the comparison tell you about whether the argument is specific to the electron? *(Tests: can execute the angular-momentum estimate for a different particle; can generalize the refutation)*

**6.3** For the state $|\hat{x},+\rangle = (|\!\uparrow\rangle + |\!\downarrow\rangle)/\sqrt{2}$, compute: (a) the probability of measuring $\hat{S}_z = +\hbar/2$; (b) $\langle\hat{S}_z\rangle$; (c) $\langle\hat{S}_z^2\rangle$; (d) $\Delta S_z = \sqrt{\langle\hat{S}_z^2\rangle - \langle\hat{S}_z\rangle^2}$. Verify that $\Delta S_z = \hbar/2$ — maximal uncertainty. *(Tests: can apply the Born rule and compute expectation values in a two-state system; understands what maximal uncertainty means)*

### Application

**6.4** A spin is prepared in the state $|\psi\rangle = \cos(\pi/8)|\!\uparrow\rangle + \sin(\pi/8)|\!\downarrow\rangle$ (real coefficients, $\phi = 0$, $\theta = \pi/4$). The analyzer is set along $\hat{n} = (\sin(\pi/3)\cos(\pi/6),\, \sin(\pi/3)\sin(\pi/6),\, \cos(\pi/3))$. (a) Compute $\cos\gamma$ using the Bloch-sphere formula. (b) Compute $P(+) = \cos^2(\gamma/2)$. (c) Verify $P(+) + P(-) = 1$. *(Tests: can apply the Born-rule formula $P(+) = \cos^2(\gamma/2)$ with a general analyzer; can use the dot-product formula for $\cos\gamma$)*

**6.5** A proton is placed in a field $\vec{B} = 1.5\,\hat{z}$ T. The initial spin state is $|\psi(0)\rangle = (|\!\uparrow\rangle + |\!\downarrow\rangle)/\sqrt{2}$ (Bloch angles $\theta_0 = \pi/2$, $\phi_0 = 0$). (a) Write down $|\psi(t)\rangle$ using the Larmor time-evolution operator. (b) Compute $\langle\hat{S}_x\rangle(t)$, $\langle\hat{S}_y\rangle(t)$, $\langle\hat{S}_z\rangle(t)$. (c) What is the Larmor frequency in MHz? (d) What is the precession period in nanoseconds? *(Tests: can apply the diagonal time-evolution operator; connects the formula to a physically meaningful number)*

**6.6** Work through the sequential Stern–Gerlach calculation explicitly: (a) Start with $|\!\uparrow\rangle$. Express it in the $\sigma_x$ eigenbasis $\{|\hat{x},+\rangle, |\hat{x},-\rangle\}$ and state the Born-rule probabilities. (b) After selecting $|\hat{x},+\rangle$, express it in the $\sigma_z$ eigenbasis and state the Born-rule probabilities. (c) State the classical hidden-variable prediction for step (b), and identify which result — the QM prediction or the classical prediction — agrees with experiment. *(Tests: can carry out a two-stage basis change; can articulate the contrast between the QM prediction and the hidden-variable prediction)*

**6.7** Derive the eigenvalues of $\hat{S}_{\hat{n}} = (\hbar/2)\hat{n}\cdot\vec{\sigma}$ for a general unit vector $\hat{n}$, starting from the explicit $2\times 2$ matrix. Confirm the eigenvalues are $\pm\hbar/2$ regardless of $\hat{n}$. State in one sentence why this mathematical fact is the direct formal explanation of "two spots for any axis." *(Tests: can compute eigenvalues of a general $2\times 2$ Hermitian matrix; can connect the formal result to the experimental observation)*

### Synthesis

**6.8** The Robertson uncertainty principle (Chapter 4) applied to $\hat{A} = \hat{S}_x$ and $\hat{B} = \hat{S}_z$ gives $\sigma_{S_x}\sigma_{S_z} \geq \frac{1}{2}|\langle[\hat{S}_x, \hat{S}_z]\rangle|$. (a) Compute the commutator $[\hat{S}_x, \hat{S}_z]$ using the Pauli algebra. (b) For the state $|\hat{x},+\rangle$, evaluate both sides of the inequality. (c) Is the bound saturated? Find a state on the Bloch sphere that saturates it, and describe it geometrically. *(Tests: can apply Robertson to spin operators; connects spin algebra to the general uncertainty structure from Chapter 4)*

**6.9** The spinor double-cover property says a $2\pi$ rotation of the analyzer acquires an overall phase of $-1$ in the eigenstate, which is observable in interference but not in single-component probability. (a) Show explicitly: in $|\hat{n},+\rangle = \cos(\theta/2)|\!\uparrow\rangle + e^{i\phi}\sin(\theta/2)|\!\downarrow\rangle$, setting $\theta \to \theta + 2\pi$ sends the state to $-|\hat{n},+\rangle$. (b) Show that $P(+)$ computed from $|\hat{n},+\rangle$ and from $-|\hat{n},+\rangle$ is the same. (c) Describe an experiment (in words) that would in principle distinguish $|\hat{n},+\rangle$ from $-|\hat{n},+\rangle$. Why does such an experiment require interference? *(Tests: can execute the half-angle arithmetic; understands the distinction between global phase (unobservable) and relative phase (observable via interference))*

### Challenge

**6.10** The g-factor of the electron is $g_e \approx 2.00232$. The leading QED correction is $a_e = (g_e - 2)/2 \approx \alpha/(2\pi)$, where $\alpha \approx 1/137$. (a) Compute $\alpha/(2\pi)$ and compare to the measured $a_e \approx 0.00116$. How good is the leading-order estimate? (b) The Hamiltonian $\hat{H} = \gamma\hat{S}_z B_0$ uses the experimental $\gamma = g_e(e/2m_e)$, not the Dirac-theory value $g = 2$. Compute the fractional error in the predicted Larmor frequency if you used $g = 2$ instead of $g_e = 2.00232$ for an electron in a 1 T field. Is this error detectable in a typical laboratory ESR experiment? (c) The fractional precision of the best measurements of $a_e$ is about one part in $10^{12}$. State what physical quantity would have to be measured to this precision, and explain briefly why this makes $a_e$ one of the most precisely tested predictions in physics. *(Tests: can evaluate a perturbative correction numerically; can connect the anomalous g-factor to a measurable frequency difference; understands orders-of-magnitude precision in fundamental physics)*

## LLM Exercise — Building the Stern–Gerlach Simulator

The chapter's deliverable is `06-stern-gerlach.html`: a three-panel interactive simulation where you drag a state on the Bloch sphere, drag an analyzer axis, watch the beam split with the correct $\cos^2(\gamma/2)$ probabilities, and turn on a magnetic field to watch Larmor precession in real time.

### Part 1 — CLAUDE.md extension

Open your project's CLAUDE.md and append this block:

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

### Part 2 — The simulation prompt

```
Build me a D3 v7 Stern–Gerlach simulator following CLAUDE.md.

SHOW.
The spin state is a unit vector on the Bloch sphere at (θ_ψ, φ_ψ).
The analyzer is a unit vector at (θ_n, φ_n). The Born-rule probability
of outcome +ℏ/2 is P(+) = cos²(γ/2), where
cos γ = cos θ_ψ cos θ_n + sin θ_ψ sin θ_n cos(φ_ψ − φ_n).

SAY.
Produce a single file 06-stern-gerlach.html with three panels.
  (1) Bloch sphere: isometric projection of latitude/longitude lines, with
      two draggable arrows — state |ψ⟩ in blue, analyzer n̂ in orange.
      Numeric readouts of (θ_ψ, φ_ψ) and (θ_n, φ_n).
  (2) Stern–Gerlach apparatus: beam enters from the left, splits into upper
      and lower trajectories with stroke widths proportional to P(+) and P(−).
      A bar chart at the right shows the probabilities numerically.
  (3) Larmor precession panel: when a B-field slider is nonzero, the state
      arrow precesses around ẑ at ω_L = γ · B₀, with γ set by a particle
      dropdown (electron γ_e/2π = 28.025 GHz/T, proton γ_p/2π = 42.58 MHz/T).
      Digital readout shows ω_L/(2π) in appropriate units.

CONSTRAIN.
- D3 v7 from CDN. SVG only. Vanilla JS.
- Half-angle Born rule: P(+) = cos²(γ/2). Not cos²(γ). Verify at γ = π/2:
  P(+) must be 0.5, not 0.
- Add a "Sequential SG mode" toggle: a second SG apparatus downstream,
  user picks which branch from SG₁ survives, sets SG₂ axis independently,
  shows conditional probabilities P(SG₂=+ | SG₁=+) and P(SG₂=− | SG₁=+).
- Larmor precession: closed-form phase advance φ(t) = φ₀ + ω_L · t, not
  numerical integration. Verify ⟨S_z⟩ is constant during precession.

VERIFY.
Give me six checks:
(a) State at north pole (|↑⟩), analyzer at north pole: P(+) = 1.00.
(b) Same state, analyzer at south pole: P(+) = 0.00.
(c) Same state, analyzer at equator (any φ_n): P(+) = 0.50.
(d) For proton species at B₀ = 1 T, precession period = 1/(42.58 MHz) ≈ 23.5 ns.
(e) During Larmor precession, θ_ψ stays constant (only φ_ψ advances).
(f) P(+) + P(−) = 1.000 for every analyzer position.

List known failure modes: half-angle dropped (check (c) catches it),
wrong γ formula, Larmor units error (2π factor), wrong precession direction
for electron vs. proton, θ drift during precession, probability normalization failure.
```

### Part 3 — Exploration tasks

**Verify the antipode.** Set the state to the north pole ($|\!\uparrow\rangle$), analyzer to north pole. Read $P(+) = 1.00$. Rotate the analyzer to the south pole. Read $P(+) = 0.00$. Set the analyzer to $\theta_n = \pi/3$ and predict $P(+) = \cos^2(\pi/6) = 3/4$. Verify.

**Verify the half-angle.** Set the state to the equator ($\theta_\psi = \pi/2$). For analyzer along $\hat{z}$ ($\theta_n = 0$), confirm $P(+) = 1/2$. Verify at three other analyzer angles. If any give $P(+) = 0$ at $\theta_n = \pi/2$, the half-angle is missing.

**Larmor period.** Set species to proton, $B_0 = 1$ T. Read the precession period and confirm it is $1/(42.58\ \text{MHz}) \approx 23.5$ ns. Set $B_0 = 0.5$ T and confirm the period doubles.

**The sequential SG headline.** Sequential SG mode. Initial state $|\!\uparrow\rangle$, $\mathrm{SG}_1$ along $\hat{z}$, keep the $+$ branch. Set $\mathrm{SG}_2$ along $\hat{x}$: confirm 50/50. Keep the $+$ branch of $\mathrm{SG}_2$. Set $\mathrm{SG}_3$ along $\hat{z}$: confirm 50/50 again. The atoms started definitely spin-up along $\hat{z}$ and ended randomly along $\hat{z}$.

**The control.** Now run $\mathrm{SG}_z \to \mathrm{SG}_z$ (no intermediate $\hat{x}$ stage). Both stages aligned: confirm the second $\mathrm{SG}_z$ gives $P(+) = 1.00$. The contrast with task 4 is the signature of measurement incompatibility.

<!-- → [IMAGE: screenshot mockup of the completed 06-stern-gerlach.html simulator — three stacked panels visible: top panel shows a wireframe Bloch sphere with two colored arrows (blue state, orange analyzer); middle panel shows beam splitting into two trajectories of different thickness; bottom panel shows the Larmor precession cone; a right-side control panel shows B-field slider and particle dropdown; caption: "Target interface for the LLM exercise. Students should match this layout and verify the six checks before proceeding to the exploration tasks"] -->

### Part 4 — Extension prompt: Monte Carlo mode

```
Extend 06-stern-gerlach.html to include a Monte Carlo mode.

When the user clicks "Fire atom," generate a uniform random u in [0, 1].
If u < P(+), the atom goes up; else it goes down. Animate the atom traveling
through the apparatus and landing on one of the two output collectors.

Maintain running tallies n_+ and n_- of outcomes. Display the empirical
frequencies n_+/(n_+ + n_-) and n_-/(n_+ + n_-) alongside the theoretical
P(+) and P(-).

Add a "Fire 1000" button that fires 1000 atoms in rapid succession and
plots a histogram of the running deviation |empirical − theoretical| against
atom count. The user should see the deviation shrink roughly as 1/√N.

Do not regress the three existing panels.
```

When the empirical frequencies converge toward $\cos^2(\gamma/2)$ after a few hundred atoms, the Born rule is no longer a formula on a page. It is a frequency you watched build.

### Part 5 — Six failure modes to check

When the simulation misbehaves, the bug is usually one of these six:

**Half-angle dropped.** If $|\hat{x},+\rangle$ comes out as $|\!\downarrow\rangle$ rather than $(|\!\uparrow\rangle + |\!\downarrow\rangle)/\sqrt{2}$, the $\theta/2$ factor is missing. At $\gamma = \pi/2$, $P(+)$ should be $1/2$, not $0$.

**Wrong $\gamma$ formula.** Some students compute the angle between Bloch vectors correctly but then use $\cos^2\gamma$ instead of $\cos^2(\gamma/2)$. Easy to spot at $\gamma = \pi/2$.

**Larmor units error.** $\gamma_p/(2\pi) = 42.58$ MHz/T, so $\omega_L = 2\pi \times 42.58 \times 10^6 \times B_0$ rad/s. Using $\gamma_p$ directly without the $2\pi$ makes the precession $2\pi$ times too slow.

**Wrong precession direction.** Electron and proton precess in opposite senses because $\gamma_e < 0$ (the magnetic moment is antiparallel to the spin). If both look the same, check the sign.

**Polar angle drift.** During Larmor precession, only $\phi$ should advance; $\theta$ should stay fixed. If the Bloch arrow spirals inward, the time-evolution operator is wrong.

**Normalization failure.** $P(+) + P(-) = 1.000$ for every analyzer position. Deviation beyond floating-point tolerance signals an arithmetic bug.


*Bridge to Chapter 7: Spin is the fourth quantum number. Chapter 7 returns to the hydrogen atom and adds $m_s = \pm 1/2$ to the three quantum numbers $(n, \ell, m_\ell)$ derived from orbital angular momentum. The $2n^2$ degeneracy of the hydrogen energy levels and the entire electron-count structure of the periodic table both depend on the two-state structure built in this chapter.*
