# Research Notes: Chapter 05 — Quantum Mechanics in Three Dimensions
**Source:** TIKTOC.md chapter entry (lines 303–346)
**Notes file:** 05-quantum-mechanics-in-three-dimensions_notes.md
**Corresponding chapter:** chapters/05-three-dimensions.md (not yet written)
**Generated:** 2026-05-13

---

## Chapter summary (from TIKTOC.md)

**One-line:** Students extend quantum mechanics to three dimensions, solve the central force problem using separation of variables, and build a 3D probability density visualizer for the first few hydrogen-like orbitals.

**Chapter description:** Three-dimensional quantum mechanics introduces spherical coordinates, the separation of the Schrödinger equation for central potentials into radial and angular parts, and the spherical harmonics as the universal solutions to the angular equation. This chapter is a prerequisite for the hydrogen atom (Chapter 7) but focuses on the mathematics of 3D: separation of variables, the angular equation, spherical harmonics $Y_{\ell m}(\theta,\phi)$, and the radial equation for a general central potential. The simulation visualizes the angular probability distributions $|Y_{\ell m}|^2$ as 3D surface plots projected onto 2D — giving students their first visual sense of orbital shapes.

**Core concepts (from TIKTOC):** 3D Schrödinger equation; separation of variables; spherical harmonics with quantum numbers $\ell, m$; radial equation with centrifugal barrier; angular momentum operators and their commutators; $L^2$ and $L_z$ as compatible observables.

**Arc position:** Act Two, the chapter that turns 1D techniques into 3D ones and prepares hydrogen in Chapter 7. Pedagogically: the chapter where students first see the mathematical machinery behind atomic orbital shapes.

---

## A. Conceptual foundations

### A.1 The 3D Schrödinger equation and spherical coordinates

The 3D time-independent Schrödinger equation is the natural generalization of the 1D case:
$$-\frac{\hbar^2}{2m}\nabla^2\psi(\vec{r}) + V(\vec{r})\psi(\vec{r}) = E\psi(\vec{r})$$
with $\nabla^2 = \partial_x^2 + \partial_y^2 + \partial_z^2$ in Cartesian coordinates. In principle, this can be solved by separation of variables in Cartesian if $V(\vec{r}) = V_x(x) + V_y(y) + V_z(z)$ — a 3D box becomes three independent 1D box problems multiplied together. Done. But almost no physical potential factors this way.

The case that *does* matter physically is the **central potential**: $V(\vec{r}) = V(r)$ depends only on the radial distance $r = |\vec{r}|$. This covers the hydrogen atom (Coulomb), the 3D harmonic oscillator, the 3D spherical well, and every spherically symmetric system. For these, the natural coordinates are spherical $(r, \theta, \phi)$ with $\theta \in [0,\pi]$ the polar angle and $\phi \in [0, 2\pi)$ the azimuth. The Laplacian becomes:
$$\nabla^2 = \frac{1}{r^2}\frac{\partial}{\partial r}\!\left(r^2\frac{\partial}{\partial r}\right) + \frac{1}{r^2\sin\theta}\frac{\partial}{\partial\theta}\!\left(\sin\theta\frac{\partial}{\partial\theta}\right) + \frac{1}{r^2\sin^2\theta}\frac{\partial^2}{\partial\phi^2}$$

That second-and-third group of terms — everything that does not differentiate $r$ — is, up to a factor, the angular-momentum operator $\hat{L}^2$:
$$\hat{L}^2 = -\hbar^2\left[\frac{1}{\sin\theta}\frac{\partial}{\partial\theta}\!\left(\sin\theta\frac{\partial}{\partial\theta}\right) + \frac{1}{\sin^2\theta}\frac{\partial^2}{\partial\phi^2}\right]$$
So the kinetic term naturally splits: $-\hbar^2\nabla^2/2m = -\hbar^2/(2m)\cdot(\text{radial})\, + \, \hat{L}^2/(2mr^2)$.

**Why specify?** "Three dimensions" sounds like a small upgrade from 1D — just add some derivatives. The actual change is that the 3D Schrödinger equation, when separated, becomes *two equations*: one purely angular (the eigenvalue equation for $\hat{L}^2$ and $\hat{L}_z$) and one radial (a 1D equation in $r$ with an extra "centrifugal" term). The angular part is universal — it has the same solutions for every central potential. The radial part depends on which $V(r)$ you chose. The chapter solves the universal angular problem once and for all.

**Misconception:** *"Going to 3D just means three independent 1D problems."* True for the Cartesian box. False for everything physically interesting. The 3D box and the 3D harmonic oscillator are pedagogical exceptions, not the rule. The Coulomb potential, the spherical well, the Yukawa potential — none factor in Cartesian, all separate in spherical.

**Worked example:** Solve the 3D Cartesian infinite cubic box. Energies $E_{n_x n_y n_z} = (\pi^2\hbar^2/2mL^2)(n_x^2 + n_y^2 + n_z^2)$. Note the degeneracy: $(1,1,2)$, $(1,2,1)$, $(2,1,1)$ all have the same energy. Compare to the spherical well below.

**Sources:** Griffiths §4.1; Liboff Ch. 9 (Angular Momentum); pantry confirms angular momentum content at lines 418–423.

### A.2 Separation of variables and the angular equation

For $V(\vec{r}) = V(r)$, try $\psi(r,\theta,\phi) = R(r)\,Y(\theta,\phi)$. Substitute into the Schrödinger equation, divide by $R Y$, and multiply by $r^2$. The result splits cleanly:
$$\underbrace{\frac{1}{R}\frac{d}{dr}\!\left(r^2\frac{dR}{dr}\right) + \frac{2mr^2}{\hbar^2}[E - V(r)]}_{\text{function of }r\text{ only}} = \underbrace{-\frac{1}{Y}\left[\frac{1}{\sin\theta}\frac{\partial}{\partial\theta}\!\left(\sin\theta\frac{\partial Y}{\partial\theta}\right) + \frac{1}{\sin^2\theta}\frac{\partial^2 Y}{\partial\phi^2}\right]}_{\text{function of }\theta,\phi\text{ only}}$$
Each side is a function of disjoint variables, so each side equals a constant. Conventionally that constant is written $\ell(\ell+1)$ — the choice will be justified shortly. The angular equation is:
$$\hat{L}^2 Y(\theta,\phi) = \hbar^2\ell(\ell+1)\,Y(\theta,\phi)$$
This is an eigenvalue equation for $\hat{L}^2$. Its solutions are the **spherical harmonics** $Y_{\ell m}(\theta,\phi)$.

A second separation $Y(\theta,\phi) = \Theta(\theta)\Phi(\phi)$ peels off the $\phi$ dependence. The $\phi$ equation is $\Phi''(\phi) = -m^2\Phi$, with solutions $\Phi_m(\phi) = e^{im\phi}/\sqrt{2\pi}$. Single-valuedness ($\Phi(\phi+2\pi) = \Phi(\phi)$) forces $m$ to be an integer. The $\theta$ equation, after substituting $u = \cos\theta$, becomes the **associated Legendre equation**, whose physically acceptable solutions are the associated Legendre polynomials $P_\ell^m(\cos\theta)$ with $\ell = 0, 1, 2, \ldots$ and $|m| \leq \ell$.

The full spherical harmonic:
$$Y_{\ell m}(\theta,\phi) = \sqrt{\frac{(2\ell+1)}{4\pi}\frac{(\ell-|m|)!}{(\ell+|m|)!}}\,P_\ell^m(\cos\theta)\,e^{im\phi}$$
(with various sign conventions across textbooks — Griffiths and Jackson differ; pick one and document).

**Misconception:** *"Spherical harmonics are the wave function in 3D."* No. They are the *angular part* of the wave function for a central potential. The full wave function is $\psi(r,\theta,\phi) = R(r)Y_{\ell m}(\theta,\phi)$, and the radial part $R(r)$ depends on the specific $V(r)$. Spherical harmonics are universal across central potentials; radial functions are not.

**Worked example:** Write out $Y_0^0, Y_1^0, Y_1^{\pm 1}, Y_2^0$ explicitly:
- $Y_0^0 = \frac{1}{\sqrt{4\pi}}$ (constant — the s-orbital has no angular structure)
- $Y_1^0 = \sqrt{\frac{3}{4\pi}}\cos\theta$ (the $p_z$ orbital)
- $Y_1^{\pm 1} = \mp\sqrt{\frac{3}{8\pi}}\sin\theta\,e^{\pm i\phi}$
- $Y_2^0 = \sqrt{\frac{5}{16\pi}}(3\cos^2\theta - 1)$

Note the nodes: $Y_\ell^m$ has $\ell - |m|$ nodes in $\theta$ (at zeros of $P_\ell^m$) and effectively no nodes in $\phi$ for the modulus-squared (which is independent of $\phi$).

**Sources:** Griffiths §4.1.2 and §4.1.3; Liboff Ch. 9 §9.3; Arfken & Weber spherical-harmonics chapter [verify exact section].

### A.3 Angular momentum operators and their algebra

The orbital angular momentum vector $\vec{L} = \vec{r}\times\vec{p}$ becomes, in QM, three Hermitian operators:
$$\hat{L}_x = \hat{y}\hat{p}_z - \hat{z}\hat{p}_y, \quad \hat{L}_y = \hat{z}\hat{p}_x - \hat{x}\hat{p}_z, \quad \hat{L}_z = \hat{x}\hat{p}_y - \hat{y}\hat{p}_x$$
Their commutators, from $[\hat{x}_i, \hat{p}_j] = i\hbar\delta_{ij}$, are:
$$[\hat{L}_x, \hat{L}_y] = i\hbar\hat{L}_z, \quad [\hat{L}_y, \hat{L}_z] = i\hbar\hat{L}_x, \quad [\hat{L}_z, \hat{L}_x] = i\hbar\hat{L}_y$$
(cyclic). This is the **angular momentum algebra**. Note: the three components do not commute among themselves, but each commutes with $\hat{L}^2 = \hat{L}_x^2 + \hat{L}_y^2 + \hat{L}_z^2$:
$$[\hat{L}^2, \hat{L}_i] = 0, \quad i = x, y, z$$
By the compatibility theorem of Chapter 4, this means $\hat{L}^2$ and *any one* component (conventionally $\hat{L}_z$) can be simultaneously diagonalized. Their joint eigenstates are the spherical harmonics:
$$\hat{L}^2 Y_{\ell m} = \hbar^2\ell(\ell+1)Y_{\ell m}, \quad \hat{L}_z Y_{\ell m} = \hbar m\,Y_{\ell m}$$
with $\ell = 0, 1, 2, \ldots$ and $m \in \{-\ell, -\ell+1, \ldots, +\ell\}$.

The same algebra can be derived purely from the commutation relations using ladder operators $\hat{L}_\pm = \hat{L}_x \pm i\hat{L}_y$ — a structural rerun of the QHO algebra from Chapter 3. The fact that the eigenvalues of $\hat{L}^2$ are $\hbar^2\ell(\ell+1)$ rather than $\hbar^2\ell^2$ is forced by this algebra and is one of those things that looks weird until you see the derivation.

**Misconception 1:** *"$\hat{L}_x$ and $\hat{L}_y$ can't be measured together because the experimental apparatus is in the way."* No — they cannot be simultaneously sharp because $[\hat{L}_x, \hat{L}_y] = i\hbar\hat{L}_z \neq 0$. This is the same misconception as the Heisenberg-microscope error from Chapter 4, applied here. The Robertson uncertainty relation gives $\sigma_{L_x}\sigma_{L_y} \geq \hbar|\langle L_z\rangle|/2$ — a *statistical* statement about ensemble spreads, not an apparatus limitation.

**Misconception 2:** *"$L^2 = (\ell\hbar)^2$."* No — it is $\hbar^2\ell(\ell+1)$. The extra $\ell$ matters. Even the maximum measurable value of any single component, $|L_z|_{\max} = \ell\hbar$, is *less* than $\sqrt{\langle L^2\rangle} = \hbar\sqrt{\ell(\ell+1)}$. The angular momentum vector can never be fully aligned with the $z$-axis — there is always some "transverse" component, related to the non-commuting algebra. This is a worth-pausing-on geometric fact.

**Worked example:** Verify $[\hat{L}_x, \hat{L}_y] = i\hbar\hat{L}_z$ explicitly from $[\hat{x}, \hat{p}_x] = i\hbar$ and similar. Use bilinearity and the Leibniz-like rule $[\hat{A}\hat{B}, \hat{C}] = \hat{A}[\hat{B},\hat{C}] + [\hat{A},\hat{C}]\hat{B}$. The calculation is tedious but illuminating — it shows how the *abstract* algebra emerges from the *concrete* canonical commutator.

**Sources:** Griffiths §4.3; Liboff Ch. 9 §9.1–9.3; Sakurai Ch. 3.

### A.4 The radial equation and the centrifugal barrier

With $\psi = R(r)Y_{\ell m}(\theta,\phi)$, substituting back into the full Schrödinger equation gives a radial equation for $R(r)$. The standard trick is to define $u(r) = rR(r)$, which converts the radial equation to:
$$-\frac{\hbar^2}{2m}\frac{d^2u}{dr^2} + \left[V(r) + \frac{\hbar^2\ell(\ell+1)}{2mr^2}\right]u = Eu$$
This is *exactly* a 1D Schrödinger equation in $u(r)$ on the half-line $r \in [0,\infty)$ with **effective potential**:
$$V_{\text{eff}}(r) = V(r) + \frac{\hbar^2\ell(\ell+1)}{2mr^2}$$
The extra term, the **centrifugal barrier**, is positive and diverges at $r=0$. For $\ell > 0$, it forces $u(0) = 0$ and pushes probability away from the origin. For $\ell = 0$ (s-states), there is no barrier and the wave function can have finite amplitude at the origin.

This recasting is *the* most powerful pedagogical move in the chapter. A 3D central-force problem is reduced to a 1D bound-state problem — exactly the kind students have been solving since Chapter 2 — with an extra centrifugal term in the potential. The technique is universal: once $\hat{L}^2$ has fixed $\ell$, the radial problem is just 1D again.

**Boundary conditions:** $u(0) = 0$ (to keep $R(r) = u(r)/r$ finite at the origin), and $u(r) \to 0$ as $r\to\infty$ (for bound states). The wave function $\psi$ should normalize: $\int |\psi|^2 d^3r = \int_0^\infty |R|^2 r^2 dr \cdot \int |Y_{\ell m}|^2 d\Omega = \int_0^\infty |u|^2 dr = 1$ (using $|Y_{\ell m}|^2$ integrated over solid angle = 1).

**Misconception:** *"Higher $\ell$ means higher energy."* Not in general. Energy depends on the specific $V(r)$. For the hydrogen atom (Ch. 7), energies depend *only* on the principal quantum number $n$, not $\ell$ — a special degeneracy of the $1/r$ potential. For the 3D spherical well, energy depends on both. For the 3D harmonic oscillator, energy depends on $2n_r + \ell$ where $n_r$ is the radial quantum number — another accidental simplification. The centrifugal barrier *does* push higher-$\ell$ wave functions outward and raise their kinetic energy, but whether this dominates over the potential depends on shape.

**Worked example:** The 3D infinite spherical well. $V = 0$ for $r < a$ and $V = \infty$ for $r \geq a$. The radial equation inside is $u'' + k^2 u = 0$ with $k^2 = 2mE/\hbar^2$ minus the centrifugal term, giving $u(r) = r j_\ell(kr)$ where $j_\ell$ is the spherical Bessel function. Boundary condition $u(a) = 0$ requires $j_\ell(ka) = 0$, so $ka = $ the $n$-th zero of $j_\ell$, written $\beta_{n\ell}$. Energies: $E_{n\ell} = \hbar^2\beta_{n\ell}^2/(2ma^2)$. For $\ell = 0$, $j_0(x) = \sin x/x$ has zeros at $\pi, 2\pi, 3\pi, \ldots$, giving energies $E_{n0} = n^2\pi^2\hbar^2/(2ma^2)$ — identical to the 1D infinite well, as expected (the s-states have no angular structure to add). For $\ell = 1$, the first zero of $j_1$ is at $x \approx 4.493$, giving $E_{1,1} = (4.493)^2\hbar^2/(2ma^2) \approx 1.18\,E_{2,0}$. The ordering of states is now non-trivial: $1s, 1p, 1d, 2s, 1f, \ldots$

**Sources:** Griffiths §4.1.3, §4.2; Liboff Ch. 10 [verify section]; Arfken & Weber for spherical Bessel functions.

---

## B. Domain examples and cases

### B.1 The 3D infinite spherical well — the cleanest separable problem
$V = 0$ for $r < a$, $V = \infty$ outside. The angular part is the universal spherical harmonics; the radial part is spherical Bessel. Used in nuclear physics as the toy model for nucleons in a nucleus — the **shell model** in its crudest form. Real nuclei have additional spin-orbit splitting (Mayer & Jensen 1949 Nobel for the shell model with spin-orbit coupling [verify]), but the bare spherical well captures the gross structure of nuclear magic numbers (2, 8, 20, 28, 50, 82, 126).

### B.2 The 3D harmonic oscillator — separable two ways
$V(r) = (1/2)m\omega^2 r^2$. Separates in *both* Cartesian (three independent 1D harmonic oscillators) *and* spherical (angular = spherical harmonics, radial = Laguerre polynomials). Same energy levels $E = (n_x + n_y + n_z + 3/2)\hbar\omega = (2n_r + \ell + 3/2)\hbar\omega$ written two ways. The degenerate eigenstates rotate freely between the two bases — a useful concrete example of how the same Hilbert space supports multiple natural bases (Chapter 4 in action).

### B.3 The Coulomb potential preview (Chapter 7 setup)
$V(r) = -e^2/(4\pi\epsilon_0 r)$. The radial equation has, after the centrifugal-barrier addition, a specific structure that supports bound states $E_n = -13.6\text{ eV}/n^2$. Chapter 5 sets up the angular machinery; Chapter 7 solves the radial equation. The famous "accidental degeneracy" of hydrogen — energies depend only on $n$, not $\ell$ — emerges from a deeper symmetry (Runge-Lenz vector, the SO(4) symmetry of the Kepler problem) that is worth a sidebar in Chapter 7 but is *not* a property of central potentials in general.

### B.4 Failure mode: non-central potentials
The Stark effect (atom in a uniform electric field) breaks spherical symmetry: $V = -e^2/r + eEz$ is *not* central. Separation of variables in $(r,\theta,\phi)$ fails. The whole apparatus of this chapter — universal angular solutions, 1D radial equation — collapses, and one needs perturbation theory (Chapter 9). Lesson: the elegance of the central-potential framework is conditional on the symmetry. Break the symmetry, lose the elegance. The mathematical move that makes 3D tractable is the *symmetry*, not the dimension count.

---

## C. Connections and dependencies

**Backward:**
- Chapter 1 (3D Schrödinger equation) — was presented in 1D for simplicity. Now the full machinery comes online.
- Chapter 2 (infinite square well) — the 1D bound-state intuition transfers directly to the radial equation.
- Chapter 3 (harmonic oscillator, ladder operators) — the angular momentum ladder operators $\hat{L}_\pm$ have exactly the same algebraic structure as $\hat{a}_\pm$.
- Chapter 4 (operators, commutators, compatible observables) — $\hat{L}^2$ and $\hat{L}_z$ are the canonical example of compatible non-trivial observables. The chapter's $|\ell, m\rangle$ kets *are* the simultaneous eigenstates of the operator-formalism chapter.

**Forward:**
- Chapter 6 (spin) — generalizes angular momentum to allow half-integer $j$. The same commutation algebra, broader solution set. Pauli matrices replace spherical harmonics.
- Chapter 7 (hydrogen atom) — uses every result of this chapter. The Coulomb potential's specific radial equation, the $\ell(\ell+1)$ centrifugal barrier, the $|n,\ell,m\rangle$ kets — all set up here.
- Chapter 8 (identical particles, multi-electron atoms) — requires knowing the single-particle orbitals built in Chapters 5–7.
- Chapter 10 (or later) (selection rules, atomic transitions) — depend on matrix elements like $\langle Y_{\ell'm'}|\hat{z}|Y_{\ell m}\rangle$, computed using spherical-harmonic addition formulas.

---

## D. Current state of the field

The math here is from the 1700s and 1800s — Legendre 1782 [verify], Laplace 1782, the spherical harmonics having existed before Schrödinger as solutions to Laplace's equation in electrostatics. What is alive is the *use*:

- **Quantum chemistry and DFT.** Every electronic structure code (Gaussian, VASP, Quantum ESPRESSO) uses spherical-harmonic angular bases for atomic orbitals — the workhorse of computational chemistry.
- **Cosmology.** The cosmic microwave background's temperature anisotropies are decomposed in spherical harmonics on the sky, and the power spectrum $C_\ell$ as a function of $\ell$ is *the* primary observable of Planck and WMAP ([Planck 2018 results — A&A 641, A6](https://www.aanda.org/articles/aa/full_html/2020/09/aa33910-18/aa33910-18.html) [verify exact DOI]). The $\ell$ here is exactly the angular-momentum quantum number, applied to scalar fields on the celestial sphere.
- **Geophysics, planetary science.** Earth's gravity field, magnetic field, and topography are routinely expanded in spherical harmonics. GRACE and GRACE-FO missions report gravity anomalies as spherical-harmonic coefficients.
- **Nuclear physics.** The shell model based on a more sophisticated central potential (with spin-orbit coupling) continues to be a working tool, especially with phenomenological corrections.
- **Quantum optics, atomic clocks.** Selection rules from spherical-harmonic matrix elements govern which transitions are allowed in atomic spectroscopy — directly relevant to optical lattice clocks setting today's frequency standards.

The student should leave the chapter knowing that $Y_{\ell m}$ is not an academic exercise but the lingua franca of physical scientists who work on spheres — atomic, terrestrial, or cosmic.

---

## E. Teaching considerations

**Hardest concepts to teach:**

1. **Orbital shapes are not the wave function.** Chemistry classes teach "s, p, d, f orbital shapes" as if they were drawings of where the electron is. Physics students arrive having seen the dumbbell pictures and the four-leaf-clover pictures, and they think these are wave functions. They are $|Y_{\ell m}|^2$ — the angular probability densities. The full orbital is $R_{n\ell}(r)\cdot Y_{\ell m}(\theta,\phi)$, and $|R_{n\ell}|^2 r^2$ gives the radial probability density. The chapter has to actively undo the chemistry-class mental model.

2. **$\ell(\ell+1)$, not $\ell^2$.** A persistent stumble. The angular momentum magnitude squared has eigenvalue $\hbar^2\ell(\ell+1)$, but the maximum projection has eigenvalue $\ell\hbar$. The quantum vector "tilts" — it cannot fully align with any axis. The chemistry-orbital cartoon often shows arrows aligned cleanly with $z$, which reinforces the misconception. The simulation can fix this by drawing the *uncertainty cone* — a cone of half-angle $\arccos(m/\sqrt{\ell(\ell+1)})$ around the $z$-axis showing where the angular momentum "vector" can be found.

3. **The centrifugal barrier as part of an effective potential.** Students who saw centripetal force in mechanics easily confuse the $\hbar^2\ell(\ell+1)/(2mr^2)$ term with a real force. It is a *kinetic energy* contribution that appears as a potential-like term *because* we have already projected onto an angular momentum eigenstate. The trade is: kill the explicit angle dependence by going to $u(r)$, pay for it with the effective potential.

4. **Real vs. complex spherical harmonics.** Physics convention uses complex $Y_{\ell m} = P_\ell^m(\cos\theta)e^{im\phi}$. Chemistry uses real combinations $Y_{\ell m}^{\text{real}}$ to get the familiar $p_x, p_y, p_z$ shapes. Both are bases of the same $\ell$-subspace, related by $|p_x\rangle = (|Y_1^{-1}\rangle - |Y_1^1\rangle)/\sqrt{2}$, $|p_y\rangle = i(|Y_1^{-1}\rangle + |Y_1^1\rangle)/\sqrt{2}$, $|p_z\rangle = |Y_1^0\rangle$. Chapter should show both and explain which is preferred where.

5. **Why $m$ is bounded by $|\ell|$.** Falls out of the algebra (the ladder operator $\hat{L}_+$ must terminate going up), but pedagogically: $L_z^2 \leq L^2$ as operators, so $\hbar^2 m^2 \leq \hbar^2 \ell(\ell+1)$, so $|m| \leq \sqrt{\ell(\ell+1)}$, and since $m$ is an integer, $|m| \leq \ell$.

**Education research:** The Turkish prospective-teachers study ([Karaçöp & Doymuş 2013 — verify via researchgate.net/publication/236172215](https://www.researchgate.net/publication/236172215_INSTRUCTIONAL_MISCONCEPTIONS_OF_TURKISH_PROSPECTIVE_CHEMISTRY_TEACHERS_ABOUT_ATOMIC_ORBITALS_AND_HYBRIDIZATION)) found that ~51% of students still conflate orbitals with Bohr-model shells/orbits. This is a chemistry-education result, but it applies directly: the chapter cannot assume students arrive with a clean separation between "orbit" (classical trajectory) and "orbital" (probability density). State the distinction in plain language; repeat it in the simulation context.

**Prerequisite calibration:** Spherical coordinates from vector calculus. Most second-QM students have seen them; many have not used them confidently. A one-page review of the volume element $dV = r^2 \sin\theta\,dr\,d\theta\,d\phi$ and the area element $d\Omega = \sin\theta\,d\theta\,d\phi$ pays off when normalizing wave functions.

---

## F. Library files relevant to this chapter

- `pantry/436681929-Introductory-Quantum-Mechanics-by-Richard-L-Liboff-pdf.txt` — Ch. 9 Angular Momentum (lines 418–423), §9.1 spherical harmonics table (line 532), Ch. 10 plane-wave expansion in spherical harmonics (line 612). The primary pantry source for this chapter's content.
- `pantry/993201189-Solution-Manual-Introduction-to-Quantum-Mechanics-3e-Griffiths.txt` — Griffiths Ch. 4 problem solutions.
- Pantry "Quantum Physics for Beginners" titles — conceptual orbital-shape language for misconception sidebars, not primary derivations.
- **External primary:** Griffiths *Introduction to Quantum Mechanics* 3rd ed. §4.1–4.3 (the actual primary; pantry "Griffiths" .txt is mislabeled).
- **External primary:** Arfken, Weber & Harris *Mathematical Methods for Physicists* — chapter on spherical harmonics and associated Legendre functions for the math the chapter draft will lean on.
- **External primary:** Sakurai & Napolitano *Modern Quantum Mechanics* Ch. 3 — for the operator-algebra derivation of $\ell(\ell+1)$ that complements Griffiths' analytic approach.
- **External primary:** Jackson *Classical Electrodynamics* Ch. 3 — for the historical/mathematical context of spherical harmonics in potential theory (independent of QM).
- **External primary:** [NIST Digital Library of Mathematical Functions, Ch. 14 on Legendre and related functions](https://dlmf.nist.gov/14) — authoritative reference for formulas and sign conventions.

---

## F.5 Simulation pedagogy and D3 specifics

**Target deliverable:** `05-spherical-harmonics.html` — single-page D3 v7 SVG simulation showing the angular probability distribution $|Y_{\ell m}(\theta,\phi)|^2$ for a chosen $(\ell, m)$.

**Two-panel layout (~1000×600 SVG):**

1. **Left panel — angular cross-section (polar plot):** $|Y_{\ell m}(\theta,\phi=0)|^2$ as $r(\theta) = |Y_{\ell m}(\theta,0)|^2$ in polar coordinates, with $\theta$ measured from the $+z$-axis. Lobes appear naturally — $Y_1^0$ gives a dumbbell, $Y_2^0$ gives a peanut-with-belt, etc. Color: filled region with semi-transparent fill, outline darker. Sign of the *real part* of $Y_{\ell m}$ shown with color: positive lobes blue, negative lobes red (or whatever DESIGN.md specifies).
2. **Right panel — pseudo-3D angular surface:** $|Y_{\ell m}|^2$ on the unit sphere, projected to 2D via an isometric or perspective transformation. Render as a meshed surface (latitude/longitude grid, ~30×30 patches), with each patch shaded by $|Y_{\ell m}(\theta,\phi)|^2$ at its center. The pseudo-3D view shows the $\phi$ structure that the polar cross-section hides (e.g., $Y_1^{\pm 1}$ has $|Y|^2$ independent of $\phi$, just like $Y_1^0$ — only the phase distinguishes them).
3. **Bottom strip — eigenvalue display:** "$\hat{L}^2 \to \hbar^2 \ell(\ell+1) = $ [value]"; "$\hat{L}_z \to \hbar m = $ [value]"; "Nodes in $\theta$: $\ell - |m|$"; node positions drawn as small dots in the polar plot.

**Controls:**

- $\ell$ selector (integer 0 to 4, possibly 5).
- $m$ selector (integer from $-\ell$ to $+\ell$), updates range whenever $\ell$ changes.
- Toggle: "complex (physics convention)" vs. "real (chemistry convention)" — switches between $Y_\ell^m e^{im\phi}$ and the real combinations.
- Toggle: "show nodes" — highlight nodal planes/cones.
- Mode: "$|Y_{\ell m}|^2$" (probability density) vs. "$\text{Re}(Y_{\ell m})$" (signed wave function).
- View angle drag handler for the 3D panel.

**Physics computation:**

- **Associated Legendre polynomials** via the recurrence:
  - $P_\ell^\ell(x) = (-1)^\ell(2\ell-1)!!\,(1-x^2)^{\ell/2}$
  - $P_{\ell+1}^\ell(x) = x(2\ell+1)P_\ell^\ell(x)$
  - $(\ell-m+1)P_{\ell+1}^m(x) = (2\ell+1)x P_\ell^m(x) - (\ell+m)P_{\ell-1}^m(x)$

  Implement carefully — sign conventions vary (Condon-Shortley phase is the physics standard).
- **Spherical harmonic**:
  $$Y_\ell^m(\theta,\phi) = \sqrt{\frac{(2\ell+1)}{4\pi}\frac{(\ell-m)!}{(\ell+m)!}}\,P_\ell^m(\cos\theta)e^{im\phi}$$
- **Real combinations** (for chemistry mode):
  - $m > 0$: $Y_{\ell, m}^{\text{real}} = \frac{1}{\sqrt{2}}(Y_\ell^{-m} + (-1)^m Y_\ell^m)$
  - $m = 0$: $Y_{\ell, 0}^{\text{real}} = Y_\ell^0$
  - $m < 0$: $Y_{\ell, m}^{\text{real}} = \frac{i}{\sqrt{2}}(Y_\ell^m - (-1)^m Y_\ell^{-m})$
- **3D projection** for the right panel: standard orthographic with adjustable view angles. Each surface patch has coordinates $(r\sin\theta\cos\phi, r\sin\theta\sin\phi, r\cos\theta)$ where $r$ is either 1 (unit sphere with color-coded $|Y|^2$) or $r = |Y_{\ell m}(\theta,\phi)|^2$ (radial-extent view, the famous "balloon" shape).

**D3 v7 patterns:**

- `d3.line().curve(d3.curveCardinalClosed)` for the polar-cross-section outline.
- `d3.lineRadial()` ([D3 docs](https://d3js.org/d3-shape/line)) for radial-angular plots — directly suited to $r(\theta)$.
- `d3.scaleLinear()` for polar-to-Cartesian conversion.
- `d3.range(0, Math.PI, Math.PI/180)` for angular sampling.
- For the 3D panel: build a 2D mesh of $(\theta_i, \phi_j)$ pairs, project each, and render as `<path>` patches sorted by depth (painter's algorithm — render back-to-front for occlusion).

**Animation:** None required by default — these are stationary eigenstates. Optional: when toggled to "$\text{Re}(Y_{\ell m})$" mode, animate $e^{im\phi}\to e^{im\phi}e^{-i\omega t}$ to show the *azimuthal phase rotation* that makes the complex $Y_\ell^m$ different from the real $Y_{\ell m}^{\text{real}}$. The $\phi$-rotation is what $\hat{L}_z$ generates — making this visible connects geometry to operator algebra.

**Known LLM-generated physics-code failure modes:**

1. **Condon-Shortley phase confusion.** LLMs frequently drop or add the $(-1)^m$ factor in the definition of $P_\ell^m$ or $Y_\ell^m$. Test against Griffiths' explicit table: $Y_1^1 = -\sqrt{3/(8\pi)}\sin\theta\,e^{i\phi}$ (note the *minus* sign). Get it wrong and the chemistry-real-combination $p_x$ orbital comes out negative-pointing.
2. **Factorial overflow.** $\ell = 10$ gives $(\ell+m)! \approx 10^{18}$, overflowing some JavaScript integer reps. For the small $\ell \leq 4$ this chapter uses, this is fine; for an extension prompt going higher, use logarithms or gamma functions.
3. **Negative argument under the square root in $P_\ell^m$.** $(1-x^2)^{m/2}$ with $x = \cos\theta$ is always $\geq 0$, but numerical drift near $\theta = 0$ or $\pi$ can produce slightly negative $1 - x^2$. Clamp to $\max(0, 1-x^2)$ before taking the root.
4. **Wrong normalization of $|Y_{\ell m}|^2$.** The integral $\int|Y_\ell^m|^2 d\Omega = 1$ — check by Riemann-summing on the simulation's mesh as a runtime sanity test. LLMs sometimes implement the $P_\ell^m$ recursion correctly but the normalization prefactor wrong, and the plot still *looks* right (it is the right *shape*) but the colors / radial scaling are off by a factor.
5. **3D mesh painter's algorithm bugs.** Without back-to-front sorting, surface patches get drawn in wrong order and the orbital looks "inside out." If using SVG (no z-buffer), sort triangles by mean depth before appending.
6. **Real-combination indexing.** The Condon-Shortley convention for real combinations involves which $m$ gets which sign — easy to flip. Verify against the chemistry-textbook canon: $p_x \propto \sin\theta\cos\phi$, $p_y \propto \sin\theta\sin\phi$, $p_z \propto \cos\theta$.
7. **Misinterpreting "$|Y|^2$" as a wave function rather than a probability density.** Some LLMs label the y-axis as "$\psi$" instead of "$|Y_{\ell m}|^2$." Label correctly to avoid reinforcing the misconception this chapter exists to dispel.

**What the simulation must show that no textbook figure can:**

- **The polar cross-section being identical for $Y_1^0$ and $Y_1^{\pm 1}$ — but different colors / phase rotations.** The static figure in a textbook obscures that $|Y_1^{\pm 1}|^2$ is independent of $\phi$ (so its polar cross-section at $\phi = 0$ is the same shape as $|Y_1^0|^2$'s cross-section rotated 90°). The interactive sim lets the student rotate the view and *see* the rotational symmetry of $|Y_1^{\pm 1}|^2$ around the $z$-axis.
- **The transition from physics to chemistry conventions, in real time.** Toggle and watch the complex $Y_1^{\pm 1}$ collapse into the real $p_x, p_y$ — the chemistry orbitals are visibly *linear combinations* of the physics ones, and the bottom strip's eigenvalue readout shows $\hat{L}_z$ losing its definite value when the chemistry basis is selected.
- **Animation of the azimuthal phase rotation.** $e^{im\phi}$ as a phase wheel rotating at rate $m$ — the operational meaning of "magnetic quantum number" as the rate of azimuthal phase accumulation.

**Comparison anchors:** Standard chemistry-orbital visualizers (Falstad's *applet*, the various d3-orbital examples on Observable) typically show only real combinations and only $|Y|^2$. The +1 simulation's contribution is foregrounding the complex-vs-real distinction and the $\phi$-phase animation.

---

## G. Gaps and flags

- **[verify]** Mayer & Jensen 1949 papers on nuclear shell model — exact citation needed (often given as Mayer, *Phys. Rev.* 75, 1969 (1949) and Haxel, Jensen & Suess, *Phys. Rev.* 75, 1766 (1949)).
- **[verify]** Planck 2018 cosmological parameters paper — A&A 641, A6 (2020) but verify DOI before citing.
- **[verify]** Karaçöp & Doymuş or original Turkish PER citation for the 51% Bohr-model conflation figure — accessed via researchgate.net but should verify the publication is peer-reviewed and the figure is from the paper, not the abstract summary.
- **[verify]** Legendre's 1782 work on what we now call Legendre polynomials, vs. Laplace's 1782 spherical-harmonic work — both same year, easy to confuse. Get historical citation correct.
- **[verify]** Sign convention for $Y_1^{\pm 1}$ in Griffiths 3rd vs. 2nd ed. (some editions flip a sign).
- **Pantry gap:** Same as Ch 3 and Ch 4 — Griffiths .txt is mislabeled. Liboff Ch. 9 is the pantry primary; print Griffiths must be cited for the chapter draft.
- **Voice anchor:** Check `style/` and `books/quantum-mechanics-with-llms/style/`. Flag `voice-unanchored` if empty.
- **Scope warning:** The chapter as outlined deliberately stops short of solving hydrogen (deferred to Ch. 7). Maintain that discipline — it is tempting to push through the radial equation for the Coulomb potential here, but the chapter is already dense, and Ch. 7 needs its own room.
- **Math density:** The angular-momentum algebra derivation (using ladder operators $\hat{L}_\pm$ to prove $\ell(\ell+1)$ eigenvalues from commutators alone) is beautiful but may need to be a sidebar rather than the main path. Decision for the draft: include the analytic derivation via the Legendre equation as the main path, with the algebraic derivation in a "Chapter 4 callback" sidebar.
- **Simulation scope:** 3D rendering in pure D3 is harder than the chapter brief admits. The pseudo-3D panel requires mesh generation, painter's-algorithm sorting, and view rotation — material that goes beyond standard D3-as-data-viz tutorials. Two options: (a) stick with pure D3 SVG and accept that the 3D view will be visually rough; (b) allow a single dependency on three.js for the 3D panel (with Brutalist `PROJECT.md` noting the exception). Recommendation: (a) for consistency with the rest of the book; the polar cross-section is the pedagogically central view anyway, and the 3D mesh is supplementary.
- **PER-specific gap:** No physics-education-research study yet identified that specifically tests interactive spherical-harmonic simulations against static images for student learning outcomes. Worth a search; if none exists, the chapter's pedagogical claims rest on inference from related orbital-misconception literature.

**Word count target:** ~3,000 words for this notes file. Reached.
